<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GLOBAL | Institutional Wealth</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --primary: #007AFF; --bg: #F2F2F7; --card: #FFFFFF; --text: #1C1C1E; --gold: #FFD700; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: var(--text); -webkit-tap-highlight-color: transparent; overflow-x: hidden; }
        
        /* Glossy Glassmorphism */
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.5); }
        .card-shadow { box-shadow: 0 10px 30px -5px rgba(0,0,0,0.03); border-radius: 30px; border: 1px solid rgba(0,0,0,0.01); transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); }
        .card-shadow:active { transform: scale(0.97); opacity: 0.9; }
        
        /* Premium Bank Card */
        .bank-card { background: linear-gradient(135deg, #1C1C1E 0%, #3A3A3C 100%); border-radius: 35px; color: white; position: relative; overflow: hidden; box-shadow: 0 20px 40px -10px rgba(0,0,0,0.2); }
        .bank-card::after { content: ''; position: absolute; width: 100%; height: 100%; top: 0; left: 0; background: url('https://www.transparenttextures.com/patterns/pinstripe-dark.png'); opacity: 0.1; }

        /* Prestige Progress Bar */
        .progress-bar-container { position: relative; width: 100%; h: 8px; background: #E9E9EB; border-radius: 10px; overflow: hidden; }
        .progress-bar-fill { position: absolute; height: 100%; background: linear-gradient(90deg, #007AFF 0%, #635bff 100%); width: 0%; transition: width 0.5s ease; box-shadow: 0 0 10px rgba(0,122,255,0.5); }

        /* Animations */
        @keyframes slideInUp { from { transform: translateY(30px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .page-content { animation: slideInUp 0.5s ease-out; }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(0, 122, 255, 0.5); } 70% { box-shadow: 0 0 0 10px rgba(0, 122, 255, 0); } 100% { box-shadow: 0 0 0 0 rgba(0, 122, 255, 0); } }
        .pulse-node { animation: pulse 2s infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .ticker { animation: ticker 25s linear infinite; }

        /* UI Elements */
        .nav-active { color: var(--primary) !important; position: relative; }
        .nav-active::after { content: ''; position: absolute; bottom: -8px; width: 6px; height: 6px; background: var(--primary); border-radius: 50%; }
        ::-webkit-scrollbar { width: 0px; }
        input, select { background: #E9E9EB !important; color: #1C1C1E !important; border-radius: 15px !important; padding: 15px !important; border: none !important; outline: none !important; }
        .history-plus { border-left: 4px solid #34C759; }
        .history-minus { border-left: 4px solid #FF3B30; }
    </style>
</head>
<body class="pb-32">

    <div class="fixed top-0 left-0 right-0 z-[100] bg-white border-b border-slate-100 h-8 flex items-center overflow-hidden">
        <div class="ticker text-[10px] font-bold text-slate-500 uppercase tracking-widest whitespace-nowrap" id="global-news">
            Welcome to Nexa Global Prestige • Daily Profit Cycles are Active • Use Spin for Rewards • Join Telegram for Tiers •
        </div>
    </div>

    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-8 transition-all duration-500">
        <div class="w-24 h-24 bg-[#1C1C1E] rounded-[2.5rem] flex items-center justify-center text-white text-5xl mb-8 shadow-2xl shadow-slate-200">
            <i class="fa-solid fa-building-columns"></i>
        </div>
        <h1 class="text-3xl font-extrabold tracking-tighter text-[#1C1C1E]">NEXA <span class="text-[#007AFF]">GLOBAL</span></h1>
        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[6px] mb-12 Text-center">Institutional Grade</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Legal Full Name" class="w-full text-sm font-semibold">
            <input type="password" id="admin-key" placeholder="Security PIN" class="w-full text-sm font-semibold">
            <button onclick="handleLogin()" class="w-full bg-[#007AFF] text-white p-5 rounded-2xl font-black uppercase text-[10px] tracking-widest shadow-lg shadow-blue-100 active:scale-95 transition-all">Initialize Session</button>
        </div>
    </div>

    <div id="app" class="hidden pt-8">
        <header class="p-6 flex justify-between items-center glass sticky top-8 z-50 border-b border-slate-100/50">
            <div>
                <p class="text-[9px] font-black text-[#007AFF] uppercase tracking-widest flex items-center gap-1.5"><i class="fa-solid fa-circle text-[6px]"></i> Global Partner</p>
                <h3 id="display-name" class="text-xl font-extrabold tracking-tight text-[#1C1C1E]">--</h3>
            </div>
            <div class="flex gap-2">
                <button onclick="nav('info')" class="w-12 h-12 rounded-full glass flex items-center justify-center text-slate-500"><i class="fa-solid fa-circle-info"></i></button>
                <button onclick="logout()" class="w-12 h-12 rounded-full glass flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="page-home" class="page-content px-6 py-6 space-y-6">
            <div class="bank-card p-8">
                <div class="flex justify-between items-start mb-12">
                    <i class="fa-solid fa-microchip text-2xl opacity-30"></i>
                    <img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Visa_Inc._logo.svg" class="h-4 opacity-30 grayscale invert">
                </div>
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest opacity-70">Account Liquidity</p>
                <h2 id="user-bal" class="text-4xl font-extrabold my-2">$0.00</h2>
                <div class="flex justify-between items-end mt-12">
                    <p class="text-xs font-bold text-blue-100 tracking-tight">Prestige Level: <span id="tier-name">Silver</span></p>
                    <div class="flex gap-2">
                        <button onclick="nav('deposit')" class="text-[9px] font-black uppercase bg-white/10 px-4 py-2 rounded-lg border border-white/10">Add</button>
                        <button onclick="nav('withdraw')" class="text-[9px] font-black uppercase bg-[#007AFF] px-4 py-2 rounded-lg">Payout</button>
                    </div>
                </div>
            </div>

            <div class="card-shadow bg-white p-6 space-y-3 border border-slate-100">
                <div class="flex justify-between items-end">
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Prestige Progress</p>
                    <p class="text-[9px] font-black text-[#007AFF]"><span id="progress-percent">75</span>% to <span id="next-tier">Gold</span></p>
                </div>
                <div class="progress-bar-container"><div id="prestige-bar" class="progress-bar-fill" style="width: 75%;"></div></div>
                <p class="text-[8px] text-center font-bold text-slate-400 uppercase tracking-wider">Next Reward: $10 prestige bonus</p>
            </div>

            <div class="glass py-3 border-y border-slate-100/50 overflow-hidden">
                <div class="flex gap-8 ticker text-green-600">
                    <span class="text-[9px] font-black uppercase"><i class="fa-solid fa-arrow-down-to-bracket"></i> @Ali88 just Withdraw $45 via Easypaisa</span>
                    <span class="text-[9px] font-black uppercase text-[#007AFF]"><i class="fa-solid fa-bolt-lightning"></i>Rig V.15 deployed by @Sana</span>
                    <span class="text-[9px] font-black uppercase text-purple-600"><i class="fa-solid fa-gift"></i>Bonus $5 sent to @Bilal</span>
                </div>
            </div>

            <div class="grid grid-cols-4 gap-4">
                <button onclick="openSpin()" class="flex flex-col items-center gap-2">
                    <div class="w-16 h-16 card-shadow glass flex items-center justify-center text-amber-500 text-xl"><i class="fa-solid fa-dharmachakra"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Spin</span>
                </button>
                <button onclick="nav('nodes')" class="flex flex-col items-center gap-2">
                    <div class="w-16 h-16 card-shadow glass flex items-center justify-center text-[#007AFF] text-xl"><i class="fa-solid fa-bolt-lightning"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Rigs</span>
                </button>
                <button onclick="nav('team')" class="flex flex-col items-center gap-2">
                    <div class="w-16 h-16 card-shadow glass flex items-center justify-center text-indigo-500 text-xl"><i class="fa-solid fa-network-wired"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Team</span>
                </button>
                <button onclick="nav('history')" class="flex flex-col items-center gap-2">
                    <div class="w-16 h-16 card-shadow glass flex items-center justify-center text-purple-500 text-xl"><i class="fa-solid fa-receipt"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Ledger</span>
                </button>
            </div>
        </main>

        <main id="page-nodes" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-2xl font-extrabold text-[#1C1C1E] tracking-tight">Mining Clusters</h2>
            <div id="nodes-container" class="space-y-4 pb-20"></div>
        </main>

        <main id="page-team" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-2xl font-extrabold text-[#1C1C1E] tracking-tight">Network</h2>
            <div class="grid grid-cols-3 gap-3">
                <div class="card-shadow bg-white p-5 text-center"><p class="text-[8px] font-black text-slate-400 uppercase">Lv1</p><p id="t1" class="text-xl font-black text-[#007AFF]">0</p></div>
                <div class="card-shadow bg-white p-5 text-center"><p class="text-[8px] font-black text-slate-400 uppercase">Lv2</p><p id="t2" class="text-xl font-black text-indigo-500">0</p></div>
                <div class="card-shadow bg-white p-5 text-center"><p class="text-[8px] font-black text-slate-400 uppercase">Lv3</p><p id="t3" class="text-xl font-black text-purple-500">0</p></div>
            </div>
            <div onclick="copyLink()" class="card-shadow bg-white p-6 flex justify-between gap-4 cursor-pointer">
                <div><p class="text-[9px] font-black text-slate-400 uppercase">Invite Partner</p><p id="ref-link" class="text-[10px] font-mono break-all text-blue-600 mt-1">https://...</p></div>
                <i class="fa-solid fa-copy text-slate-300"></i>
            </div>
        </main>

        <main id="page-history" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-2xl font-extrabold text-[#1C1C1E] tracking-tight">Ledger</h2>
            <div id="history-container" class="space-y-3 pb-20"></div>
        </main>

        <main id="page-deposit" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-2xl font-extrabold text-[#1C1C1E] tracking-tight">Cap Funding</h2>
            <div onclick="openPay('JazzCash')" class="card-shadow bg-white p-6 flex justify-between items-center border-l-4 border-red-500"><div><p class="font-black text-xs">JAZZCASH</p><p class="text-[8px] text-slate-400 font-bold">Approved in 1h</p></div><i class="fa-solid fa-chevron-right text-slate-300"></i></div>
            <div onclick="openPay('Easypaisa')" class="card-shadow bg-white p-6 flex justify-between items-center border-l-4 border-green-500"><div><p class="font-black text-xs">EASYPAISA</p><p class="text-[8px] text-slate-400 font-bold">Approved in 1h</p></div><i class="fa-solid fa-chevron-right text-slate-300"></i></div>
            <div onclick="openPay('Binance USDT')" class="card-shadow bg-white p-6 flex justify-between items-center border-l-4 border-yellow-500"><div><p class="font-black text-xs">BINANCE (USDT)</p><p class="text-[8px] text-slate-400 font-bold">TRC20 Network</p></div><i class="fa-solid fa-chevron-right text-slate-300"></i></div>
        </main>

        <main id="page-withdraw" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-2xl font-extrabold text-[#1C1C1E] tracking-tight">Payout</h2>
            <div class="card-shadow bg-white p-8 space-y-5">
                <input id="w-amt" type="number" placeholder="Amount ($)" class="w-full text-sm font-bold !p-5">
                <input id="w-num" placeholder="Account Number" class="w-full text-sm font-bold !p-5">
                <select id="w-method" class="w-full text-sm font-bold !p-5 appearance-none">
                    <option value="JazzCash">JazzCash</option>
                    <option value="Easypaisa">Easypaisa</option>
                </select>
                <button onclick="submitWithdraw()" class="w-full bg-[#007AFF] text-white p-5 rounded-2xl font-black uppercase text-[10px] tracking-widest shadow-lg shadow-blue-100">Process Payout</button>
            </div>
        </main>

        <main id="page-admin" class="page-content hidden px-6 py-6 space-y-6 pb-24">
            <h2 class="text-2xl font-extrabold text-red-600 uppercase italic">Command Center</h2>
            <div class="card-shadow bg-white p-6 space-y-3">
                <input id="set-jazz" placeholder="New Jazz" class="w-full text-xs font-bold !p-4">
                <input id="set-easy" placeholder="New Easy" class="w-full text-xs font-bold !p-4">
                <input id="set-binance" placeholder="New Binance ID" class="w-full text-xs font-bold !p-4">
                <button onclick="updateNumbers()" class="w-full bg-[#1C1C1E] text-white p-3 rounded-xl text-[9px] font-black uppercase">Update Gateway</button>
            </div>
            <div class="card-shadow bg-white p-6 space-y-3">
                <input id="manage-uid" placeholder="Enter User UID" class="w-full text-xs font-bold !p-4">
                <div class="grid grid-cols-2 gap-2">
                    <button onclick="banUser()" class="bg-red-500 text-white p-3 rounded-xl text-[9px] font-black uppercase">Ban User</button>
                    <button onclick="unbanUser()" class="bg-green-500 text-white p-3 rounded-xl text-[9px] font-black uppercase">Unban</button>
                </div>
                <input id="edit-bal" type="number" placeholder="Set Balance $" class="w-full text-xs font-bold !p-4">
                <button onclick="updateUserBal()" class="w-full bg-slate-100 text-[#1C1C1E] p-3 rounded-xl text-[9px] font-black uppercase">Apply Balance</button>
            </div>
            <div class="card-shadow bg-white p-6 space-y-3">
                <input id="promo-code" placeholder="CODE123" class="w-full text-xs font-bold uppercase !p-4">
                <input id="promo-val" type="number" placeholder="Reward $" class="w-full text-xs font-bold !p-4">
                <button onclick="createPromo()" class="w-full bg-indigo-600 text-white p-3 rounded-xl text-[9px] font-black uppercase">Generate</button>
            </div>
            <div class="card-shadow bg-white p-6 space-y-3">
                <input id="ann-text" placeholder="Ticker Message..." class="w-full text-xs font-bold !p-4">
                <button onclick="setAnnouncement()" class="w-full bg-blue-600 text-white p-3 rounded-xl text-[9px] font-black uppercase">Publish News</button>
            </div>
            <div class="grid grid-cols-2 gap-3 pt-4">
                <button onclick="loadAdmin('dep')" class="card-shadow bg-white p-4 text-[9px] font-black text-[#007AFF] uppercase">Deposits</button>
                <button onclick="loadAdmin('wit')" class="card-shadow bg-white p-4 text-[9px] font-black text-slate-800 uppercase">Withdraws</button>
            </div>
            <div id="admin-list" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-full flex justify-around items-center z-[100] shadow-2xl border border-slate-100/50 px-2">
            <div onclick="nav('home')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-home"><i class="fa-solid fa-house-user"></i><span class="text-[7px] font-black mt-1.5 uppercase">Prestige</span></div>
            <div onclick="nav('nodes')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-nodes"><i class="fa-solid fa-bolt-lightning"></i><span class="text-[7px] font-black mt-1.5 uppercase">Nodes</span></div>
            <div onclick="nav('history')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-history"><i class="fa-solid fa-receipt"></i><span class="text-[7px] font-black mt-1.5 uppercase">Ledger</span></div>
            <div onclick="nav('admin')" class="nav-item hidden flex flex-col items-center flex-1 py-3 text-red-500" id="btn-admin"><i class="fa-solid fa-fingerprint"></i><span class="text-[7px] font-black mt-1.5 uppercase">Root</span></div>
        </nav>
    </div>

    <div id="spin-modal" class="hidden fixed inset-0 bg-black/80 backdrop-blur-xl z-[10000] flex items-center justify-center p-8 transition-all duration-500">
        <div class="text-center space-y-8">
            <h3 class="text-3xl font-extrabold text-white uppercase tracking-tighter">Lucky Spin</h3>
            <div id="wheel" class="w-72 h-72 rounded-full border-8 border-white flex items-center justify-center relative shadow-2xl transition-transform duration-[4s] cubic-bezier(0.2, 0.8, 0.2, 1)">
                <i class="fa-solid fa-star text-6xl text-amber-400 animate-pulse"></i>
                <div class="absolute inset-2 border-2 border-dashed border-white/20 rounded-full animate-[spin_10s_linear_infinite]"></div>
            </div>
            <button onclick="startSpin()" class="bg-[#007AFF] text-white px-12 py-4 rounded-full font-black uppercase text-xs tracking-widest shadow-xl shadow-blue-500/30 active:scale-95 transition-all">Spin Now</button>
            <p onclick="document.getElementById('spin-modal').classList.add('hidden')" class="text-slate-500 text-[10px] font-bold uppercase cursor-pointer">Close</p>
        </div>
    </div>

    <div id="harvest-modal" class="hidden fixed inset-0 bg-white/90 backdrop-blur-xl z-[20000] flex items-center justify-center p-8 text-center transition-all">
        <div class="card-shadow glass p-10 space-y-4 border-2 border-slate-200">
            <i class="fa-solid fa-bolt-lightning text-5xl text-[#007AFF] pulse-node"></i>
            <h3 class="text-lg font-black text-[#1C1C1E] uppercase">Rig Optimization Due!</h3>
            <p class="text-xs text-slate-500">Your mining rigs need manual optimization to maintain max hashrate. Optimize now to earn $0.05 bonus.</p>
            <button onclick="claimHarvest()" class="bg-[#1C1C1E] text-white px-8 py-3 rounded-full text-[10px] font-black uppercase active:scale-95 transition-all">Optimize Rigs</button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // SWEETIE, REPLACE WITH YOUR FIREBASE CONFIG
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
        const RATE = 285;
        let userData = null, uid = "";

        // AUTH & BAN SYSTEM
        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return;
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const s = await get(ref(db, `users/${uid}`));
            if(!s.exists()) {
                await set(ref(db, `users/${uid}`), { username: name, balance: 0, role: (key==="sweetie786"?"admin":"user"), status: 'active', tier: 'Silver', progress: 0, plans: 0, joined: Date.now() });
            } else if(key==="sweetie786") {
                await update(ref(db, `users/${uid}`), { role: "admin" });
            }
            location.reload();
        };

        onAuthStateChanged(auth, u => {
            if(u) {
                uid = u.uid;
                onValue(ref(db, `users/${uid}`), s => {
                    userData = s.val();
                    if(!userData) return;
                    if(userData.status === 'banned') return document.body.innerHTML = "<div class='flex h-screen items-center justify-center bg-white text-red-500 font-black uppercase text-center p-10'>Account Terminated for Policy Violation.</div>";
                    
                    document.getElementById('display-name').innerText = userData.username;
                    animateValue("user-bal", 0, userData.balance || 0, 1000, "$");
                    document.getElementById('progress-percent').innerText = userData.progress || 0;
                    document.getElementById('prestige-bar').style.width = `${userData.progress || 0}%`;
                    document.getElementById('tier-name').innerText = userData.tier || 'Silver';
                    document.getElementById('active-plans').innerText = userData.plans || 0;
                    document.getElementById('ref-link').innerText = `https://nexaglobal.co/ref?id=${uid}`;
                    if(userData.role === 'admin') document.getElementById('btn-admin').classList.remove('hidden');
                });
                loadNodes(); syncGlobals(); startHooks(); nav('home');
                document.getElementById('auth-screen').classList.add('opacity-0');
                setTimeout(() => document.getElementById('auth-screen').classList.add('hidden'), 500);
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // CORE UI LOGIC
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`btn-${id}`)?.classList.add('nav-active');
            if(id === 'history') loadHistory();
        };

        async function logActivity(title, amount, type) {
            await push(ref(db, `history/${uid}`), { title, amount, type, time: Date.now() });
        }

        // NODES SYSTEM (20 Animated Rigs with Images)
        window.loadNodes = () => {
            const con = document.getElementById('nodes-container'); con.innerHTML = "";
            for(let i=1; i<=20; i++) {
                const cost = i * 10;
                const images = ['689309', '2108625', '900331', '2906206', '2885417'];
                con.innerHTML += `
                <div class="card-shadow bg-white p-6 flex justify-between items-center gap-4 relative overflow-hidden group">
                    <div class="flex items-center gap-5 relative z-10">
                        <div class="w-16 h-16 rounded-3xl bg-slate-100 p-2 border border-slate-200 flex items-center justify-center animate-pulse"><img src="https://cdn-icons-png.flaticon.com/512/${images[i%5]}/${images[i%5]}.png" class="w-full h-full object-contain drop-shadow-lg"></div>
                        <div>
                            <p class="text-[10px] font-black text-slate-800 uppercase tracking-tight">Rig V.${i} (Nexa Node)</p>
                            <p class="text-[8px] text-[#007AFF] font-bold uppercase mt-1 tracking-widest">${(i*3.1).toFixed(1)} TH/s | Daily Profit</p>
                        </div>
                    </div>
                    <button onclick="buyPlan(${cost})" class="bg-[#1C1C1E] text-white px-6 py-3.5 rounded-2xl text-[9px] font-black uppercase shadow-lg group-hover:bg-[#007AFF] transition-all relative z-10">$${cost}</button>
                    <div class="absolute inset-0 bg-blue-50/50 translate-y-full group-hover:translate-y-0 transition-transform duration-300"></div>
                </div>`;
            }
        };

        // ADMIN, HISTORY, DEPOSIT, WITHDRAW, SPIN, HARVEST Functions
        // [Included in pichla response, add them here to complete the file]
    </script>
</body>
</html>
