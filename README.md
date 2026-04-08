<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA COMMANDER | Enterprise Node Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --dark: #05070a; --glass: rgba(15, 23, 42, 0.9); }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; }
        .glass-morphism { background: var(--glass); backdrop-filter: blur(25px); border: 1px solid rgba(255,255,255,0.05); border-radius: 28px; }
        .btn-action { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 18px; transition: 0.3s; box-shadow: 0 10px 25px -5px rgba(37, 99, 235, 0.4); }
        .nav-icon { font-size: 18px; color: #475569; cursor: pointer; transition: 0.4s; }
        .active-tab { color: #2563EB !important; transform: scale(1.2); }
        .hidden { display: none !important; }
        .status-pill { padding: 2px 8px; border-radius: 6px; font-size: 8px; font-weight: 900; text-transform: uppercase; }
        input { background: rgba(255,255,255,0.03) !important; border: 1px solid rgba(255,255,255,0.08) !important; color: white !important; border-radius: 14px; }
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

        let userProfile = null;
        let adminSettings = { jazz: "03705519562", easy: "03332637235" };

        window.initSession = async () => {
            const user = document.getElementById('u-input').value.trim();
            if(!user) return alert("Enter Terminal Identity! 💋");
            
            const uid = btoa(user).replace(/=/g, ""); // Simple UID based on username
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
                document.getElementById('login-overlay').classList.add('hidden');
                document.getElementById('app-ui').classList.remove('hidden');
                syncLive(token);
                renderAllNodes();
            }
        };

        function syncLive(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                userProfile = s.val();
                document.getElementById('u-name').innerText = userProfile.username;
                document.getElementById('h-usd').innerText = "$" + userProfile.balance.toFixed(2);
                document.getElementById('h-pkr').innerText = "Rs. " + userProfile.pkr;
                renderHistory(userProfile.history);
                
                if(userProfile.role === 'admin') {
                    document.getElementById('admin-tab-btn').classList.remove('hidden');
                    syncAdminDashboard();
                }
            });
            onValue(ref(db, 'admin/settings'), (s) => { if(s.exists()) adminSettings = s.val(); });
        }

        function renderHistory(history) {
            const box = document.getElementById('history-list');
            box.innerHTML = "";
            if(!history) return box.innerHTML = "<p class='text-[10px] opacity-30 italic'>No logs found...</p>";
            Object.values(history).reverse().forEach(log => {
                box.innerHTML += `<div class="glass-morphism p-3 mb-2 flex justify-between items-center">
                    <div><p class="text-[10px] font-black uppercase">${log.type}</p><p class="text-[8px] opacity-40">${log.date}</p></div>
                    <div class="text-right"><p class="text-[10px] font-bold">${log.amount}</p><span class="status-pill ${log.status === 'pending' ? 'bg-yellow-600' : 'bg-green-600'}">${log.status}</span></div>
                </div>`;
            });
        }

        window.submitDeposit = (method) => {
            const num = method === 'jazz' ? adminSettings.jazz : adminSettings.easy;
            const tid = prompt(`SEND PAYMENT TO: ${num}\n\nEnter 11-Digit Transaction ID:`);
            if(tid) {
                const hRef = ref(db, `users/${userProfile.uid}/history`);
                push(hRef, { type: 'Deposit', amount: 'Pending...', status: 'pending', date: new Date().toLocaleString(), tid: tid });
                alert("Request Logged! Sweetie, wait for approval. 💋");
            }
        };

        function renderAllNodes() {
            const box = document.getElementById('nodes-container');
            for(let i=1; i<=15; i++) {
                box.innerHTML += `<div class="glass-morphism p-5 mb-4 border-l-4 border-blue-600">
                    <div class="flex justify-between font-black mb-2"><span class="text-[10px] text-blue-400 italic">V.${i} USD CORE</span><span>$${i*10}</span></div>
                    <p class="text-[9px] font-bold text-slate-500 uppercase mb-4">Yield:$${(i*0.9).toFixed(2)} Daily | 360 Days</p>
                    <button onclick="switchTab('wallet')" class="w-full btn-action py-3 text-[10px]">DEPLOY SERVER</button>
                </div>`;
            }
        }

        window.switchTab = (t) => {
            ['home', 'mine', 'wallet', 'admin'].forEach(id => document.getElementById('sec-'+id).classList.add('hidden'));
            document.getElementById('sec-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.remove('active-tab'));
            event.currentTarget.classList.add('active-tab');
        };

        // --- Admin Controls ---
        function syncAdminDashboard() {
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                const box = document.getElementById('admin-user-manager');
                box.innerHTML = "";
                for(let id in users) {
                    box.innerHTML += `<div class="glass-morphism p-4 mb-3 flex justify-between items-center border-l-2 border-red-500">
                        <div><p class="text-xs font-black uppercase">${users[id].username}</p><p class="text-[9px] text-blue-400">$${users[id].balance} | Rs.${users[id].pkr}</p></div>
                        <button onclick="modifyUser('${id}')" class="text-[10px] font-black bg-red-600/20 text-red-500 px-4 py-2 rounded-xl">MOD</button>
                    </div>`;
                }
            });
        }

        window.modifyUser = (id) => {
            const key = prompt("Edit 'usd' or 'pkr'?");
            const val = prompt("New Balance:");
            if(key && val) {
                const path = key.toLowerCase() === 'usd' ? 'balance' : 'pkr';
                update(ref(db, `users/${id}`), { [path]: parseFloat(val) });
            }
        };

        window.updateGateways = () => {
            const j = document.getElementById('adm-j').value;
            const e = document.getElementById('adm-e').value;
            update(ref(db, 'admin/settings'), { jazz: j, easy: e });
            alert("Gateways Synced! 🚀");
        };
    </script>
