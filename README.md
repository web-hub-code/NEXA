<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Finance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(0,0,0,0.05); }
        .dock { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); width: 92%; max-width: 450px; background: #0f172a; border-radius: 28px; padding: 14px; display: flex; justify-content: space-around; z-index: 1000; }
        .dock-item { color: #64748b; font-size: 10px; font-weight: 700; text-align: center; flex: 1; }
        .dock-item.active { color: #3b82f6; }
        .dock-item i { font-size: 22px; display: block; margin-bottom: 4px; }
        .btn-gradient { background: linear-gradient(135deg, #2563eb, #7c3aed); color: white; }
        .hidden { display: none; }
        .method-card { border: 2px solid transparent; transition: 0.3s; cursor: pointer; }
        .method-card.selected { border-color: #2563eb; background: #eff6ff; }
    </style>
</head>
<body class="bg-slate-50">

    <div class="max-w-md mx-auto min-h-screen pb-32">
        
        <!-- MODERN LOGO & LOGOUT -->
        <header class="p-6 flex justify-between items-center sticky top-0 z-[100] glass">
            <div class="flex items-center gap-2">
                <div id="admin-trigger" class="w-9 h-9 bg-blue-600 rounded-xl flex items-center justify-center text-white font-black shadow-lg shadow-blue-200">N</div>
                <h1 class="text-xl font-extrabold tracking-tighter">NEXA<span class="text-blue-600">.</span></h1>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-red-50 text-red-500 flex items-center justify-center">
                <i class="fa-solid fa-power-off"></i>
            </button>
        </header>

        <!-- PAGE: LOGIN -->
        <div id="page-login" class="px-8 pt-12">
            <div class="mb-10">
                <h2 class="text-4xl font-black tracking-tight">Access <br>Your <span class="text-blue-600">Vault</span>.</h2>
                <p class="text-gray-400 text-sm mt-2">Login to manage your 20+ active nodes.</p>
            </div>
            <div class="space-y-4">
                <input type="text" id="username" placeholder="Username" class="w-full p-5 rounded-3xl bg-white border-none outline-none shadow-sm font-bold">
                <input type="password" id="password" placeholder="Access Key" class="w-full p-5 rounded-3xl bg-white border-none outline-none shadow-sm font-bold">
                <button onclick="login()" class="w-full btn-gradient py-5 rounded-3xl font-black uppercase tracking-widest text-sm shadow-xl">Secure Login</button>
            </div>
        </div>

        <!-- PAGE: HOME -->
        <div id="page-home" class="hidden px-6 pt-6 animate-fade">
            <div class="bg-slate-900 rounded-[40px] p-8 text-white relative overflow-hidden shadow-2xl">
                <p class="text-[10px] font-bold opacity-50 uppercase tracking-widest">Available for Withdrawal</p>
                <h2 id="balance" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                <div class="flex gap-3 mt-8">
                    <button onclick="showPage('deposit')" class="flex-1 bg-blue-600 py-3 rounded-2xl text-xs font-black">DEPOSIT</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 py-3 rounded-2xl text-xs font-black backdrop-blur-md">WITHDRAW</button>
                </div>
            </div>

            <h3 class="font-black text-lg mt-10 mb-6">Investment Nodes (20 Available)</h3>
            <div id="plans-grid" class="grid grid-cols-1 gap-4"></div>
        </div>

        <!-- PAGE: DEPOSIT (MODERN METHOD) -->
        <div id="page-deposit" class="hidden px-6 pt-6">
            <h3 class="font-black text-2xl mb-6">Funding Method</h3>
            <div class="grid grid-cols-2 gap-4 mb-6">
                <div onclick="selectMethod('Easypaisa')" class="method-card p-4 glass rounded-3xl text-center">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/f/ff/Easypaisa_logo.png" class="h-8 mx-auto mb-2 grayscale opacity-50">
                    <p class="text-[10px] font-black">Easypaisa</p>
                </div>
                <div onclick="selectMethod('JazzCash')" class="method-card p-4 glass rounded-3xl text-center">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/a/ab/JazzCash_Logo.png" class="h-8 mx-auto mb-2 grayscale opacity-50">
                    <p class="text-[10px] font-black">JazzCash</p>
                </div>
                <div onclick="selectMethod('SadaPay')" class="method-card p-4 glass rounded-3xl text-center">
                    <i class="fa-solid fa-credit-card text-2xl mb-2 text-pink-500"></i>
                    <p class="text-[10px] font-black">SadaPay</p>
                </div>
                <div class="p-4 glass rounded-3xl text-center opacity-30">
                    <i class="fa-brands fa-bitcoin text-2xl mb-2"></i>
                    <p class="text-[8px] font-black italic">Binance (Soon)</p>
                </div>
            </div>

            <div id="dep-details" class="hidden space-y-4">
                <div class="p-6 bg-blue-50 rounded-[30px] border border-blue-100">
                    <p class="text-xs font-bold text-blue-600 mb-1">Transfer to:</p>
                    <p id="method-name" class="font-black text-xl">---</p>
                    <p class="text-lg font-black mt-2">Account: <span class="text-blue-600">03379827882</span></p>
                </div>
                <input type="number" id="d-amt" placeholder="Amount ($)" class="w-full p-4 rounded-2xl bg-white border-none outline-none font-bold shadow-sm">
                <input type="text" id="d-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-2xl bg-white border-none outline-none font-bold shadow-sm">
                
                <div class="p-4 border-2 border-dashed border-gray-200 rounded-2xl text-center">
                    <input type="file" id="d-proof" class="hidden">
                    <label for="d-proof" class="cursor-pointer text-xs font-bold text-gray-400">
                        <i class="fa-solid fa-cloud-arrow-up text-2xl block mb-2 text-blue-500"></i>
                        Upload Screenshot Proof
                    </label>
                </div>
                <button onclick="submitDeposit()" class="w-full btn-gradient py-4 rounded-2xl font-black shadow-lg">VERIFY DEPOSIT</button>
            </div>
        </div>

        <!-- PAGE: FAQ & POLICY -->
        <div id="page-help" class="hidden px-6 pt-6">
            <h3 class="font-black text-2xl mb-6">Protocol Help</h3>
            <div class="space-y-4">
                <div class="p-5 glass rounded-[30px]">
                    <h4 class="font-black text-sm text-blue-600 mb-2">How to start sweetie?</h4>
                    <p class="text-[11px] text-gray-500 leading-relaxed">Deposit funds using your preferred method. Once approved, choose a node from the home screen and click 'Stake'. Your daily yield will auto-credit.</p>
                </div>
                <div class="p-5 glass rounded-[30px]">
                    <h4 class="font-black text-sm text-blue-600 mb-2">Withdrawal Timing?</h4>
                    <p class="text-[11px] text-gray-500 leading-relaxed">Withdrawals are processed every 24 hours. Minimum limit is $10.00. No extra fees for Gold tier users.</p>
                </div>
                <div class="p-5 glass rounded-[30px]">
                    <h4 class="font-black text-sm text-blue-600 mb-2">Privacy Policy</h4>
                    <p class="text-[11px] text-gray-500 leading-relaxed">NEXA Corporation does not share user identities. All node data is stored on decentralized encrypted shards for maximum safety.</p>
                </div>
            </div>
        </div>

        <!-- DOCK NAV -->
        <nav id="dock" class="hidden dock">
            <button onclick="showPage('home')" class="dock-item active" id="nav-home"><i class="fa-solid fa-house"></i>Home</button>
            <button onclick="showPage('help')" class="dock-item" id="nav-help"><i class="fa-solid fa-circle-question"></i>Help</button>
            <button onclick="showPage('deposit')" class="dock-item" id="nav-deposit"><i class="fa-solid fa-wallet"></i>Wallet</button>
            <button onclick="showPage('withdraw')" class="dock-item" id="nav-withdraw"><i class="fa-solid fa-money-bill-transfer"></i>Payout</button>
        </nav>

    </div>

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

        window.showPage = (id) => {
            ['login', 'home', 'deposit', 'help', 'withdraw'].forEach(p => document.getElementById('page-' + p)?.classList.add('hidden'));
            document.getElementById('page-' + id).classList.remove('hidden');
            document.querySelectorAll('.dock-item').forEach(d => d.classList.remove('active'));
            document.getElementById('nav-' + id)?.classList.add('active');
        };

        window.selectMethod = (m) => {
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('selected'));
            event.currentTarget.classList.add('selected');
            document.getElementById('dep-details').classList.remove('hidden');
            document.getElementById('method-name').innerText = m;
        };

        window.login = async () => {
            const user = document.getElementById('username').value;
            const res = await signInAnonymously(auth);
            localStorage.setItem('nexa_uid', res.user.uid);
            const snap = await get(ref(db, 'users/' + res.user.uid));
            if(!snap.exists()) await set(ref(db, 'users/' + res.user.uid), { username: user, balance: 0 });
            location.reload();
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            showPage('home');
            document.getElementById('dock').classList.remove('hidden');
            onValue(ref(db, 'users/' + uid), s => {
                if(s.exists()) document.getElementById('balance').innerText = `$${s.val().balance.toFixed(2)}`;
            });

            // Loading 20 Plans (15+5)
            onValue(ref(db, 'plans'), s => {
                const grid = document.getElementById('plans-grid');
                grid.innerHTML = "";
                s.forEach(p => {
                    grid.innerHTML += `<div class="glass p-5 rounded-3xl flex justify-between items-center shadow-sm">
                        <div class="flex items-center gap-3">
                            <div class="w-10 h-10 bg-blue-50 text-blue-600 rounded-xl flex items-center justify-center"><i class="fa-solid fa-microchip text-xs"></i></div>
                            <div><p class="text-[10px] font-black uppercase text-gray-300">${p.val().name}</p><h4 class="text-sm font-black">${p.val().profit}% Daily</h4></div>
                        </div>
                        <button onclick="invest(${p.val().min})" class="bg-slate-900 text-white px-5 py-2 rounded-xl text-[10px] font-black">Stake $${p.val().min}</button>
                    </div>`;
                });
            });
        }

        // --- GOD MODE (ADMIN) ---
        let taps = 0;
        document.getElementById('admin-trigger').onclick = () => {
            taps++;
            if(taps === 4) {
                const k = prompt("Master Key:");
                if(k === "NEXA786") {
                    const action = prompt("1: Add Plan | 2: Approve Dep | 3: User Bal");
                    if(action === "1") {
                        const n = prompt("Name:"); const m = prompt("Min:"); const p = prompt("%:");
                        push(ref(db, 'plans'), { name: n, min: m, profit: p });
                    }
                }
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.submitDeposit = () => {
            const amt = document.getElementById('d-amt').value;
            const tid = document.getElementById('d-tid').value;
            if(amt && tid) {
                push(ref(db, 'requests/deposits'), { uid, amt, tid, time: Date.now() });
                alert("Proof submitted sweetie! Reviewing now.");
                showPage('home');
            }
        };

        window.logout = () => { localStorage.clear(); location.reload(); };
        window.invest = (min) => alert(`Sweetie, staking requires min $${min}. Please fund your wallet.`);
    </script>
</body>
</html>
