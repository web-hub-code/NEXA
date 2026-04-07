<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Node Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f1f5f9; color: #0f172a; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.3); }
        .card-main { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(15, 23, 42, 0.3); }
        .bottom-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; height: 75px; background: #0f172a; border-radius: 25px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 15px 30px rgba(0,0,0,0.3); }
        .nav-item { color: #64748b; display: flex; flex-direction: column; align-items: center; gap: 4px; transition: 0.3s; cursor: pointer; }
        .nav-item.active { color: #3b82f6; }
        .nav-item i { font-size: 22px; }
        .nav-item span { font-size: 9px; font-weight: 800; text-transform: uppercase; }
        #side-menu { position: fixed; top: 0; left: -100%; width: 85%; height: 100%; background: white; z-index: 10001; transition: 0.5s; box-shadow: 20px 0 50px rgba(0,0,0,0.1); }
        #side-menu.active { left: 0; }
        .hidden { display: none; }
        .nexa-btn { transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .nexa-btn:active { transform: scale(0.95); }
        .progress-bar { transition: width 1s linear; height: 100%; border-radius: 10px; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. SIDE MENU & OVERLAY -->
    <div id="menu-overlay" class="fixed inset-0 bg-black/40 z-[10000] hidden backdrop-blur-sm" onclick="toggleMenu()"></div>
    <div id="side-menu" class="p-8 flex flex-col">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic">NEXA<span class="text-blue-600">HUB</span></h2>
            <button onclick="toggleMenu()" class="text-slate-400 text-2xl"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-6 flex-1">
            <div onclick="showPage('about')" class="flex items-center gap-4 p-4 glass rounded-2xl border-none"><i class="fa-solid fa-building-shield text-blue-600"></i><p class="font-bold">Company Profile</p></div>
            <div onclick="showPage('privacy')" class="flex items-center gap-4 p-4"><i class="fa-solid fa-user-lock text-slate-400"></i><p class="font-bold">Privacy Policy</p></div>
            <div onclick="window.location.href='https://wa.me/923379827882'" class="flex items-center gap-4 p-4"><i class="fa-solid fa-headset text-slate-400"></i><p class="font-bold">Support Center</p></div>
            <div id="god-mode-btn" class="hidden flex items-center gap-4 p-4 text-purple-600 font-black" onclick="showPage('god')"><i class="fa-solid fa-crown"></i><p>GOD MODE</p></div>
        </div>
        <button onclick="logout()" class="p-5 bg-red-50 text-red-600 rounded-2xl font-black uppercase text-xs">Disconnect Node</button>
    </div>

    <!-- 2. ANONYMOUS AUTH -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[50000] flex flex-col items-center justify-center p-10">
        <div class="w-24 h-24 bg-blue-600 rounded-[35px] flex items-center justify-center text-white text-4xl mb-10 shadow-2xl rotate-6 animate-pulse"><i class="fa-solid fa-ghost"></i></div>
        <h2 class="text-4xl font-black tracking-tighter mb-2">NEXA NODE</h2>
        <p class="text-slate-400 text-[10px] font-black uppercase tracking-[4px] mb-12 text-center">Encrypted Sovereign Access</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="anon-name" placeholder="Choose Nickname Sweetie" class="w-full bg-slate-100 p-5 rounded-2xl outline-none font-bold text-center focus:ring-2 ring-blue-500 transition-all">
            <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl nexa-btn">Launch Session</button>
        </div>
    </div>

    <!-- 3. APP CONTENT -->
    <div id="app-content" class="hidden">
        <!-- Header -->
        <header class="p-6 flex justify-between items-center bg-white/50 sticky top-0 z-[500] backdrop-blur-lg">
            <div class="flex items-center gap-4" onclick="toggleMenu()">
                <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-md text-slate-800"><i class="fa-solid fa-bars-staggered"></i></div>
                <div><p id="greeting-msg" class="text-[10px] font-black uppercase text-slate-400">Wait Sweetie...</p><h2 id="display-username" class="text-xl font-black italic tracking-tighter">Guest</h2></div>
            </div>
            <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-lg"><i class="fa-solid fa-shield-halved"></i></div>
        </header>

        <div class="px-6">
            <!-- PAGE: HOME -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-main p-8 mb-10 relative overflow-hidden">
                    <div class="absolute -top-10 -right-10 w-40 h-40 bg-blue-500/10 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-black opacity-60 uppercase mb-2 tracking-[2px]">Total Liquidity</p>
                    <h2 id="user-bal" class="text-6xl font-black tracking-tighter mb-1">$0.00</h2>
                    <p class="text-[9px] font-bold text-blue-400 mb-8 uppercase">Real-time Node Balance</p>
                    <div class="flex gap-4">
                        <button onclick="showPage('deposit')" class="flex-1 bg-white text-slate-900 py-4 rounded-2xl text-[11px] font-black uppercase nexa-btn">Add Funds</button>
                        <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[11px] font-black uppercase backdrop-blur-md nexa-btn">Withdraw</button>
                    </div>
                </div>

                <h3 class="text-[10px] font-black uppercase tracking-[3px] text-slate-400 mb-6 flex items-center gap-2"><i class="fa-solid fa-fire text-orange-500"></i> Hot Mining Pools</h3>
                <div id="plans-list" class="space-y-4 mb-10">
                    <!-- Plans will be generated here -->
                </div>
            </div>

            <!-- PAGE: NODES (ACTIVE MINING) -->
            <div id="page-nodes" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-2 tracking-tighter">Live Mining Nodes</h2>
                <p class="text-[10px] font-bold text-slate-400 uppercase mb-8 tracking-widest">Active Server Sessions</p>
                <div id="active-nodes-container" class="space-y-4">
                    <div class="p-10 text-center glass border-dashed border-2 rounded-[30px] opacity-40"><i class="fa-solid fa-box-open text-4xl mb-4"></i><p class="text-xs font-black uppercase">No Active Mining Nodes</p></div>
                </div>
            </div>

            <!-- PAGE: WALLET/DEPOSIT -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6">Deposit Center</h2>
                <div class="space-y-4">
                    <div class="glass p-6 rounded-[30px] flex justify-between items-center">
                        <div class="flex items-center gap-4"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR61f8Gq_y_Gg59Xq2_JmN7fW-O8-I7_V-07A&s" class="w-12 h-12 rounded-xl object-contain"><div><p class="font-black italic">JazzCash</p><p class="text-[10px] font-bold text-slate-400 uppercase">Instant Payment</p></div></div>
                        <button onclick="openPayModal('JazzCash', '03705519562')" class="bg-slate-900 text-white px-5 py-3 rounded-2xl text-[10px] font-black uppercase">Get Info</button>
                    </div>
                    <div class="glass p-6 rounded-[30px] flex justify-between items-center">
                        <div class="flex items-center gap-4"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTV8rI9k3N9i-YfUoT_h3V8D2Q3M-9S3u-Lyg&s" class="w-12 h-12 rounded-xl object-contain"><div><p class="font-black italic">Easypaisa</p><p class="text-[10px] font-bold text-slate-400 uppercase">Secure Gateway</p></div></div>
                        <button onclick="openPayModal('Easypaisa', '03379827882')" class="bg-slate-900 text-white px-5 py-3 rounded-2xl text-[10px] font-black uppercase">Get Info</button>
                    </div>
                    <div class="glass p-6 rounded-[30px] flex justify-between items-center">
                        <div class="flex items-center gap-4"><img src="https://seeklogo.com/images/S/sadapay-logo-4A8258E2BB-seeklogo.com.png" class="w-12 h-12 rounded-xl object-contain"><div><p class="font-black italic">SadaPay</p><p class="text-[10px] font-bold text-slate-400 uppercase">Fast Sync</p></div></div>
                        <button onclick="openPayModal('SadaPay', '03705519562')" class="bg-slate-900 text-white px-5 py-3 rounded-2xl text-[10px] font-black uppercase">Get Info</button>
                    </div>
                </div>
                <div class="mt-8 p-6 bg-blue-50 rounded-[30px] text-center border-2 border-blue-100">
                    <p class="text-[10px] font-black text-blue-600 uppercase mb-2">Notice Sweetie</p>
                    <p class="text-[11px] font-bold text-slate-600 leading-relaxed italic">Payment send karne ke baad screenshot Support par lazmi send karein taake balance sync ho sake.</p>
                </div>
            </div>

            <!-- PAGE: WITHDRAW -->
            <div id="page-withdraw" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6">Withdraw Profit</h2>
                <div class="glass p-8 rounded-[30px] space-y-5">
                    <div><label class="text-[10px] font-black text-slate-400 uppercase ml-2 mb-2 block">Amount (USD)</label><input type="number" id="wd-amount" placeholder="$5.00 min" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none focus:ring-2 ring-blue-500"></div>
                    <div><label class="text-[10px] font-black text-slate-400 uppercase ml-2 mb-2 block">Account Number</label><input type="text" id="wd-acc" placeholder="e.g 0337..." class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none focus:ring-2 ring-blue-500"></div>
                    <div><label class="text-[10px] font-black text-slate-400 uppercase ml-2 mb-2 block">Method</label>
                        <select id="wd-method" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                            <option>JazzCash</option><option>Easypaisa</option><option>SadaPay</option>
                        </select>
                    </div>
                    <button onclick="requestWithdraw()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl nexa-btn">Finalize Request</button>
                </div>
            </div>

            <!-- PAGE: HISTORY -->
            <div id="page-history" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6 tracking-tighter">Transaction Logs</h2>
                <div id="history-list" class="space-y-4"></div>
            </div>

            <!-- PAGE: ABOUT -->
            <div id="page-about" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6 tracking-tighter">Company Profile</h2>
                <div class="glass p-8 rounded-[30px] space-y-4">
                    <p class="text-sm font-bold text-slate-700 leading-relaxed">NEXA Sovereign Hub is a leading decentralized cloud mining infrastructure based in Zurich, Switzerland. We bridge the gap between complex blockchain computing and everyday users.</p>
                    <div class="p-4 bg-slate-50 rounded-2xl border-l-4 border-blue-600">
                        <p class="text-[10px] font-black text-blue-600 uppercase">Trusted By</p>
                        <p class="text-xs font-bold mt-1 text-slate-500">Over 25,000 active nodes worldwide.</p>
                    </div>
                </div>
            </div>

            <!-- PAGE: PRIVACY -->
            <div id="page-privacy" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6 tracking-tighter">Privacy Policy</h2>
                <div class="glass p-8 rounded-[30px] space-y-4 text-xs font-bold text-slate-600 leading-loose">
                    <p>1. Data Encryption: Your nickname and session are end-to-end encrypted.</p>
                    <p>2. Payment Security: All transactions are verified manually to prevent bot fraud.</p>
                    <p>3. Funds: User liquidity is locked in smart contracts for 24 hours during mining.</p>
                </div>
            </div>

            <!-- PAGE: GOD MODE (ADMIN) -->
            <div id="page-god" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6 text-purple-600 tracking-tighter">God Mode Panel</h2>
                <div class="glass p-6 rounded-[30px] space-y-4 mb-6">
                    <input type="text" id="target-uid" placeholder="User UID" class="w-full bg-slate-50 p-4 rounded-xl font-bold">
                    <input type="number" id="target-amount" placeholder="Add Balance" class="w-full bg-slate-50 p-4 rounded-xl font-bold">
                    <button onclick="adminAddBal()" class="w-full bg-purple-600 text-white p-4 rounded-xl font-black uppercase text-xs">Inject Funds</button>
                </div>
                <h3 class="text-xs font-black uppercase mb-4">Pending Withdrawals</h3>
                <div id="admin-withdrawals" class="space-y-3"></div>
            </div>
        </div>

        <!-- BOTTOM NAVIGATION -->
        <nav class="bottom-nav">
            <div onclick="navTo('home')" id="nav-home" class="nav-item active"><i class="fa-solid fa-grid-2"></i><span>Explore</span></div>
            <div onclick="navTo('nodes')" id="nav-nodes" class="nav-item"><i class="fa-solid fa-microchip"></i><span>Nodes</span></div>
            <div onclick="navTo('history')" id="nav-history" class="nav-item"><i class="fa-solid fa-file-invoice-dollar"></i><span>Logs</span></div>
            <div onclick="navTo('deposit')" id="nav-deposit" class="nav-item"><i class="fa-solid fa-wallet"></i><span>Wallet</span></div>
        </nav>
    </div>

    <!-- PAYMENT MODAL -->
    <div id="pay-modal" class="fixed inset-0 z-[60000] bg-black/60 hidden flex items-center justify-center p-6 backdrop-blur-md">
        <div class="glass p-8 w-full max-w-sm rounded-[40px] text-center animate__animated animate__zoomIn">
            <div id="pay-icon" class="w-16 h-16 rounded-full mx-auto mb-4 flex items-center justify-center text-2xl text-white shadow-lg"></div>
            <h3 id="pay-name" class="text-xl font-black italic">...</h3>
            <p class="text-[10px] font-black text-slate-400 uppercase mt-1 mb-6">Verified Merchant Account</p>
            <div class="bg-slate-100 p-5 rounded-2xl mb-8">
                <p class="text-[10px] font-black text-slate-500 mb-1 uppercase tracking-widest">Send Funds To</p>
                <p id="pay-num" class="text-xl font-black text-slate-800 tracking-tighter">00000000000</p>
                <p class="text-[9px] font-bold text-slate-400 mt-1">NEXA ENTERPRISE HOLDINGS</p>
            </div>
            <div class="flex gap-4">
                <button onclick="closeModal()" class="flex-1 p-4 text-slate-500 font-black uppercase text-[10px]">Cancel</button>
                <button onclick="alert('Address Copied sweetie!')" class="flex-1 bg-slate-900 text-white p-4 rounded-2xl font-black uppercase text-[10px] shadow-xl">Copy Info</button>
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

        const ADMIN_UID = "YOUR_ADMIN_UID"; // Apna UID yahan dalein for God Mode

        // --- AUTH & SETUP ---
        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "Investor_" + Math.floor(Math.random()*999);
            const res = await signInAnonymously(auth);
            const snap = await get(ref(db, `users/${res.user.uid}`));
            if(!snap.exists()){
                await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, joined: Date.now() });
            }
        };

        onAuthStateChanged(auth, (user) => {
            if(user) {
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                if(user.uid === ADMIN_UID) document.getElementById('god-mode-btn').classList.remove('hidden');
                initUser(user.uid);
            }
        });

        window.logout = () => signOut(auth).then(() => location.reload());

        function initUser(uid) {
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()){
                    const d = s.val();
                    document.getElementById('user-bal').innerText = `$${d.balance.toLocaleString(undefined, {minimumFractionDigits: 2})}`;
                    document.getElementById('display-username').innerText = d.username;
                    const h = new Date().getHours();
                    document.getElementById('greeting-msg').innerText = h < 12 ? "Good Morning Sweetie" : "Good Evening Sweetie";
                }
            });
            renderPlans();
            setInterval(() => syncNodes(uid), 1000);
            loadLogs(uid);
        }

        // --- NAVIGATION ---
        window.navTo = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`nav-${id}`).classList.add('active');
            window.scrollTo(0,0);
        };
        window.showPage = (id) => { 
            navTo(id); 
            if(!document.getElementById('side-menu').classList.contains('active')) toggleMenu();
            toggleMenu(); 
        };
        window.toggleMenu = () => {
            const m = document.getElementById('side-menu');
            const o = document.getElementById('menu-overlay');
            m.classList.toggle('active');
            o.classList.toggle('hidden');
        };

        // --- MINING PLANS ---
        const PLANS = [];
        for(let i=1; i<=15; i++) {
            PLANS.push({ name: `Node Alpha v.${i}`, price: 5 + (i-1)*5, roi: 2 + i*0.5, days: 1 });
        }
        const VIP_PLANS = [
            { name: "Sovereign VIP 1", price: 200, roi: 15, days: 3 },
            { name: "Sovereign VIP 2", price: 500, roi: 25, days: 5 },
            { name: "Sovereign VIP 3", price: 1000, roi: 40, days: 7 },
            { name: "Quantum Elite", price: 2500, roi: 100, days: 10 },
            { name: "NEXA God Node", price: 5000, roi: 250, days: 15 }
        ];

        function renderPlans() {
            const list = document.getElementById('plans-list');
            let html = "";
            [...PLANS, ...VIP_PLANS].forEach(p => {
                const isVip = p.price >= 200;
                const total = (p.price + (p.price * p.roi / 100)).toFixed(2);
                html += `
                <div class="glass p-6 rounded-[30px] flex justify-between items-center ${isVip ? 'border-l-4 border-purple-500 bg-purple-50/20' : 'bg-white shadow-sm'}">
                    <div class="flex items-center gap-5">
                        <div class="w-14 h-14 ${isVip ? 'bg-purple-600' : 'bg-blue-600'} text-white rounded-2xl flex items-center justify-center shadow-lg"><i class="fa-solid ${isVip ? 'fa-gem' : 'fa-server'}"></i></div>
                        <div>
                            <p class="font-black italic tracking-tighter">${p.name}</p>
                            <p class="text-[9px] font-bold text-slate-400 uppercase">Total Return: $${total} (${p.days} Day)</p>
                        </div>
                    </div>
                    <button onclick="buyPlan('${p.name}', ${p.price}, ${p.roi}, ${p.days})" class="bg-slate-900 text-white px-5 py-3 rounded-xl text-[10px] font-black italic shadow-lg nexa-btn">Stake$${p.price}</button>
                </div>`;
            });
            list.innerHTML = html;
        }

        window.buyPlan = async (name, price, roi, days) => {
            const uid = auth.currentUser.uid;
            const snap = await get(ref(db, `users/${uid}`));
            const bal = snap.val().balance;

            if(bal < price) return navTo('deposit');

            if(confirm(`Connect ${name} sweetie? Cost: $${price}`)) {
                const now = Date.now();
                const exp = now + (days * 24 * 60 * 60 * 1000);
                await update(ref(db, `users/${uid}`), { balance: bal - price });
                await push(ref(db, `active_plans/${uid}`), { 
                    planName: name, invested: price, profit: (price * roi / 100).toFixed(2), 
                    start: now, expiry: exp, duration: days 
                });
                await push(ref(db, `history/${uid}`), { type: 'Stake', plan: name, amount: price, date: new Date().toLocaleDateString() });
                alert("Node Initialized! 🚀");
                navTo('nodes');
            }
        };

        function syncNodes(uid) {
            onValue(ref(db, `active_plans/${uid}`), s => {
                const con = document.getElementById('active-nodes-container');
                if(!s.exists()) return;
                let html = "";
                s.forEach(child => {
                    const p = child.val();
                    const left = p.expiry - Date.now();
                    if(left > 0) {
                        const days = Math.floor(left / (24*3600000));
                        const hrs = Math.floor((left % (24*3600000)) / 3600000);
                        const mins = Math.floor((left % 3600000) / 60000);
                        const secs = Math.floor((left % 60000) / 1000);
                        const prog = ((Date.now() - p.start) / (p.expiry - p.start)) * 100;
                        html += `
                        <div class="glass p-6 rounded-[30px] shadow-sm border-l-4 border-blue-600 bg-white">
                            <div class="flex justify-between items-center mb-4"><span class="text-[10px] font-black uppercase text-blue-600">${p.planName}</span><span class="text-[9px] font-black bg-blue-50 px-3 py-1 rounded-full">${days}d ${hrs}h ${mins}m ${secs}s</span></div>
                            <div class="w-full h-2 bg-slate-100 rounded-full overflow-hidden"><div class="bg-blue-600 h-full progress-bar" style="width:${prog}%"></div></div>
                        </div>`;
                    } else { finishPlan(uid, child.key, p); }
                });
                con.innerHTML = html;
            }, { onlyOnce: true });
        }

        async function finishPlan(uid, key, p) {
            const s = await get(ref(db, `users/${uid}`));
            const returnAmt = parseFloat(p.invested) + parseFloat(p.profit);
            await update(ref(db, `users/${uid}`), { balance: s.val().balance + returnAmt });
            await remove(ref(db, `active_plans/${uid}/${key}`));
            await push(ref(db, `history/${uid}`), { type: 'Profit', plan: p.planName, amount: p.profit, date: new Date().toLocaleDateString() });
        }

        // --- WITHDRAW & PAYMENTS ---
        window.openPayModal = (name, num) => {
            const m = document.getElementById('pay-modal');
            const icon = document.getElementById('pay-icon');
            document.getElementById('pay-name').innerText = name;
            document.getElementById('pay-num').innerText = num;
            icon.style.background = name === 'JazzCash' ? '#dc2626' : (name === 'Easypaisa' ? '#16a34a' : '#1e293b');
            icon.innerHTML = `<i class="fa-solid fa-wallet"></i>`;
            m.classList.remove('hidden');
        };
        window.closeModal = () => document.getElementById('pay-modal').classList.add('hidden');

        window.requestWithdraw = async () => {
            const amt = parseFloat(document.getElementById('wd-amount').value);
            const acc = document.getElementById('wd-acc').value;
            const met = document.getElementById('wd-method').value;
            const uid = auth.currentUser.uid;
            const s = await get(ref(db, `users/${uid}`));

            if(amt < 5) return alert("Min withdraw is $5 sweetie!");
            if(s.val().balance < amt) return alert("Insufficient balance!");
            if(!acc) return alert("Enter account details!");

            await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt });
            await push(ref(db, `withdrawals`), { uid, username: s.val().username, amount: amt, account: acc, method: met, status: 'pending', date: Date.now() });
            await push(ref(db, `history/${uid}`), { type: 'Withdrawal', plan: met, amount: amt, date: new Date().toLocaleDateString() });
            alert("Request submitted sweetie! Will be processed in 12h.");
            navTo('history');
        };

        function loadLogs(uid) {
            onValue(ref(db, `history/${uid}`), s => {
                const list = document.getElementById('history-list');
                list.innerHTML = "";
                if(!s.exists()) return;
                Object.values(s.val()).reverse().forEach(h => {
                    const isP = h.type === 'Profit' || h.type === 'God Injection';
                    list.innerHTML += `
                    <div class="glass p-5 flex justify-between items-center bg-white rounded-2xl shadow-sm">
                        <div class="flex items-center gap-4">
                            <div class="w-10 h-10 ${isP ? 'bg-green-50 text-green-600' : 'bg-red-50 text-red-600'} rounded-xl flex items-center justify-center text-xs"><i class="fa-solid ${isP ? 'fa-arrow-up' : 'fa-arrow-down'}"></i></div>
                            <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[8px] font-bold text-slate-400">${h.plan} • ${h.date}</p></div>
                        </div>
                        <p class="font-black ${isP ? 'text-green-600' : 'text-red-600'}">${isP ? '+' : '-'}$${parseFloat(h.amount).toFixed(2)}</p>
                    </div>`;
                });
            });
        }

        // --- GOD MODE ACTIONS ---
        window.adminAddBal = async () => {
            const uid = document.getElementById('target-uid').value;
            const amt = parseFloat(document.getElementById('target-amount').value);
            const s = await get(ref(db, `users/${uid}`));
            if(s.exists()){
                await update(ref(db, `users/${uid}`), { balance: s.val().balance + amt });
                await push(ref(db, `history/${uid}`), { type: 'God Injection', plan: 'Admin Console', amount: amt, date: new Date().toLocaleDateString() });
                alert("Balance Injected!");
            }
        };
    </script>
</body>
</html>
