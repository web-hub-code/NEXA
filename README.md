<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | Sovereign Node Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f4f7fa; color: #0f172a; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.75); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.5); border-radius: 28px; }
        .card-main { background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%); color: white; border-radius: 35px; box-shadow: 0 20px 40px -10px rgba(79, 70, 229, 0.4); }
        .bottom-nav { position: fixed; bottom: 15px; left: 15px; right: 15px; height: 75px; background: #ffffff; border-radius: 25px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 10px 30px rgba(0,0,0,0.05); border: 1px solid #e2e8f0; }
        .nav-item { color: #94a3b8; flex-direction: column; align-items: center; display: flex; cursor: pointer; transition: 0.3s; }
        .nav-item.active { color: #4f46e5; transform: translateY(-3px); }
        .nav-item i { font-size: 22px; }
        .nav-item span { font-size: 9px; font-weight: 800; text-transform: uppercase; margin-top: 4px; }
        #side-menu { position: fixed; top: 0; left: -100%; width: 85%; height: 100%; background: white; z-index: 2001; transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        #side-menu.active { left: 0; }
        .hidden { display: none !important; }
        .tap-scale:active { transform: scale(0.95); }
    </style>
</head>
<body class="pb-32">

    <!-- 1. LOGIN / AUTH -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[5000] flex flex-col items-center justify-center p-10 text-center">
        <div onclick="handleSecretTap()" class="cursor-pointer mb-10">
            <div class="w-24 h-24 bg-indigo-600 rounded-[35px] flex items-center justify-center text-white text-4xl mx-auto shadow-2xl rotate-6 animate__animated animate__bounceIn">
                <i class="fa-solid fa-microchip"></i>
            </div>
            <h2 class="text-4xl font-black tracking-tighter mt-6">NEXA <span class="text-indigo-600">PRO</span></h2>
            <p class="text-[9px] font-black uppercase tracking-[3px] text-slate-400 opacity-60 mt-2">Tap logo for God Mode</p>
        </div>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="anon-name" placeholder="Enter Nickname Sweetie..." class="w-full bg-slate-100 p-5 rounded-3xl outline-none font-bold text-center focus:ring-2 ring-indigo-500 transition-all">
            <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-3xl font-black uppercase text-xs tracking-widest shadow-xl tap-scale">Enter Hub</button>
        </div>
    </div>

    <!-- 2. SIDE MENU -->
    <div id="menu-overlay" class="fixed inset-0 bg-black/30 z-[2000] hidden backdrop-blur-sm" onclick="toggleMenu()"></div>
    <div id="side-menu" class="p-8 flex flex-col">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic tracking-tighter text-indigo-600">NEXA PRO</h2>
            <button onclick="toggleMenu()" class="text-slate-300 text-2xl"><i class="fa-solid fa-circle-xmark"></i></button>
        </div>
        <div class="space-y-3 flex-1 overflow-y-auto">
            <div onclick="showPage('about')" class="flex items-center gap-4 p-5 glass bg-slate-50 border-none rounded-2xl"><i class="fa-solid fa-id-card text-indigo-600"></i><p class="font-bold text-sm">About System</p></div>
            <div onclick="showPage('privacy')" class="flex items-center gap-4 p-5"><i class="fa-solid fa-lock text-slate-400"></i><p class="font-bold text-sm">Privacy Policy</p></div>
            <div onclick="window.location.href='https://wa.me/923705519562'" class="flex items-center gap-4 p-5"><i class="fa-brands fa-whatsapp text-green-500"></i><p class="font-bold text-sm">Official Support</p></div>
            <hr class="opacity-10">
            <div id="god-mode-link" class="hidden flex items-center gap-4 p-5 text-indigo-600 font-black animate__animated animate__pulse animate__infinite" onclick="showPage('admin')"><i class="fa-solid fa-crown"></i><p>ADMIN PANEL</p></div>
        </div>
        <button onclick="logout()" class="p-5 bg-red-50 text-red-500 rounded-2xl font-black uppercase text-[10px] tracking-widest mt-4">Terminate Session</button>
    </div>

    <!-- 3. MAIN APP -->
    <div id="app-content" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#f4f7fa]/80 backdrop-blur-md z-50">
            <div class="flex items-center gap-4" onclick="toggleMenu()">
                <div class="w-12 h-12 glass flex items-center justify-center text-slate-800 shadow-sm"><i class="fa-solid fa-bars-staggered"></i></div>
                <div><p id="greet" class="text-[9px] font-black uppercase text-slate-400">Welcome Sweetie</p><h2 id="user-display" class="text-xl font-black italic tracking-tighter">...</h2></div>
            </div>
            <div class="flex gap-2">
                <div onclick="navTo('promo')" class="w-11 h-11 bg-white rounded-xl flex items-center justify-center text-indigo-600 shadow-sm border border-indigo-50"><i class="fa-solid fa-gift"></i></div>
            </div>
        </header>

        <main class="px-6">
            <!-- PAGE: HOME -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-main p-8 mb-8 relative overflow-hidden">
                    <div class="absolute -right-10 -top-10 w-40 h-40 bg-white/10 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-bold opacity-70 uppercase tracking-widest mb-1">Node Balance</p>
                    <h2 id="user-bal" class="text-5xl font-black tracking-tighter mb-8">$0.00</h2>
                    <div class="flex gap-3">
                        <button onclick="navTo('deposit')" class="flex-1 bg-white text-indigo-600 py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg tap-scale">Deposit</button>
                        <button onclick="navTo('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[10px] font-black uppercase backdrop-blur-md tap-scale">Withdraw</button>
                    </div>
                </div>
                <h3 class="text-[10px] font-black uppercase tracking-[3px] text-slate-400 mb-6 px-1">Cloud Mining Hub</h3>
                <div id="plans-list" class="space-y-4"></div>
            </div>

            <!-- PAGE: DEPOSIT -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">Add Funds</h2>
                <div class="space-y-4">
                    <div onclick="openPay('JazzCash','03705519562')" class="glass p-6 flex justify-between items-center shadow-sm border-none bg-white tap-scale">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-red-600 rounded-2xl flex items-center justify-center text-white font-black">JC</div><p class="font-black italic">JazzCash</p></div>
                        <i class="fa-solid fa-angle-right text-slate-300"></i>
                    </div>
                    <div onclick="openPay('Easypaisa','03379827882')" class="glass p-6 flex justify-between items-center shadow-sm border-none bg-white tap-scale">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-green-500 rounded-2xl flex items-center justify-center text-white font-black">EP</div><p class="font-black italic">Easypaisa</p></div>
                        <i class="fa-solid fa-angle-right text-slate-300"></i>
                    </div>
                </div>
            </div>

            <!-- PAGE: WITHDRAW -->
            <div id="page-withdraw" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">Cash Out</h2>
                <div class="glass p-8 bg-white space-y-5 shadow-xl border-none">
                    <input type="number" id="wd-amt" placeholder="Amount ($5 Minimum)" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                    <select id="wd-meth" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                        <option>JazzCash</option><option>Easypaisa</option><option>SadaPay</option><option>USDT</option>
                    </select>
                    <input type="text" id="wd-acc" placeholder="Account Number / Wallet" class="w-full bg-slate-50 p-5 rounded-2xl font-bold border-none outline-none">
                    <button onclick="requestWithdraw()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl tap-scale">Request Payout</button>
                </div>
            </div>

            <!-- PAGE: PROMO -->
            <div id="page-promo" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">Redeem Bonus</h2>
                <div class="glass p-8 bg-white border-none shadow-xl text-center">
                    <div class="w-20 h-20 bg-indigo-50 rounded-full flex items-center justify-center text-indigo-600 text-2xl mx-auto mb-6"><i class="fa-solid fa-gift"></i></div>
                    <input type="text" id="promo-input" placeholder="Enter Secret Code" class="w-full bg-slate-50 p-5 rounded-2xl font-black text-center uppercase tracking-widest outline-none mb-6">
                    <button onclick="applyPromo()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-lg tap-scale">Claim Reward</button>
                </div>
            </div>

            <!-- PAGE: ADMIN -->
            <div id="page-admin" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-8 text-indigo-600">GOD PANEL</h2>
                <div class="bg-white p-6 rounded-[30px] shadow-sm mb-8 border border-indigo-50">
                    <p class="text-[9px] font-black uppercase text-slate-400 mb-3 ml-2">Manual Bonus Injector</p>
                    <div class="space-y-3">
                        <input type="text" id="adm-uid" placeholder="User UID" class="w-full bg-slate-50 p-4 rounded-xl text-xs font-bold outline-none">
                        <input type="number" id="adm-amt" placeholder="Amount ($)" class="w-full bg-slate-50 p-4 rounded-xl text-xs font-bold outline-none">
                        <button onclick="injectBonus()" class="w-full bg-indigo-600 text-white p-4 rounded-xl font-black text-[10px] uppercase">Inject Cash</button>
                    </div>
                </div>
                <div class="space-y-8">
                    <div><h3 class="text-[10px] font-black text-slate-400 uppercase mb-4 ml-2">Deposits</h3><div id="adm-dep-list" class="space-y-3"></div></div>
                    <div><h3 class="text-[10px] font-black text-slate-400 uppercase mb-4 ml-2">Withdrawals</h3><div id="adm-wd-list" class="space-y-3"></div></div>
                </div>
            </div>

            <!-- PAGE: ABOUT / PRIVACY -->
            <div id="page-about" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">About Nexa</h2>
                <div class="glass p-8 bg-white text-slate-600 font-medium text-sm leading-relaxed space-y-4">
                    <p>Nexa Pro is a decentralized node mining platform. We offer 24/7 automated earnings through cloud clusters.</p>
                    <div class="bg-indigo-50 p-4 rounded-2xl text-indigo-700 font-bold italic text-center">"Sovereign wealth for sovereign users sweetie."</div>
                </div>
            </div>
            <div id="page-privacy" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">Privacy</h2>
                <div class="glass p-8 bg-white text-slate-400 font-black uppercase text-[10px] space-y-4 tracking-tighter">
                    <p>1. Accounts are anonymous.</p>
                    <p>2. Data is encrypted via Firebase.</p>
                    <p>3. Logs purged after 30 days.</p>
                </div>
            </div>
        </main>

        <nav class="bottom-nav">
            <div onclick="navTo('home')" id="nav-home" class="nav-item active"><i class="fa-solid fa-house-user"></i><span>Home</span></div>
            <div onclick="navTo('deposit')" id="nav-deposit" class="nav-item"><i class="fa-solid fa-plus-circle"></i><span>Deposit</span></div>
            <div onclick="navTo('withdraw')" id="nav-withdraw" class="nav-item"><i class="fa-solid fa-money-bill-transfer"></i><span>Cash</span></div>
            <div onclick="toggleMenu()" class="nav-item"><i class="fa-solid fa-ellipsis"></i><span>More</span></div>
        </nav>
    </div>

    <!-- MODAL: PROOF -->
    <div id="pay-modal" class="fixed inset-0 bg-black/60 z-[6000] hidden flex items-center justify-center p-6 backdrop-blur-md">
        <div class="glass p-8 bg-white w-full max-w-sm rounded-[40px] animate__animated animate__zoomIn text-center">
            <h3 id="pm-name" class="text-2xl font-black italic mb-1">...</h3>
            <p id="pm-num" class="text-xl font-black text-indigo-600 mb-8">00000000000</p>
            <input type="number" id="pm-amt" placeholder="Sent Amount ($)" class="w-full bg-slate-50 p-4 rounded-2xl font-bold mb-3 outline-none">
            <input type="text" id="pm-tid" placeholder="Transaction ID (TID)" class="w-full bg-slate-50 p-4 rounded-2xl font-bold mb-6 outline-none">
            <button onclick="submitDep()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl tap-scale">Submit Proof</button>
            <button onclick="closePay()" class="mt-4 text-slate-400 font-black text-[10px] uppercase">Close</button>
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

        // --- SECRET AUTH ---
        let taps = 0, lastT = 0, isGod = false;
        window.handleSecretTap = () => {
            const now = Date.now();
            if(now - lastT < 400) taps++; else taps = 1;
            lastT = now;
            if(taps === 4) {
                if(prompt("God Key sweetie?") === "admin786") { isGod = true; alert("Access Unlocked! 👑"); }
                taps = 0;
            }
        };

        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "User_" + Math.floor(Math.random()*999);
            const res = await signInAnonymously(auth);
            const snap = await get(ref(db, `users/${res.user.uid}`));
            if(!snap.exists()) {
                await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, role: isGod ? 'admin' : 'user' });
            } else if(isGod) {
                await update(ref(db, `users/${res.user.uid}`), { role: 'admin' });
            }
            location.reload();
        };

        onAuthStateChanged(auth, async (u) => {
            if(u) {
                const s = await get(ref(db, `users/${u.uid}`));
                if(s.exists()){
                    if(s.val().role === 'admin') document.getElementById('god-mode-link').classList.remove('hidden');
                    document.getElementById('user-display').innerText = s.val().username;
                    onValue(ref(db, `users/${u.uid}/balance`), snap => {
                        document.getElementById('user-bal').innerText = `$${(snap.val() || 0).toFixed(2)}`;
                    });
                }
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                renderPlans();
                if(s.val().role === 'admin') loadAdminData();
            }
        });

        // --- CORE NAV ---
        window.navTo = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            if(document.getElementById(`nav-${id}`)) document.getElementById(`nav-${id}`).classList.add('active');
            window.scrollTo(0,0);
        };
        window.showPage = (id) => { navTo(id); toggleMenu(); };
        window.toggleMenu = () => {
            document.getElementById('side-menu').classList.toggle('active');
            document.getElementById('menu-overlay').classList.toggle('hidden');
        };

        function renderPlans() {
            const con = document.getElementById('plans-list');
            let h = "";
            for(let i=1; i<=25; i++){
                const p = 5 + (i-1)*10;
                h += `<div class="glass p-6 bg-white border-none flex justify-between items-center shadow-sm">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-server"></i></div>
                        <div><p class="font-black italic">Node X-${i}</p><p class="text-[9px] font-bold text-green-500 uppercase">ROI: ${6+i}% Monthly</p></div>
                    </div>
                    <button class="bg-indigo-600 text-white px-5 py-3 rounded-2xl text-[10px] font-black italic shadow-lg">Buy $${p}</button>
                </div>`;
            }
            con.innerHTML = h;
        }

        // --- TX SYSTEMS ---
        window.openPay = (n, m) => { document.getElementById('pm-name').innerText = n; document.getElementById('pm-num').innerText = m; document.getElementById('pay-modal').classList.remove('hidden'); };
        window.closePay = () => document.getElementById('pay-modal').classList.add('hidden');
        
        window.submitDep = async () => {
            const a = parseFloat(document.getElementById('pm-amt').value);
            const t = document.getElementById('pm-tid').value;
            if(!a || !t) return alert("Missing info!");
            await push(ref(db, `deposit_requests`), { uid: auth.currentUser.uid, username: document.getElementById('user-display').innerText, amount: a, tid: t });
            alert("Sent for approval sweetie! 😘"); closePay();
        };

        window.requestWithdraw = async () => {
            const a = parseFloat(document.getElementById('wd-amt').value);
            const ac = document.getElementById('wd-acc').value;
            const m = document.getElementById('wd-meth').value;
            const u = auth.currentUser.uid;
            const s = await get(ref(db, `users/${u}`));
            if(a < 5 || s.val().balance < a) return alert("Invalid amount/balance!");
            await update(ref(db, `users/${u}`), { balance: s.val().balance - a });
            await push(ref(db, `withdraw_requests`), { uid: u, username: s.val().username, amount: a, account: ac, method: m });
            alert("Withdrawal Logged! 💸"); navTo('home');
        };

        window.applyPromo = async () => {
            if(document.getElementById('promo-input').value === "GOLD786") {
                const u = auth.currentUser.uid;
                const s = await get(ref(db, `users/${u}`));
                await update(ref(db, `users/${u}`), { balance: (s.val().balance || 0) + 5 });
                alert("$5 Bonus Added! 🎁"); navTo('home');
            } else alert("Wrong code!");
        };

        // --- ADMIN ACTIONS ---
        window.injectBonus = async () => {
            const id = document.getElementById('adm-uid').value;
            const am = parseFloat(document.getElementById('adm-amt').value);
            const s = await get(ref(db, `users/${id}`));
            if(s.exists()){
                await update(ref(db, `users/${id}`), { balance: (s.val().balance || 0) + am });
                alert("Cash Injected! 💉");
            } else alert("No such user!");
        };

        function loadAdminData() {
            onValue(ref(db, `deposit_requests`), s => {
                const con = document.getElementById('adm-dep-list'); con.innerHTML = "";
                s.forEach(c => {
                    const r = c.val();
                    con.innerHTML += `<div class="glass p-5 bg-white border-none flex justify-between items-center shadow-md">
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">${r.username}</p><p class="text-xl font-black text-indigo-600">$${r.amount}</p></div>
                        <button onclick="approveDep('${c.key}','${r.uid}',${r.amount})" class="w-10 h-10 bg-green-500 text-white rounded-xl"><i class="fa-solid fa-check"></i></button>
                    </div>`;
                });
            });
            onValue(ref(db, `withdraw_requests`), s => {
                const con = document.getElementById('adm-wd-list'); con.innerHTML = "";
                s.forEach(c => {
                    const r = c.val();
                    con.innerHTML += `<div class="glass p-5 bg-white border-none flex justify-between items-center shadow-md">
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">${r.username}</p><p class="text-xl font-black text-red-500">$${r.amount}</p></div>
                        <button onclick="doneWd('${c.key}')" class="w-10 h-10 bg-indigo-600 text-white rounded-xl"><i class="fa-solid fa-check-double"></i></button>
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
        window.doneWd = async (k) => { await remove(ref(db, `withdraw_requests/${k}`)); alert("Paid!"); };
        window.logout = () => signOut(auth).then(() => location.reload());
    </script>
</body>
</html>
