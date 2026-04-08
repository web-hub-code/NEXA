<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GLOBAL | Institutional Engine</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --primary: #007AFF; --bg: #09090B; --card: #18181B; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #FAFAFA; overflow-x: hidden; }
        .glass-nav { background: rgba(24, 24, 27, 0.8); backdrop-filter: blur(20px); border-top: 1px solid rgba(255,255,255,0.05); }
        .neo-card { background: var(--card); border-radius: 24px; border: 1px solid rgba(255,255,255,0.05); transition: 0.3s; }
        .neo-card:active { transform: scale(0.97); }
        .accent-btn { background: linear-gradient(135deg, #007AFF 0%, #00C6FF 100%); box-shadow: 0 10px 20px -5px rgba(0, 122, 255, 0.4); }
        .hidden { display: none; }
        input, select { background: #27272A !important; border: 1px solid #3F3F46 !important; color: white !important; border-radius: 12px !important; padding: 12px !important; width: 100%; outline: none; }
        .tab-content { animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="pb-28">

    <!-- Auth Section -->
    <div id="auth-screen" class="fixed inset-0 bg-[#09090B] z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-20 h-20 accent-btn rounded-[2rem] flex items-center justify-center text-3xl mb-6"><i class="fa-solid fa-vault"></i></div>
        <h1 class="text-3xl font-black mb-10 tracking-tighter">NEXA <span class="text-[#007AFF]">GLOBAL</span></h1>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Full Name">
            <input type="text" id="refer-code" placeholder="Referral Code (Optional)">
            <button id="login-btn" class="w-full accent-btn p-4 rounded-xl font-black uppercase text-[11px] tracking-widest">Access Account</button>
        </div>
    </div>

    <!-- Main Interface -->
    <div id="main-app" class="hidden">
        <!-- Top Bar -->
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#09090B]/80 backdrop-blur-md z-40">
            <div>
                <p id="greeting" class="text-[10px] font-bold text-blue-500 uppercase">Welcome back,</p>
                <h2 id="display-name" class="text-xl font-black tracking-tight">User</h2>
            </div>
            <div class="flex items-center gap-3">
                <select id="currency-select" class="!p-1 !text-[10px] !w-16 bg-transparent border-none">
                    <option value="USD">USD</option>
                    <option value="PKR">PKR</option>
                </select>
                <div class="w-10 h-10 rounded-full bg-zinc-800 flex items-center justify-center border border-zinc-700">
                    <i class="fa-solid fa-user-tie text-blue-400"></i>
                </div>
            </div>
        </header>

        <!-- Dynamic Tabs -->
        <div id="tab-home" class="tab-content p-6 space-y-6">
            <!-- Bank Card -->
            <div class="neo-card p-6 accent-btn relative overflow-hidden">
                <div class="absolute -right-10 -top-10 w-40 h-40 bg-white/10 rounded-full blur-3xl"></div>
                <p class="text-[10px] font-bold uppercase opacity-80">Total Liquidity</p>
                <h1 id="user-balance" class="text-4xl font-black my-2">$0.00</h1>
                <div class="flex gap-2 mt-6">
                    <button onclick="switchTab('wallet')" class="flex-1 bg-white/20 backdrop-blur-md p-3 rounded-xl text-[10px] font-black uppercase">Deposit</button>
                    <button onclick="switchTab('wallet')" class="flex-1 bg-black/20 backdrop-blur-md p-3 rounded-xl text-[10px] font-black uppercase">Withdraw</button>
                </div>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-2 gap-4">
                <div class="neo-card p-4">
                    <p class="text-[9px] font-bold text-zinc-500 uppercase">Active Nodes</p>
                    <h3 id="active-nodes-count" class="text-lg font-black">0</h3>
                </div>
                <div class="neo-card p-4">
                    <p class="text-[9px] font-bold text-zinc-500 uppercase">Ref. Bonus</p>
                    <h3 id="ref-earned" class="text-lg font-black">$0.00</h3>
                </div>
            </div>

            <!-- Promotion -->
            <div class="neo-card p-4 bg-blue-500/10 border-blue-500/20 flex items-center gap-4">
                <div class="text-blue-500 text-xl"><i class="fa-solid fa-gift"></i></div>
                <div>
                    <h4 class="text-xs font-bold">Refer & Earn 10%</h4>
                    <p class="text-[10px] text-zinc-400">Your ID: <span id="my-ref-id" class="text-blue-400 font-bold">...</span></p>
                </div>
            </div>
        </div>

        <!-- Nodes Tab -->
        <div id="tab-nodes" class="tab-content hidden p-6 pb-24">
            <h2 class="text-2xl font-black mb-6">Cloud Mining <span class="text-blue-500">Nodes</span></h2>
            <div id="plans-grid" class="grid grid-cols-1 gap-4">
                <!-- 30 Plans Generated Here -->
            </div>
        </div>

        <!-- Wallet Tab -->
        <div id="tab-wallet" class="tab-content hidden p-6 pb-24">
            <h2 class="text-2xl font-black mb-6">Financial <span class="text-blue-500">Hub</span></h2>
            <div class="space-y-4">
                <div class="neo-card p-6">
                    <h4 class="text-sm font-bold mb-4">Deposit Funds</h4>
                    <select id="dep-method" class="mb-4">
                        <option value="JazzCash">JazzCash</option>
                        <option value="EasyPaisa">EasyPaisa</option>
                        <option value="Binance (USDT)">Binance (USDT)</option>
                    </select>
                    <input type="number" id="dep-amt" placeholder="Amount" class="mb-4">
                    <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="mb-4">
                    <button onclick="handleDeposit()" class="w-full accent-btn p-4 rounded-xl font-bold uppercase text-[10px]">Submit Proof</button>
                </div>
            </div>
        </div>

        <!-- Settings/More Tab -->
        <div id="tab-more" class="tab-content hidden p-6 pb-24">
            <h2 class="text-2xl font-black mb-6">System <span class="text-blue-500">Engine</span></h2>
            <div class="space-y-2">
                <div onclick="showAbout()" class="neo-card p-4 flex justify-between items-center"><span class="text-sm">Company Details</span><i class="fa-solid fa-chevron-right text-xs opacity-30"></i></div>
                <div onclick="showFAQ()" class="neo-card p-4 flex justify-between items-center"><span class="text-sm">FAQ & Help</span><i class="fa-solid fa-chevron-right text-xs opacity-30"></i></div>
                <div onclick="showPrivacy()" class="neo-card p-4 flex justify-between items-center"><span class="text-sm">Privacy Policy</span><i class="fa-solid fa-chevron-right text-xs opacity-30"></i></div>
                <div class="neo-card p-4">
                    <input type="text" id="promo-input" placeholder="Enter Promo Code" class="!mb-2">
                    <button onclick="applyPromo()" class="w-full bg-zinc-800 p-2 rounded-lg text-[10px] font-bold uppercase">Apply Code</button>
                </div>
                <button onclick="logout()" class="w-full p-4 text-red-500 font-bold text-sm mt-10">Sign Out Securely</button>
            </div>
        </div>

        <!-- Bottom Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-18 glass-nav rounded-[2rem] flex justify-around items-center px-4 z-50 border border-white/5 shadow-2xl">
            <button onclick="switchTab('home')" class="nav-btn text-blue-500 flex flex-col items-center"><i class="fa-solid fa-grid-2"></i><span class="text-[8px] font-bold mt-1 uppercase tracking-tighter">Home</span></button>
            <button onclick="switchTab('nodes')" class="nav-btn text-zinc-500 flex flex-col items-center"><i class="fa-solid fa-microchip"></i><span class="text-[8px] font-bold mt-1 uppercase tracking-tighter">Nodes</span></button>
            <button onclick="switchTab('wallet')" class="nav-btn text-zinc-500 flex flex-col items-center"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-bold mt-1 uppercase tracking-tighter">Wallet</span></button>
            <button onclick="switchTab('more')" class="nav-btn text-zinc-500 flex flex-col items-center"><i class="fa-solid fa-sliders"></i><span class="text-[8px] font-bold mt-1 uppercase tracking-tighter">More</span></button>
        </nav>
    </div>

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

        let uData = null;
        let currency = 'USD';
        const rate = 285;

        // --- 30 DYNAMIC PLANS DATA ---
        const generatePlans = () => {
            let p = [];
            for(let i=1; i<=30; i++) {
                p.push({
                    id: i,
                    name: `Node Cluster v.${i}`,
                    priceUSD: i * 10, // $10, $20... $300
                    pricePKR: i * 2500, // 2500, 5000... 75000
                    daily: (i * 10) * 0.05 // 5% Daily ROI
                });
            }
            return p;
        };
        const plans = generatePlans();

        // --- AUTH & INITIALIZATION ---
        document.getElementById('login-btn').onclick = async () => {
            const name = document.getElementById('user-name').value;
            const refBy = document.getElementById('refer-code').value;
            if(name.length < 3) return alert("Sweetie, enter your name!");

            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            const userRef = ref(db, `users/${uid}`);
            const snap = await get(userRef);

            if(!snap.exists()) {
                await set(userRef, {
                    uid, username: name, balance: 0, 
                    referBy: refBy || "None", 
                    refId: Math.random().toString(36).substring(7).toUpperCase(),
                    role: "user", nodes: 0, earnings: 0, status: "active"
                });
            }
        };

        onAuthStateChanged(auth, (user) => {
            if(user) {
                onValue(ref(db, `users/${user.uid}`), (snap) => {
                    uData = snap.val();
                    updateDashboard();
                    document.getElementById('auth-screen').classList.add('hidden');
                    document.getElementById('main-app').classList.remove('hidden');
                });
            } else {
                document.getElementById('auth-screen').classList.remove('hidden');
                document.getElementById('main-app').classList.add('hidden');
            }
        });

        // --- CORE FUNCTIONS ---
        const updateDashboard = () => {
            const bal = currency === 'USD' ? uData.balance : uData.balance * rate;
            document.getElementById('display-name').innerText = uData.username;
            document.getElementById('user-balance').innerText = (currency === 'USD' ? '$' : 'Rs ') + bal.toLocaleString();
            document.getElementById('my-ref-id').innerText = uData.refId;
            document.getElementById('active-nodes-count').innerText = uData.nodes || 0;
            renderPlans();
        };

        const renderPlans = () => {
            const grid = document.getElementById('plans-grid');
            grid.innerHTML = plans.map(p => `
                <div class="neo-card p-5 flex justify-between items-center">
                    <div>
                        <h4 class="text-sm font-black">${p.name}</h4>
                        <p class="text-[9px] text-green-400 font-bold uppercase tracking-widest">
                            ROI: ${currency==='USD' ? '$'+p.daily.toFixed(2) : 'Rs '+(p.daily*rate).toLocaleString()}/Day
                        </p>
                    </div>
                    <button onclick="buyNode(${p.id})" class="accent-btn px-4 py-2 rounded-xl text-[10px] font-black uppercase">
                        ${currency==='USD' ? '$'+p.priceUSD : 'Rs '+p.pricePKR.toLocaleString()}
                    </button>
                </div>
            `).join('');
        };

        window.switchTab = (tab) => {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.replace('text-blue-500', 'text-zinc-500'));
            event.currentTarget.classList.replace('text-zinc-500', 'text-blue-500');
        };

        window.handleDeposit = async () => {
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const method = document.getElementById('dep-method').value;
            if(!amt || !tid) return alert("Sweetie, fill all fields!");

            await push(ref(db, 'admin/deposits'), {
                uid: uData.uid, name: uData.username, amt, tid, method, status: 'pending', time: Date.now()
            });
            alert("Sent! Waiting for God Mode approval. 💎");
        };

        document.getElementById('currency-select').onchange = (e) => {
            currency = e.target.value;
            updateDashboard();
        };

        window.logout = () => signOut(auth);
        
        // --- PROMO CODE LOGIC ---
        window.applyPromo = () => {
            const code = document.getElementById('promo-input').value;
            if(code === "NAZIM786") {
                alert("Sweetie, you got $5 Bonus! 🔥");
                // Logic to add balance in DB
            } else {
                alert("Invalid Code!");
            }
        };

    </script>
</body>
</html>
