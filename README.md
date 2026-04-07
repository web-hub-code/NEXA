<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA | Digital Investment Nodes</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        :root { --primary: #3b82f6; --bg: #020617; --card: rgba(255,255,255,0.03); }
        .light-mode { --primary: #2563eb; --bg: #f8fafc; --card: rgba(0,0,0,0.05); color: #1e293b; }
        body { background: var(--bg); font-family: 'Plus Jakarta Sans', sans-serif; transition: 0.3s; }
        .glass { background: var(--card); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.1); }
        .nav-active { border-bottom: 2px solid var(--primary); color: var(--primary); }
        .hidden { display: none; }
    </style>
</head>
<body class="dark">

    <!-- TOP NAVIGATION -->
    <nav class="glass sticky top-0 z-[100] px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <h1 id="logo" class="text-3xl font-black text-blue-500 cursor-pointer">NEXA</h1>
            <div class="hidden md:flex gap-4 text-xs font-bold opacity-70">
                <button onclick="showSec('home')" class="hover:text-blue-500"><i class="fa-solid fa-house"></i> Home</button>
                <button onclick="showSec('about')" class="hover:text-blue-500"><i class="fa-solid fa-circle-info"></i> About</button>
                <button onclick="showSec('policy')" class="hover:text-blue-500"><i class="fa-solid fa-shield-halved"></i> Policy</button>
            </div>
        </div>
        <div class="flex items-center gap-4">
            <button onclick="toggleTheme()" class="w-8 h-8 rounded-full bg-white/5"><i class="fa-solid fa-moon"></i></button>
            <div id="user-info" class="hidden flex items-center gap-3">
                <span id="top-bal" class="text-green-400 font-bold text-sm">$0.00</span>
                <button onclick="logout()" class="text-red-500"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </div>
    </nav>

    <!-- SECTION: AUTH -->
    <div id="auth-sec" class="min-h-[80vh] flex items-center justify-center p-6">
        <div class="glass p-10 rounded-[3rem] w-full max-w-md text-center">
            <i class="fa-solid fa-share-nodes text-5xl text-blue-500 mb-4"></i>
            <h2 class="text-2xl font-bold mb-6">Secure Node Access</h2>
            <form id="login-form" class="space-y-4">
                <input type="text" id="user-id" placeholder="Username" class="w-full p-4 rounded-2xl bg-black/20 outline-none border border-white/5" required>
                <input type="password" id="user-key" placeholder="Access Key" class="w-full p-4 rounded-2xl bg-black/20 outline-none border border-white/5" required>
                <button class="w-full bg-blue-600 py-4 rounded-2xl font-bold shadow-xl">Initialize Session</button>
            </form>
        </div>
    </div>

    <!-- SECTION: DASHBOARD -->
    <div id="main-sec" class="hidden p-6 max-w-7xl mx-auto space-y-8">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="glass p-8 rounded-3xl">
                <p class="text-xs opacity-50 uppercase">Active Node Balance</p>
                <h3 id="dash-bal" class="text-4xl font-black text-blue-500 mt-2">$0.00</h3>
                <div class="flex gap-2 mt-6">
                    <button onclick="openModal('dep-modal')" class="bg-blue-600 px-6 py-2 rounded-xl text-xs font-bold"><i class="fa-solid fa-plus mr-1"></i> Deposit</button>
                    <button onclick="openModal('wit-modal')" class="bg-white/10 px-6 py-2 rounded-xl text-xs font-bold"><i class="fa-solid fa-minus mr-1"></i> Withdraw</button>
                </div>
            </div>
            <div class="glass p-8 rounded-3xl md:col-span-2">
                <h4 class="text-sm font-bold mb-4"><i class="fa-solid fa-clock-rotate-left mr-2"></i> Recent Node Activity</h4>
                <div id="history" class="text-[10px] space-y-2 opacity-60">No recent transactions.</div>
            </div>
        </div>

        <h3 class="text-xl font-bold flex items-center gap-2"><i class="fa-solid fa-microchip text-blue-500"></i> Investment Nodes</h3>
        <div id="plans-list" class="grid grid-cols-2 md:grid-cols-4 gap-4"></div>
    </div>

    <!-- SECTION: ABOUT & POLICY -->
    <div id="about-sec" class="hidden p-10 max-w-3xl mx-auto glass rounded-3xl my-10">
        <h2 class="text-3xl font-bold mb-4">About NEXA Corp</h2>
        <p class="opacity-70 text-sm leading-relaxed">NEXA is a next-generation decentralized node investment platform. We specialize in high-frequency trading and liquidity mining to generate consistent daily returns for our global investors.</p>
    </div>

    <!-- MODALS -->
    <div id="dep-modal" class="hidden fixed inset-0 bg-black/80 z-[200] flex items-center justify-center p-6">
        <div class="glass p-8 rounded-3xl w-full max-w-md">
            <h3 class="text-xl font-bold mb-6">Deposit Node Funds</h3>
            <div class="text-[10px] bg-blue-500/10 p-4 rounded-xl mb-4 leading-loose">
                <b>EASYPAISA:</b> 03379827882<br><b>JAZZCASH/SADAPAY:</b> 03705519562
            </div>
            <input type="number" id="d-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl mb-4 bg-black/20 outline-none">
            <input type="text" id="d-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-xl mb-4 bg-black/20 outline-none">
            <button onclick="submitDep()" class="w-full bg-blue-600 py-4 rounded-xl font-bold">Submit Verification</button>
            <button onclick="closeModals()" class="w-full text-xs mt-4 opacity-50">Close</button>
        </div>
    </div>

    <!-- GOD MODE ADMIN PANEL -->
    <div id="admin-sec" class="hidden fixed inset-0 bg-slate-900 z-[300] p-8 overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h1 class="text-2xl font-black">GOD MODE <span class="text-red-500">ADMIN</span></h1>
            <button onclick="location.reload()" class="bg-red-600 px-4 py-2 rounded-lg text-xs">Exit God Mode</button>
        </div>
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
            <div class="glass p-6 rounded-2xl">
                <h3 class="font-bold mb-4">Manage Plans (Supreme Control)</h3>
                <div class="space-y-4 mb-6">
                    <input type="text" id="p-name" placeholder="Plan Name" class="w-full p-2 rounded bg-black/20">
                    <input type="number" id="p-min" placeholder="Min Start ($5)" class="w-full p-2 rounded bg-black/20">
                    <input type="number" id="p-profit" placeholder="Daily Profit %" class="w-full p-2 rounded bg-black/20">
                    <button onclick="addPlan()" class="w-full bg-green-600 py-2 rounded font-bold">Create New Node Plan</button>
                </div>
                <div id="admin-plans" class="space-y-2"></div>
            </div>
            <div class="glass p-6 rounded-2xl">
                <h3 class="font-bold mb-4">Pending Requests</h3>
                <div id="admin-reqs" class="space-y-2 text-xs"></div>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, push, onValue, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        const auth = getAuth(app);
        const db = getDatabase(app);

        // --- THEME ---
        window.toggleTheme = () => document.body.classList.toggle('light-mode');

        // --- AUTH ---
        document.getElementById('login-form').onsubmit = async (e) => {
            e.preventDefault();
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            const user = document.getElementById('user-id').value;
            const snap = await get(ref(db, 'users/' + uid));
            if(!snap.exists()) await set(ref(db, 'users/' + uid), { username: user, balance: 0 });
            localStorage.setItem('nexa_uid', uid);
            location.reload();
        };

        // --- CORE NAVIGATION ---
        window.showSec = (id) => {
            ['auth-sec', 'main-sec', 'about-sec', 'admin-sec'].forEach(s => document.getElementById(s).classList.add('hidden'));
            document.getElementById(id + (id==='home'?'main':'') + '-sec').classList.remove('hidden');
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            document.getElementById('auth-sec').classList.add('hidden');
            document.getElementById('main-sec').classList.remove('hidden');
            document.getElementById('user-info').classList.remove('hidden');
            
            onValue(ref(db, 'users/' + uid), s => {
                const d = s.val();
                document.getElementById('dash-bal').innerText = `$${d.balance.toFixed(2)}`;
                document.getElementById('top-bal').innerText = `$${d.balance.toFixed(2)}`;
            });

            onValue(ref(db, 'plans'), s => {
                const list = document.getElementById('plans-list');
                list.innerHTML = "";
                s.forEach(p => {
                    const pd = p.val();
                    list.innerHTML += `<div class="glass p-4 rounded-2xl text-center border-t-2 border-blue-500">
                        <p class="text-[8px] font-bold opacity-50">${pd.name}</p>
                        <h5 class="text-xl font-black text-blue-500">${pd.profit}%</h5>
                        <p class="text-[10px] mb-4">Daily Profit</p>
                        <button onclick="invest(${pd.min})" class="w-full py-2 bg-blue-600 rounded-lg text-[10px] font-bold uppercase">Invest $${pd.min}</button>
                    </div>`;
                });
            });
        }

        // --- GOD MODE ADMIN ---
        let taps = 0;
        document.getElementById('logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const k = prompt("Master Access Key:");
                if(k === "NEXA786") {
                    showSec('admin');
                    loadAdminData();
                }
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.addPlan = () => {
            const name = document.getElementById('p-name').value;
            const min = document.getElementById('p-min').value;
            const profit = document.getElementById('p-profit').value;
            push(ref(db, 'plans'), { name, min, profit });
            alert("Plan created sweetie!");
        };

        function loadAdminData() {
            onValue(ref(db, 'plans'), s => {
                const list = document.getElementById('admin-plans');
                list.innerHTML = "";
                s.forEach(p => {
                    list.innerHTML += `<div class="flex justify-between bg-white/5 p-2 rounded">
                        <span>${p.val().name} ($${p.val().min})</span>
                        <button onclick="removePlan('${p.key}')" class="text-red-500">Delete</button>
                    </div>`;
                });
            });
        }
        window.removePlan = (key) => remove(ref(db, 'plans/' + key));
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.openModal = (id) => document.getElementById(id).classList.remove('hidden');
        window.closeModals = () => document.getElementById('dep-modal').classList.add('hidden');
        window.submitDep = () => {
            const amt = document.getElementById('d-amt').value;
            const tid = document.getElementById('d-tid').value;
            push(ref(db, 'requests/deposits'), { uid, amt, tid, status: 'pending' });
            alert("Request sent sweetie!");
            closeModals();
        };
    </script>
</body>
</html>
