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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.3); border-radius: 32px; }
        .card-pro { background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%); color: white; border-radius: 35px; box-shadow: 0 20px 40px -10px rgba(99, 102, 241, 0.4); }
        .bottom-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; height: 75px; background: #0f172a; border-radius: 25px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 20px 40px rgba(0,0,0,0.2); }
        .nav-item { color: #64748b; display: flex; flex-direction: column; align-items: center; gap: 4px; transition: 0.3s; cursor: pointer; }
        .nav-item.active { color: #818cf8; }
        .nav-item i { font-size: 20px; }
        .nav-item span { font-size: 9px; font-weight: 800; text-transform: uppercase; }
        .hidden { display: none; }
        #side-menu { position: fixed; top: 0; left: -100%; width: 85%; height: 100%; background: white; z-index: 10001; transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 20px 0 60px rgba(0,0,0,0.1); }
        #side-menu.active { left: 0; }
        .status-tag { padding: 4px 10px; border-radius: 10px; font-size: 8px; font-weight: 900; text-transform: uppercase; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. SIDE MENU -->
    <div id="menu-overlay" class="fixed inset-0 bg-black/40 z-[10000] hidden backdrop-blur-sm" onclick="toggleMenu()"></div>
    <div id="side-menu" class="p-8 flex flex-col">
        <div class="flex justify-between items-center mb-12">
            <h2 class="text-2xl font-black italic">NEXA <span class="text-indigo-600">HUB</span></h2>
            <button onclick="toggleMenu()" class="text-slate-300 text-3xl"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-6 flex-1">
            <div onclick="showPage('about')" class="flex items-center gap-4 p-5 glass border-none bg-slate-50"><i class="fa-solid fa-building-shield text-indigo-600"></i><p class="font-bold text-sm">Company Info</p></div>
            <div onclick="showPage('privacy')" class="flex items-center gap-4 p-5"><i class="fa-solid fa-user-lock text-slate-400"></i><p class="font-bold text-sm">Privacy Policy</p></div>
            <div onclick="window.location.href='https://wa.me/923379827882'" class="flex items-center gap-4 p-5"><i class="fa-solid fa-headset text-slate-400"></i><p class="font-bold text-sm">Help Center</p></div>
            <hr class="opacity-10">
            <div id="god-mode-link" class="hidden flex items-center gap-4 p-5 text-indigo-600 font-black" onclick="showPage('admin')"><i class="fa-solid fa-crown"></i><p>ADMIN PANEL</p></div>
        </div>
        <button onclick="logout()" class="p-5 bg-red-50 text-red-600 rounded-2xl font-black uppercase text-xs tracking-widest">Logout Session</button>
    </div>

    <!-- 2. LOGIN MODULE -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[50000] flex flex-col items-center justify-center p-10">
        <div class="w-24 h-24 bg-indigo-600 rounded-[35px] flex items-center justify-center text-white text-4xl mb-10 shadow-2xl rotate-6 animate-pulse"><i class="fa-solid fa-ghost"></i></div>
        <h2 class="text-4xl font-black tracking-tighter mb-2">NEXA PRO</h2>
        <p class="text-slate-400 text-[10px] font-black uppercase tracking-[4px] mb-12">Sovereign Access</p>
        <div class="w-full max-w-xs space-y-4 text-center">
            <input type="text" id="anon-name" placeholder="Enter Nickname Sweetie" class="w-full bg-slate-100 p-5 rounded-2xl outline-none font-bold text-center border-2 border-transparent focus:border-indigo-500 transition-all">
            <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Initialize Node</button>
        </div>
    </div>

    <!-- 3. MAIN APP -->
    <div id="app-content" class="hidden">
        
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/70 backdrop-blur-lg z-50">
            <div class="flex items-center gap-4" onclick="toggleMenu()">
                <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-sm text-slate-800 border"><i class="fa-solid fa-bars-staggered"></i></div>
                <div><p id="greet" class="text-[9px] font-black uppercase text-slate-400">Loading...</p><h2 id="user-display" class="text-xl font-black italic tracking-tighter text-indigo-900">Guest</h2></div>
            </div>
            <div class="w-12 h-12 bg-indigo-600 rounded-2xl flex items-center justify-center text-white shadow-lg shadow-indigo-200"><i class="fa-solid fa-shield-halved"></i></div>
        </header>

        <main class="px-6">
            <!-- PAGE: HOME -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-pro p-8 mb-10 relative overflow-hidden">
                    <div class="absolute -right-10 -top-10 w-40 h-40 bg-white/10 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-black opacity-60 uppercase mb-2 tracking-[2px]">Portfolio Balance</p>
                    <h2 id="user-bal" class="text-6xl font-black tracking-tighter mb-8">$0.00</h2>
                    <div class="flex gap-4">
                        <button onclick="navTo('deposit')" class="flex-1 bg-white text-indigo-600 py-4 rounded-2xl text-[11px] font-black uppercase shadow-lg">Deposit</button>
                        <button onclick="navTo('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[11px] font-black uppercase backdrop-blur-md">Withdraw</button>
                    </div>
                </div>

                <h3 class="text-[10px] font-black uppercase tracking-[3px] text-slate-400 mb-6">Premium Mining Nodes</h3>
                <div id="plans-list" class="space-y-4 mb-10"></div>
            </div>

            <!-- PAGE: ACTIVE NODES -->
            <div id="page-nodes" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-2 tracking-tighter">Live Nodes</h2>
                <p class="text-[10px] font-bold text-slate-400 uppercase mb-8 tracking-widest">Active Server Sessions</p>
                <div id="active-nodes-container" class="space-y-4"></div>
            </div>

            <!-- PAGE: DEPOSIT (USER) -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6 tracking-tighter">Add Liquidity</h2>
                <div class="space-y-4">
                    <div onclick="openPay('JazzCash','03705519562')" class="glass p-6 flex justify-between items-center shadow-sm border-none bg-white">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-red-600 rounded-2xl flex items-center justify-center text-white text-xs font-black">JC</div><p class="font-black italic">JazzCash</p></div>
                        <i class="fa-solid fa-chevron-right text-slate-300"></i>
                    </div>
                    <div onclick="openPay('Easypaisa','03379827882')" class="glass p-6 flex justify-between items-center shadow-sm border-none bg-white">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-green-600 rounded-2xl flex items-center justify-center text-white text-xs font-black">EP</div><p class="font-black italic">Easypaisa</p></div>
                        <i class="fa-solid fa-chevron-right text-slate-300"></i>
                    </div>
                </div>
            </div>

            <!-- PAGE: WITHDRAW (USER) -->
            <div id="page-withdraw" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6 tracking-tighter">Withdraw Funds</h2>
                <div class="glass p-8 bg-white space-y-5 border-none shadow-xl shadow-slate-200">
                    <input type="number" id="wd-amt" placeholder="Amount ($5 min)" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                    <input type="text" id="wd-acc" placeholder="Account Number" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                    <select id="wd-meth" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                        <option>JazzCash</option><option>Easypaisa</option><option>SadaPay</option>
                    </select>
                    <button onclick="requestWithdraw()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl">Confirm Withdrawal</button>
                </div>
            </div>

            <!-- PAGE: ADMIN (GOD MODE) -->
            <div id="page-admin" class="page-view hidden animate__animated animate__fadeIn">
                <div class="p-8 bg-indigo-900 text-white rounded-[40px] mb-8 shadow-2xl">
                    <p class="text-[10px] font-black uppercase opacity-60 mb-2">Central Authority</p>
                    <h2 class="text-3xl font-black italic tracking-tighter">GOD PANEL</h2>
                    <div class="grid grid-cols-2 gap-4 mt-8">
                        <div class="bg-white/10 p-4 rounded-2xl"><p class="text-[8px] font-black">USERS</p><p id="adm-users" class="text-xl font-black">--</p></div>
                        <div class="bg-white/10 p-4 rounded-2xl"><p class="text-[8px] font-black">REVENUE</p><p id="adm-rev" class="text-xl font-black">$0.0</p></div>
                    </div>
                </div>

                <div class="space-y-8">
                    <div><h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 px-2">Deposit Requests</h3><div id="adm-dep-list" class="space-y-3"></div></div>
                    <div><h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 px-2">Withdraw Requests</h3><div id="adm-wd-list" class="space-y-3"></div></div>
                </div>
            </div>
        </main>

        <nav class="bottom-nav">
            <div onclick="navTo('home')" id="nav-home" class="nav-item active"><i class="fa-solid fa-house"></i><span>Home</span></div>
            <div onclick="navTo('nodes')" id="nav-nodes" class="nav-item"><i class="fa-solid fa-microchip"></i><span>Nodes</span></div>
            <div onclick="navTo('withdraw')" id="nav-withdraw" class="nav-item"><i class="fa-solid fa-wallet"></i><span>Wallet</span></div>
            <div onclick="toggleMenu()" class="nav-item"><i class="fa-solid fa-ellipsis"></i><span>Menu</span></div>
        </nav>
    </div>

    <!-- PAYMENT MODAL -->
    <div id="pay-modal" class="fixed inset-0 bg-black/60 z-[60000] hidden flex items-center justify-center p-6 backdrop-blur-md">
        <div class="glass p-8 bg-white w-full max-w-sm rounded-[40px] animate__animated animate__zoomIn text-center">
            <h3 id="pm-name" class="text-2xl font-black italic mb-1">...</h3>
            <p id="pm-num" class="text-xl font-black text-indigo-600 tracking-tighter mb-8">0000000</p>
            <input type="number" id="pm-amt" placeholder="Sent Amount ($)" class="w-full bg-slate-50 p-4 rounded-xl font-bold mb-3 border-none outline-none">
            <input type="text" id="pm-tid" placeholder="Transaction ID (TID)" class="w-full bg-slate-50 p-4 rounded-xl font-bold mb-6 border-none outline-none">
            <button onclick="submitDepRequest()" class="w-full bg-indigo-600 text-white p-4 rounded-2xl font-black uppercase text-xs shadow-xl">Submit Proof</button>
            <button onclick="closePay()" class="mt-4 text-slate-400 font-black text-[10px] uppercase">Cancel</button>
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

        const ADMIN_UID = "YOUR_ADMIN_UID_HERE"; // Apna UID yahan dalein sweetie!

        // --- AUTH & LOGIN ---
        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "User_" + Math.floor(Math.random()*999);
            const res = await signInAnonymously(auth);
            const snap = await get(ref(db, `users/${res.user.uid}`));
            if(!snap.exists()) {
                await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, joined: Date.now() });
            }
        };

        onAuthStateChanged(auth, (user) => {
            if(user) {
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                if(user.uid === ADMIN_UID) document.getElementById('god-mode-link').classList.remove('hidden');
                initApp(user.uid);
            }
        });

        window.logout = () => signOut(auth).then(() => location.reload());

        function initApp(uid) {
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()){
                    const d = s.val();
                    document.getElementById('user-bal').innerText = `$${d.balance.toFixed(2)}`;
                    document.getElementById('user-display').innerText = d.username;
                    const hr = new Date().getHours();
                    document.getElementById('greet').innerText = hr < 12 ? "Good Morning Sweetie" : "Welcome Back Sweetie";
                }
            });
            renderPlans();
            setInterval(() => syncNodes(uid), 1000);
            if(uid === ADMIN_UID) loadAdminData();
        }

        // --- NAVIGATION ---
        window.navTo = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            const nav = document.getElementById(`nav-${id}`);
            if(nav) nav.classList.add('active');
            window.scrollTo(0,0);
        };
        window.showPage = (id) => { navTo(id); toggleMenu(); };
        window.toggleMenu = () => {
            document.getElementById('side-menu').classList.toggle('active');
            document.getElementById('menu-overlay').classList.toggle('hidden');
        };

        // --- PLANS & MINING ---
        function renderPlans() {
            const list = document.getElementById('plans-list');
            let html = "";
            for(let i=1; i<=15; i++){
                const price = 5 + (i-1)*5;
                const roi = 2 + (i*0.5);
                html += `
                <div class="glass p-6 bg-white border-none flex justify-between items-center shadow-sm">
                    <div class="flex items-center gap-5">
                        <div class="w-14 h-14 bg-indigo-50 text-indigo-600 rounded-3xl flex items-center justify-center shadow-inner"><i class="fa-solid fa-server"></i></div>
                        <div><p class="font-black italic">Alpha Node v.${i}</p><p class="text-[9px] font-bold text-green-500 uppercase">${roi}% Profit / 24h</p></div>
                    </div>
                    <button onclick="buyPlan('Alpha Node v.${i}', ${price}, ${roi})" class="bg-indigo-600 text-white px-5 py-3 rounded-2xl text-[10px] font-black italic">Stake$${price}</button>
                </div>`;
            }
            list.innerHTML = html;
        }

        window.buyPlan = async (name, price, roi) => {
            const uid = auth.currentUser.uid;
            const s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return navTo('deposit');
            
            const now = Date.now();
            const exp = now + (24 * 60 * 60 * 1000);
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `active_plans/${uid}`), { name, invested: price, profit: (price * roi / 100).toFixed(2), start: now, expiry: exp });
            alert("Mining Session Started! 🚀");
            navTo('nodes');
        };

        function syncNodes(uid) {
            onValue(ref(db, `active_plans/${uid}`), s => {
                const con = document.getElementById('active-nodes-container');
                if(!s.exists()){ con.innerHTML = "<p class='text-center opacity-30 text-xs py-10 font-bold'>NO ACTIVE NODES</p>"; return; }
                let html = "";
                s.forEach(child => {
                    const p = child.val();
                    const left = p.expiry - Date.now();
                    if(left > 0) {
                        const prog = ((Date.now() - p.start) / (p.expiry - p.start)) * 100;
                        html += `
                        <div class="glass p-6 bg-white border-none shadow-sm">
                            <div class="flex justify-between items-center mb-4"><span class="text-[10px] font-black uppercase text-indigo-600">${p.name}</span><span class="text-[9px] font-black opacity-40">Syncing...</span></div>
                            <div class="w-full h-1.5 bg-slate-100 rounded-full overflow-hidden"><div class="h-full bg-indigo-600" style="width:${prog}%"></div></div>
                        </div>`;
                    } else { finalizeNode(uid, child.key, p); }
                });
                con.innerHTML = html;
            }, { onlyOnce: true });
        }

        async function finalizeNode(uid, key, p) {
            const s = await get(ref(db, `users/${uid}`));
            const total = parseFloat(p.invested) + parseFloat(p.profit);
            await update(ref(db, `users/${uid}`), { balance: s.val().balance + total });
            await remove(ref(db, `active_plans/${uid}/${key}`));
        }

        // --- MANUAL DEPOSIT / WITHDRAW ---
        window.openPay = (n, m) => {
            document.getElementById('pm-name').innerText = n;
            document.getElementById('pm-num').innerText = m;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closePay = () => document.getElementById('pay-modal').classList.add('hidden');

        window.submitDepRequest = async () => {
            const amt = document.getElementById('pm-amt').value;
            const tid = document.getElementById('pm-tid').value;
            const uid = auth.currentUser.uid;
            const name = (await get(ref(db, `users/${uid}`))).val().username;

            if(!amt || !tid) return alert("Details fill karein sweetie!");
            await push(ref(db, `deposit_requests`), { uid, username: name, amount: parseFloat(amt), tid, date: Date.now(), status: 'pending' });
            alert("Sent to Admin for Approval! ✨");
            closePay();
            navTo('home');
        };

        window.requestWithdraw = async () => {
            const amt = parseFloat(document.getElementById('wd-amt').value);
            const acc = document.getElementById('wd-acc').value;
            const meth = document.getElementById('wd-meth').value;
            const uid = auth.currentUser.uid;
            const s = await get(ref(db, `users/${uid}`));

            if(amt < 5 || isNaN(amt)) return alert("Minimum $5 sweetie!");
            if(s.val().balance < amt) return alert("Insufficient Balance!");

            await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt });
            await push(ref(db, `withdraw_requests`), { uid, username: s.val().username, amount: amt, account: acc, method: meth, status: 'pending' });
            alert("Withdraw request submitted! Pending approval.");
            navTo('home');
        };

        // --- ADMIN PANEL (GOD MODE) ---
        function loadAdminData() {
            onValue(ref(db, `deposit_requests`), s => {
                const con = document.getElementById('adm-dep-list');
                con.innerHTML = "";
                if(!s.exists()) return;
                s.forEach(child => {
                    const r = child.val();
                    con.innerHTML += `
                    <div class="glass p-5 bg-white border-none flex justify-between items-center shadow-sm">
                        <div><p class="text-[10px] font-black uppercase text-slate-400">${r.username}</p><p class="text-xl font-black text-indigo-600">$${r.amount}</p><p class="text-[8px] font-bold">TID: ${r.tid}</p></div>
                        <div class="flex gap-2">
                            <button onclick="approveDep('${child.key}', '${r.uid}', ${r.amount})" class="w-10 h-10 bg-green-500 text-white rounded-xl"><i class="fa-solid fa-check"></i></button>
                            <button onclick="rejectReq('deposit_requests','${child.key}')" class="w-10 h-10 bg-red-100 text-red-500 rounded-xl"><i class="fa-solid fa-x"></i></button>
                        </div>
                    </div>`;
                });
            });

            onValue(ref(db, `withdraw_requests`), s => {
                const con = document.getElementById('adm-wd-list');
                con.innerHTML = "";
                if(!s.exists()) return;
                s.forEach(child => {
                    const r = child.val();
                    con.innerHTML += `
                    <div class="glass p-5 bg-white border-none flex justify-between items-center shadow-sm">
                        <div><p class="text-[10px] font-black uppercase text-slate-400">${r.username}</p><p class="text-xl font-black text-red-600">$${r.amount}</p><p class="text-[8px] font-bold">${r.method}: ${r.account}</p></div>
                        <div class="flex gap-2">
                            <button onclick="approveWd('${child.key}')" class="w-10 h-10 bg-indigo-600 text-white rounded-xl"><i class="fa-solid fa-check-double"></i></button>
                            <button onclick="rejectReq('withdraw_requests','${child.key}')" class="w-10 h-10 bg-red-100 text-red-500 rounded-xl"><i class="fa-solid fa-x"></i></button>
                        </div>
                    </div>`;
                });
            });

            onValue(ref(db, `users`), s => document.getElementById('adm-users').innerText = s.exists() ? Object.keys(s.val()).length : 0);
        }

        window.approveDep = async (key, uid, amt) => {
            const s = await get(ref(db, `users/${uid}`));
            await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + amt });
            await remove(ref(db, `deposit_requests/${key}`));
            alert("Deposit Confirmed Sweetie! ✅");
        };

        window.approveWd = async (key) => {
            await remove(ref(db, `withdraw_requests/${key}`));
            alert("Withdraw Marked as Paid! 💸");
        };

        window.rejectReq = async (path, key) => {
            await remove(ref(db, `${path}/${key}`));
            alert("Request Removed.");
        };

    </script>
</body>
</html>