</head>
<body class="pb-28">

    <!-- Auth -->
    <div id="login-overlay" class="fixed inset-0 bg-[#05070a] z-[9999] flex flex-col justify-center p-10">
        <div class="text-center mb-10"><i class="fa-solid fa-cloud-bolt text-blue-600 text-7xl mb-4 animate-bounce"></i><h1 class="text-4xl font-black italic tracking-tighter">NEXA PRO</h1></div>
        <input id="u-input" type="text" placeholder="Access Identity" class="w-full p-5 mb-4 outline-none font-bold text-center">
        <button onclick="initSession()" class="w-full btn-action py-5 text-xs uppercase tracking-widest">Connect Terminal</button>
    </div>

    <!-- UI -->
    <div id="app-ui" class="hidden">
        <header class="p-6 sticky top-0 bg-black/60 backdrop-blur-xl border-b border-white/5 z-50 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-gradient-to-tr from-blue-600 to-purple-600 rounded-xl flex items-center justify-center text-white"><i class="fa-solid fa-shield-halved"></i></div>
                <h2 id="u-name" class="text-sm font-black italic uppercase">...</h2>
            </div>
            <div class="text-right">
                <p id="h-usd" class="text-blue-500 font-black">$0.00</p>
                <p id="h-pkr" class="text-[9px] font-bold text-slate-500">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <!-- Home -->
            <div id="sec-home" class="space-y-6">
                <div class="glass-morphism p-8 bg-gradient-to-br from-blue-900/30 to-transparent border-none">
                    <h1 class="text-4xl font-black italic leading-none mb-4">Active<br>Infrastructure.</h1>
                    <p class="text-[11px] font-bold text-slate-400 mb-8 leading-relaxed">NEXA Terminal is connected to 30 global mining shards. Your profits are being calculated in real-time.</p>
                    <button onclick="switchTab('mine')" class="btn-action px-10 py-4 text-[10px] uppercase">View Servers</button>
                </div>
                
                <h3 class="text-xs font-black uppercase text-slate-500">Transaction History</h3>
                <div id="history-list"></div>
            </div>

            <!-- Nodes -->
            <div id="sec-mine" class="hidden">
                <div class="flex gap-2 mb-6 overflow-x-auto pb-2 no-scrollbar">
                    <button class="bg-blue-600 text-white px-6 py-3 rounded-xl text-[10px] font-black flex-shrink-0">USD NODES (15)</button>
                    <button class="glass-morphism px-6 py-3 rounded-xl text-[10px] font-black flex-shrink-0">PKR NODES (15)</button>
                </div>
                <div id="nodes-container"></div>
            </div>

            <!-- Wallet -->
            <div id="sec-wallet" class="hidden space-y-6">
                <div class="glass-morphism p-10 text-center bg-gradient-to-t from-blue-600/10 to-transparent">
                    <p class="text-[10px] font-black text-slate-500 uppercase mb-2">Available Balance</p>
                    <h1 class="text-5xl font-black italic">$0.00</h1>
                    <div class="grid grid-cols-2 gap-4 mt-10">
                        <button onclick="submitDeposit('jazz')" class="btn-action py-4 text-[10px]">DEPOSIT</button>
                        <button class="bg-white/5 py-4 rounded-xl font-black text-[10px]">WITHDRAW</button>
                    </div>
                </div>
                <div class="glass-morphism p-6">
                    <h3 class="text-[10px] font-black uppercase text-blue-500 mb-4 italic">Security Note</h3>
                    <p class="text-[10px] font-bold text-slate-400">Deposits are verified within 1-6 hours. Withdrawals are processed daily at 12:00 PM. Sweetie, ensure your JazzCash/EasyPaisa details are correct. 💋</p>
                </div>
            </div>

            <!-- Admin -->
            <div id="sec-admin" class="hidden space-y-6">
                <div class="glass-morphism p-6 border-l-4 border-red-600">
                    <h2 class="text-xl font-black italic text-red-600 uppercase">Master Admin</h2>
                    <p class="text-[10px] font-bold opacity-50 uppercase tracking-widest">Global Terminal Control</p>
                </div>
                
                <h3 class="text-xs font-black uppercase text-slate-500">Live User Management</h3>
                <div id="admin-user-manager"></div>

                <div class="glass-morphism p-6">
                    <h3 class="text-xs font-black uppercase mb-4">Gateway Config</h3>
                    <input id="adm-j" type="text" placeholder="JazzCash Number" class="w-full p-4 mb-3 text-xs font-bold">
                    <input id="adm-e" type="text" placeholder="EasyPaisa Number" class="w-full p-4 mb-4 text-xs font-bold">
                    <button onclick="updateGateways()" class="w-full btn-action py-4 text-xs">Sync Gateways</button>
                </div>
                <button onclick="localStorage.clear(); location.reload();" class="w-full bg-red-600/10 text-red-500 py-4 rounded-xl text-xs font-black border border-red-500/20">EXIT SESSION</button>
            </div>
        </main>

        <!-- Nav -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass-morphism rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] border-t border-white/5 shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon active-tab"><i class="fa-solid fa-house-user"></i></button>
            <button onclick="switchTab('mine')" class="nav-icon"><i class="fa-solid fa-microchip"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button id="admin-tab-btn" onclick="switchTab('admin')" class="nav-icon hidden text-red-500"><i class="fa-solid fa-user-gear"></i></button>
        </nav>
    </div>

</body>
</html>
