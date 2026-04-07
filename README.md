<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | The Sovereign Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f0f2f5; color: #0f172a; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.5); border-radius: 28px; }
        .card-pro { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25); }
        .bottom-nav { position: fixed; bottom: 15px; left: 15px; right: 15px; height: 75px; background: #ffffff; border-radius: 25px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 10px 30px rgba(0,0,0,0.08); border: 1px solid #edf2f7; }
        .nav-item { color: #94a3b8; flex-direction: column; align-items: center; display: flex; cursor: pointer; transition: 0.3s; }
        .nav-item.active { color: #4f46e5; transform: translateY(-5px); }
        .nav-item i { font-size: 22px; }
        .nav-item span { font-size: 9px; font-weight: 800; text-transform: uppercase; margin-top: 4px; }
        #side-menu { position: fixed; top: 0; left: -100%; width: 85%; height: 100%; background: white; z-index: 2001; transition: 0.4s; box-shadow: 20px 0 60px rgba(0,0,0,0.1); }
        #side-menu.active { left: 0; }
        .hidden { display: none !important; }
        input::-webkit-outer-spin-button, input::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. AUTH MODULE -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[5000] flex flex-col items-center justify-center p-10 text-center">
        <div onclick="handleSecretTap()" class="cursor-pointer mb-10">
            <div class="w-24 h-24 bg-indigo-600 rounded-[35px] flex items-center justify-center text-white text-4xl mx-auto shadow-2xl rotate-6 animate__animated animate__pulse animate__infinite"><i class="fa-solid fa-gem"></i></div>
            <h2 class="text-4xl font-extrabold tracking-tighter mt-6">NEXA <span class="text-indigo-600">PRO</span></h2>
            <p class="text-[9px] font-black uppercase tracking-[3px] text-slate-400 opacity-60">Sovereign Node Access</p>
        </div>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="anon-name" placeholder="Enter Nickname..." class="w-full bg-slate-100 p-5 rounded-3xl outline-none font-bold text-center border-2 border-transparent focus:border-indigo-500">
            <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-3xl font-black uppercase text-xs tracking-widest shadow-xl active:scale-95 transition-all">Launch Engine</button>
        </div>
    </div>

    <!-- 2. SIDE MENU (DRAWER) -->
    <div id="menu-overlay" class="fixed inset-0 bg-black/30 z-[2000] hidden backdrop-blur-sm" onclick="toggleMenu()"></div>
    <div id="side-menu" class="p-8 flex flex-col">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic">MENU</h2>
            <button onclick="toggleMenu()" class="text-slate-300 text-2xl"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-3 flex-1 overflow-y-auto">
            <div onclick="showPage('about')" class="flex items-center gap-4 p-5 glass bg-indigo-50/50 border-none rounded-2xl"><i class="fa-solid fa-building-columns text-indigo-600"></i><p class="font-bold text-sm">About Company</p></div>
            <div onclick="showPage('privacy')" class="flex items-center gap-4 p-5"><i class="fa-solid fa-shield-halved text-slate-400"></i><p class="font-bold text-sm">Privacy Policy</p></div>
            <div onclick="window.location.href='https://wa.me/923705519562'" class="flex items-center gap-4 p-5"><i class="fa-solid fa-headset text-slate-400"></i><p class="font-bold text-sm">Live Support</p></div>
            <hr class="opacity-10">
            <div id="god-mode-link" class="hidden flex items-center gap-4 p-5 text-indigo-600 font-black animate__animated animate__flash animate__infinite" onclick="showPage('admin')"><i class="fa-solid fa-fingerprint"></i><p>ADMIN CONTROL</p></div>
        </div>
        <button onclick="logout()" class="p-5 bg-red-50 text-red-500 rounded-2xl font-black uppercase text-[10px] tracking-widest mt-4">Close Session</button>
    </div>

    <!-- 3. APP CONTENT -->
    <div id="app-content" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#f0f2f5]/80 backdrop-blur-md z-50">
            <div class="flex items-center gap-4" onclick="toggleMenu()">
                <div class="w-12 h-12 glass flex items-center justify-center text-slate-800 shadow-sm"><i class="fa-solid fa-bars-staggered"></i></div>
                <div><p id="greet" class="text-[9px] font-black uppercase text-slate-400">Loading...</p><h2 id="user-display" class="text-xl font-black italic tracking-tighter">User</h2></div>
            </div>
            <div onclick="navTo('promo')" class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center text-indigo-600 shadow-sm border border-indigo-100"><i class="fa-solid fa-ticket"></i></div>
        </header>

        <main class="px-6 pb-20">
            <!-- PAGE: HOME (DASHBOARD) -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-pro p-8 mb-8 relative overflow-hidden">
                    <div class="absolute -right-10 -top-10 w-48 h-48 bg-white/5 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-bold opacity-60 uppercase tracking-[2px] mb-2">Available Balance</p>
                    <h2 id="user-bal" class="text-6xl font-black tracking-tighter mb-8">$0.00</h2>
                    <div class="flex gap-3">
                        <button onclick="navTo('deposit')" class="flex-1 bg-indigo-500 text-white py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg shadow-indigo-500/30">Deposit</button>
                        <button onclick="navTo('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[10px] font-black uppercase backdrop-blur-md">Withdraw</button>
                    </div>
                </div>
                <h3 class="text-[10px] font-black uppercase tracking-[3px] text-slate-400 mb-6">Investment Clusters (20+ Nodes)</h3>
                <div id="plans-list" class="space-y-4"></div>
            </div>

            <!-- PAGE: WITHDRAW -->
            <div id="page-withdraw" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6 tracking-tighter">Withdraw Funds</h2>
                <div class="glass p-8 bg-white space-y-4 border-none shadow-xl shadow-slate-200">
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Amount (Min $5)</label>
                        <input type="number" id="wd-amt" placeholder="0.00" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none mt-2">
                    </div>
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Select Gateway</label>
                        <select id="wd-meth" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none mt-2">
                            <option>JazzCash</option><option>Easypaisa</option><option>SadaPay</option><option>USDT (BEP20)</option>
                        </select>
                    </div>
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Account Number / Address</label>
                        <input type="text" id="wd-acc" placeholder="Account detail" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none mt-2">
                    </div>
                    <button onclick="requestWithdraw()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest mt-4 shadow-xl">Process Payout</button>
                </div>
                <p class="text-[9px] text-slate-400 mt-6 text-center font-bold">Withdrawals are processed within 2-24 hours sweetie.</p>
            </div>

            <!-- PAGE: PROMOCODE -->
            <div id="page-promo" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6 tracking-tighter">Redeem Code</h2>
                <div class="glass p-8 bg-white border-none shadow-xl text-center">
                    <div class="w-20 h-20 bg-indigo-50 rounded-full flex items-center justify-center text-indigo-600 text-2xl mx-auto mb-6"><i class="fa-solid fa-gift"></i></div>
                    <input type="text" id="promo-input" placeholder="Enter Secret Code" class="w-full bg-slate-50 p-5 rounded-2xl font-black text-center uppercase tracking-widest outline-none border-2 border-transparent focus:border-indigo-500 mb-6">
                    <button onclick="applyPromo()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-lg">Apply Code</button>
                </div>
            </div>

            <!-- PAGE: ABOUT -->
            <div id="page-about" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6 tracking-tighter">About Nexa Pro</h2>
                <div class="glass p-8 bg-white space-y-6 text-sm leading-relaxed text-slate-600 font-medium">
                    <p>Nexa Pro is a leading decentralized cloud mining ecosystem designed to provide secure, transparent, and profitable node-based investment opportunities.</p>
                    <p>Founded at **Prime Solutions**, our mission is to simplify digital assets staking through automated sovereign nodes that work 24/7 for our users.</p>
                    <div class="bg-indigo-50 p-4 rounded-2xl text-indigo-700 font-bold italic">"Your trust is our greatest asset sweetie."</div>
                </div>
            </div>

            <!-- PAGE: PRIVACY -->
            <div id="page-privacy" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6 tracking-tighter">Privacy Policy</h2>
                <div class="glass p-8 bg-white space-y-4 text-[12px] font-bold text-slate-400 uppercase tracking-tight">
                    <p>1. We do not store personal identification data; all accounts are anonymous nodes.</p>
                    <p>2. Transaction logs are encrypted via Firebase Realtime infrastructure.</p>
                    <p>3. Withdrawal details are purged once processed for maximum security.</p>
                    <p>4. Cookies are used only to maintain your session sweetie.</p>
                </div>
            </div>

            <!-- PAGE: ADMIN PANEL (GOD MODE) -->
            <div id="page-admin" class="page-view hidden animate__animated animate__fadeIn pb-20">
                <h2 class="text-3xl font-black italic mb-8 tracking-tighter text-indigo-600">GOD PANEL</h2>
                
                <!-- Manual Bonus Section -->
                <div class="bg-white p-6 rounded-[30px] shadow-sm mb-8">
                    <h4 class="text-[10px] font-black uppercase text-slate-400 mb-4">Manual Bonus Injector</h4>
                    <div class="space-y-3">
                        <input type="text" id="adm-target-uid" placeholder="User UID" class="w-full bg-slate-50 p-4 rounded-xl text-xs font-bold outline-none">
                        <input type="number" id="adm-bonus-amt" placeholder="Amount ($)" class="w-full bg-slate-50 p-4 rounded-xl text-xs font-bold outline-none">
                        <button onclick="addManualBonus()" class="w-full bg-indigo-600 text-white p-4 rounded-xl font-black text-[10px] uppercase">Inject Bonus</button>
                    </div>
                </div>

                <div class="space-y-10">
                    <div><h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 ml-2">Deposit Pipeline</h3><div id="adm-dep-list" class="space-y-3"></div></div>
                    <div><h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 ml-2">Withdraw Pipeline</h3><div id="adm-wd-list" class="space-y-3"></div></div>
                </div>
            </div>
        </main>

        <nav class="bottom-nav">
            <div onclick="navTo('home')" id="nav-home" class="nav-item active"><i class="fa-solid fa-house-chimney-window"></i><span>Home</span></div>
            <div onclick="navTo('withdraw')" id="nav-withdraw" class="nav-item"><i class="fa-solid fa-wallet"></i><span>Payout</span></div>
            <div onclick="navTo('promo')" id="nav-promo" class="nav-item"><i class="fa-solid fa-bolt"></i><span>Promo</span></div>
            <div onclick="toggleMenu()" class="nav-item"><i class="fa-solid fa-bars"></i><span>More</span></div>
        </nav>
    </div>

    <!-- MODAL: DEPOSIT PROOF -->
    <div id="pay-modal" class="fixed inset-0 bg-black/50 z-[6000] hidden flex items-center justify-center p-6 backdrop-blur-md">
        <div class="glass p-8 bg-white w-full max-w-sm rounded-[40px] animate__animated animate__zoomIn text-center">
            <h3 id="pm-name" class="text-2xl font-black italic mb-1">...</h3>
            <p id="pm-num" class="text-xl font-black text-indigo-600 tracking-tighter mb-8">0000000</p>
            <input type="number" id="pm-amt" placeholder="Sent Amount ($)" class="w-full bg-slate-50 p-4 rounded-2xl font-bold mb-3 outline-none border-2 border-transparent focus:border-indigo-500">
            <input type="text" id="pm-tid" placeholder="Transaction ID (TID)" class="w-full bg-slate-50 p-4 rounded-2xl font-bold mb-6 outline-none">
            <button onclick="submitDepRequest()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl">Submit for Approval</button>
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

        // --- SECRET ACCESS ---
        let tapCount = 0, lastTap = 0, isAdminSession = false;
        window.handleSecretTap = () => {
            const now = Date.now();
            if(now - lastTap < 400) tapCount++; else tapCount = 1;
            lastTap = now;
            if(tapCount === 4) {
                if(prompt("Secret Admin Key:") === "admin786") {
                    isAdminSession = true;
                    alert("GOD ACCESS GRANTED! 👑");
                }
                tapCount = 0;
            }
        };

        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "User_" + Math.floor(Math.random()*999);
            const res = await signInAnonymously(auth);
            const snap = await get(ref(db, `users/${res.user.uid}`));
            if(!snap.exists()) {
                await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, role: isAdminSession ? 'admin' : 'user' });
            } else if(isAdminSession) {
                await update(ref(db, `users/${res.user.uid}`), { role: 'admin' });
            }
            location.reload();
        };

        onAuthStateChanged(auth, async (user) => {
            if(user) {
                const snap = await get(ref(db, `users/${user.uid}`));
                if(snap.exists()){
                    if(snap.val().role === 'admin') document.getElementById('god-mode-link').classList.remove('hidden');
                    document.getElementById('user-display').innerText = snap.val().username;
                    onValue(ref(db, `users/${user.uid}/balance`), s => {
                        document.getElementById('user-bal').innerText = `$${(s.val() || 0).toFixed(2)}`;
                    });
                    const hr = new Date().getHours();
                    document.getElementById('greet').innerText = hr < 12 ? "Good Morning Sweetie" : "Active Session Sweetie";
                }
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                renderPlans();
                if(snap.val().role === 'admin') loadAdminData();
            }
        });

        // --- SYSTEM CORE ---
        window.navTo = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            const n = document.getElementById(`nav-${id}`); if(n) n.classList.add('active');
            window.scrollTo(0,0);
        };
        window.showPage = (id) => { navTo(id); toggleMenu(); };
        window.toggleMenu = () => {
            document.getElementById('side-menu').classList.toggle('active');
            document.getElementById('menu-overlay').classList.toggle('hidden');
        };

        function renderPlans() {
            const list = document.getElementById('plans-list');
            let html = "";
            for(let i=1; i<=25; i++) { // 25 Plans
                const price = 5 + (i-1)*10;
                const daily = (price * (0.05 + (i*0.01))).toFixed(2);
                html += `
                <div class="glass p-6 bg-white border-none flex justify-between items-center shadow-sm">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-microchip"></i></div>
                        <div><p class="font-black italic">Alpha Cluster v.${i}</p><p class="text-[9px] font-bold text-green-500 uppercase">$${daily} Daily Profit</p></div>
                    </div>
                    <button class="bg-indigo-600 text-white px-5 py-3 rounded-2xl text-[10px] font-black italic shadow-lg active:scale-90 transition-all">Buy$${price}</button>
                </div>`;
            }
            list.innerHTML = html;
        }

        // --- WITHDRAW & PROMO ---
        window.requestWithdraw = async () => {
            const amt = parseFloat(document.getElementById('wd-amt').value);
            const acc = document.getElementById('wd-acc').value;
            const meth = document.getElementById('wd-meth').value;
            const uid = auth.currentUser.uid;
            const s = await get(ref(db, `users/${uid}`));

            if(amt < 5 || isNaN(amt)) return alert("Minimum $5 sweetie!");
            if(s.val().balance < amt) return alert("Low balance!");

            await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt });
            await push(ref(db, `withdraw_requests`), { uid, username: s.val().username, amount: amt, account: acc, method: meth, date: Date.now() });
            alert("Withdrawal submitted sweetie! 💸");
            navTo('home');
        };

        window.applyPromo = async () => {
            const code = document.getElementById('promo-input').value.toUpperCase();
            if(code === "GOLD214") {
                const uid = auth.currentUser.uid;
                const s = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + 2 }); // $2 Bonus
                alert("Bonus $2 Added! 🎁");
                navTo('home');
            } else { alert("Invalid Secret Code!"); }
        };

        // --- ADMIN GOD MODE ---
        window.addManualBonus = async () => {
            const target = document.getElementById('adm-target-uid').value;
            const amt = parseFloat(document.getElementById('adm-bonus-amt').value);
            if(!target || !amt) return alert("Fill fields!");
            const s = await get(ref(db, `users/${target}`));
            if(s.exists()){
                await update(ref(db, `users/${target}`), { balance: (s.val().balance || 0) + amt });
                alert("Bonus Injected successfully! 💉");
            } else { alert("User not found!"); }
        };

        function loadAdminData() {
            onValue(ref(db, `deposit_requests`), s => {
                const con = document.getElementById('adm-dep-list'); con.innerHTML = "";
                if(!s.exists()) return;
                s.forEach(child => {
                    const r = child.val();
                    con.innerHTML += `<div class="glass p-5 bg-white border-none flex justify-between items-center shadow-md">
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">${r.username}</p><p class="text-xl font-black text-indigo-600">$${r.amount}</p><p class="text-[8px] font-bold">UID: ${r.uid}</p></div>
                        <div class="flex gap-2"><button onclick="approveDep('${child.key}', '${r.uid}', ${r.amount})" class="w-10 h-10 bg-green-500 text-white rounded-xl"><i class="fa-solid fa-check"></i></button></div>
                    </div>`;
                });
            });
            onValue(ref(db, `withdraw_requests`), s => {
                const con = document.getElementById('adm-wd-list'); con.innerHTML = "";
                if(!s.exists()) return;
                s.forEach(child => {
                    const r = child.val();
                    con.innerHTML += `<div class="glass p-5 bg-white border-none flex justify-between items-center shadow-md">
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">${r.username}</p><p class="text-xl font-black text-red-500">$${r.amount}</p><p class="text-[8px] font-bold">${r.method}: ${r.account}</p></div>
                        <div class="flex gap-2"><button onclick="approveWd('${child.key}')" class="w-10 h-10 bg-indigo-600 text-white rounded-xl"><i class="fa-solid fa-check-double"></i></button></div>
                    </div>`;
                });
            });
        }

        window.approveDep = async (k, u, a) => {
            const s = await get(ref(db, `users/${u}`));
            await update(ref(db, `users/${u}`), { balance: (s.val().balance || 0) + a });
            await remove(ref(db, `deposit_requests/${k}`));
            alert("Approved!");
        };
        window.approveWd = async (k) => { await remove(ref(db, `withdraw_requests/${k}`)); alert("Paid!"); };

        window.openPay = (n, m) => { document.getElementById('pm-name').innerText = n; document.getElementById('pm-num').innerText = m; document.getElementById('pay-modal').classList.remove('hidden'); };
        window.closePay = () => document.getElementById('pay-modal').classList.add('hidden');
        window.submitDepRequest = async () => {
            const amt = parseFloat(document.getElementById('pm-amt').value);
            const tid = document.getElementById('pm-tid').value;
            if(!amt || !tid) return alert("Fill all!");
            await push(ref(db, `deposit_requests`), { uid: auth.currentUser.uid, username: document.getElementById('user-display').innerText, amount: amt, tid: tid });
            alert("Request sent sweetie! 😘");
            closePay();
        };

        window.logout = () => signOut(auth).then(() => location.reload());
    </script>
</body>
</html>
