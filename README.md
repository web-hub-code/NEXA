<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Mining Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        /* UI Elements */
        .glass-panel { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border-radius: 28px; border: 1px solid rgba(255,255,255,0.3); }
        .card-elite { background: linear-gradient(145deg, #0052D1 0%, #001C48 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0, 82, 209, 0.4); position: relative; overflow: hidden; }
        .nexa-input { background: #f1f5f9; border-radius: 20px; padding: 18px; width: 100%; outline: none; border: 2px solid transparent; transition: 0.3s; font-weight: 700; font-size: 14px; }
        .nexa-input:focus { border-color: #0066ff; background: white; }
        
        /* Animation & Progress */
        .progress-fill { transition: width 1s linear; height: 100%; border-radius: 100px; }
        .timer-badge { background: rgba(0, 102, 255, 0.1); color: #0066ff; padding: 4px 12px; border-radius: 100px; font-size: 10px; font-weight: 800; border: 1px solid rgba(0, 102, 255, 0.2); }
        .hidden { display: none; }
        
        /* Plan Hover */
        .plan-card { transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .plan-card:hover { transform: translateY(-8px); box-shadow: 0 20px 40px -10px rgba(0,0,0,0.1); }
    </style>
</head>
<body class="pb-24">

    <!-- 1. AUTHENTICATION MODULE -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[50000] flex flex-col items-center justify-center p-8 overflow-y-auto">
        <div class="w-16 h-16 bg-blue-600 rounded-[22px] flex items-center justify-center text-white text-2xl mb-8 shadow-2xl rotate-3">
            <i class="fa-solid fa-shield-halved"></i>
        </div>
        
        <!-- Signup Form -->
        <div id="signup-box" class="w-full max-w-xs animate__animated animate__fadeIn">
            <h2 class="text-3xl font-black italic tracking-tighter mb-1">Create Account</h2>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-widest mb-8">Join the Sovereign Node Network</p>
            <div class="space-y-4">
                <input type="text" id="reg-user" placeholder="Your Name" class="nexa-input">
                <input type="email" id="reg-email" placeholder="Email Address" class="nexa-input">
                <input type="password" id="reg-pass" placeholder="Secure Password" class="nexa-input">
                <button onclick="handleAuth('signup')" class="w-full bg-blue-600 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Initialize Node</button>
            </div>
            <p class="mt-8 text-center text-xs font-bold text-slate-400">Member already? <span onclick="toggleAuth('login')" class="text-blue-600 cursor-pointer">Login Sweetie</span></p>
        </div>

        <!-- Login Form -->
        <div id="login-box" class="w-full max-w-xs hidden animate__animated animate__fadeIn">
            <h2 class="text-3xl font-black italic tracking-tighter mb-1">Welcome Back</h2>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-widest mb-8">Synchronize assets</p>
            <div class="space-y-4">
                <input type="email" id="log-email" placeholder="Email Address" class="nexa-input">
                <input type="password" id="log-pass" placeholder="Password" class="nexa-input">
                <button onclick="handleAuth('login')" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Secure Login</button>
            </div>
            <p class="mt-8 text-center text-xs font-bold text-slate-400">New to NEXA? <span onclick="toggleAuth('signup')" class="text-blue-600 cursor-pointer">Create Account</span></p>
        </div>
    </div>

    <!-- 2. MAIN APPLICATION -->
    <div id="app-content" class="hidden">
        <div class="max-w-md mx-auto px-6 pt-8">
            
            <!-- Dynamic Header -->
            <header class="flex justify-between items-center mb-10">
                <div class="flex items-center gap-4">
                    <div class="w-14 h-14 bg-slate-900 rounded-[20px] flex items-center justify-center text-white text-xl shadow-lg border-4 border-white">
                        <i class="fa-solid fa-user-ninja"></i>
                    </div>
                    <div>
                        <p id="greeting-msg" class="text-[10px] font-black uppercase text-slate-400 tracking-widest">Wait sweetie...</p>
                        <h2 id="display-username" class="text-2xl font-black italic tracking-tighter">Investor</h2>
                    </div>
                </div>
                <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500 shadow-sm"><i class="fa-solid fa-power-off"></i></button>
            </header>

            <!-- Page: Home -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-elite p-8 mb-10">
                    <div class="absolute -top-10 -right-10 w-32 h-32 bg-white/10 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-black opacity-60 uppercase tracking-[2px] mb-2">Total Node Balance</p>
                    <h2 id="user-bal" class="text-6xl font-black tracking-tighter mb-8">$0.00</h2>
                    <div class="grid grid-cols-2 gap-4">
                        <button onclick="showPage('deposit')" class="bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-xl">Deposit</button>
                        <button onclick="showPage('history')" class="bg-white/10 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest backdrop-blur-md">History</button>
                    </div>
                </div>

                <!-- Active Nodes Section -->
                <h3 class="text-xs font-black uppercase tracking-[3px] text-slate-400 mb-6 flex items-center gap-2">
                    <i class="fa-solid fa-bolt text-yellow-500 animate-pulse"></i> Live Mining
                </h3>
                <div id="active-nodes-container" class="space-y-4 mb-10">
                    <div class="glass-panel p-10 text-center border-dashed border-2 border-slate-200">
                        <p class="text-[10px] font-bold text-slate-300 uppercase">No nodes active sweetie</p>
                    </div>
                </div>

                <!-- Available Pools -->
                <h3 class="text-xs font-black uppercase tracking-[3px] text-slate-400 mb-6">Mining Pools</h3>
                <div class="space-y-4">
                    <!-- Starter -->
                    <div class="glass-panel p-6 plan-card bg-white flex justify-between items-center">
                        <div class="flex items-center gap-5">
                            <div class="w-14 h-14 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl shadow-inner"><i class="fa-solid fa-microchip"></i></div>
                            <div>
                                <p class="text-lg font-black italic tracking-tighter">Starter Alpha</p>
                                <p class="text-[10px] font-black text-green-500 uppercase">Yield: 2.5% / 24h</p>
                            </div>
                        </div>
                        <button onclick="buyPlan('Starter Alpha', 20, 2.5)" class="bg-slate-900 text-white px-5 py-3 rounded-xl text-[10px] font-black uppercase italic shadow-lg">Stake $20</button>
                    </div>
                    <!-- Pro -->
                    <div class="glass-panel p-6 plan-card bg-slate-900 text-white flex justify-between items-center border-none">
                        <div class="flex items-center gap-5">
                            <div class="w-14 h-14 bg-white/10 text-blue-400 rounded-2xl flex items-center justify-center text-xl backdrop-blur-xl"><i class="fa-solid fa-atom"></i></div>
                            <div>
                                <p class="text-lg font-black italic tracking-tighter">Pro Quantum</p>
                                <p class="text-[10px] font-black text-blue-400 uppercase">Yield: 5.0% / 24h</p>
                            </div>
                        </div>
                        <button onclick="buyPlan('Pro Quantum', 100, 5.0)" class="bg-blue-600 text-white px-5 py-3 rounded-xl text-[10px] font-black uppercase italic shadow-blue-500/50 shadow-lg">Stake $100</button>
                    </div>
                </div>
            </div>

            <!-- Page: History -->
            <div id="page-history" class="page-view hidden animate__animated animate__fadeIn">
                <div class="flex items-center gap-4 mb-8">
                    <button onclick="showPage('home')" class="w-12 h-12 glass-panel flex items-center justify-center text-slate-800"><i class="fa-solid fa-arrow-left"></i></button>
                    <h2 class="text-2xl font-black italic">Node Logs</h2>
                </div>
                <div id="history-list" class="space-y-4"></div>
            </div>

            <!-- Page: Deposit -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <div class="flex items-center gap-4 mb-8">
                    <button onclick="showPage('home')" class="w-12 h-12 glass-panel flex items-center justify-center"><i class="fa-solid fa-arrow-left"></i></button>
                    <h2 class="text-2xl font-black italic">Add Liquidity</h2>
                </div>
                <div class="glass-panel p-8 text-center bg-white shadow-xl">
                    <div class="w-20 h-20 bg-blue-50 rounded-full flex items-center justify-center mx-auto mb-6 text-blue-600 text-3xl"><i class="fa-solid fa-wallet"></i></div>
                    <p class="text-xs font-bold text-slate-400 mb-2 uppercase tracking-widest">USDT (BEP20) Address</p>
                    <div class="bg-slate-100 p-5 rounded-2xl break-all font-black text-[11px] text-slate-600 mb-8 border-2 border-dashed border-slate-200">
                        0x71C7656EC7ab88b098defB751B7401B5f6d8976F
                    </div>
                    <button onclick="alert('Screenshot sent to Admin sweetie!')" class="w-full bg-blue-600 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Confirm Payment</button>
                </div>
            </div>

        </div>
    </div>

    <!-- CORE LOGIC & FIREBASE -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // Your Config
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

        // -- Navigation --
        window.showPage = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            window.scrollTo(0,0);
        };

        window.toggleAuth = (type) => {
            document.getElementById('signup-box').classList.toggle('hidden', type === 'login');
            document.getElementById('login-box').classList.toggle('hidden', type === 'signup');
        };

        // -- Authentication --
        window.handleAuth = async (type) => {
            const email = document.getElementById(type === 'signup' ? 'reg-email' : 'log-email').value;
            const pass = document.getElementById(type === 'signup' ? 'reg-pass' : 'log-pass').value;
            const name = document.getElementById('reg-user').value;

            try {
                if(type === 'signup') {
                    const res = await createUserWithEmailAndPassword(auth, email, pass);
                    await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, email: email, joined: Date.now() });
                } else {
                    await signInWithEmailAndPassword(auth, email, pass);
                }
            } catch (err) { alert(err.message); }
        };

        window.logout = () => signOut(auth).then(() => location.reload());

        // -- User Initialization --
        onAuthStateChanged(auth, (user) => {
            if (user) {
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                initApp(user.uid);
            } else {
                document.getElementById('auth-module').classList.remove('hidden');
                document.getElementById('app-content').classList.add('hidden');
            }
        });

        function initApp(uid) {
            // Profile & Balance
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()){
                    const data = s.val();
                    document.getElementById('user-bal').innerText = `$${data.balance.toLocaleString(undefined, {minimumFractionDigits: 2})}`;
                    document.getElementById('display-username').innerText = data.username || "Investor";
                    const hr = new Date().getHours();
                    document.getElementById('greeting-msg').innerText = hr < 12 ? "Good Morning Sweetie" : "Good Evening Sweetie";
                }
            });

            // Live Updates
            setInterval(() => syncMiningNodes(uid), 1000);
            loadLogs(uid);
        }

        // -- Mining Engine --
        window.buyPlan = async (name, price, roi) => {
            const uid = auth.currentUser.uid;
            const snap = await get(ref(db, `users/${uid}`));
            const bal = snap.val().balance;

            if(bal < price) {
                alert("Balance low sweetie! Redirecting to deposit.");
                return showPage('deposit');
            }

            if(confirm(`Activate ${name} Node for $${price}?`)) {
                const now = Date.now();
                await update(ref(db, `users/${uid}`), { balance: bal - price });
                await push(ref(db, `active_plans/${uid}`), {
                    planName: name, invested: price, profit: (price * roi / 100).toFixed(2),
                    start: now, expiry: now + (24 * 60 * 60 * 1000)
                });
                await push(ref(db, `history/${uid}`), { type: 'Invest', plan: name, amount: price, date: new Date().toLocaleDateString() });
                alert("Boom! Mining started sweetie! 🚀");
            }
        };

        function syncMiningNodes(uid) {
            onValue(ref(db, `active_plans/${uid}`), (snap) => {
                const container = document.getElementById('active-nodes-container');
                if(!snap.exists()) return container.innerHTML = `<div class="glass-panel p-10 text-center opacity-40"><p class="text-[10px] font-bold uppercase">No nodes running</p></div>`;
                
                let html = "";
                snap.forEach(child => {
                    const p = child.val();
                    const timeLeft = p.expiry - Date.now();

                    if(timeLeft > 0) {
                        const h = Math.floor(timeLeft / 3600000);
                        const m = Math.floor((timeLeft % 3600000) / 60000);
                        const s = Math.floor((timeLeft % 60000) / 1000);
                        const prog = ((Date.now() - p.start) / (p.expiry - p.start)) * 100;
                        
                        html += `
                        <div class="glass-panel p-6 bg-white shadow-sm border-l-4 border-blue-600">
                            <div class="flex justify-between items-center mb-4"><span class="text-[11px] font-black uppercase text-blue-600 tracking-tighter">${p.planName}</span><span class="timer-badge"><i class="fa-regular fa-clock mr-1"></i> ${h}h ${m}m ${s}s</span></div>
                            <div class="flex justify-between items-end mb-2"><p class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Pending Profit</p><p class="text-sm font-black text-green-500">+$${p.profit}</p></div>
                            <div class="w-full h-1.5 bg-slate-100 rounded-full overflow-hidden"><div class="bg-blue-600 progress-fill" style="width:${prog}%"></div></div>
                        </div>`;
                    } else {
                        finishNode(uid, child.key, p);
                    }
                });
                container.innerHTML = html;
            }, { onlyOnce: true });
        }

        async function finishNode(uid, key, p) {
            const userSnap = await get(ref(db, `users/${uid}`));
            const newBal = userSnap.val().balance + parseFloat(p.profit) + parseFloat(p.invested); // Return Capital + Profit
            await update(ref(db, `users/${uid}`), { balance: newBal });
            await remove(ref(db, `active_plans/${uid}/${key}`));
            await push(ref(db, `history/${uid}`), { type: 'Profit', plan: p.planName, amount: p.profit, date: new Date().toLocaleDateString() });
        }

        function loadLogs(uid) {
            onValue(ref(db, `history/${uid}`), s => {
                const list = document.getElementById('history-list');
                list.innerHTML = "";
                if(!s.exists()) return list.innerHTML = "<p class='text-center py-10 text-slate-300 font-bold'>No logs found</p>";
                Object.values(s.val()).reverse().forEach(h => {
                    const isProfit = h.type === 'Profit';
                    list.innerHTML += `
                    <div class="glass-panel p-5 flex justify-between items-center bg-white shadow-sm">
                        <div class="flex items-center gap-4">
                            <div class="w-10 h-10 ${isProfit ? 'bg-green-50 text-green-600' : 'bg-slate-50 text-slate-500'} rounded-xl flex items-center justify-center"><i class="fa-solid ${isProfit ? 'fa-arrow-trend-up' : 'fa-receipt'}"></i></div>
                            <div><p class="text-[10px] font-black uppercase tracking-tighter">${h.type}</p><p class="text-[9px] font-bold text-slate-400">${h.date} • ${h.plan}</p></div>
                        </div>
                        <p class="font-black ${isProfit ? 'text-green-600' : 'text-slate-800'}">${isProfit ? '+' : '-'}$${h.amount}</p>
                    </div>`;
                });
            });
        }
    </script>
</body>
</html>
