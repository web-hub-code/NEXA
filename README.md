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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; -webkit-tap-highlight-color: transparent; }
        
        /* UI Elements */
        .glass-panel { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border-radius: 24px; border: 1px solid rgba(255,255,255,0.3); }
        .card-elite { background: linear-gradient(145deg, #0052D1 0%, #001C48 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0, 82, 209, 0.4); }
        .nexa-input { background: #f1f5f9; border-radius: 18px; padding: 16px; width: 100%; outline: none; border: 2px solid transparent; transition: 0.3s; font-weight: 700; }
        .nexa-input:focus { border-color: #0066ff; background: white; }
        
        /* Plan Cards */
        .plan-card { transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .plan-card:hover { transform: translateY(-8px); border-color: #0066ff; }
        .timer-badge { background: rgba(0, 102, 255, 0.1); color: #0066ff; padding: 4px 10px; border-radius: 100px; font-size: 10px; font-weight: 800; }
        .progress-fill { transition: width 1s linear; }
        .hidden { display: none; }
    </style>
</head>
<body class="pb-24">

    <!-- 1. AUTHENTICATION MODULE -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[5000] flex flex-col items-center justify-center p-8 overflow-y-auto">
        <div class="w-16 h-16 bg-blue-600 rounded-2xl flex items-center justify-center text-white text-2xl mb-8 shadow-xl rotate-3">
            <i class="fa-solid fa-shield-halved"></i>
        </div>
        
        <div id="signup-box" class="w-full max-w-xs animate__animated animate__fadeIn">
            <h2 class="text-3xl font-black italic tracking-tighter mb-1">Create Account</h2>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-widest mb-8">Join the Sovereign Node Network</p>
            <div class="space-y-3">
                <input type="text" id="reg-user" placeholder="Full Name" class="nexa-input">
                <input type="email" id="reg-email" placeholder="Email Address" class="nexa-input">
                <input type="password" id="reg-pass" placeholder="Password" class="nexa-input">
                <button onclick="handleAuth('signup')" class="w-full bg-blue-600 text-white p-4 rounded-xl font-black uppercase text-xs tracking-widest shadow-lg">Initialize Node</button>
            </div>
            <p class="mt-8 text-center text-xs font-bold text-slate-400">Already a member? <span onclick="toggleAuth('login')" class="text-blue-600 cursor-pointer">Login</span></p>
        </div>

        <div id="login-box" class="w-full max-w-xs hidden animate__animated animate__fadeIn">
            <h2 class="text-3xl font-black italic tracking-tighter mb-1">Welcome Back</h2>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-widest mb-8">Sync your assets</p>
            <div class="space-y-3">
                <input type="email" id="log-email" placeholder="Email Address" class="nexa-input">
                <input type="password" id="log-pass" placeholder="Password" class="nexa-input">
                <button onclick="handleAuth('login')" class="w-full bg-slate-900 text-white p-4 rounded-xl font-black uppercase text-xs tracking-widest shadow-lg">Secure Login</button>
            </div>
            <p class="mt-8 text-center text-xs font-bold text-slate-400">New here? <span onclick="toggleAuth('signup')" class="text-blue-600 cursor-pointer">Create Account</span></p>
        </div>
    </div>

    <!-- 2. MAIN APP CONTENT -->
    <div id="app-content" class="hidden">
        <div class="max-w-md mx-auto px-6 pt-8">
            
            <!-- Header -->
            <div id="p-header" class="flex justify-between items-center mb-8">
                <div class="flex items-center gap-3">
                    <div class="w-12 h-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white shadow-lg">
                        <i class="fa-solid fa-user-astronaut"></i>
                    </div>
                    <div>
                        <p id="greeting-msg" class="text-[10px] font-black uppercase text-slate-400">Syncing...</p>
                        <h2 id="display-username" class="text-xl font-black italic">Investor</h2>
                    </div>
                </div>
                <button onclick="logout()" class="w-10 h-10 glass-panel flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></button>
            </div>

            <!-- Page: HOME -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-elite p-8 mb-8 relative overflow-hidden">
                    <p class="text-[10px] font-black opacity-60 uppercase tracking-widest mb-1">Available Liquidity</p>
                    <h2 id="user-bal" class="text-5xl font-black tracking-tighter mb-6">$0.00</h2>
                    <div class="grid grid-cols-2 gap-2">
                        <button onclick="showPage('deposit')" class="bg-white text-blue-600 py-3 rounded-xl text-[10px] font-black uppercase tracking-widest">Deposit</button>
                        <button onclick="showPage('history')" class="bg-white/10 py-3 rounded-xl text-[10px] font-black uppercase tracking-widest">History</button>
                    </div>
                </div>

                <!-- Active Mining Section -->
                <h3 class="text-xs font-black uppercase tracking-[2px] text-slate-400 mb-4">Active Mining Nodes</h3>
                <div id="active-nodes-container" class="space-y-4 mb-8">
                    <div class="glass-panel p-6 text-center opacity-40"><p class="text-[10px] font-bold">No Active Nodes</p></div>
                </div>

                <!-- Available Plans -->
                <h3 class="text-xs font-black uppercase tracking-[2px] text-slate-400 mb-4">Available Pools</h3>
                <div class="space-y-4" id="plans-list">
                    <!-- Starter Plan -->
                    <div class="glass-panel p-5 plan-card bg-white flex justify-between items-center">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-xl flex items-center justify-center"><i class="fa-solid fa-microchip"></i></div>
                            <div>
                                <p class="text-sm font-black">Starter Alpha</p>
                                <p class="text-[9px] font-bold text-green-500 uppercase">Yield: 2.5% Daily</p>
                            </div>
                        </div>
                        <button onclick="buyPlan('Starter Alpha', 20, 2.5)" class="bg-slate-900 text-white px-4 py-2 rounded-lg text-[9px] font-black uppercase italic">Stake $20</button>
                    </div>

                    <!-- Pro Plan -->
                    <div class="glass-panel p-5 plan-card bg-slate-900 text-white flex justify-between items-center">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-white/10 text-blue-400 rounded-xl flex items-center justify-center"><i class="fa-solid fa-bolt"></i></div>
                            <div>
                                <p class="text-sm font-black">Pro Quantum</p>
                                <p class="text-[9px] font-bold text-blue-400 uppercase">Yield: 5.0% Daily</p>
                            </div>
                        </div>
                        <button onclick="buyPlan('Pro Quantum', 100, 5.0)" class="bg-blue-600 text-white px-4 py-2 rounded-lg text-[9px] font-black uppercase italic">Stake $100</button>
                    </div>
                </div>
            </div>

            <!-- Page: HISTORY -->
            <div id="page-history" class="page-view hidden animate__animated animate__fadeIn">
                <div class="flex items-center gap-4 mb-6">
                    <button onclick="showPage('home')" class="w-10 h-10 glass-panel flex items-center justify-center"><i class="fa-solid fa-arrow-left"></i></button>
                    <h2 class="text-xl font-black italic">Transaction Logs</h2>
                </div>
                <div id="history-list" class="space-y-3"></div>
            </div>

            <!-- Page: DEPOSIT (Simple Example) -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <div class="flex items-center gap-4 mb-6">
                    <button onclick="showPage('home')" class="w-10 h-10 glass-panel flex items-center justify-center"><i class="fa-solid fa-arrow-left"></i></button>
                    <h2 class="text-xl font-black italic">Deposit Funds</h2>
                </div>
                <div class="glass-panel p-8 text-center">
                    <p class="text-xs font-bold text-slate-400 mb-4 uppercase">Send USDT (BEP20) to address:</p>
                    <p class="text-[10px] font-black bg-slate-100 p-4 rounded-xl break-all">0x71C7656EC7ab88b098defB751B7401B5f6d8976F</p>
                    <button onclick="alert('Screenshot sent to Admin!')" class="mt-6 w-full bg-blue-600 text-white p-4 rounded-xl font-black uppercase text-xs">I Have Paid</button>
                </div>
            </div>

        </div>
    </div>

    <!-- FIREBASE & LOGIC -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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

        // --- NAVIGATION ---
        window.showPage = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
        };

        window.toggleAuth = (type) => {
            document.getElementById('signup-box').classList.toggle('hidden', type === 'login');
            document.getElementById('login-box').classList.toggle('hidden', type === 'signup');
        };

        // --- AUTHENTICATION ---
        window.handleAuth = async (type) => {
            const email = document.getElementById(type === 'signup' ? 'reg-email' : 'log-email').value;
            const pass = document.getElementById(type === 'signup' ? 'reg-pass' : 'log-pass').value;
            const user = document.getElementById('reg-user').value;

            try {
                if(type === 'signup') {
                    const res = await createUserWithEmailAndPassword(auth, email, pass);
                    await set(ref(db, `users/${res.user.uid}`), { username: user, balance: 0, email: email, joined: Date.now() });
                } else {
                    await signInWithEmailAndPassword(auth, email, pass);
                }
            } catch (err) { alert(err.message); }
        };

        window.logout = () => signOut(auth).then(() => location.reload());

        // --- CORE SYSTEM ---
        onAuthStateChanged(auth, (user) => {
            if (user) {
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                initUserSystem(user.uid);
            } else {
                document.getElementById('auth-module').classList.remove('hidden');
                document.getElementById('app-content').classList.add('hidden');
            }
        });

        function initUserSystem(uid) {
            // Load User Profile & Balance
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()){
                    const data = s.val();
                    document.getElementById('user-bal').innerText = `$${data.balance.toFixed(2)}`;
                    document.getElementById('display-username').innerText = data.username;
                    const hours = new Date().getHours();
                    document.getElementById('greeting-msg').innerText = hours < 12 ? "Good Morning Sweetie" : "Good Evening Sweetie";
                }
            });

            // Start Live Timers
            setInterval(() => updateLiveTimers(uid), 1000);
            loadHistory(uid);
        }

        // --- MINING & PLANS ---
        window.buyPlan = async (name, price, roi) => {
            const uid = auth.currentUser.uid;
            const snap = await get(ref(db, `users/${uid}`));
            const bal = snap.val().balance;

            if(bal < price) return alert("Balance low sweetie! Please deposit.");

            if(confirm(`Activate ${name} Node for $${price}?`)) {
                const now = Date.now();
                await update(ref(db, `users/${uid}`), { balance: bal - price });
                await push(ref(db, `active_plans/${uid}`), {
                    planName: name, invested: price, profit: (price * roi / 100).toFixed(2),
                    start: now, expiry: now + (24 * 60 * 60 * 1000)
                });
                await push(ref(db, `history/${uid}`), { type: 'Investment', plan: name, amount: price, date: new Date().toLocaleDateString() });
                alert("Mining Started! 🚀");
            }
        };

        function updateLiveTimers(uid) {
            onValue(ref(db, `active_plans/${uid}`), (snap) => {
                const container = document.getElementById('active-nodes-container');
                if(!snap.exists()) return container.innerHTML = `<div class="glass-panel p-6 text-center opacity-40"><p class="text-[10px] font-bold uppercase">No Active Mining</p></div>`;
                
                let html = "";
                snap.forEach(child => {
                    const plan = child.val();
                    const timeLeft = plan.expiry - Date.now();

                    if(timeLeft > 0) {
                        const h = Math.floor(timeLeft / 3600000);
                        const m = Math.floor((timeLeft % 3600000) / 60000);
                        const s = Math.floor((timeLeft % 60000) / 1000);
                        const prog = ((Date.now() - plan.start) / (plan.expiry - plan.start)) * 100;
                        
                        html += `
                        <div class="glass-panel p-5 bg-white border-l-4 border-blue-600">
                            <div class="flex justify-between mb-3"><span class="text-[10px] font-black uppercase text-blue-600">${plan.planName}</span><span class="timer-badge">${h}h ${m}m ${s}s</span></div>
                            <div class="flex justify-between items-end mb-2"><p class="text-[10px] font-black text-green-500">+$${plan.profit}</p><p class="text-[8px] font-bold text-slate-400">${prog.toFixed(1)}%</p></div>
                            <div class="w-full h-1 bg-slate-100 rounded-full overflow-hidden"><div class="h-full bg-blue-600 progress-fill" style="width:${prog}%"></div></div>
                        </div>`;
                    } else {
                        finalizePlan(uid, child.key, plan);
                    }
                });
                container.innerHTML = html;
            }, { onlyOnce: true });
        }

        async function finalizePlan(uid, key, plan) {
            const userSnap = await get(ref(db, `users/${uid}`));
            const newBal = userSnap.val().balance + parseFloat(plan.profit);
            await update(ref(db, `users/${uid}`), { balance: newBal });
            await remove(ref(db, `active_plans/${uid}/${key}`));
            await push(ref(db, `history/${uid}`), { type: 'Profit', plan: plan.planName, amount: plan.profit, date: new Date().toLocaleDateString() });
        }

        function loadHistory(uid) {
            onValue(ref(db, `history/${uid}`), s => {
                const list = document.getElementById('history-list');
                list.innerHTML = "";
                if(!s.exists()) return;
                Object.values(s.val()).reverse().forEach(h => {
                    const isProfit = h.type === 'Profit';
                    list.innerHTML += `
                    <div class="glass-panel p-4 flex justify-between items-center bg-white">
                        <div class="flex items-center gap-3">
                            <div class="w-8 h-8 ${isProfit ? 'bg-green-50 text-green-600' : 'bg-red-50 text-red-600'} rounded-lg flex items-center justify-center text-[10px]"><i class="fa-solid fa-wallet"></i></div>
                            <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[8px] font-bold text-slate-400">${h.date}</p></div>
                        </div>
                        <p class="text-xs font-black ${isProfit ? 'text-green-600' : 'text-red-600'}">${isProfit ? '+' : '-'}$${h.amount}</p>
                    </div>`;
                });
            });
        }
    </script>
</body>
</html>
