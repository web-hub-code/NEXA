<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | Sovereign Node</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        
        :root { --primary: #6366f1; --dark: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--dark); overflow-x: hidden; }
        
        /* Modern Glassmorphism */
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.4); border-radius: 30px; }
        .card-grad { background: linear-gradient(135deg, #6366f1 0%, #a855f7 100%); color: white; border-radius: 35px; box-shadow: 0 20px 40px -10px rgba(99, 102, 241, 0.3); }
        
        /* Navigation */
        .bottom-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; height: 75px; background: var(--dark); border-radius: 24px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 15px 30px rgba(0,0,0,0.2); }
        .nav-item { color: #64748b; display: flex; flex-direction: column; align-items: center; gap: 4px; cursor: pointer; transition: 0.3s; }
        .nav-item.active { color: #818cf8; transform: translateY(-5px); }
        .nav-item i { font-size: 22px; }
        .nav-item span { font-size: 9px; font-weight: 800; text-transform: uppercase; letter-spacing: 0.5px; }

        /* Hidden Side Menu */
        #side-menu { position: fixed; top: 0; left: -100%; width: 80%; height: 100%; background: white; z-index: 2000; transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 20px 0 60px rgba(0,0,0,0.05); }
        #side-menu.active { left: 0; }
        .hidden { display: none !important; }
        
        /* Animations */
        .tap-pulse:active { transform: scale(0.95); transition: 0.1s; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. SECRET ADMIN LINK (SIDE MENU) -->
    <div id="menu-overlay" class="fixed inset-0 bg-black/20 z-[1900] hidden backdrop-blur-sm" onclick="toggleMenu()"></div>
    <div id="side-menu" class="p-8 flex flex-col">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic tracking-tighter">NEXA <span class="text-indigo-600">PRO</span></h2>
            <button onclick="toggleMenu()" class="text-slate-300 text-2xl"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-4 flex-1">
            <div onclick="showPage('about')" class="flex items-center gap-4 p-5 glass border-none bg-slate-50 rounded-2xl"><i class="fa-solid fa-circle-info text-indigo-600"></i><p class="font-bold text-sm">About System</p></div>
            <div onclick="window.location.href='https://wa.me/923379827882'" class="flex items-center gap-4 p-5"><i class="fa-solid fa-headset text-slate-400"></i><p class="font-bold text-sm">Support</p></div>
            <hr class="opacity-5">
            <div id="god-mode-link" class="hidden flex items-center gap-4 p-5 text-indigo-600 font-black animate__animated animate__pulse animate__infinite" onclick="showPage('admin')">
                <i class="fa-solid fa-crown"></i><p>GOD MODE PANEL</p>
            </div>
        </div>
        <button onclick="logout()" class="p-5 bg-red-50 text-red-500 rounded-2xl font-black uppercase text-[10px] tracking-widest">Logout Session</button>
    </div>

    <!-- 2. LOGIN PAGE WITH SECRET TAP -->
    <div id="auth-module" class="fixed inset-0 bg-white z-[50000] flex flex-col items-center justify-center p-10 overflow-hidden">
        <div class="absolute top-[-10%] left-[-10%] w-64 h-64 bg-indigo-100 rounded-full blur-3xl opacity-50"></div>
        <div class="absolute bottom-[-10%] right-[-10%] w-64 h-64 bg-purple-100 rounded-full blur-3xl opacity-50"></div>
        
        <div onclick="handleSecretTap()" class="cursor-pointer text-center z-10">
            <div class="w-24 h-24 bg-indigo-600 rounded-[35px] flex items-center justify-center text-white text-4xl mb-8 shadow-2xl rotate-6 animate__animated animate__bounceIn">
                <i class="fa-solid fa-fingerprint"></i>
            </div>
            <h2 id="nexa-logo" class="text-4xl font-black tracking-tighter mb-2">NEXA PRO</h2>
        </div>
        <p class="text-slate-400 text-[10px] font-black uppercase tracking-[4px] mb-12">Tap logo for secrets</p>
        
        <div class="w-full max-w-xs space-y-4 z-10">
            <input type="text" id="anon-name" placeholder="Nickname sweetie..." class="w-full bg-slate-100 p-5 rounded-3xl outline-none font-bold text-center focus:ring-2 ring-indigo-500 transition-all">
            <button onclick="loginAnonymously()" class="w-full bg-slate-900 text-white p-5 rounded-3xl font-black uppercase text-xs tracking-widest shadow-2xl tap-pulse">Initialize Access</button>
        </div>
    </div>

    <!-- 3. MAIN APPLICATION CONTENT -->
    <div id="app-content" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-md z-50">
            <div class="flex items-center gap-4" onclick="toggleMenu()">
                <div class="w-12 h-12 glass flex items-center justify-center text-slate-800 shadow-sm"><i class="fa-solid fa-bars-staggered"></i></div>
                <div><p id="greet" class="text-[9px] font-black uppercase text-slate-400">Welcome Sweetie</p><h2 id="user-display" class="text-xl font-black italic tracking-tighter">...</h2></div>
            </div>
            <div class="w-12 h-12 bg-indigo-600 rounded-2xl flex items-center justify-center text-white shadow-lg"><i class="fa-solid fa-bolt"></i></div>
        </header>

        <main class="px-6 space-y-8">
            <!-- PAGE: HOME -->
            <div id="page-home" class="page-view animate__animated animate__fadeIn">
                <div class="card-grad p-8 mb-8 relative overflow-hidden">
                    <div class="absolute -right-5 -top-5 w-32 h-32 bg-white/10 rounded-full blur-2xl"></div>
                    <p class="text-[10px] font-black opacity-70 uppercase tracking-widest mb-2">Portfolio Balance</p>
                    <h2 id="user-bal" class="text-5xl font-black tracking-tighter mb-8 animate__animated animate__fadeInUp">$0.00</h2>
                    <div class="flex gap-3">
                        <button onclick="navTo('deposit')" class="flex-1 bg-white text-indigo-600 py-4 rounded-2xl text-[10px] font-black uppercase shadow-xl">Deposit</button>
                        <button onclick="navTo('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[10px] font-black uppercase backdrop-blur-md">Withdraw</button>
                    </div>
                </div>
                <h3 class="text-[10px] font-black uppercase tracking-[3px] text-slate-400 mb-6">Active Nodes</h3>
                <div id="plans-list" class="space-y-4"></div>
            </div>

            <!-- PAGE: DEPOSIT -->
            <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn">
                <h2 class="text-2xl font-black italic mb-6">Add Liquidity</h2>
                <div class="space-y-3">
                    <div onclick="openPay('JazzCash','03705519562')" class="glass p-6 flex justify-between items-center shadow-sm border-none bg-white tap-pulse">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-red-600 rounded-2xl flex items-center justify-center text-white font-black text-xs">JC</div><p class="font-black italic">JazzCash</p></div>
                        <i class="fa-solid fa-arrow-right text-slate-300"></i>
                    </div>
                    <div onclick="openPay('Easypaisa','03379827882')" class="glass p-6 flex justify-between items-center shadow-sm border-none bg-white tap-pulse">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-green-600 rounded-2xl flex items-center justify-center text-white font-black text-xs">EP</div><p class="font-black italic">Easypaisa</p></div>
                        <i class="fa-solid fa-arrow-right text-slate-300"></i>
                    </div>
                </div>
            </div>

            <!-- PAGE: ADMIN (GOD MODE) -->
            <div id="page-admin" class="page-view hidden animate__animated animate__fadeIn">
                <div class="p-8 bg-slate-900 text-white rounded-[40px] mb-8 shadow-2xl relative">
                    <div class="absolute top-4 right-6 text-yellow-400 text-2xl"><i class="fa-solid fa-crown"></i></div>
                    <p class="text-[10px] font-black uppercase opacity-50 mb-1">Central Authority</p>
                    <h2 class="text-3xl font-black italic tracking-tighter">ADMIN CORE</h2>
                </div>
                <div class="space-y-8">
                    <div><h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 px-2">Deposit Approvals</h3><div id="adm-dep-list" class="space-y-3"></div></div>
                    <div><h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 px-2">Withdraw Approvals</h3><div id="adm-wd-list" class="space-y-3"></div></div>
                </div>
            </div>
        </main>

        <nav class="bottom-nav">
            <div onclick="navTo('home')" id="nav-home" class="nav-item active"><i class="fa-solid fa-house"></i><span>Home</span></div>
            <div onclick="navTo('deposit')" id="nav-deposit" class="nav-item"><i class="fa-solid fa-circle-plus"></i><span>Add</span></div>
            <div onclick="navTo('withdraw')" id="nav-withdraw" class="nav-item"><i class="fa-solid fa-wallet"></i><span>Cash</span></div>
            <div onclick="toggleMenu()" class="nav-item"><i class="fa-solid fa-gear"></i><span>More</span></div>
        </nav>
    </div>

    <!-- MODAL: PAYMENT PROOF -->
    <div id="pay-modal" class="fixed inset-0 bg-black/60 z-[60000] hidden flex items-center justify-center p-6 backdrop-blur-sm">
        <div class="glass p-8 bg-white w-full max-w-sm rounded-[40px] animate__animated animate__zoomIn text-center">
            <h3 id="pm-name" class="text-2xl font-black italic mb-1">...</h3>
            <p id="pm-num" class="text-xl font-black text-indigo-600 tracking-tighter mb-8 underline">0000000</p>
            <input type="number" id="pm-amt" placeholder="Sent Amount ($)" class="w-full bg-slate-50 p-4 rounded-2xl font-bold mb-3 outline-none border-2 border-transparent focus:border-indigo-500">
            <input type="text" id="pm-tid" placeholder="Transaction ID (TID)" class="w-full bg-slate-50 p-4 rounded-2xl font-bold mb-6 outline-none">
            <button onclick="submitDepRequest()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl tap-pulse">Confirm Proof</button>
            <button onclick="closePay()" class="mt-4 text-slate-400 font-black text-[10px] uppercase tracking-widest">Close</button>
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

        // --- SECRET ACCESS SYSTEM ---
        let tapCount = 0, lastTap = 0, secretUnlocked = false;
        window.handleSecretTap = () => {
            const now = Date.now();
            if(now - lastTap < 400) tapCount++; else tapCount = 1;
            lastTap = now;
            if(tapCount === 4) {
                if(prompt("Enter Admin Secret Key Sweetie:") === "admin786") {
                    secretUnlocked = true;
                    alert("Admin Key Accepted! ✨");
                }
                tapCount = 0;
            }
        };

        window.loginAnonymously = async () => {
            const name = document.getElementById('anon-name').value || "Guest";
            const res = await signInAnonymously(auth);
            const snap = await get(ref(db, `users/${res.user.uid}`));
            if(!snap.exists()) {
                await set(ref(db, `users/${res.user.uid}`), { 
                    username: name, balance: 0, 
                    role: secretUnlocked ? 'admin' : 'user' 
                });
            } else if(secretUnlocked) {
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
                    document.getElementById('user-bal').innerText = `$${snap.val().balance.toFixed(2)}`;
                }
                document.getElementById('auth-module').classList.add('hidden');
                document.getElementById('app-content').classList.remove('hidden');
                initApp(user.uid);
            }
        });

        function initApp(uid) {
            renderPlans();
            if(document.getElementById('god-mode-link').classList.contains('hidden') === false) loadAdminData();
            onValue(ref(db, `users/${uid}/balance`), s => {
                document.getElementById('user-bal').innerText = `$${(s.val() || 0).toFixed(2)}`;
            });
        }

        window.navTo = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`nav-${id}`).classList.add('active');
        };

        window.showPage = (id) => { navTo(id); toggleMenu(); };
        window.toggleMenu = () => {
            document.getElementById('side-menu').classList.toggle('active');
            document.getElementById('menu-overlay').classList.toggle('hidden');
        };

        function renderPlans() {
            const list = document.getElementById('plans-list');
            let html = "";
            for(let i=1; i<=10; i++){
                const price = i*10;
                html += `
                <div class="glass p-6 bg-white border-none flex justify-between items-center shadow-sm animate__animated animate__fadeInUp" style="animation-delay: ${i*0.1}s">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-indigo-50 text-indigo-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-server"></i></div>
                        <div><p class="font-black italic">Node v.${i}</p><p class="text-[9px] font-bold text-green-500 uppercase">Active ROI: ${5+i}%</p></div>
                    </div>
                    <button class="bg-indigo-600 text-white px-5 py-3 rounded-2xl text-[10px] font-black italic shadow-lg">Buy $${price}</button>
                </div>`;
            }
            list.innerHTML = html;
        }

        // --- MANUAL ADMIN FUNCTIONS ---
        window.openPay = (n, m) => {
            document.getElementById('pm-name').innerText = n;
            document.getElementById('pm-num').innerText = m;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closePay = () => document.getElementById('pay-modal').classList.add('hidden');

        window.submitDepRequest = async () => {
            const amt = parseFloat(document.getElementById('pm-amt').value);
            const tid = document.getElementById('pm-tid').value;
            if(!amt || !tid) return alert("Empty fields sweetie!");
            const uid = auth.currentUser.uid;
            const name = document.getElementById('user-display').innerText;
            await push(ref(db, `deposit_requests`), { uid, username: name, amount: amt, tid, status: 'pending' });
            alert("Sent! Waiting for Admin approval. 😘");
            closePay();
        };

        function loadAdminData() {
            onValue(ref(db, `deposit_requests`), s => {
                const con = document.getElementById('adm-dep-list');
                con.innerHTML = "";
                if(!s.exists()) return;
                s.forEach(child => {
                    const r = child.val();
                    con.innerHTML += `
                    <div class="glass p-5 bg-white border-none flex justify-between items-center shadow-md animate__animated animate__slideInRight">
                        <div><p class="text-[10px] font-black uppercase text-slate-400">${r.username}</p><p class="text-xl font-black text-indigo-600">$${r.amount}</p><p class="text-[8px] font-bold">TID: ${r.tid}</p></div>
                        <div class="flex gap-2">
                            <button onclick="approveDep('${child.key}', '${r.uid}', ${r.amount})" class="w-10 h-10 bg-green-500 text-white rounded-xl shadow-lg"><i class="fa-solid fa-check"></i></button>
                            <button onclick="rejectReq('deposit_requests','${child.key}')" class="w-10 h-10 bg-red-100 text-red-500 rounded-xl"><i class="fa-solid fa-x"></i></button>
                        </div>
                    </div>`;
                });
            });
        }

        window.approveDep = async (key, uid, amt) => {
            const snap = await get(ref(db, `users/${uid}`));
            const current = snap.val().balance || 0;
            await update(ref(db, `users/${uid}`), { balance: current + amt });
            await remove(ref(db, `deposit_requests/${key}`));
            alert("Approved! Balance Synced.");
        };

        window.rejectReq = async (path, key) => {
            await remove(ref(db, `${path}/${key}`));
            alert("Request Trasheed.");
        };

        window.logout = () => signOut(auth).then(() => location.reload());
    </script>
</body>
</html>
