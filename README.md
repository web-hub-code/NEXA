<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Digital Assets</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #1a1a1a; -webkit-tap-highlight-color: transparent; }
        .app-shell { max-width: 480px; margin: 0 auto; min-height: 100vh; background: #ffffff; position: relative; padding-bottom: 90px; }
        .glass-header { position: sticky; top: 0; z-index: 50; background: rgba(255,255,255,0.8); backdrop-filter: blur(20px); border-bottom: 1px solid #f1f5f9; }
        .bottom-nav { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 480px; background: rgba(255,255,255,0.95); backdrop-filter: blur(15px); border-top: 1px solid #f1f5f9; display: flex; justify-content: space-around; padding: 12px 0 25px 0; z-index: 1000; }
        .nav-link { text-align: center; color: #94a3b8; font-size: 10px; font-weight: 700; flex: 1; transition: 0.3s; }
        .nav-link.active { color: #2563eb; transform: translateY(-2px); }
        .nav-link i { font-size: 20px; display: block; margin-bottom: 4px; }
        .asset-card { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); color: white; border-radius: 32px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); }
        .node-btn { transition: 0.2s active; }
        .node-btn:active { transform: scale(0.96); }
        .hidden { display: none; }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <div class="app-shell shadow-2xl shadow-gray-200">
        
        <!-- TOP HEADER -->
        <header class="glass-header px-6 py-5 flex justify-between items-center">
            <h1 id="main-logo" class="text-2xl font-black text-blue-600 tracking-tighter cursor-pointer">NEXA</h1>
            <div id="user-actions" class="hidden flex items-center gap-4">
                <button onclick="toggleTheme()" class="w-10 h-10 rounded-full bg-gray-50 flex items-center justify-center"><i class="fa-solid fa-moon text-gray-400"></i></button>
                <button onclick="logout()" class="w-10 h-10 rounded-full bg-red-50 flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <!-- PAGE: LOGIN -->
        <div id="page-login" class="px-8 pt-16">
            <div class="mb-12">
                <h2 class="text-3xl font-black mb-2">Welcome to <span class="text-blue-600">NEXA</span></h2>
                <p class="text-gray-400 font-medium">The most trusted digital node network.</p>
            </div>
            <form id="login-form" class="space-y-4">
                <input type="text" id="username" placeholder="Username" class="w-full p-5 rounded-2xl bg-gray-50 border-none outline-none focus:ring-2 ring-blue-100 transition" required>
                <input type="password" id="password" placeholder="Access Key" class="w-full p-5 rounded-2xl bg-gray-50 border-none outline-none focus:ring-2 ring-blue-100 transition" required>
                <button type="submit" class="w-full bg-blue-600 text-white py-5 rounded-2xl font-black shadow-xl shadow-blue-100 mt-4">AUTHENTICATE</button>
            </form>
        </div>

        <!-- PAGE: HOME (DASHBOARD) -->
        <div id="page-home" class="hidden px-6 pt-4 space-y-8">
            <div class="asset-card p-8 relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold opacity-60 uppercase tracking-[2px]">Net Portfolio Value</p>
                    <h2 id="balance" class="text-4xl font-black mt-2 tracking-tight">$0.00</h2>
                    <div class="flex gap-3 mt-8">
                        <button onclick="openModal('deposit-modal')" class="flex-1 bg-blue-600 py-3 rounded-xl text-xs font-black">DEPOSIT</button>
                        <button onclick="openModal('withdraw-modal')" class="flex-1 bg-white/10 py-3 rounded-xl text-xs font-black backdrop-blur-md">WITHDRAW</button>
                    </div>
                </div>
                <div class="absolute -right-6 -bottom-6 w-32 h-32 bg-blue-500 rounded-full blur-[60px] opacity-20"></div>
            </div>

            <div>
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-black text-gray-800 text-lg">Active Nodes</h3>
                    <button onclick="showPage('nodes')" class="text-blue-600 text-[10px] font-black uppercase">View All</button>
                </div>
                <div id="plans-grid" class="grid grid-cols-2 gap-4">
                    <!-- Dynamic Plans $5+ -->
                </div>
            </div>
        </div>

        <!-- PAGE: HISTORY -->
        <div id="page-history" class="hidden px-6 pt-4">
            <h3 class="font-black text-2xl mb-6">Activity Logs</h3>
            <div id="history-list" class="space-y-3">
                <p class="text-center text-gray-300 text-xs py-20">No transactions recorded yet.</p>
            </div>
        </div>

        <!-- PAGE: ABOUT & POLICY -->
        <div id="page-policy" class="hidden px-6 pt-4">
            <h3 class="font-black text-2xl mb-6">Security & Policy</h3>
            <div class="space-y-4">
                <div class="p-6 bg-gray-50 rounded-3xl border border-gray-100">
                    <h4 class="font-bold text-sm mb-2 text-blue-600">Data Encryption</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">NEXA uses end-to-end 256-bit encryption to protect your node access and financial data. We never store keys on public servers.</p>
                </div>
                <div class="p-6 bg-gray-50 rounded-3xl border border-gray-100">
                    <h4 class="font-bold text-sm mb-2 text-green-600">Withdrawal Rules</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">Minimum withdrawal is $10. Transfers are processed via Easypaisa/JazzCash within 24 hours of verification.</p>
                </div>
            </div>
        </div>

        <!-- MODAL: DEPOSIT -->
        <div id="deposit-modal" class="hidden fixed inset-0 bg-black/60 backdrop-blur-sm z-[2000] flex items-end">
            <div class="w-full bg-white rounded-t-[40px] p-10 animate-slide-up">
                <h3 class="text-2xl font-black mb-6 text-center">Fund Account</h3>
                <div class="bg-blue-50 p-6 rounded-3xl mb-6">
                    <p class="text-[10px] font-bold text-blue-500 uppercase mb-2">Payment Details</p>
                    <p class="text-sm font-bold opacity-70">Easypaisa: <span class="text-blue-600">03379827882</span></p>
                    <p class="text-sm font-bold opacity-70 mt-1">SadaPay: <span class="text-blue-600">03705519562</span></p>
                </div>
                <input type="number" id="d-amount" placeholder="Amount ($)" class="w-full p-5 rounded-2xl bg-gray-50 mb-4 outline-none border-none">
                <input type="text" id="d-tid" placeholder="Transaction ID (TID)" class="w-full p-5 rounded-2xl bg-gray-50 mb-6 outline-none border-none">
                <button onclick="submitDeposit()" class="w-full bg-blue-600 text-white py-5 rounded-2xl font-black shadow-lg">NOTIFY ADMIN</button>
                <button onclick="closeModal('deposit-modal')" class="w-full mt-4 text-xs font-bold text-gray-300">CANCEL</button>
            </div>
        </div>

        <!-- BOTTOM NAVIGATION -->
        <nav id="navbar" class="hidden bottom-nav">
            <button onclick="showPage('home')" id="btn-home" class="nav-link active"><i class="fa-solid fa-house-chimney"></i>Home</button>
            <button onclick="showPage('history')" id="btn-history" class="nav-link"><i class="fa-solid fa-chart-line"></i>Logs</button>
            <button onclick="showPage('policy')" id="btn-policy" class="nav-link"><i class="fa-solid fa-shield-halved"></i>Policy</button>
        </nav>

    </div>

    <!-- SCRIPT (FIREBASE & LOGIC) -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, push, onValue, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // --- NAVIGATION ENGINE ---
        window.showPage = (id) => {
            const pages = ['login', 'home', 'history', 'policy'];
            pages.forEach(p => document.getElementById('page-' + p).classList.add('hidden'));
            document.getElementById('page-' + id).classList.remove('hidden');
            
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            const activeNav = document.getElementById('btn-' + id);
            if(activeNav) activeNav.classList.add('active');
        };

        // --- LOGIN LOGIC ---
        document.getElementById('login-form').onsubmit = async (e) => {
            e.preventDefault();
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            const name = document.getElementById('username').value;
            
            const snap = await get(ref(db, 'users/' + uid));
            if(!snap.exists()) await set(ref(db, 'users/' + uid), { username: name, balance: 0, joins: Date.now() });
            
            localStorage.setItem('nexa_uid', uid);
            location.reload();
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            document.getElementById('page-login').classList.add('hidden');
            document.getElementById('page-home').classList.remove('hidden');
            document.getElementById('navbar').classList.remove('hidden');
            document.getElementById('user-actions').classList.remove('hidden');

            // Listen for balance updates
            onValue(ref(db, 'users/' + uid), s => {
                const d = s.val();
                if(d) document.getElementById('balance').innerText = `$${d.balance.toFixed(2)}`;
            });

            // Fetch Plans ($5 start)
            onValue(ref(db, 'plans'), s => {
                const grid = document.getElementById('plans-grid');
                grid.innerHTML = "";
                if(s.exists()) {
                    s.forEach(p => {
                        const pd = p.val();
                        grid.innerHTML += `
                        <div class="p-6 bg-gray-50 rounded-[30px] border border-gray-100 text-center node-btn">
                            <p class="text-[9px] font-black text-gray-300 uppercase">${pd.name}</p>
                            <h4 class="text-2xl font-black text-gray-800 my-1">${pd.profit}%</h4>
                            <p class="text-[9px] text-blue-600 font-bold mb-4 italic">Daily Farm</p>
                            <button onclick="invest(${pd.min})" class="w-full py-2 bg-white border border-gray-200 rounded-xl text-[10px] font-black hover:bg-blue-600 hover:text-white transition">STAKE $${pd.min}</button>
                        </div>`;
                    });
                }
            });
        }

        // --- ADMIN GOD MODE ---
        let clicks = 0;
        document.getElementById('main-logo').onclick = () => {
            clicks++;
            if(clicks === 4) {
                const k = prompt("Master Access Key:");
                if(k === "NEXA786") {
                    const action = prompt("1: Add Plan | 2: View Requests");
                    if(action === "1") {
                        const n = prompt("Plan Name:");
                        const m = prompt("Min Stake ($):");
                        const p = prompt("Daily %:");
                        push(ref(db, 'plans'), { name: n, min: m, profit: p });
                        alert("Created!");
                    } else if (action === "2") {
                        alert("Checking server for pending requests sweetie...");
                    }
                }
            }
            setTimeout(() => clicks = 0, 2000);
        };

        window.openModal = (id) => document.getElementById(id).classList.remove('hidden');
        window.closeModal = (id) => document.getElementById(id).classList.add('hidden');
        window.logout = () => { localStorage.clear(); location.reload(); };
        
        window.submitDeposit = () => {
            const amt = document.getElementById('d-amount').value;
            const tid = document.getElementById('d-tid').value;
            if(amt && tid) {
                push(ref(db, 'requests/deposits'), { uid, amt, tid, time: Date.now() });
                alert("Request filed sweetie! Wait for verification.");
                closeModal('deposit-modal');
            }
        };

        window.invest = (min) => alert(`Insufficient node fuel sweetie! Deposit $${min} or more.`);

    </script>
</body>
</html>
