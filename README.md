<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Ultimate Node</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        .glass-panel { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border-radius: 28px; border: 1px solid rgba(255,255,255,0.3); }
        .card-elite { background: linear-gradient(135deg, #0062ff 0%, #001c48 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0, 82, 209, 0.4); }
        
        /* Bottom Nav Styling */
        .bottom-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; height: 70px; background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(15px); border-radius: 25px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 20px 40px rgba(0,0,0,0.2); }
        .nav-item { color: #94a3b8; display: flex; flex-direction: column; align-items: center; gap: 4px; transition: 0.3s; cursor: pointer; }
        .nav-item.active { color: #3b82f6; }
        .nav-item i { font-size: 20px; }
        .nav-item span { font-size: 9px; font-weight: 800; text-transform: uppercase; }

        /* Sidebar Menu */
        #side-menu { position: fixed; top: 0; left: -100%; width: 80%; height: 100%; background: white; z-index: 10000; transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 20px 0 50px rgba(0,0,0,0.1); }
        #side-menu.active { left: 0; }
        .menu-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.4); z-index: 9999; display: none; backdrop-filter: blur(4px); }
        
        .hidden { display: none; }
        .nexa-input { background: #f1f5f9; border-radius: 20px; padding: 18px; width: 100%; outline: none; border: 2px solid transparent; text-align: center; font-weight: 700; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. SIDE MENU (DRAWER) -->
    <div id="menu-overlay" class="menu-overlay" onclick="toggleMenu()"></div>
    <div id="side-menu" class="p-8">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic">NEXA <span class="text-blue-600">PRO</span></h2>
            <button onclick="toggleMenu()" class="text-slate-400 text-xl"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-6">
            <div class="flex items-center gap-4 p-4 glass-panel bg-slate-50 border-none">
                <i class="fa-solid fa-circle-info text-blue-600"></i>
                <div><p class="text-sm font-black">About NEXA</p><p class="text-[10px] text-slate-400">v2.0.4 Sovereign Edition</p></div>
            </div>
            <div class="flex items-center gap-4 p-4" onclick="alert('Help center coming soon!')">
                <i class="fa-solid fa-headset text-slate-400"></i>
                <p class="text-sm font-bold">Support Center</p>
            </div>
            <div class="flex items-center gap-4 p-4 text-red-500" onclick="logout()">
                <i class="fa-solid fa-right-from-bracket"></i>
                <p class="text-sm font-bold">Disconnect Node</p>
            </div>
        </div>
    </div>

    <!-- 2. ANONYMOUS AUTH -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[5000] flex flex-col items-center justify-center p-10">
        <div class="w-20 h-20 bg-blue-600 rounded-[28px] flex items-center justify-center text-white text-3xl mb-8 shadow-2xl rotate-6 animate-bounce">
            <i class="fa-solid fa-bolt"></i>
        </div>
        <div class="w-full max-w-xs text-center">
            <h2 class="text-3xl font-black italic mb-2 tracking-tighter">NEXA Hub</h2>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-[3px] mb-8">Accessing Encrypted Network</p>
            <input type="text" id="anon-name" placeholder="Choose Nickname sweetie" class="nexa-input mb-4">
            <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Initialize Node</button>
        </div>
    </div>

    <!-- 3. MAIN APP -->
    <div id="app-content" class="hidden">
        
        <!-- Header -->
        <header class="p-6 flex justify-between items-center">
            <div class="flex items-center gap-4" onclick="toggleMenu()">
                <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-sm text-slate-800">
                    <i class="fa-solid fa-bars-staggered"></i>
                </div>
                <div>
                    <p id="greeting-msg" class="text-[10px] font-black uppercase text-slate-400">Hello Sweetie</p>
                    <h2 id="display-username" class="text-xl font-black italic tracking-tighter">Guest</h2>
                </div>
            </div>
            <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-lg shadow-blue-500/30">
                <i class="fa-solid fa-shield-halved"></i>
            </div>
        </header>

        <div class="px-6">
            <!-- PAGE: HOME -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-elite p-8 mb-10">
                    <p class="text-[10px] font-black opacity-60 uppercase mb-2">Total Balance</p>
                    <h2 id="user-bal" class="text-5xl font-black tracking-tighter">$0.00</h2>
                </div>
                
                <h3 class="text-[10px] font-black uppercase tracking-[3px] text-slate-400 mb-6">Available Pools</h3>
                <div class="space-y-4">
                    <!-- Simple Plan List -->
                    <div class="glass-panel p-6 bg-white flex justify-between items-center shadow-sm">
                        <div class="flex items-center gap-4">
                            <i class="fa-solid fa-microchip text-2xl text-blue-600"></i>
                            <div><p class="font-black italic">Alpha Pool</p><p class="text-[9px] font-bold text-green-500 uppercase">2.5% Daily</p></div>
                        </div>
                        <button onclick="buyPlan('Alpha Pool', 20, 2.5)" class="bg-slate-900 text-white px-4 py-2 rounded-xl text-[10px] font-black italic">Stake $20</button>
                    </div>
                </div>
            </div>

            <!-- PAGE: NODES (Active Mining) -->
            <div id="page-nodes" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6">Active Nodes</h2>
                <div id="active-nodes-container" class="space-y-4 text-center py-10 opacity-40">
                    <i class="fa-solid fa-box-open text-4xl mb-2"></i>
                    <p class="text-[10px] font-black uppercase">No Active Mining</p>
                </div>
            </div>

            <!-- PAGE: HISTORY -->
            <div id="page-history" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6">Transaction Logs</h2>
                <div id="history-list" class="space-y-3"></div>
            </div>

            <!-- PAGE: DEPOSIT -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6">Add Funds</h2>
                <div class="glass-panel p-8 text-center bg-white">
                    <p class="text-[10px] font-black text-slate-400 mb-4 uppercase">USDT (BEP20) Address</p>
                    <div class="bg-slate-100 p-4 rounded-xl break-all font-mono text-[10px] mb-6">0x71C7656EC7ab88b098defB751B7401B5f6d8976F</div>
                    <button class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black text-xs uppercase shadow-xl">Copy Address</button>
                </div>
            </div>
        </div>

        <!-- 4. BOTTOM NAVIGATION -->
        <nav class="bottom-nav">
            <div onclick="navTo('home')" id="nav-home" class="nav-item active">
                <i class="fa-solid fa-house"></i>
                <span>Home</span>
            </div>
            <div onclick="navTo('nodes')" id="nav-nodes" class="nav-item">
                <i class="fa-solid fa-microchip"></i>
                <span>Nodes</span>
            </div>
            <div onclick="navTo('deposit')" id="nav-deposit" class="nav-item">
                <i class="fa-solid fa-wallet"></i>
                <span>Wallet</span>
            </div>
            <div onclick="navTo('history')" id="nav-history" class="nav-item">
                <i class="fa-solid fa-clock-rotate-left"></i>
                <span>History</span>
            </div>
        </nav>

    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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
        const auth = getAuth(app);

        // --- GLOBAL UI FUNCTIONS ---
        window.navTo = (pageId) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${pageId}`).classList.remove('hidden');
            document.getElementById(`nav-${pageId}`).classList.add('active');
        };

        window.toggleMenu = () => {
            const menu = document.getElementById('side-menu');
            const overlay = document.getElementById('menu-overlay');
            menu.classList.toggle('active');
            overlay.style.display = menu.classList.contains('active') ? 'block' : 'none';
        };

        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "User_" + Math.floor(Math.random()*999);
            const res = await signInAnonymously(auth);
            const snap = await get(ref(db, `users/${res.user.uid}`));
            if(!snap.exists()) {
                await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, joined: Date.now() });
            }
        };

        window.logout = () => signOut(auth).then(() => location.reload());

        // --- CORE LOGIC ---
        onAuthStateChanged(auth, (user) => {
            if (user) {
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                initApp(user.uid);
            }
        });

        function initApp(uid) {
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()){
                    document.getElementById('user-bal').innerText = `$${s.val().balance.toFixed(2)}`;
                    document.getElementById('display-username').innerText = s.val().username;
                }
            });
            setInterval(() => syncNodes(uid), 1000);
            loadHistory(uid);
        }

        window.buyPlan = async (name, price, roi) => {
            const uid = auth.currentUser.uid;
            const snap = await get(ref(db, `users/${uid}`));
            const bal = snap.val().balance;
            if(bal < price) return navTo('deposit');
            
            const now = Date.now();
            await update(ref(db, `users/${uid}`), { balance: bal - price });
            await push(ref(db, `active_plans/${uid}`), {
                planName: name, invested: price, profit: (price * roi / 100).toFixed(2),
                start: now, expiry: now + (24 * 60 * 60 * 1000)
            });
            await push(ref(db, `history/${uid}`), { type: 'Stake', plan: name, amount: price, date: new Date().toLocaleDateString() });
            alert("Mining Activated sweetie! 🚀");
            navTo('nodes');
        };

        function syncNodes(uid) {
            onValue(ref(db, `active_plans/${uid}`), (snap) => {
                const container = document.getElementById('active-nodes-container');
                if(!snap.exists()) return;
                let html = "";
                snap.forEach(child => {
                    const p = child.val();
                    const left = p.expiry - Date.now();
                    if(left > 0) {
                        const prog = ((Date.now() - p.start) / (p.expiry - p.start)) * 100;
                        html += `
                        <div class="glass-panel p-6 bg-white text-left mb-4 shadow-sm border-l-4 border-blue-600">
                            <div class="flex justify-between mb-2"><span class="text-[10px] font-black uppercase text-blue-600">${p.planName}</span><span class="text-[10px] font-bold text-slate-400">Mining...</span></div>
                            <div class="w-full h-1.5 bg-slate-100 rounded-full overflow-hidden"><div class="h-full bg-blue-600" style="width:${prog}%"></div></div>
                        </div>`;
                    } else { finalizeNode(uid, child.key, p); }
                });
                container.innerHTML = html;
                container.classList.remove('opacity-40');
            }, { onlyOnce: true });
        }

        async function finalizeNode(uid, key, p) {
            const s = await get(ref(db, `users/${uid}`));
            await update(ref(db, `users/${uid}`), { balance: s.val().balance + parseFloat(p.profit) + parseFloat(p.invested) });
            await remove(ref(db, `active_plans/${uid}/${key}`));
            await push(ref(db, `history/${uid}`), { type: 'Profit', plan: p.planName, amount: p.profit, date: new Date().toLocaleDateString() });
        }

        function loadHistory(uid) {
            onValue(ref(db, `history/${uid}`), s => {
                const list = document.getElementById('history-list');
                list.innerHTML = "";
                if(!s.exists()) return;
                Object.values(s.val()).reverse().forEach(h => {
                    const isP = h.type === 'Profit';
                    list.innerHTML += `
                    <div class="glass-panel p-4 flex justify-between items-center bg-white shadow-sm">
                        <div><p class="text-[10px] font-black uppercase tracking-tighter">${h.type}</p><p class="text-[8px] font-bold text-slate-400">${h.plan} • ${h.date}</p></div>
                        <p class="font-black ${isP ? 'text-green-600' : 'text-slate-800'}">${isP ? '+' : '-'}$${h.amount}</p>
                    </div>`;
                });
            });
        }
    </script>
</body>
</html>
