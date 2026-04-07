<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Quantum Finance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        
        :root { --p: #2563eb; --s: #f8fafc; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; overflow-x: hidden; }

        /* Modern Blurs */
        .orb { position: absolute; border-radius: 50%; filter: blur(80px); z-index: -1; opacity: 0.4; }
        .glass { background: rgba(255, 255, 255, 0.75); backdrop-filter: blur(25px); border: 1px solid rgba(0,0,0,0.05); }
        
        /* Node Animation */
        .node-pulse { animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.1); opacity: 0.7; } 100% { transform: scale(1); opacity: 1; } }

        /* Floating Nav */
        .dock { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); width: 90%; max-width: 400px; 
                background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(15px); border-radius: 24px; padding: 12px;
                display: flex; justify-content: space-around; z-index: 2000; box-shadow: 0 20px 50px rgba(0,0,0,0.2); }
        .dock-item { color: #94a3b8; font-size: 10px; font-weight: 700; text-align: center; flex: 1; transition: 0.3s; }
        .dock-item.active { color: #3b82f6; transform: translateY(-5px); }
        .dock-item i { font-size: 20px; display: block; margin-bottom: 4px; }

        .btn-quantum { background: linear-gradient(135deg, #2563eb, #7c3aed); color: white; transition: 0.4s; border-radius: 18px; }
        .btn-quantum:hover { box-shadow: 0 15px 30px rgba(37, 99, 235, 0.3); transform: translateY(-2px); }
        
        .hidden { display: none; }
        ::-webkit-scrollbar { width: 0px; }
    </style>
</head>
<body class="bg-slate-50">

    <!-- Background Orbs -->
    <div class="orb w-64 h-64 bg-blue-200 top-10 -left-20"></div>
    <div class="orb w-80 h-80 bg-purple-100 bottom-20 -right-20"></div>

    <div class="max-w-md mx-auto min-h-screen relative pb-32">
        
        <!-- HEADER -->
        <header class="p-6 flex justify-between items-center sticky top-0 z-[100] glass mb-4">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center text-white font-black" id="app-logo">N</div>
                <h1 class="text-xl font-extrabold tracking-tighter">NEXA<span class="text-blue-600">.</span></h1>
            </div>
            <div id="top-actions" class="hidden flex gap-3">
                <div class="px-3 py-1 bg-green-50 text-green-600 rounded-full text-[10px] font-black border border-green-100 flex items-center gap-1">
                    <span class="w-1.5 h-1.5 bg-green-500 rounded-full animate-ping"></span> SECURE
                </div>
            </div>
        </header>

        <!-- PAGE: AUTH -->
        <div id="page-auth" class="px-8 pt-12 animate__animated animate__fadeIn">
            <h2 class="text-4xl font-black mb-2 tracking-tight">Digital <br><span class="text-blue-600">Quantum</span> Node.</h2>
            <p class="text-gray-400 text-sm mb-10 font-medium">Verified autonomous staking protocol.</p>
            
            <div class="space-y-4">
                <div class="glass p-2 rounded-3xl">
                    <input type="text" id="username" placeholder="Node Identity" class="w-full p-4 rounded-2xl bg-white border-none outline-none text-sm font-bold">
                </div>
                <div class="glass p-2 rounded-3xl">
                    <input type="password" id="password" placeholder="Access Key" class="w-full p-4 rounded-2xl bg-white border-none outline-none text-sm font-bold">
                </div>
                <button onclick="login()" class="w-full btn-quantum py-5 font-black uppercase tracking-widest text-sm shadow-2xl">Initialize Connection</button>
            </div>
        </div>

        <!-- PAGE: HOME -->
        <div id="page-home" class="hidden px-6 pt-4 animate__animated animate__fadeIn">
            <!-- Balance Card -->
            <div class="glass p-8 rounded-[40px] border-none shadow-2xl bg-gradient-to-br from-white to-blue-50 relative overflow-hidden">
                <div class="relative z-10">
                    <div class="flex justify-between items-start mb-6">
                        <p class="text-[10px] font-black text-gray-400 uppercase tracking-widest">Active Liquidity</p>
                        <i class="fa-solid fa-signal text-blue-600 text-xs node-pulse"></i>
                    </div>
                    <h2 id="balance" class="text-5xl font-black tracking-tighter text-slate-900">$0.00</h2>
                    <p class="text-[10px] text-green-500 font-bold mt-2">+2.4% Yield Today</p>
                    
                    <div class="grid grid-cols-2 gap-3 mt-8">
                        <button onclick="openModal('dep-modal')" class="btn-quantum py-3 text-xs font-black">STAKE</button>
                        <button onclick="openModal('wit-modal')" class="bg-slate-900 text-white py-3 rounded-[18px] text-xs font-black">HARVEST</button>
                    </div>
                </div>
                <i class="fa-solid fa-chart-pie absolute -right-4 -bottom-4 text-8xl opacity-[0.03]"></i>
            </div>

            <!-- Stats Bar -->
            <div class="grid grid-cols-3 gap-4 mt-8">
                <div class="text-center p-4 glass rounded-3xl">
                    <i class="fa-solid fa-link text-blue-500 mb-2"></i>
                    <p class="text-[9px] font-bold opacity-40">NODES</p>
                    <p class="text-sm font-black">128</p>
                </div>
                <div class="text-center p-4 glass rounded-3xl">
                    <i class="fa-solid fa-shield text-green-500 mb-2"></i>
                    <p class="text-[9px] font-bold opacity-40">SAFE</p>
                    <p class="text-sm font-black">100%</p>
                </div>
                <div class="text-center p-4 glass rounded-3xl">
                    <i class="fa-solid fa-users text-purple-500 mb-2"></i>
                    <p class="text-[9px] font-bold opacity-40">USER</p>
                    <p class="text-sm font-black">9k+</p>
                </div>
            </div>

            <h3 class="font-black text-lg mt-10 mb-6 flex items-center gap-2">
                <span class="w-1 h-6 bg-blue-600 rounded-full"></span> Available Nodes
            </h3>
            <div id="plans-grid" class="grid grid-cols-1 gap-4">
                <!-- Advanced Plans Go Here -->
            </div>
        </div>

        <!-- PAGE: ACCOUNT (Referrals & Support) -->
        <div id="page-account" class="hidden px-6 pt-4 animate__animated animate__fadeIn">
            <h3 class="font-black text-2xl mb-6">User Protocol</h3>
            <div class="glass p-6 rounded-[30px] mb-4">
                <p class="text-xs font-bold text-gray-400 mb-2 uppercase">Referral Link</p>
                <div class="flex gap-2">
                    <input type="text" readonly value="https://nexa.com/join?ref=786" class="flex-1 bg-white/50 p-3 rounded-xl text-[10px] border border-dashed border-gray-200">
                    <button class="bg-blue-600 text-white px-4 rounded-xl text-xs font-bold">COPY</button>
                </div>
            </div>
            <div class="p-6 bg-slate-900 rounded-[30px] text-white">
                <h4 class="font-bold text-sm mb-4">Need Assistance sweetie?</h4>
                <button class="w-full bg-white text-slate-900 py-3 rounded-xl font-black text-xs">CHAT WITH AI SUPPORT</button>
            </div>
        </div>

        <!-- DOCK NAVIGATION -->
        <nav id="dock" class="hidden dock">
            <button onclick="showPage('home')" class="dock-item active" id="nav-home"><i class="fa-solid fa-ghost"></i>Home</button>
            <button onclick="showPage('nodes')" class="dock-item" id="nav-nodes"><i class="fa-solid fa-microchip"></i>Nodes</button>
            <button onclick="showPage('account')" class="dock-item" id="nav-account"><i class="fa-solid fa-user-astronaut"></i>Profile</button>
            <button onclick="showPage('policy')" class="dock-item" id="nav-policy"><i class="fa-solid fa-fingerprint"></i>Secure</button>
        </nav>

        <!-- MODAL: DEPOSIT -->
        <div id="dep-modal" class="hidden fixed inset-0 bg-white z-[5000] p-8 animate__animated animate__slideInUp">
            <div class="flex justify-between mb-10">
                <h2 class="text-3xl font-black italic">TRANSFER</h2>
                <button onclick="closeModal('dep-modal')" class="text-2xl">&times;</button>
            </div>
            <div class="space-y-6">
                <div class="p-6 bg-blue-600 rounded-[30px] text-white shadow-xl">
                    <p class="text-[10px] font-bold opacity-60 uppercase mb-4">Official Gateways</p>
                    <p class="text-lg font-black">Easypaisa: 03379827882</p>
                    <p class="text-lg font-black mt-2">JazzCash: 03705519562</p>
                </div>
                <input type="number" id="d-amt" placeholder="Enter Amount ($)" class="w-full p-5 rounded-3xl bg-gray-50 border-none outline-none font-bold">
                <input type="text" id="d-tid" placeholder="Enter TID Code" class="w-full p-5 rounded-3xl bg-gray-50 border-none outline-none font-bold">
                <button onclick="submitDep()" class="w-full btn-quantum py-5 font-black shadow-lg">CONFIRM STAKING</button>
            </div>
        </div>

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

        // --- ENGINE ---
        window.showPage = (id) => {
            ['auth', 'home', 'account', 'policy'].forEach(p => document.getElementById('page-' + p)?.classList.add('hidden'));
            document.getElementById('page-' + id).classList.remove('hidden');
            document.querySelectorAll('.dock-item').forEach(d => d.classList.remove('active'));
            document.getElementById('nav-' + id)?.classList.add('active');
        };

        window.login = async () => {
            const user = document.getElementById('username').value;
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            
            const snap = await get(ref(db, 'users/' + uid));
            if(!snap.exists()) await set(ref(db, 'users/' + uid), { username: user, balance: 0, rank: 'Bronze' });
            
            localStorage.setItem('nexa_uid', uid);
            location.reload();
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            document.getElementById('page-auth').classList.add('hidden');
            document.getElementById('page-home').classList.remove('hidden');
            document.getElementById('dock').classList.remove('hidden');
            document.getElementById('top-actions').classList.remove('hidden');

            onValue(ref(db, 'users/' + uid), s => {
                const d = s.val();
                if(d) document.getElementById('balance').innerText = `$${d.balance.toFixed(2)}`;
            });

            onValue(ref(db, 'plans'), s => {
                const grid = document.getElementById('plans-grid');
                grid.innerHTML = "";
                s.forEach(p => {
                    const pd = p.val();
                    grid.innerHTML += `
                    <div class="glass p-6 rounded-[35px] flex justify-between items-center border-none shadow-sm mb-2">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-blue-100 rounded-2xl flex items-center justify-center text-blue-600">
                                <i class="fa-solid fa-microchip"></i>
                            </div>
                            <div>
                                <h4 class="font-black text-sm">${pd.name}</h4>
                                <p class="text-[10px] text-gray-400 font-bold">${pd.profit}% Daily Yield</p>
                            </div>
                        </div>
                        <button onclick="invest(${pd.min})" class="bg-slate-900 text-white px-5 py-2 rounded-xl text-[10px] font-black">STAKE $${pd.min}</button>
                    </div>`;
                });
            });
        }

        // --- GOD MODE (ADMIN) ---
        let taps = 0;
        document.getElementById('app-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const k = prompt("Quantum Master Key:");
                if(k === "NEXA786") {
                    const cmd = prompt("1: Add Plan | 2: Edit User Balance");
                    if(cmd === "1") {
                        const n = prompt("Name:"); const m = prompt("Min ($):"); const p = prompt("Profit %:");
                        push(ref(db, 'plans'), { name: n, min: m, profit: p });
                    } else if(cmd === "2") {
                        const target = prompt("User ID:"); const amt = prompt("New Balance:");
                        update(ref(db, 'users/' + target), { balance: parseFloat(amt) });
                    }
                }
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.openModal = (id) => document.getElementById(id).classList.remove('hidden');
        window.closeModal = (id) => document.getElementById(id).classList.add('hidden');
        window.submitDep = () => {
            const amt = document.getElementById('d-amt').value;
            const tid = document.getElementById('d-tid').value;
            if(amt && tid) {
                push(ref(db, 'requests/deposits'), { uid, amt, tid, status: 'pending' });
                alert("Quantum Staking Request Sent sweetie!");
                closeModal('dep-modal');
            }
        };

        window.invest = (min) => alert(`Sweetie, you need $${min} in your vault to unlock this node!`);
    </script>
</body>
</html>
