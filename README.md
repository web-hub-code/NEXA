<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | Institutional Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        
        :root { --primary: #2563eb; --accent: #3b82f6; --bg: #F8FAFC; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #1e293b; overflow-x: hidden; }

        /* Premium Glassmorphism */
        .glass { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.5); }
        .trust-card { border-radius: 28px; transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); border: 1px solid rgba(0,0,0,0.03); }
        .trust-card:active { transform: scale(0.97); }

        /* Animated Background & UI */
        .premium-gradient { background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%); }
        .live-dot { height: 6px; width: 6px; background: #22c55e; border-radius: 50%; display: inline-block; box-shadow: 0 0 10px #22c55e; animation: pulse 1.5s infinite; }
        
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
        
        /* Smooth Navigation */
        .nav-active { color: var(--primary) !important; position: relative; }
        .nav-active::after { content: ''; position: absolute; top: -10px; left: 50%; transform: translateX(-50%); width: 20px; height: 3px; background: var(--primary); border-radius: 10px; }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 0px; }
        .history-item { border-left: 3px solid #e2e8f0; transition: 0.3s; }
        .history-item.approved { border-left-color: #22c55e; }
        .history-item.pending { border-left-color: #f59e0b; }
    </style>
</head>
<body class="pb-24">

    <!-- LOGIN SCREEN -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-8">
        <div class="absolute top-0 right-0 w-64 h-64 bg-blue-50 rounded-full -mr-32 -mt-32 blur-3xl opacity-50"></div>
        <div class="w-20 h-20 premium-gradient rounded-[2rem] flex items-center justify-center text-white text-4xl mb-6 shadow-2xl shadow-blue-200 rotate-12">
            <i class="fa-solid fa-cube"></i>
        </div>
        <h1 class="text-2xl font-extrabold tracking-tight mb-1">NEXA <span class="text-blue-600">PRO</span></h1>
        <p class="text-[9px] font-black text-slate-400 uppercase tracking-[4px] mb-10 text-center">Future of Cloud Mining</p>
        
        <div class="w-full max-w-xs space-y-4">
            <div class="relative">
                <i class="fa-solid fa-user absolute left-4 top-4 text-slate-300 text-xs"></i>
                <input type="text" id="user-name" placeholder="Full Member Name" class="w-full p-4 pl-12 rounded-2xl bg-slate-50 border border-slate-100 outline-none text-sm font-semibold focus:border-blue-300 transition-all">
            </div>
            <div class="relative">
                <i class="fa-solid fa-lock absolute left-4 top-4 text-slate-300 text-xs"></i>
                <input type="password" id="admin-key" placeholder="Access Key (Optional)" class="w-full p-4 pl-12 rounded-2xl bg-slate-50 border border-slate-100 outline-none text-sm font-semibold focus:border-blue-300 transition-all">
            </div>
            <button onclick="handleLogin()" class="w-full premium-gradient text-white p-5 rounded-2xl font-bold uppercase text-[10px] tracking-widest shadow-xl shadow-blue-200 active:scale-95 transition-all">Authenticate Member</button>
        </div>
    </div>

    <!-- MAIN APP -->
    <div id="app" class="hidden">
        <!-- Header -->
        <header class="p-6 flex justify-between items-center glass sticky top-0 z-50">
            <div>
                <p class="text-[8px] font-black text-blue-600 uppercase tracking-widest flex items-center mb-1"><span class="live-dot mr-2"></span> System Online</p>
                <h3 id="display-name" class="text-base font-extrabold text-slate-800">--</h3>
            </div>
            <div class="flex gap-3">
                <button onclick="nav('history')" class="w-10 h-10 rounded-xl bg-slate-100 text-slate-500 flex items-center justify-center"><i class="fa-solid fa-clock-rotate-left text-xs"></i></button>
                <button onclick="logout()" class="w-10 h-10 rounded-xl bg-red-50 text-red-400 flex items-center justify-center"><i class="fa-solid fa-power-off text-xs"></i></button>
            </div>
        </header>

        <!-- PAGE: HOME -->
        <main id="page-home" class="page-content px-6 py-6 space-y-6">
            <div class="trust-card premium-gradient p-8 text-white relative overflow-hidden shadow-2xl shadow-blue-200">
                <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-white/10 rounded-full blur-2xl"></div>
                <p class="text-[9px] font-bold text-blue-100 uppercase tracking-[3px] mb-2 opacity-80">Institutional Balance</p>
                <h2 id="user-bal" class="text-4xl font-extrabold">$0.00</h2>
                <p id="pkr-bal" class="text-xs font-medium text-blue-100 mt-1 opacity-70">≈ Rs. 0.00</p>
                
                <div class="flex gap-3 mt-8">
                    <button onclick="nav('deposit')" class="flex-1 bg-white text-blue-600 py-3.5 rounded-2xl text-[9px] font-black uppercase shadow-lg">Add Capital</button>
                    <button onclick="nav('withdraw')" class="flex-1 bg-blue-400/30 backdrop-blur text-white py-3.5 rounded-2xl text-[9px] font-black uppercase border border-white/20">Payout</button>
                </div>
            </div>

            <!-- STATS GRID -->
            <div class="grid grid-cols-2 gap-4">
                <div class="trust-card bg-white p-5 border border-slate-100">
                    <div class="w-8 h-8 rounded-lg bg-blue-50 text-blue-600 flex items-center justify-center mb-3"><i class="fa-solid fa-microchip text-xs"></i></div>
                    <p class="text-[8px] font-bold text-slate-400 uppercase tracking-widest">Active Rigs</p>
                    <p id="active-plans" class="text-xl font-extrabold text-slate-800">0</p>
                </div>
                <div class="trust-card bg-white p-5 border border-slate-100">
                    <div class="w-8 h-8 rounded-lg bg-indigo-50 text-indigo-600 flex items-center justify-center mb-3"><i class="fa-solid fa-users text-xs"></i></div>
                    <p class="text-[8px] font-bold text-slate-400 uppercase tracking-widest">Team Size</p>
                    <p id="team-count" class="text-xl font-extrabold text-slate-800">0</p>
                </div>
            </div>

            <!-- PROMO CARD -->
            <div class="trust-card bg-amber-50 p-6 border border-amber-100">
                <h4 class="text-[10px] font-black text-amber-700 uppercase tracking-widest mb-3">Redeem Partnership Voucher</h4>
                <div class="flex gap-2">
                    <input id="promo-input" placeholder="ENTER CODE" class="flex-1 p-3.5 rounded-xl bg-white text-[10px] uppercase font-bold outline-none border border-amber-200">
                    <button onclick="submitPromo()" class="bg-amber-500 text-white px-6 rounded-xl text-[9px] font-black uppercase">Claim</button>
                </div>
                <p id="promo-msg" class="text-[8px] mt-2 font-bold text-amber-600"></p>
            </div>

            <!-- LIVE ACTIVITY -->
            <div class="py-2 overflow-hidden">
                <div class="flex gap-8 whitespace-nowrap animate-marquee">
                    <div class="text-[9px] font-bold text-slate-400 uppercase"><span class="text-green-500">●</span> Ali just withdrew $55.00</div>
                    <div class="text-[9px] font-bold text-slate-400 uppercase"><span class="text-green-500">●</span> Sana earned $12.50 bonus</div>
                    <div class="text-[9px] font-bold text-slate-400 uppercase"><span class="text-green-500">●</span> Rig v.15 Activated by User_99</div>
                </div>
            </div>
        </main>

        <!-- PAGE: HISTORY (NEW) -->
        <main id="page-history" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-xl font-extrabold text-slate-800 tracking-tight">Financial Records</h2>
            <div id="history-container" class="space-y-3 pb-10">
                <!-- Records injected here -->
            </div>
        </main>

        <!-- PAGE: NODES -->
        <main id="page-nodes" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-xl font-extrabold text-slate-800 tracking-tight">Mining Clusters</h2>
            <div id="nodes-container" class="space-y-4 pb-10"></div>
        </main>

        <!-- PAGE: DEPOSIT -->
        <main id="page-deposit" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-xl font-extrabold text-slate-800 tracking-tight">Capital Funding</h2>
            <div class="space-y-4">
                <div onclick="openPay('JazzCash','03705519562')" class="trust-card bg-white p-6 flex justify-between items-center border-l-[6px] border-red-500 shadow-sm">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-red-50 rounded-2xl flex items-center justify-center text-red-500 text-xl font-black italic">J</div>
                        <div><p class="text-[11px] font-black uppercase">JazzCash Official</p><p class="text-[8px] text-slate-400 font-bold">Limit: $1 - $5000</p></div>
                    </div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="openPay('Easypaisa','03332637235')" class="trust-card bg-white p-6 flex justify-between items-center border-l-[6px] border-green-500 shadow-sm">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-green-50 rounded-2xl flex items-center justify-center text-green-500 text-xl font-black italic">E</div>
                        <div><p class="text-[11px] font-black uppercase">Easypaisa Fast</p><p class="text-[8px] text-slate-400 font-bold">Limit: $1 - $5000</p></div>
                    </div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
            </div>
        </main>

        <!-- PAGE: WITHDRAW -->
        <main id="page-withdraw" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-xl font-extrabold text-slate-800 tracking-tight">Withdraw Funds</h2>
            <div class="trust-card bg-white p-7 space-y-5 shadow-sm border border-slate-100">
                <div class="space-y-2">
                    <label class="text-[9px] font-black text-slate-400 uppercase ml-1">Payout Method</label>
                    <select id="w-method" class="w-full p-4 rounded-2xl bg-slate-50 border-none outline-none text-sm font-bold">
                        <option value="JazzCash">JazzCash</option>
                        <option value="Easypaisa">Easypaisa</option>
                    </select>
                </div>
                <div class="space-y-2">
                    <label class="text-[9px] font-black text-slate-400 uppercase ml-1">Account Number</label>
                    <input type="text" id="w-num" placeholder="03XXXXXXXXX" class="w-full p-4 rounded-2xl bg-slate-50 border-none outline-none text-sm font-bold">
                </div>
                <div class="space-y-2">
                    <label class="text-[9px] font-black text-slate-400 uppercase ml-1">Amount ($)</label>
                    <input type="number" id="w-amt" placeholder="Min $1" class="w-full p-4 rounded-2xl bg-slate-50 border-none outline-none text-sm font-bold">
                </div>
                <button onclick="submitWithdraw()" class="w-full premium-gradient text-white p-5 rounded-2xl font-black uppercase text-[10px] tracking-[2px] shadow-lg">Process Payout</button>
            </div>
        </main>

        <!-- PAGE: ADMIN -->
        <main id="page-admin" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-xl font-extrabold text-red-600 uppercase italic">Admin Authority</h2>
            <div class="grid grid-cols-2 gap-2">
                <button onclick="loadAdmin('dep')" class="bg-blue-600 text-white p-3 rounded-xl text-[9px] font-black">DEPOSITS</button>
                <button onclick="loadAdmin('wit')" class="bg-slate-800 text-white p-3 rounded-xl text-[9px] font-black">PAYOUTS</button>
                <button onclick="loadAdminPromo()" class="bg-amber-500 text-white p-3 rounded-xl text-[9px] font-black">VOUCHERS</button>
                <button onclick="loadUsers()" class="bg-indigo-600 text-white p-3 rounded-xl text-[9px] font-black">MEMBERS</button>
            </div>
            <div id="admin-list" class="space-y-4"></div>
        </main>

        <!-- NAVIGATION -->
        <nav class="fixed bottom-0 left-0 right-0 h-24 glass border-t border-white/50 flex justify-around items-center z-50 px-4">
            <div onclick="nav('home')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400 transition-all" id="btn-home"><i class="fa-solid fa-house-chimney text-lg"></i><span class="text-[7px] font-black mt-1 uppercase">Vault</span></div>
            <div onclick="nav('nodes')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400 transition-all" id="btn-nodes"><i class="fa-solid fa-microchip text-lg"></i><span class="text-[7px] font-black mt-1 uppercase">Rigs</span></div>
            <div onclick="nav('withdraw')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400 transition-all" id="btn-withdraw"><i class="fa-solid fa-wallet text-lg"></i><span class="text-[7px] font-black mt-1 uppercase">Payout</span></div>
            <div onclick="nav('admin')" class="nav-item hidden flex flex-col items-center flex-1 py-3 text-red-500 animate-pulse" id="btn-admin"><i class="fa-solid fa-user-shield text-lg"></i><span class="text-[7px] font-black mt-1 uppercase">Root</span></div>
        </nav>
    </div>

    <!-- MODALS & SCRIPT (FIREBASE) -->
    <div id="pay-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-md z-[10000] hidden flex items-center justify-center p-8">
        <div class="trust-card bg-white p-8 w-full max-w-sm shadow-2xl">
            <h3 id="m-gw" class="text-lg font-black text-blue-600 mb-1 uppercase italic tracking-tighter">--</h3>
            <p class="text-[10px] text-slate-400 font-bold mb-6">Send funds to the account below</p>
            <div class="bg-slate-50 p-5 rounded-2xl flex justify-between items-center mb-6 border border-slate-100" onclick="copyNum()">
                <span id="m-num" class="font-extrabold text-slate-900 tracking-widest">--</span>
                <i class="fa-solid fa-copy text-slate-300"></i>
            </div>
            <div class="space-y-4">
                <input type="number" id="m-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl bg-slate-50 border-none outline-none text-sm font-bold">
                <input type="text" id="m-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-xl bg-slate-50 border-none outline-none text-sm font-bold">
                <button onclick="submitDep()" class="w-full premium-gradient text-white p-5 rounded-2xl font-black uppercase text-[10px]">Verify Payment</button>
                <button onclick="closeModal()" class="w-full text-slate-400 text-[8px] font-bold uppercase tracking-widest">Discard</button>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
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
        const RATE = 285;
        let userData = null, uid = "";

        // LOGIN WITH ANIMATION
        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return alert("Sweetie, enter your name!");
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const s = await get(ref(db, `users/${uid}`));
            if(!s.exists()) {
                await set(ref(db, `users/${uid}`), { username: name, balance: 0, role: (key==="sweetie786"?"admin":"user"), plans: 0, team: 0 });
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
                    document.getElementById('display-name').innerText = userData.username;
                    animateValue("user-bal", 0, userData.balance || 0, 1000, "$");
                    document.getElementById('pkr-bal').innerText = `≈ Rs. ${(userData.balance * RATE).toLocaleString()}`;
                    document.getElementById('active-plans').innerText = userData.plans || 0;
                    document.getElementById('team-count').innerText = userData.team || 0;
                    if(userData.role === 'admin') document.getElementById('btn-admin').classList.remove('hidden');
                });
                loadNodes(); loadHistory(); nav('home');
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // ANIMATED NUMBERS
        function animateValue(id, start, end, duration, prefix="") {
            const obj = document.getElementById(id);
            let startTimestamp = null;
            const step = (timestamp) => {
                if (!startTimestamp) startTimestamp = timestamp;
                const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                obj.innerHTML = prefix + (progress * (end - start) + start).toFixed(2);
                if (progress < 1) window.requestAnimationFrame(step);
            };
            window.requestAnimationFrame(step);
        }

        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`btn-${id}`)?.classList.add('nav-active');
            if(id === 'history') loadHistory();
        };

        // NODES & RIGS
        function loadNodes() {
            const con = document.getElementById('nodes-container');
            con.innerHTML = "";
            for(let i=1; i<=15; i++) con.innerHTML += createNode(`Titan Cluster v.${i}`, i*5, 'blue');
            [500, 1000, 2500, 5000].forEach((c, idx) => con.innerHTML += createNode(`VIP Institutional ${idx+1}`, c, 'indigo'));
        }
        function createNode(n, c, col) {
            return `<div class="trust-card bg-white p-5 flex justify-between items-center shadow-sm border border-slate-100">
                <div class="flex items-center gap-4">
                    <div class="w-12 h-12 bg-${col}-50 rounded-2xl flex items-center justify-center text-${col}-600"><i class="fa-solid fa-bolt-lightning text-xs"></i></div>
                    <div><p class="text-[10px] font-black uppercase text-slate-800">${n}</p><p class="text-[8px] text-slate-400 font-bold">$${c} • Rs. ${c*RATE}</p></div>
                </div>
                <button onclick="buyPlan(${c})" class="bg-slate-50 text-${col}-600 px-5 py-2.5 rounded-xl text-[8px] font-black uppercase border border-slate-100 active:scale-95 transition-all">Deploy</button>
            </div>`;
        }
        window.buyPlan = async (c) => {
            if(userData.balance < c) return alert("Sweetie, insufficient capital!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - c, plans: (userData.plans || 0) + 1 });
            alert("Rig Deployment Successful!");
        };

        // HISTORY SYSTEM (NEW)
        window.loadHistory = () => {
            const con = document.getElementById('history-container');
            con.innerHTML = "<p class='text-center text-[9px] text-slate-400 font-bold uppercase'>Synchronizing Records...</p>";
            
            // Get combined history from deposits & withdraws
            onValue(ref(db), (snapshot) => {
                const data = snapshot.val();
                let list = [];
                if(data.deposits) Object.values(data.deposits).forEach(d => { if(d.uid === uid) list.push({...d, type: 'Deposit'}); });
                if(data.withdraws) Object.values(data.withdraws).forEach(w => { if(w.uid === uid) list.push({...w, type: 'Withdraw'}); });
                
                con.innerHTML = list.length ? "" : "<div class='text-center py-20 text-slate-300'><i class='fa-solid fa-folder-open text-3xl mb-3'></i><p class='text-[9px] font-bold uppercase'>No Activity Found</p></div>";
                list.sort((a,b) => b.time - a.time).forEach(item => {
                    con.innerHTML += `<div class="history-item ${item.status} trust-card bg-white p-4 shadow-sm">
                        <div class="flex justify-between items-center">
                            <div>
                                <p class="text-[9px] font-black uppercase ${item.type==='Deposit'?'text-blue-600':'text-red-500'}">${item.type}</p>
                                <p class="text-[7px] text-slate-400 font-bold">${item.method || 'Internal'}</p>
                            </div>
                            <div class="text-right">
                                <p class="text-sm font-extrabold text-slate-800">$${item.amount.toFixed(2)}</p>
                                <p class="text-[7px] font-black uppercase ${item.status==='approved'?'text-green-500':'text-amber-500'}">${item.status}</p>
                            </div>
                        </div>
                    </div>`;
                });
            });
        };

        // ADMIN FUNCTIONS
        window.loadAdmin = (tab) => {
            const path = tab === 'dep' ? 'deposits' : 'withdraws';
            onValue(ref(db, path), s => {
                const con = document.getElementById('admin-list'); con.innerHTML = "";
                s.forEach(c => {
                    const d = c.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `<div class="trust-card p-5 bg-slate-50 border-none shadow-sm">
                            <p class="font-black text-slate-800 text-[10px] uppercase">${d.username} | <span class="text-blue-600">$${d.amount}</span></p>
                            <p class="text-slate-400 text-[8px] font-bold mb-4">${tab==='dep'?'TID: '+d.tid : 'No: '+d.number}</p>
                            <button onclick="approveAction('${path}', '${c.key}', '${d.uid}', ${d.amount}, '${tab}')" class="w-full premium-gradient text-white py-3 rounded-xl font-black uppercase text-[8px]">Authorize</button>
                        </div>`;
                    }
                });
            });
        };

        // Standard Utility Functions
        window.openPay = (gw, n) => { document.getElementById('m-gw').innerText = gw; document.getElementById('m-num').innerText = n; document.getElementById('pay-modal').classList.remove('hidden'); };
        window.closeModal = () => document.getElementById('pay-modal').classList.add('hidden');
        window.submitDep = async () => {
            const a = parseFloat(document.getElementById('m-amt').value);
            const t = document.getElementById('m-tid').value;
            if(!a || !t) return alert("Sweetie, data enter karein!");
            await push(ref(db, 'deposits'), { uid, username: userData.username, amount: a, tid: t, method: document.getElementById('m-gw').innerText, status: 'pending', time: Date.now() });
            alert("Verification Request Logged!"); closeModal();
        };
        window.submitWithdraw = async () => {
            const a = parseFloat(document.getElementById('w-amt').value);
            const n = document.getElementById('w-num').value;
            if(userData.balance < a || a < 1) return alert("Liquidity Error!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - a });
            await push(ref(db, 'withdraws'), { uid, username: userData.username, amount: a, number: n, method: document.getElementById('w-method').value, status: 'pending', time: Date.now() });
            alert("Withdrawal Sequence Initiated!");
        };
        window.approveAction = async (path, key, u_uid, amt, tab) => {
            if(tab === 'dep') {
                const snap = await get(ref(db, `users/${u_uid}/balance`));
                await update(ref(db, `users/${u_uid}`), { balance: (snap.val() || 0) + amt });
            }
            await update(ref(db, `${path}/${key}`), { status: 'approved' });
            alert("Authorized!");
        };
        window.copyNum = () => { navigator.clipboard.writeText(document.getElementById('m-num').innerText); alert("Copied!"); };
        window.logout = () => signOut(auth).then(() => location.reload());
    </script>

    <style>
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .animate-marquee { display: flex; animation: marquee 20s linear infinite; }
    </style>
</body>
</html>
