<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | Authority v3</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&display=swap');
        body { font-family: 'Outfit', sans-serif; background: #FBFCFE; color: #0F172A; -webkit-tap-highlight-color: transparent; }
        .node-card { background: white; border-radius: 24px; border: 1px solid #F1F5F9; transition: 0.3s; position: relative; overflow: hidden; }
        .node-card:active { transform: scale(0.97); background: #F8FAFC; }
        .icon-box { width: 45px; height: 45px; border-radius: 14px; display: flex; align-items: center; justify-content: center; font-size: 18px; }
        .grad-blue { background: linear-gradient(135deg, #3B82F6, #2563EB); color: white; }
        .grad-purple { background: linear-gradient(135deg, #8B5CF6, #7C3AED); color: white; }
        .grad-orange { background: linear-gradient(135deg, #F59E0B, #D97706); color: white; }
        .bottom-bar { position: fixed; bottom: 0; left: 0; right: 0; height: 80px; background: rgba(255,255,255,0.85); backdrop-filter: blur(20px); display: flex; justify-content: space-around; align-items: center; border-top: 1px solid #F1F5F9; z-index: 1000; padding-bottom: 15px; }
        .nav-link { display: flex; flex-direction: column; align-items: center; gap: 4px; color: #94A3B8; font-weight: 600; font-size: 10px; transition: 0.3s; }
        .nav-link.active { color: #2563EB; }
        .nav-link i { font-size: 22px; }
        .price-badge { background: #EEF2FF; color: #4F46E5; padding: 4px 10px; border-radius: 8px; font-size: 10px; font-weight: 800; }
        .notif-popup { animation: slideInRight 0.5s, fadeOut 0.5s 4s forwards; }
    </style>
</head>
<body class="pb-24">

    <!-- FAKE LIVE NOTIFICATIONS -->
    <div id="notif-container" class="fixed top-20 right-4 z-[5000] w-64 pointer-events-none"></div>

    <!-- AUTH SCREEN -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-10">
        <div class="w-20 h-20 grad-blue rounded-[28px] flex items-center justify-center text-3xl mb-6 shadow-xl animate__animated animate__bounceIn">
            <i class="fa-solid fa-microchip"></i>
        </div>
        <h1 class="text-2xl font-extrabold tracking-tight mb-2">NEXA <span class="text-blue-600">NODES</span></h1>
        <p class="text-[9px] font-bold text-slate-400 tracking-[3px] uppercase mb-10">Cloud Mining Network</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Enter Full Name" class="w-full p-4 rounded-2xl bg-slate-50 border border-slate-100 outline-none font-semibold text-center focus:border-blue-500 transition-all">
            <input type="password" id="admin-key" placeholder="Security Key (Optional)" class="w-full p-4 rounded-2xl bg-slate-50 border border-slate-100 outline-none font-semibold text-center text-xs">
            <button onclick="handleLogin()" class="w-full grad-blue p-4 rounded-2xl font-bold uppercase text-xs tracking-widest shadow-lg shadow-blue-100">Access Dashboard</button>
        </div>
    </div>

    <!-- MAIN APP -->
    <div id="app" class="hidden animate__animated animate__fadeIn">
        
        <!-- TOP NAV -->
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/90 backdrop-blur-md z-[100]">
            <div class="flex items-center gap-3">
                <div onclick="alert('Menu Opening...')" class="w-10 h-10 flex items-center justify-center text-slate-400 bg-slate-50 rounded-xl active:scale-90 transition-all">
                    <i class="fa-solid fa-bars-staggered"></i>
                </div>
                <div>
                    <h2 id="display-name" class="text-sm font-bold text-slate-800">User</h2>
                    <p class="text-[8px] font-black text-blue-500 uppercase">Pro Member</p>
                </div>
            </div>
            <div class="flex gap-2">
                <button onclick="nav('admin')" id="admin-btn" class="hidden w-10 h-10 bg-red-50 text-red-500 rounded-xl flex items-center justify-center"><i class="fa-solid fa-screwdriver-wrench"></i></button>
                <button onclick="logout()" class="w-10 h-10 bg-slate-50 text-slate-400 rounded-xl flex items-center justify-center"><i class="fa-solid fa-right-from-bracket"></i></button>
            </div>
        </header>

        <main class="px-6 space-y-8">
            <!-- HOME PAGE -->
            <div id="page-home" class="page-content space-y-8">
                <!-- TOTAL ASSETS -->
                <div class="grad-blue p-8 rounded-[35px] shadow-2xl shadow-blue-100 relative overflow-hidden">
                    <div class="absolute -right-6 -bottom-6 w-32 h-32 bg-white/10 rounded-full blur-2xl"></div>
                    <div class="flex justify-between items-start mb-10">
                        <div>
                            <p class="text-[10px] font-bold opacity-70 uppercase tracking-widest">Available Credit</p>
                            <h2 id="user-bal" class="text-4xl font-extrabold tracking-tighter mt-1">$0.00</h2>
                        </div>
                        <i class="fa-solid fa-shield-check text-2xl opacity-50"></i>
                    </div>
                    <div class="flex gap-3">
                        <button onclick="nav('deposit')" class="flex-1 bg-white text-blue-600 py-3 rounded-xl text-[10px] font-black uppercase">Add Fund</button>
                        <button onclick="nav('withdraw')" class="flex-1 bg-white/20 py-3 rounded-xl text-[10px] font-black uppercase backdrop-blur-md">Withdraw</button>
                    </div>
                </div>

                <!-- NODES LIST -->
                <div>
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="text-xs font-bold uppercase text-slate-400 tracking-widest">Active Nodes</h3>
                        <span class="text-[9px] font-bold text-blue-500">View All</span>
                    </div>
                    
                    <div id="nodes-container" class="space-y-4">
                        <!-- Node 1 -->
                        <div class="node-card p-5 flex items-center justify-between">
                            <div class="flex items-center gap-4">
                                <div class="icon-box grad-blue"><i class="fa-solid fa-bolt"></i></div>
                                <div><h4 class="text-sm font-bold">Alpha Node</h4><p class="text-[9px] text-slate-400 font-bold uppercase">Daily Yield: $0.50</p></div>
                            </div>
                            <span class="price-badge">$5.00</span>
                        </div>
                        <!-- Node 2 -->
                        <div class="node-card p-5 flex items-center justify-between">
                            <div class="flex items-center gap-4">
                                <div class="icon-box grad-purple"><i class="fa-solid fa-server"></i></div>
                                <div><h4 class="text-sm font-bold">Quantum Rack</h4><p class="text-[9px] text-slate-400 font-bold uppercase">Daily Yield: $3.20</p></div>
                            </div>
                            <span class="price-badge">$30.00</span>
                        </div>
                        <!-- Node 3 -->
                        <div class="node-card p-5 flex items-center justify-between">
                            <div class="flex items-center gap-4">
                                <div class="icon-box grad-orange"><i class="fa-solid fa-microchip"></i></div>
                                <div><h4 class="text-sm font-bold">Titan Cluster</h4><p class="text-[9px] text-slate-400 font-bold uppercase">Daily Yield: $12.50</p></div>
                            </div>
                            <span class="price-badge">$100.00</span>
                        </div>
                    </div>
                </div>

                <!-- COMPANY TRUST SECTION -->
                <div class="bg-slate-100/50 p-6 rounded-3xl space-y-4">
                    <div class="flex items-center gap-3"><i class="fa-solid fa-building-shield text-blue-500"></i> <p class="text-[10px] font-bold text-slate-600 uppercase">Registered Assets Company</p></div>
                    <div class="flex items-center gap-3"><i class="fa-solid fa-fingerprint text-blue-500"></i> <p class="text-[10px] font-bold text-slate-600 uppercase">Biometric Encrypted Security</p></div>
                </div>
            </div>

            <!-- PAGES (DEPOSIT/WITHDRAW/INFO) -->
            <div id="page-deposit" class="page-content hidden animate__animated animate__fadeIn">
                <h2 class="text-xl font-bold mb-6">Funding Center</h2>
                <div class="space-y-3">
                    <div onclick="openPay('JazzCash','03705519562')" class="node-card p-6 flex justify-between items-center"><span class="font-bold">JazzCash</span><i class="fa-solid fa-chevron-right text-slate-300"></i></div>
                    <div onclick="openPay('Easypaisa','03332637235')" class="node-card p-6 flex justify-between items-center"><span class="font-bold">Easypaisa</span><i class="fa-solid fa-chevron-right text-slate-300"></i></div>
                </div>
                <div id="dep-history" class="mt-10 space-y-2"></div>
            </div>

            <div id="page-withdraw" class="page-content hidden animate__animated animate__fadeIn">
                <h2 class="text-xl font-bold mb-6">Payout Request</h2>
                <div class="node-card p-8 space-y-4">
                    <input type="number" id="wd-amt" placeholder="Amount (Min $10)" class="w-full p-4 rounded-xl bg-slate-50 border-none outline-none font-bold">
                    <input type="text" id="wd-acc" placeholder="Payment Details" class="w-full p-4 rounded-xl bg-slate-50 border-none outline-none font-bold">
                    <button onclick="submitWithdraw()" class="w-full grad-blue p-4 rounded-xl font-bold text-[10px] uppercase">Initialize Payout</button>
                </div>
            </div>

            <div id="page-info" class="page-content hidden animate__animated animate__fadeIn">
                <h2 class="text-xl font-bold mb-6">Company Assets</h2>
                <div class="space-y-4">
                    <div class="node-card p-5"><h4 class="font-bold text-xs mb-2">Terms of Service</h4><p class="text-[10px] text-slate-500 leading-relaxed">Nexa Nodes provides cloud-based computational power. All investments are locked for a 30-day cycle with daily profit releases.</p></div>
                    <div class="node-card p-5"><h4 class="font-bold text-xs mb-2">Security Protocol</h4><p class="text-[10px] text-slate-500 leading-relaxed">We use AES-256 bank-grade encryption to secure your transactions and personal data.</p></div>
                </div>
            </div>

            <!-- ADMIN CONTROL -->
            <div id="page-admin" class="page-content hidden">
                <h2 class="text-xl font-bold text-red-600 mb-6 uppercase tracking-widest">Master Panel</h2>
                <div id="admin-list" class="space-y-4"></div>
            </div>

        </main>

        <!-- BOTTOM NAVIGATION -->
        <nav class="bottom-bar">
            <div onclick="nav('home')" id="nav-home" class="nav-link active"><i class="fa-solid fa-house-chimney-window"></i><span>Home</span></div>
            <div onclick="nav('deposit')" id="nav-deposit" class="nav-link"><i class="fa-solid fa-square-plus"></i><span>Deposit</span></div>
            <div onclick="nav('withdraw')" id="nav-withdraw" class="nav-link"><i class="fa-solid fa-money-bill-trend-up"></i><span>Withdraw</span></div>
            <div onclick="nav('info')" id="nav-info" class="nav-link"><i class="fa-solid fa-shield-halved"></i><span>Company</span></div>
        </nav>
    </div>

    <!-- MODAL -->
    <div id="pay-modal" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-[10000] hidden flex items-center justify-center p-6">
        <div class="bg-white p-8 rounded-[40px] w-full max-w-sm animate__animated animate__zoomIn">
            <h3 id="m-gw" class="text-xl font-bold mb-6 italic text-blue-600">--</h3>
            <div class="bg-blue-50 p-4 rounded-2xl flex justify-between items-center mb-6">
                <span id="m-num" class="font-bold text-blue-700">--</span>
                <i onclick="copyNum()" class="fa-solid fa-copy text-blue-300"></i>
            </div>
            <input type="number" id="m-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl bg-slate-50 mb-3 font-bold outline-none">
            <input type="text" id="m-tid" placeholder="TID (Transaction ID)" class="w-full p-4 rounded-xl bg-slate-50 mb-6 font-bold outline-none">
            <button onclick="submitDep()" class="w-full grad-blue p-4 rounded-2xl font-bold text-[10px] uppercase shadow-lg shadow-blue-100">Confirm Transfer</button>
            <button onclick="closeModal()" class="w-full text-slate-400 text-[9px] font-bold uppercase mt-6">Back to Dashboard</button>
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

        let user = null; let uid = "";

        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return alert("Enter Name!");
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const role = (key === "sweetie786") ? "admin" : "user";
            const snap = await get(ref(db, `users/${uid}`));
            if(!snap.exists()) await set(ref(db, `users/${uid}`), { username: name, balance: 0, role: role });
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
                    if(user.role === 'admin') {
                        document.getElementById('admin-btn').classList.remove('hidden');
                        loadAdmin();
                    }
                });
                loadHistory(); startPopups();
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        window.logout = () => signOut(auth).then(() => location.reload());

        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`nav-${id}`)?.classList.add('active');
        };

        window.openPay = (gw, n) => {
            document.getElementById('m-gw').innerText = gw;
            document.getElementById('m-num').innerText = n;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closeModal = () => document.getElementById('pay-modal').classList.add('hidden');

        window.submitDep = async () => {
            const a = parseFloat(document.getElementById('m-amt').value);
            const t = document.getElementById('m-tid').value;
            if(!a || !t) return alert("Fill all info!");
            await push(ref(db, 'deposits'), { uid, username: user.username, amount: a, tid: t, method: document.getElementById('m-gw').innerText, status: 'pending', time: Date.now() });
            alert("Verification Started!"); closeModal();
        };

        window.submitWithdraw = async () => {
            const a = parseFloat(document.getElementById('wd-amt').value);
            if(a > user.balance || a < 5) return alert("Invalid Amount!");
            await push(ref(db, 'withdrawals'), { uid, username: user.username, amount: a, account: document.getElementById('wd-acc').value, status: 'pending', time: Date.now() });
            await update(ref(db, `users/${uid}`), { balance: user.balance - a });
            alert("Requested Successfully!");
        };

        function loadHistory() {
            onValue(ref(db, 'deposits'), snap => {
                const con = document.getElementById('dep-history'); con.innerHTML = "";
                snap.forEach(c => {
                    const d = c.val();
                    if(d.uid === uid) {
                        con.innerHTML += `<div class="node-card p-4 flex justify-between items-center text-[10px] font-bold">
                            <div><p>${d.method}</p><p class="text-slate-400 font-normal">${new Date(d.time).toLocaleDateString()}</p></div>
                            <div class="text-right"><p>$${d.amount}</p><p class="text-blue-500 uppercase">${d.status}</p></div>
                        </div>`;
                    }
                });
            });
        }

        function loadAdmin() {
            onValue(ref(db, 'deposits'), s => {
                const con = document.getElementById('admin-list'); con.innerHTML = "";
                s.forEach(c => {
                    const d = c.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `<div class="node-card p-5 border-l-4 border-red-500">
                            <p class="text-xs font-bold mb-1">${d.username} sent $${d.amount}</p>
                            <p class="text-[9px] text-slate-400 mb-4">TID: ${d.tid} | ${d.method}</p>
                            <button onclick="approveDep('${c.key}', '${d.uid}', ${d.amount})" class="w-full grad-blue py-2 rounded-xl text-[9px] font-bold uppercase">Approve Now</button>
                        </div>`;
                    }
                });
            });
        }

        window.approveDep = async (key, u, a) => {
            const snap = await get(ref(db, `users/${u}/balance`));
            await update(ref(db, `users/${u}`), { balance: (snap.val() || 0) + a });
            await update(ref(db, `deposits/${key}`), { status: 'approved' });
        };

        function startPopups() {
            const names = ["Zain", "Ali", "Sana", "Sara", "Kashif", "Hamza"];
            setInterval(() => {
                const n = names[Math.floor(Math.random()*names.length)];
                const a = Math.floor(Math.random()*200) + 20;
                const area = document.getElementById('notif-container');
                const div = document.createElement('div');
                div.className = "bg-white/95 p-4 rounded-2xl shadow-xl border border-blue-50 mb-2 flex items-center gap-3 notif-popup";
                div.innerHTML = `<i class="fa-solid fa-circle-check text-green-500 text-lg"></i> <div class="text-[9px] font-bold">Payout: ${n} withdrew $${a}.00</div>`;
                area.appendChild(div);
                setTimeout(() => div.remove(), 4500);
            }, 12000);
        }

        window.copyNum = () => { navigator.clipboard.writeText(document.getElementById('m-num').innerText); alert("Copied!"); };
    </script>
</body>
</html>
