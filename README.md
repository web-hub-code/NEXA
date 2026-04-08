<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GLOBAL | God Mode</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #0F0F12; color: #E4E4E7; overflow-x: hidden; }
        .glass { background: rgba(23, 23, 26, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .neo-card { background: linear-gradient(145deg, #1C1C21, #111115); border-radius: 30px; border: 1px solid rgba(255,255,255,0.05); }
        .accent-gradient { background: linear-gradient(135deg, #007AFF 0%, #00C6FF 100%); }
        .hidden { display: none; }
        .ticker-wrap { background: rgba(0, 122, 255, 0.1); border-bottom: 1px solid rgba(0, 122, 255, 0.2); }
        input { background: #1C1C21 !important; border: 1px solid #2D2D35 !important; color: white !important; border-radius: 15px !important; padding: 12px !important; }
    </style>
</head>
<body class="pb-24">

    <!-- Trusted Ticker -->
    <div class="ticker-wrap fixed top-0 w-full z-[100] py-2 overflow-hidden">
        <div id="global-ticker" class="whitespace-nowrap flex gap-10 text-[10px] font-black uppercase tracking-tighter text-[#007AFF]">
            <span>• SERVER STATUS: OPTIMIZED</span>
            <span id="trust-msg">• LOADING LIVE PAYOUTS...</span>
        </div>
    </div>

    <!-- Auth Screen -->
    <div id="auth-screen" class="fixed inset-0 bg-[#0F0F12] z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-24 h-24 accent-gradient rounded-[2.5rem] flex items-center justify-center text-white text-5xl mb-8 shadow-[0_20px_50px_rgba(0,122,255,0.3)]">
            <i class="fa-solid fa-shield-halved"></i>
        </div>
        <h1 class="text-4xl font-black tracking-tighter mb-2">NEXA <span class="text-[#007AFF]">GLOBAL</span></h1>
        <p class="text-[10px] font-bold text-slate-500 uppercase tracking-[5px] mb-12 text-center">Decentralized Wealth Engine</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Full Name" class="w-full">
            <input type="password" id="admin-key" placeholder="Access PIN (Optional)" class="w-full text-center tracking-[10px]">
            <button id="login-btn" class="w-full accent-gradient text-white p-5 rounded-2xl font-black uppercase text-[11px] tracking-widest active:scale-95 transition-all shadow-xl">Initialize Access</button>
        </div>
    </div>

    <!-- Admin Panel (God Mode) -->
    <div id="admin-panel" class="hidden p-6 space-y-6">
        <h2 class="text-3xl font-black text-amber-400 mt-10">GOD MODE</h2>
        <div class="neo-card p-6">
            <h4 class="text-xs font-black uppercase mb-4">Pending Deposits</h4>
            <div id="admin-deposit-list" class="space-y-4 text-black">
                <!-- Deposits show here -->
            </div>
        </div>
        <button onclick="logout()" class="w-full bg-red-500/10 text-red-500 p-4 rounded-2xl font-bold uppercase text-[10px]">Exit God Mode</button>
    </div>

    <!-- Main User App -->
    <div id="app" class="hidden pt-12">
        <header class="p-6 flex justify-between items-center">
            <div>
                <p class="text-[10px] font-black text-[#007AFF] uppercase tracking-widest">Global Partner</p>
                <h3 id="display-name" class="text-2xl font-black tracking-tight">--</h3>
            </div>
            <div class="flex gap-2">
                <button onclick="switchCurr('USD')" id="btn-usd" class="w-12 h-8 rounded-lg text-[10px] font-black bg-[#007AFF]">USD</button>
                <button onclick="switchCurr('PKR')" id="btn-pkr" class="w-12 h-8 rounded-lg text-[10px] font-black bg-[#1C1C21]">PKR</button>
            </div>
        </header>

        <main class="p-6 space-y-6">
            <!-- Wallet Card -->
            <div class="neo-card p-8 relative overflow-hidden">
                <div class="absolute top-0 right-0 w-32 h-32 bg-[#007AFF] blur-[80px] opacity-20"></div>
                <p class="text-[10px] font-black text-slate-500 uppercase tracking-widest mb-2">Available Balance</p>
                <h2 id="user-bal" class="text-5xl font-black tracking-tighter text-white animate-pulse">$0.00</h2>
                <div class="mt-8 flex gap-3">
                    <button onclick="showSection('deposit')" class="flex-1 accent-gradient p-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-lg">Deposit</button>
                    <button onclick="showSection('withdraw')" class="flex-1 bg-white/5 p-4 rounded-2xl text-[10px] font-black uppercase tracking-widest">Withdraw</button>
                </div>
            </div>

            <!-- Mining Nodes -->
            <h4 class="text-lg font-black tracking-tight px-2">Active Mining Clusters</h4>
            <div id="nodes-container" class="grid grid-cols-1 gap-4">
                <!-- Nodes dynamically added -->
            </div>
        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-0 w-full h-20 glass border-t border-white/5 flex justify-around items-center px-6 z-50">
            <button onclick="showSection('home')" class="text-[#007AFF] flex flex-col items-center"><i class="fa-solid fa-bolt"></i><span class="text-[8px] font-black mt-1 uppercase">Nodes</span></button>
            <button onclick="showSection('admin')" id="admin-nav" class="hidden text-slate-500 flex flex-col items-center"><i class="fa-solid fa-crown text-amber-400"></i><span class="text-[8px] font-black mt-1 uppercase">God Mode</span></button>
            <button onclick="logout()" class="text-slate-500 flex flex-col items-center"><i class="fa-solid fa-arrow-right-from-bracket"></i><span class="text-[8px] font-black mt-1 uppercase">Logout</span></button>
        </nav>
    </div>

    <!-- Scripts -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        let currency = 'USD';

        // --- AUTH LOGIC ---
        document.getElementById('login-btn').addEventListener('click', async () => {
            const name = document.getElementById('user-name').value;
            const pin = document.getElementById('admin-key').value;
            if(name.length < 3) return alert("Enter valid name sweetie!");

            const res = await signInAnonymously(auth);
            const userRef = ref(db, `users/${res.user.uid}`);
            const snap = await get(userRef);

            if(!snap.exists()) {
                await set(userRef, {
                    username: name,
                    balance: 0,
                    plans: 0,
                    role: (pin === "sweetie786") ? "admin" : "user",
                    status: "active",
                    created: Date.now()
                });
            }
        });

        // --- CORE OBSERVER ---
        onAuthStateChanged(auth, (user) => {
            if(user) {
                onValue(ref(db, `users/${user.uid}`), (snap) => {
                    currentUserData = snap.val();
                    if(currentUserData.role === "admin") document.getElementById('admin-nav').classList.remove('hidden');
                    updateUI();
                    document.getElementById('auth-screen').classList.add('hidden');
                    document.getElementById('app').classList.remove('hidden');
                });
                loadNodes();
                startFakeTicker();
            } else {
                document.getElementById('auth-screen').classList.remove('hidden');
                document.getElementById('app').classList.add('hidden');
            }
        });

        function updateUI() {
            const bal = currency === 'USD' ? currentUserData.balance : currentUserData.balance * 280;
            document.getElementById('display-name').innerText = currentUserData.username;
            document.getElementById('user-bal').innerText = (currency === 'USD' ? '$' : 'Rs ') + bal.toLocaleString();
        }

        window.switchCurr = (c) => {
            currency = c;
            document.getElementById('btn-usd').className = `w-12 h-8 rounded-lg text-[10px] font-black ${c === 'USD' ? 'bg-[#007AFF]' : 'bg-[#1C1C21]'}`;
            document.getElementById('btn-pkr').className = `w-12 h-8 rounded-lg text-[10px] font-black ${c === 'PKR' ? 'bg-[#007AFF]' : 'bg-[#1C1C21]'}`;
            updateUI();
            loadNodes();
        };

        function loadNodes() {
            const nodes = [
                { name: "Starter Core", price: 5, pkr: 250, daily: 0.5 },
                { name: "Mega Node", price: 20, pkr: 5600, daily: 2.2 },
                { name: "Alpha Giga", price: 100, pkr: 28000, daily: 12.5 }
            ];
            const container = document.getElementById('nodes-container');
            container.innerHTML = nodes.map(n => `
                <div class="neo-card p-6 flex justify-between items-center">
                    <div>
                        <h4 class="font-black text-sm">${n.name}</h4>
                        <p class="text-[10px] text-green-500 font-bold uppercase">ROI: ${currency==='USD' ? '$'+n.daily : 'Rs '+(n.daily*280)}/Day</p>
                    </div>
                    <button class="accent-gradient px-6 py-3 rounded-2xl text-[10px] font-black uppercase">
                        ${currency==='USD' ? '$'+n.price : 'Rs '+n.pkr}
                    </button>
                </div>
            `).join('');
        }

        function startFakeTicker() {
            const msgs = ["Ali_01 withdrew $14.5", "Zain just bought Alpha Giga!", "Payment Success: Rs 4,500 via EasyPaisa"];
            setInterval(() => {
                document.getElementById('trust-msg').innerText = `• ${msgs[Math.floor(Math.random()*msgs.length)]}`;
            }, 5000);
        }

        window.logout = () => signOut(auth);
    </script>
</body>
</html>
