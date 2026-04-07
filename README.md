<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | Authority v5</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800;900&display=swap');
        body { font-family: 'Inter', sans-serif; background: #0F172A; color: #F8FAFC; -webkit-tap-highlight-color: transparent; overflow-x: hidden; }
        .glass-card { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.05); border-radius: 30px; }
        .gold-text { background: linear-gradient(to right, #FDE68A, #F59E0B); -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-weight: 900; }
        .icon-btn { width: 52px; height: 52px; border-radius: 18px; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.08); display: flex; align-items: center; justify-content: center; font-size: 18px; transition: 0.3s; }
        .icon-btn:active { transform: scale(0.9); background: rgba(99, 102, 241, 0.2); }
        .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; height: 85px; background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(20px); border-top: 1px solid rgba(255,255,255,0.05); display: flex; justify-content: space-around; align-items: center; z-index: 1000; padding-bottom: 10px; }
        .nav-item { color: #64748B; font-size: 22px; transition: 0.3s; }
        .nav-item.active { color: #6366F1; }
        .plan-card { transition: 0.3s; border-left: 4px solid #6366F1; }
        .animate-spin-slow { animation: spin 8s linear infinite; }
        @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
    </style>
</head>
<body class="pb-28">

    <!-- AUTH SCREEN -->
    <div id="auth-screen" class="fixed inset-0 bg-[#0F172A] z-[9999] flex flex-col items-center justify-center p-10">
        <div class="w-20 h-20 bg-indigo-600 rounded-[30px] flex items-center justify-center text-3xl mb-8 shadow-[0_0_40px_rgba(79,70,229,0.4)] animate-pulse">
            <i class="fa-solid fa-crown"></i>
        </div>
        <h1 class="text-2xl font-black italic tracking-widest mb-10 text-white uppercase">Nexa <span class="text-indigo-500">Nodes</span></h1>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Full Name" class="w-full p-5 rounded-2xl bg-slate-800/50 border border-slate-700 outline-none font-bold text-slate-200">
            <input type="password" id="admin-key" placeholder="Security Key (Optional)" class="w-full p-5 rounded-2xl bg-slate-800/50 border border-slate-700 outline-none font-bold text-slate-200">
            <button onclick="handleLogin()" class="w-full bg-indigo-600 p-5 rounded-2xl font-black uppercase text-xs tracking-widest text-white">Connect Rig</button>
        </div>
    </div>

    <!-- MAIN APP -->
    <div id="app" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#0F172A]/80 backdrop-blur-md z-[100]">
            <div>
                <h3 id="display-name" class="text-sm font-black uppercase tracking-tighter">User</h3>
                <p class="text-[8px] font-black text-indigo-500 uppercase">Live Node Active</p>
            </div>
            <div class="flex gap-2">
                <button onclick="nav('admin')" id="admin-btn" class="hidden w-10 h-10 bg-red-500/10 text-red-500 rounded-xl flex items-center justify-center"><i class="fa-solid fa-bolt"></i></button>
                <button onclick="logout()" class="w-10 h-10 bg-slate-800 text-slate-500 rounded-xl flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <!-- PAGE: HOME -->
        <main id="page-home" class="page-content px-6 space-y-8 animate__animated animate__fadeIn">
            <div class="glass-card p-8 text-center border-t-2 border-indigo-500/50">
                <p class="text-[9px] font-black text-slate-500 uppercase tracking-[4px] mb-4">Balance Assets</p>
                <h2 id="user-bal" class="text-5xl font-black tracking-tighter mb-2">$0.00</h2>
                <p id="pkr-bal" class="text-[10px] font-bold text-indigo-400">Rs. 0</p>
            </div>

            <div class="glass-card p-6 flex items-center justify-between border-l-4 border-green-500">
                <div>
                    <p class="text-[8px] font-black text-slate-500 uppercase">Auto-Mining Cycle</p>
                    <p id="countdown" class="text-lg font-black text-green-400 tracking-widest">23:59:59</p>
                </div>
                <div class="w-12 h-12 bg-green-500/10 rounded-full flex items-center justify-center text-green-500 animate-spin-slow">
                    <i class="fa-solid fa-gear"></i>
                </div>
            </div>

            <div class="grid grid-cols-4 gap-4">
                <div onclick="nav('nodes')" class="flex flex-col items-center">
                    <div class="icon-btn text-indigo-400"><i class="fa-solid fa-server"></i></div>
                    <span class="text-[8px] font-black text-slate-500 uppercase mt-2">Nodes</span>
                </div>
                <div onclick="nav('deposit')" class="flex flex-col items-center">
                    <div class="icon-btn text-blue-400"><i class="fa-solid fa-plus-circle"></i></div>
                    <span class="text-[8px] font-black text-slate-500 uppercase mt-2">Fund</span>
                </div>
                <div onclick="nav('withdraw')" class="flex flex-col items-center">
                    <div class="icon-btn text-red-400"><i class="fa-solid fa-arrow-up-right-from-square"></i></div>
                    <span class="text-[8px] font-black text-slate-500 uppercase mt-2">Out</span>
                </div>
                <div onclick="nav('info')" class="flex flex-col items-center">
                    <div class="icon-btn text-amber-400"><i class="fa-solid fa-shield-halved"></i></div>
                    <span class="text-[8px] font-black text-slate-500 uppercase mt-2">Legal</span>
                </div>
            </div>
        </main>

        <!-- PAGE: NODES (15+5) -->
        <main id="page-nodes" class="page-content hidden px-6 space-y-6 pb-20">
            <h2 class="text-xl font-black italic gold-text">MINING RIGS</h2>
            <div id="nodes-container" class="space-y-4"></div>
        </main>

        <!-- PAGE: DEPOSIT -->
        <main id="page-deposit" class="page-content hidden px-6 space-y-6">
            <h2 class="text-xl font-black italic uppercase">Funding Center</h2>
            <div class="grid grid-cols-2 gap-4">
                <div onclick="openPay('JazzCash','03705519562')" class="glass-card p-6 text-center border-b-4 border-red-600">
                    <i class="fa-solid fa-building-columns text-red-500 text-2xl mb-2"></i>
                    <p class="text-[10px] font-black uppercase">JazzCash</p>
                </div>
                <div onclick="openPay('Easypaisa','03332637235')" class="glass-card p-6 text-center border-b-4 border-green-600">
                    <i class="fa-solid fa-wallet text-green-500 text-2xl mb-2"></i>
                    <p class="text-[10px] font-black uppercase">Easypaisa</p>
                </div>
            </div>
        </main>

        <!-- PAGE: ADMIN -->
        <main id="page-admin" class="page-content hidden px-6 space-y-6">
            <h2 class="text-xl font-black text-red-600 italic uppercase">Master Control</h2>
            <div id="admin-requests" class="space-y-4 text-center text-slate-600 text-[10px]">Scanning for signals...</div>
        </main>

        <!-- NAV -->
        <nav class="bottom-nav">
            <div onclick="nav('home')" class="nav-item active" id="btn-home"><i class="fa-solid fa-house-user"></i></div>
            <div onclick="nav('nodes')" class="nav-item" id="btn-nodes"><i class="fa-solid fa-microchip"></i></div>
            <div onclick="nav('deposit')" class="nav-item" id="btn-deposit"><i class="fa-solid fa-circle-plus"></i></div>
            <div onclick="nav('admin')" class="nav-item hidden" id="btn-admin"><i class="fa-solid fa-bolt"></i></div>
        </nav>
    </div>

    <!-- PAYMENT MODAL -->
    <div id="pay-modal" class="fixed inset-0 bg-black/90 backdrop-blur-xl z-[10000] hidden flex items-center justify-center p-8">
        <div class="glass-card p-8 w-full max-w-sm animate__animated animate__zoomIn">
            <h3 id="m-gw" class="text-xl font-black gold-text mb-6 uppercase">--</h3>
            <div class="bg-white/5 p-4 rounded-xl flex justify-between items-center mb-6 border border-white/10">
                <span id="m-num" class="font-black text-indigo-400 tracking-widest text-lg">--</span>
                <i onclick="copyNum()" class="fa-solid fa-copy text-slate-500"></i>
            </div>
            <input type="number" id="m-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl bg-black border border-slate-800 text-white mb-4 outline-none font-bold">
            <input type="text" id="m-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-xl bg-black border border-slate-800 text-white mb-6 outline-none font-bold">
            <button onclick="submitDep()" class="w-full bg-indigo-600 p-4 rounded-xl font-black uppercase text-[10px]">Verify Assets</button>
            <button onclick="closeModal()" class="w-full text-slate-600 text-[8px] font-black uppercase mt-4">Abort Session</button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // FIREBASE CONFIG
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
        const PKR_RATE = 285;
        let user = null, uid = "";

        // AUTH
        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return alert("Sweetie, enter your name!");
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const role = (key === "sweetie786") ? "admin" : "user";
            const s = await get(ref(db, `users/${uid}`));
            if(!s.exists()) await set(ref(db, `users/${uid}`), { username: name, balance: 0, role, join_date: Date.now() });
            else if(key === "sweetie786") await update(ref(db, `users/${uid}`), { role: "admin" });
            location.reload();
        };

        onAuthStateChanged(auth, u => {
            if(u) {
                uid = u.uid;
                onValue(ref(db, `users/${uid}`), s => {
                    user = s.val();
                    document.getElementById('display-name').innerText = user.username;
                    document.getElementById('user-bal').innerText = `$${(user.balance || 0).toFixed(2)}`;
                    document.getElementById('pkr-bal').innerText = `Rs. ${(user.balance * PKR_RATE).toLocaleString()}`;
                    if(user.role === 'admin') {
                        document.getElementById('btn-admin').classList.remove('hidden');
                        document.getElementById('admin-btn').classList.remove('hidden');
                        loadAdmin();
                    }
                });
                loadNodes(); startTimer();
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // NAV
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`btn-${id}`)?.classList.add('active');
        };

        // NODES (15 STANDARD + 5 VIP)
        function loadNodes() {
            const container = document.getElementById('nodes-container');
            container.innerHTML = "";
            for(let i=1; i<=15; i++) {
                const cost = i * 5;
                container.innerHTML += createNodeCard(`Nexa Standard v${i}`, cost, 'indigo', 'fa-microchip');
            }
            const vip = [200, 500, 1000, 2500, 5000];
            vip.forEach((c, idx) => container.innerHTML += createNodeCard(`ELITE VIP ${idx+1}`, c, 'yellow', 'fa-crown'));
        }

        function createNodeCard(n, c, col, icon) {
            return `<div class="glass-card p-5 flex justify-between items-center border-l-4 border-${col}-500">
                <div class="flex items-center gap-4">
                    <div class="w-10 h-10 bg-${col}-500/10 rounded-xl flex items-center justify-center text-${col}-500"><i class="fa-solid ${icon}"></i></div>
                    <div>
                        <h4 class="text-[10px] font-black uppercase text-white">${n}</h4>
                        <p class="text-[9px] text-slate-500 font-bold">$${c} <span class="text-${col}-400">(Rs. ${(c*PKR_RATE).toLocaleString()})</span></p>
                    </div>
                </div>
                <button class="bg-${col}-600 px-4 py-2 rounded-xl text-[8px] font-black uppercase">Activate</button>
            </div>`;
        }

        // DEPOSIT
        window.openPay = (gw, n) => {
            document.getElementById('m-gw').innerText = gw;
            document.getElementById('m-num').innerText = n;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closeModal = () => document.getElementById('pay-modal').classList.add('hidden');
        window.submitDep = async () => {
            const a = parseFloat(document.getElementById('m-amt').value);
            const t = document.getElementById('m-tid').value;
            if(!a || !t) return alert("Fill all fields!");
            await push(ref(db, 'deposits'), { uid, username: user.username, amount: a, tid: t, method: document.getElementById('m-gw').innerText, status: 'pending', time: Date.now() });
            alert("Sent for verification! 🚀"); closeModal();
        };

        // ADMIN
        function loadAdmin() {
            onValue(ref(db, 'deposits'), s => {
                const con = document.getElementById('admin-requests'); con.innerHTML = "";
                s.forEach(c => {
                    const d = c.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `<div class="glass-card p-5 border-l-4 border-indigo-500 text-left">
                            <p class="text-[10px] font-bold text-white">${d.username} sent $${d.amount}</p>
                            <p class="text-[8px] text-slate-500 mb-4">TID: ${d.tid}</p>
                            <button onclick="approveDep('${c.key}', '${d.uid}', ${d.amount})" class="w-full bg-indigo-600 py-2 rounded-lg text-[8px] font-black uppercase tracking-widest">Approve</button>
                        </div>`;
                    }
                });
            });
        }
        window.approveDep = async (k, u, a) => {
            const snap = await get(ref(db, `users/${u}/balance`));
            await update(ref(db, `users/${u}`), { balance: (snap.val() || 0) + a });
            await update(ref(db, `deposits/${k}`), { status: 'approved' });
            alert("Approved!");
        };

        function startTimer() {
            let h=23, m=59, s=59;
            setInterval(() => {
                s--; if(s<0){s=59; m--;} if(m<0){m=59; h--;} if(h<0) h=23;
                document.getElementById('countdown').innerText = `${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
            }, 1000);
        }

        window.copyNum = () => { navigator.clipboard.writeText(document.getElementById('m-num').innerText); alert("Copied!"); };
        window.logout = () => signOut(auth).then(() => location.reload());
    </script>
</body>
</html>
