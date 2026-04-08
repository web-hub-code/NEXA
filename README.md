<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA LIGHT | Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --bg: #f8fafc; --card: #ffffff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #1e293b; overflow-x: hidden; }
        .glass-card { background: var(--card); border: 1px solid rgba(0,0,0,0.05); border-radius: 28px; box-shadow: 0 10px 30px -5px rgba(0,0,0,0.04); }
        .btn-action { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 18px; transition: 0.3s; box-shadow: 0 10px 20px -5px rgba(37, 99, 235, 0.3); }
        .nav-icon { font-size: 18px; color: #94a3b8; cursor: pointer; transition: 0.4s; }
        .active-tab { color: #2563EB !important; transform: scale(1.2); }
        .hidden { display: none !important; }
        input { background: #f1f5f9 !important; border: 1px solid #e2e8f0 !important; color: #1e293b !important; border-radius: 14px; }
    </style>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
            authDomain: "verbose-6c008.firebaseapp.com",
            databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
            projectId: "verbose-6c008",
            storageBucket: "verbose-6c008.firebasestorage.app",
            messagingSenderId: "867100945312",
            appId: "1:867100945312:web:315dfb48fb34496cee12c5"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        let uData = null;
        let adminSettings = { jazz: "03705519562", easy: "03332637235" };

        window.initSession = async () => {
            const user = document.getElementById('u-input').value.trim();
            if(!user) return alert("Sweetie, enter name! 💋");
            const uid = btoa(user).replace(/=/g, ""); 
            const uRef = ref(db, 'users/' + uid);
            const snap = await get(uRef);
            if(!snap.exists()) {
                await set(uRef, { username: user, balance: 0.0, pkr: 0, uid: uid, role: user.toLowerCase() === 'admin' ? 'admin' : 'user', history: [] });
            }
            localStorage.setItem('nexa_token', uid);
            location.reload();
        };

        window.onload = () => {
            const token = localStorage.getItem('nexa_token');
            if(token) {
                document.getElementById('login-screen').classList.add('hidden');
                document.getElementById('app-ui').classList.remove('hidden');
                syncLive(token);
                renderNodes();
            }
        };

        function syncLive(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                uData = s.val();
                document.getElementById('display-name').innerText = uData.username;
                document.getElementById('bal-usd').innerText = "$" + uData.balance.toFixed(2);
                document.getElementById('bal-pkr').innerText = "Rs. " + uData.pkr;
                if(uData.role === 'admin') {
                    document.getElementById('adm-btn').classList.remove('hidden');
                    loadAdminControls();
                }
            });
            onValue(ref(db, 'admin/settings'), (s) => { if(s.exists()) adminSettings = s.val(); });
        }

        function loadAdminControls() {
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                const box = document.getElementById('user-list-adm');
                box.innerHTML = "";
                for(let id in users) {
                    box.innerHTML += `<div class="glass-card p-4 mb-3 flex justify-between items-center border-l-4 border-blue-500">
                        <div><p class="text-xs font-black uppercase">${users[id].username}</p><p class="text-[9px] text-slate-500">$${users[id].balance} | Rs.${users[id].pkr}</p></div>
                        <button onclick="editBal('${id}')" class="text-[10px] font-black text-blue-600 bg-blue-50 px-4 py-2 rounded-xl">EDIT</button>
                    </div>`;
                }
            });
        }

        window.editBal = (id) => {
            const type = prompt("Edit 'usd' or 'pkr'?");
            const val = prompt("Enter Amount:");
            if(type && val) {
                const path = type.toLowerCase() === 'usd' ? 'balance' : 'pkr';
                update(ref(db, `users/${id}`), { [path]: parseFloat(val) });
            }
        };

        window.renderNodes = () => {
            const box = document.getElementById('nodes-grid');
            for(let i=1; i<=15; i++) {
                box.innerHTML += `<div class="glass-card p-5 mb-4 border-b-2 border-blue-100">
                    <div class="flex justify-between font-black mb-1"><span class="text-[10px] text-blue-600">CORE NODE V.${i}</span><span>$${i*10}</span></div>
                    <p class="text-[9px] font-bold text-slate-400 uppercase mb-4">Daily: $${(i*0.9).toFixed(2)}</p>
                    <button class="w-full btn-action py-3 text-[10px]">DEPLOY</button>
                </div>`;
            }
        };

        window.switchTab = (t) => {
            ['home', 'nodes', 'wallet', 'admin'].forEach(id => document.getElementById('sec-'+id).classList.add('hidden'));
            document.getElementById('sec-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.remove('active-tab'));
            event.currentTarget.classList.add('active-tab');
        };
    </script>
</head>
<body class="pb-28">

    <div id="login-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col justify-center p-10">
        <div class="text-center mb-10"><i class="fa-solid fa-cloud-sun text-blue-600 text-7xl mb-4"></i><h1 class="text-3xl font-black italic tracking-tighter text-slate-800">NEXA LIGHT</h1></div>
        <input id="u-input" type="text" placeholder="Your Name" class="w-full p-5 mb-4 outline-none font-bold text-center">
        <button onclick="initSession()" class="w-full btn-action py-5 text-xs uppercase tracking-widest">Connect</button>
    </div>

    <div id="app-ui" class="hidden">
        <header class="p-6 sticky top-0 bg-white/80 backdrop-blur-md border-b border-slate-100 z-50 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-100 rounded-xl flex items-center justify-center text-blue-600"><i class="fa-solid fa-user"></i></div>
                <div>
                    <h2 id="display-name" class="text-sm font-black italic uppercase text-slate-800">...</h2>
                    <button onclick="localStorage.clear(); location.reload();" class="text-[8px] font-black text-red-500 uppercase flex items-center gap-1">
                        <i class="fa-solid fa-power-off"></i> Logout
                    </button>
                </div>
            </div>
            <div class="text-right">
                <p id="bal-usd" class="text-blue-600 font-black">$0.00</p>
                <p id="bal-pkr" class="text-[9px] font-bold text-slate-400">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <div id="sec-home" class="space-y-6">
                <div class="glass-card p-8 bg-gradient-to-br from-blue-50 to-white border-none">
                    <h1 class="text-4xl font-black italic text-slate-800 leading-none mb-4">Bright<br>Earnings.</h1>
                    <p class="text-[11px] font-bold text-slate-500 mb-8">Sab features working hain sweetie. Clean UI ke saath apna system control karein. 💋</p>
                    <button onclick="switchTab('nodes')" class="btn-action px-10 py-4 text-[10px] uppercase">Servers List</button>
                </div>
            </div>

            <div id="sec-nodes" class="hidden"><div id="nodes-grid"></div></div>

            <div id="sec-wallet" class="hidden">
                <div class="glass-card p-10 text-center">
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Portfolio</p>
                    <h1 class="text-5xl font-black text-slate-800">$0.00</h1>
                    <div class="grid grid-cols-2 gap-4 mt-10">
                        <button class="btn-action py-4 text-[10px]">DEPOSIT</button>
                        <button class="bg-slate-100 py-4 rounded-xl font-black text-[10px] text-slate-600">WITHDRAW</button>
                    </div>
                </div>
            </div>

            <div id="sec-admin" class="hidden space-y-6">
                <div class="glass-card p-6 border-l-4 border-red-500">
                    <h2 class="text-xl font-black italic text-red-500 uppercase">Admin Command</h2>
                    <p class="text-[10px] font-bold text-slate-400">Manage Users & Balances</p>
                </div>
                <div id="user-list-adm"></div>
                <button onclick="localStorage.clear(); location.reload();" class="w-full bg-red-50 text-red-500 py-5 rounded-2xl font-black text-[10px] uppercase border border-red-100 mt-10">
                    <i class="fa-solid fa-door-open mr-2"></i> Exit Admin Session
                </button>
            </div>
        </main>

        <nav class="fixed bottom-6 left-6 right-6 h-20 glass-card rounded-[2.5rem] flex justify-around items-center px-4 z-[1000]">
            <button onclick="switchTab('home')" class="nav-icon active-tab"><i class="fa-solid fa-house"></i></button>
            <button onclick="switchTab('nodes')" class="nav-icon"><i class="fa-solid fa-server"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button id="adm-btn" onclick="switchTab('admin')" class="nav-icon hidden text-red-400"><i class="fa-solid fa-user-gear"></i></button>
        </nav>
    </div>

</body>
</html>
