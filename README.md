<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ULTIMATE | Light Edition</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --bg: #fdfdfd; --card: #ffffff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; overflow-x: hidden; }
        .nexa-card { background: var(--card); border: 1px solid #f1f5f9; border-radius: 24px; box-shadow: 0 10px 25px -5px rgba(0,0,0,0.03); }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 16px; transition: 0.3s; }
        .nav-icon { font-size: 18px; color: #94a3b8; cursor: pointer; transition: 0.4s; }
        .active-tab { color: #2563EB !important; transform: scale(1.15); }
        .hidden { display: none !important; }
        input { background: #f8fafc !important; border: 1px solid #e2e8f0 !important; color: #0f172a !important; border-radius: 12px; }
        .status-pill { padding: 3px 8px; border-radius: 8px; font-size: 8px; font-weight: 900; text-transform: uppercase; }
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

        window.initAuth = async () => {
            const user = document.getElementById('u-field').value.trim();
            if(!user) return alert("Please enter your identity, sweetie! 💋");
            const uid = btoa(user).replace(/=/g, ""); 
            const uRef = ref(db, 'users/' + uid);
            const snap = await get(uRef);
            if(!snap.exists()) {
                await set(uRef, { username: user, balance: 0.0, pkr: 0, uid: uid, role: user.toLowerCase() === 'admin' ? 'admin' : 'user', history: {} });
            }
            localStorage.setItem('nexa_session', uid);
            location.reload();
        };

        window.onload = () => {
            const session = localStorage.getItem('nexa_session');
            if(session) {
                document.getElementById('auth-gate').classList.add('hidden');
                document.getElementById('main-ui').classList.remove('hidden');
                syncSession(session);
                renderShardNodes();
            }
        };

        function syncSession(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                uData = s.val();
                document.getElementById('nav-username').innerText = uData.username;
                document.getElementById('top-usd').innerText = "$" + uData.balance.toFixed(2);
                document.getElementById('top-pkr').innerText = "Rs. " + uData.pkr;
                renderHistory(uData.history);
                if(uData.role === 'admin') {
                    document.getElementById('admin-trigger').classList.remove('hidden');
                    syncAdminHub();
                }
            });
            onValue(ref(db, 'admin/settings'), (s) => { if(s.exists()) adminSettings = s.val(); });
        }

        function renderHistory(history) {
            const box = document.getElementById('hist-box');
            box.innerHTML = "";
            if(!history || Object.keys(history).length === 0) {
                box.innerHTML = "<p class='text-[10px] text-slate-400 italic'>No activity logs yet...</p>";
                return;
            }
            Object.values(history).reverse().forEach(log => {
                box.innerHTML += `<div class="nexa-card p-3 mb-2 flex justify-between items-center bg-slate-50/50">
                    <div><p class="text-[10px] font-black uppercase text-slate-700">${log.type}</p><p class="text-[8px] text-slate-400">${log.date}</p></div>
                    <div class="text-right"><p class="text-[10px] font-bold text-slate-800">${log.amount}</p><span class="status-pill ${log.status === 'pending' ? 'bg-amber-100 text-amber-700' : 'bg-green-100 text-green-700'}">${log.status}</span></div>
                </div>`;
            });
        }

        window.renderShardNodes = () => {
            const box = document.getElementById('nodes-list');
            for(let i=1; i<=15; i++) {
                box.innerHTML += `<div class="nexa-card p-5 mb-4 border-l-4 border-blue-500">
                    <div class="flex justify-between items-start mb-2">
                        <div><h4 class="text-xs font-black italic">SHARD NODE v.${i}</h4><p class="text-[9px] text-slate-400">Yield: $${(i*0.9).toFixed(2)} / Daily</p></div>
                        <span class="text-sm font-black text-blue-600">$${i*10}</span>
                    </div>
                    <button onclick="switchTab('wallet')" class="w-full btn-grad py-3 text-[10px] mt-2 shadow-lg shadow-blue-200">INITIALIZE</button>
                </div>`;
            }
        };

        window.switchTab = (t) => {
            ['home', 'mine', 'wallet', 'admin'].forEach(id => document.getElementById('sec-'+id).classList.add('hidden'));
            document.getElementById('sec-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.remove('active-tab'));
            event.currentTarget.classList.add('active-tab');
        };

        window.logoutTerminal = () => {
            if(confirm("Are you sure you want to logout, sweetie? 💋")) {
                localStorage.clear();
                location.reload();
            }
        };

        // --- Admin Power Commands ---
        function syncAdminHub() {
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                const list = document.getElementById('admin-users');
                list.innerHTML = "";
                for(let id in users) {
                    list.innerHTML += `<div class="nexa-card p-4 mb-3 flex justify-between items-center border-l-2 border-red-500">
                        <div><p class="text-xs font-black uppercase">${users[id].username}</p><p class="text-[9px] text-blue-500 font-bold">$${users[id].balance} | Rs.${users[id].pkr}</p></div>
                        <button onclick="adminEdit('${id}')" class="text-[10px] font-black bg-red-50 text-red-600 px-4 py-2 rounded-xl">MODIFY</button>
                    </div>`;
                }
            });
        }

        window.adminEdit = (id) => {
            const mode = prompt("Edit 'usd' or 'pkr'?");
            const val = prompt("New Amount:");
            if(mode && val) {
                const field = mode.toLowerCase() === 'usd' ? 'balance' : 'pkr';
                update(ref(db, `users/${id}`), { [field]: parseFloat(val) });
            }
        };

        window.saveGateways = () => {
            const j = document.getElementById('adm-jazz').value;
            const e = document.getElementById('adm-easy').value;
            update(ref(db, 'admin/settings'), { jazz: j, easy: e });
            alert("Payment Numbers Updated! 💋");
        };
    </script>
</head>
<body class="pb-28">

    <!-- Auth Section -->
    <div id="auth-gate" class="fixed inset-0 bg-white z-[9999] flex flex-col justify-center p-10">
        <div class="text-center mb-12">
            <div class="w-20 h-20 bg-blue-600 rounded-3xl mx-auto mb-6 flex items-center justify-center text-white shadow-2xl rotate-3">
                <i class="fa-solid fa-bolt-lightning text-4xl"></i>
            </div>
            <h1 class="text-3xl font-extrabold italic tracking-tighter text-slate-800">NEXA COMMAND</h1>
            <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest mt-2">Quantum Node Terminal</p>
        </div>
        <input id="u-field" type="text" placeholder="Access Key / Name" class="w-full p-5 mb-4 outline-none font-bold text-center shadow-inner">
        <button onclick="initAuth()" class="w-full btn-grad py-5 text-xs uppercase tracking-widest shadow-xl">Connect Session</button>
    </div>

    <!-- Main UI Section -->
    <div id="main-ui" class="hidden">
        <header class="p-6 sticky top-0 bg-white/90 backdrop-blur-md border-b border-slate-100 z-50 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-slate-900 rounded-xl flex items-center justify-center text-white"><i class="fa-solid fa-dna"></i></div>
                <div>
                    <h2 id="nav-username" class="text-sm font-black italic uppercase text-slate-800">...</h2>
                    <button onclick="logoutTerminal()" class="text-[9px] font-black text-red-500 uppercase flex items-center gap-1">
                        <i class="fa-solid fa-power-off"></i> Sign Out
                    </button>
                </div>
            </div>
            <div class="text-right">
                <p id="top-usd" class="text-blue-600 font-black text-lg leading-none">$0.00</p>
                <p id="top-pkr" class="text-[10px] font-bold text-slate-400">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <!-- Home & History -->
            <div id="sec-home" class="space-y-6">
                <div class="nexa-card p-8 bg-gradient-to-br from-blue-500 to-indigo-600 border-none text-white shadow-blue-200">
                    <h1 class="text-4xl font-black italic leading-none mb-4">Master<br>Access.</h1>
                    <p class="text-[11px] font-bold opacity-80 mb-8">System status: Optimizing shards. Sweetie, check your daily yield in nodes tab. 💋</p>
                    <button onclick="switchTab('mine')" class="bg-white text-blue-600 px-8 py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg">Start Mining</button>
                </div>
                
                <h3 class="text-xs font-black uppercase text-slate-400 flex items-center gap-2">
                    <i class="fa-solid fa-clock-rotate-left"></i> Operation Logs
                </h3>
                <div id="hist-box"></div>
            </div>

            <!-- Nodes Shards -->
            <div id="sec-mine" class="hidden">
                <div class="flex gap-3 mb-6 overflow-x-auto pb-2 no-scrollbar">
                    <button class="bg-slate-900 text-white px-6 py-3 rounded-2xl text-[10px] font-black flex-shrink-0">USD SHARDS</button>
                    <button class="bg-white border border-slate-200 px-6 py-3 rounded-2xl text-[10px] font-black flex-shrink-0 text-slate-400">PKR SHARDS</button>
                </div>
                <div id="nodes-list"></div>
            </div>

            <!-- Wallet -->
            <div id="sec-wallet" class="hidden space-y-6">
                <div class="nexa-card p-10 text-center bg-slate-50 border-dashed border-2 border-slate-200">
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Current Liquidity</p>
                    <h1 class="text-5xl font-black text-slate-800">$0.00</h1>
                    <div class="grid grid-cols-2 gap-4 mt-10">
                        <button class="btn-grad py-4 text-[10px] shadow-lg">DEPOSIT</button>
                        <button class="bg-white border border-slate-200 py-4 rounded-2xl font-black text-[10px] text-slate-600">WITHDRAW</button>
                    </div>
                </div>
                <div class="nexa-card p-6 bg-amber-50 border-amber-100">
                    <p class="text-[10px] font-bold text-amber-800 leading-relaxed">
                        <i class="fa-solid fa-circle-info mr-1"></i> Sweetie, for deposits, please send the exact amount and paste your Transaction ID in history.
                    </p>
                </div>
            </div>

            <!-- Admin Command Panel -->
            <div id="sec-admin" class="hidden space-y-6">
                <div class="nexa-card p-6 border-l-4 border-red-500 bg-red-50/30">
                    <h2 class="text-xl font-black italic text-red-600 uppercase">Admin Command Hub</h2>
                    <p class="text-[10px] font-bold text-slate-500 uppercase">Override Mode Active</p>
                </div>

                <h3 class="text-xs font-black uppercase text-slate-400">Manage Core Users</h3>
                <div id="admin-users"></div>

                <div class="nexa-card p-6">
                    <h3 class="text-xs font-black uppercase text-slate-800 mb-4 italic">Gateway Config</h3>
                    <input id="adm-jazz" type="text" placeholder="JazzCash No." class="w-full p-4 mb-3 text-xs font-bold">
                    <input id="adm-easy" type="text" placeholder="EasyPaisa No." class="w-full p-4 mb-4 text-xs font-bold">
                    <button onclick="saveGateways()" class="w-full btn-grad py-4 text-xs shadow-purple-100">Sync Numbers</button>
                </div>

                <button onclick="logoutTerminal()" class="w-full bg-red-50 text-red-500 py-5 rounded-2xl font-black text-[10px] uppercase border border-red-100 mt-6">
                    <i class="fa-solid fa-door-open mr-2"></i> Terminate Admin Session
                </button>
            </div>
        </main>

        <!-- Dynamic Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 nexa-card rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] border-none shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon active-tab"><i class="fa-solid fa-house-chimney-window"></i></button>
            <button onclick="switchTab('mine')" class="nav-icon"><i class="fa-solid fa-microchip"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button id="admin-trigger" onclick="switchTab('admin')" class="nav-icon hidden text-red-400"><i class="fa-solid fa-user-gear"></i></button>
        </nav>
    </div>

</body>
</html>
