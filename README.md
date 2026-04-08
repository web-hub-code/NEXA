<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GLOBAL | The Ultimate Empire</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --primary: #007AFF; --bg: #09090B; --card: #18181B; --accent: #FB4444; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #FAFAFA; overflow-x: hidden; }
        .glass { background: rgba(24, 24, 27, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); }
        .neo-card { background: var(--card); border-radius: 24px; border: 1px solid rgba(255,255,255,0.05); transition: 0.3s; }
        .accent-btn { background: linear-gradient(135deg, #007AFF 0%, #00C6FF 100%); shadow: 0 10px 20px rgba(0,122,255,0.3); }
        .hidden { display: none; }
        input, select { background: #27272A !important; border: 1px solid #3F3F46 !important; color: white !important; border-radius: 12px !important; padding: 12px !important; outline: none; }
        /* Spin Wheel Styles */
        #wheel { transition: transform 5s cubic-bezier(0.15, 0, 0.15, 1); }
        .wheel-segment { position: absolute; width: 50%; height: 50%; transform-origin: 100% 100%; display: flex; justify-content: center; align-items: flex-start; padding-top: 15px; font-size: 8px; font-weight: 900; }
    </style>
</head>
<body class="pb-28">

    <!-- Flash Ticker -->
    <div class="fixed top-0 w-full z-[60] bg-blue-600/10 py-1 border-b border-blue-500/20 overflow-hidden">
        <div id="ticker" class="whitespace-nowrap flex gap-10 text-[9px] font-black uppercase text-blue-400">
            <span>• Loading Global Markets...</span>
        </div>
    </div>

    <!-- Auth Screen -->
    <div id="auth-screen" class="fixed inset-0 bg-[#09090B] z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-20 h-20 accent-btn rounded-[2.5rem] flex items-center justify-center text-3xl mb-6 shadow-2xl shadow-blue-500/20"><i class="fa-solid fa-crown"></i></div>
        <h1 class="text-3xl font-black mb-10 tracking-tighter">NEXA <span class="text-[#007AFF]">GLOBAL</span></h1>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Full Name" class="w-full">
            <input type="text" id="refer-code" placeholder="Referral ID (Optional)" class="w-full text-center">
            <button id="login-btn" class="w-full accent-btn p-4 rounded-xl font-black uppercase text-[11px] tracking-widest shadow-xl">Initialize Access</button>
        </div>
    </div>

    <!-- God Mode (Admin) -->
    <div id="admin-panel" class="hidden fixed inset-0 bg-white text-black z-[10000] p-6 overflow-y-auto">
        <div class="flex justify-between items-center mb-8">
            <h2 class="text-2xl font-black text-red-600">GOD MODE ACTIVE</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div id="admin-requests" class="space-y-4 text-black">
            <p class="text-slate-400 italic">No pending requests, sweetie!</p>
        </div>
    </div>

    <!-- Main App Content -->
    <div id="main-app" class="hidden pt-10">
        <!-- Top Nav -->
        <header class="p-6 flex justify-between items-center sticky top-4 z-40">
            <div>
                <p class="text-[9px] font-bold text-blue-500 uppercase tracking-widest">Global Partner</p>
                <h3 id="display-name" class="text-xl font-black tracking-tight">User Name</h3>
            </div>
            <select id="curr-select" class="!p-1 !w-20 !text-[10px] bg-transparent border-none">
                <option value="USD">USD ($)</option>
                <option value="PKR">PKR (Rs)</option>
            </select>
        </header>

        <!-- Home Tab -->
        <div id="tab-home" class="tab-content p-6 space-y-6">
            <div class="neo-card p-8 accent-btn relative overflow-hidden">
                <div class="absolute -right-10 -top-10 w-40 h-40 bg-white/10 rounded-full blur-3xl"></div>
                <p class="text-[10px] font-bold uppercase opacity-80">Available Liquidity</p>
                <h1 id="user-bal" class="text-5xl font-black my-2">$0.00</h1>
                <div class="flex gap-2 mt-8">
                    <button onclick="switchTab('wallet')" class="flex-1 bg-white/20 p-3 rounded-xl text-[10px] font-black uppercase">Deposit</button>
                    <button onclick="switchTab('wallet')" class="flex-1 bg-black/20 p-3 rounded-xl text-[10px] font-black uppercase">Withdraw</button>
                </div>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-2 gap-4">
                <div class="neo-card p-4 text-center">
                    <p class="text-[8px] font-bold text-zinc-500 uppercase">Active Nodes</p>
                    <h3 id="active-nodes" class="text-lg font-black">0</h3>
                </div>
                <div onclick="switchTab('spin')" class="neo-card p-4 text-center border-amber-500/20 bg-amber-500/5">
                    <p class="text-[8px] font-bold text-amber-500 uppercase">Lucky Spin</p>
                    <h3 class="text-lg font-black text-amber-500">PLAY <i class="fa-solid fa-clover"></i></h3>
                </div>
            </div>
        </div>

        <!-- Nodes Tab -->
        <div id="tab-nodes" class="tab-content hidden p-6 pb-32">
            <h2 class="text-2xl font-black mb-6">Cloud Mining <span class="text-blue-500">Clusters</span></h2>
            <div id="nodes-list" class="space-y-4"></div>
        </div>

        <!-- Spin Tab -->
        <div id="tab-spin" class="tab-content hidden p-6 pb-32 text-center">
            <h2 class="text-2xl font-black mb-10">Neon <span class="text-amber-400">Jackpot Wheel</span></h2>
            <div class="relative w-72 h-72 mx-auto mb-12">
                <div class="absolute -top-4 left-1/2 -translate-x-1/2 z-50 text-amber-400 text-3xl"><i class="fa-solid fa-caret-down"></i></div>
                <div id="wheel" class="relative w-full h-full rounded-full border-[8px] border-zinc-800 shadow-[0_0_50px_rgba(0,122,255,0.2)] overflow-hidden"></div>
                <div class="absolute inset-0 m-auto w-12 h-12 bg-zinc-900 rounded-full z-40 border-4 border-zinc-800 flex items-center justify-center shadow-2xl">
                    <div class="w-6 h-6 rounded-full bg-amber-400 animate-pulse"></div>
                </div>
            </div>
            <button onclick="handleSpin()" id="spin-btn" class="w-full accent-btn p-5 rounded-2xl font-black uppercase text-[11px] shadow-2xl active:scale-95 transition-all">Spin Wheel ($0.50)</button>
        </div>

        <!-- Wallet Tab -->
        <div id="tab-wallet" class="tab-content hidden p-6 pb-32 space-y-6">
            <h2 class="text-2xl font-black mb-6">Financial <span class="text-blue-500">Hub</span></h2>
            <div class="neo-card p-6 space-y-4">
                <h4 class="text-xs font-black uppercase">Instant Deposit</h4>
                <select id="dep-method"><option>EasyPaisa</option><option>JazzCash</option><option>USDT (BEP20)</option></select>
                <input type="number" id="dep-amt" placeholder="Amount">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)">
                <button onclick="submitDep()" class="w-full accent-btn p-4 rounded-xl font-black text-[10px] uppercase">Submit Deposit</button>
            </div>
            <div class="space-y-2">
                <h4 class="text-xs font-black uppercase px-2 text-zinc-500">History</h4>
                <div id="history-list" class="space-y-2"></div>
            </div>
        </div>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2rem] flex justify-around items-center px-4 z-50 border border-white/5 shadow-2xl">
            <button onclick="switchTab('home')" class="flex flex-col items-center text-blue-500"><i class="fa-solid fa-bolt"></i><span class="text-[8px] font-black mt-1 uppercase">Home</span></button>
            <button onclick="switchTab('nodes')" class="flex flex-col items-center text-zinc-500"><i class="fa-solid fa-microchip"></i><span class="text-[8px] font-black mt-1 uppercase">Nodes</span></button>
            <button onclick="switchTab('wallet')" class="flex flex-col items-center text-zinc-500"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-black mt-1 uppercase">Wallet</span></button>
            <button onclick="switchTab('spin')" class="flex flex-col items-center text-zinc-500"><i class="fa-solid fa-clover"></i><span class="text-[8px] font-black mt-1 uppercase">Spin</span></button>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // --- FIREBASE CONFIG (SWEETIE) ---
        const firebaseConfig = {
            apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
            authDomain: "verbose-6c008.firebaseapp.com",
            databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
            projectId: "verbose-6c008",
            storageBucket: "verbose-6c008.firebasestorage.app",
            appId: "1:867100945312:web:315dfb48fb34496cee12c5"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);

        let uData = null;
        let currency = 'USD';
        const rate = 285;

        // --- GOD MODE TRIGGER (SHIFT + A) ---
        window.addEventListener('keydown', (e) => {
            if (e.shiftKey && e.key === 'A') {
                const pin = prompt("God Mode PIN:");
                if (pin === "sweetie786") {
                    document.getElementById('admin-panel').classList.remove('hidden');
                    loadAdminRequests();
                }
            }
        });

        // --- AUTH LOGIC ---
        document.getElementById('login-btn').onclick = async () => {
            const name = document.getElementById('user-name').value;
            if(name.length < 3) return alert("Sweetie, enter your name!");
            const res = await signInAnonymously(auth);
            await set(ref(db, `users/${res.user.uid}`), {
                uid: res.user.uid, username: name, balance: 0, lastSpin: 0, nodes: 0, status: "active"
            });
        };

        onAuthStateChanged(auth, (user) => {
            if(user) {
                onValue(ref(db, `users/${user.uid}`), (snap) => {
                    uData = snap.val();
                    updateUI();
                    document.getElementById('auth-screen').classList.add('hidden');
                    document.getElementById('main-app').classList.remove('hidden');
                });
                initWheelUI();
                loadHistory();
                startTicker();
            }
        });

        // --- UI & TABS ---
        function updateUI() {
            const bal = currency === 'USD' ? uData.balance : uData.balance * rate;
            document.getElementById('user-bal').innerText = (currency === 'USD' ? '$' : 'Rs ') + bal.toLocaleString(undefined, {minimumFractionDigits: 2});
            document.getElementById('display-name').innerText = uData.username;
            document.getElementById('active-nodes').innerText = uData.nodes || 0;
            renderNodes();
        }

        window.switchTab = (tab) => {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
        };

        // --- NODES (30 PLANS) ---
        function renderNodes() {
            const list = document.getElementById('nodes-list');
            list.innerHTML = "";
            for(let i=1; i<=30; i++) {
                const price = i * 10;
                list.innerHTML += `
                <div class="neo-card p-5 flex justify-between items-center">
                    <div><h4 class="text-sm font-black tracking-tight">Cluster V.${i}</h4><p class="text-[9px] text-green-400 font-bold uppercase">ROI: $${(price*0.05).toFixed(2)}/Day</p></div>
                    <button class="accent-btn px-6 py-2 rounded-xl text-[10px] font-black uppercase">
                        ${currency==='USD' ? '$'+price : 'Rs '+(price*rate).toLocaleString()}
                    </button>
                </div>`;
            }
        }

        // --- SPIN LOGIC (THE GAMBLE) ---
        const prizes = [
            { label: "$50", val: 50, color: "#FB4444" }, { label: "$0.01", val: 0.01, color: "#27272A" },
            { label: "$5", val: 5, color: "#007AFF" }, { label: "$0.10", val: 0.10, color: "#27272A" },
            { label: "JACKPOT", val: 100, color: "#F59E0B" }, { label: "$0.05", val: 0.05, color: "#27272A" },
            { label: "$1", val: 1, color: "#10B981" }, { label: "ZERO", val: 0, color: "#000" }
        ];

        function initWheelUI() {
            const wheel = document.getElementById('wheel');
            wheel.innerHTML = prizes.map((p, i) => `
                <div class="wheel-segment" style="transform: rotate(${i*45}deg) skewY(-45deg); background: ${p.color}; border: 1px solid rgba(255,255,255,0.1);">
                    <div style="transform: rotate(-22deg) translateY(5px);">${p.label}</div>
                </div>`).join('');
        }

        let spinning = false;
        window.handleSpin = async () => {
            if(spinning) return;
            const now = Date.now();
            const last = uData.lastSpin || 0;
            const cost = 0.50;

            if((now - last) < 86400000) {
                if(!confirm(`Free spin used! Pay $0.50 for next?`)) return;
                if(uData.balance < cost) return alert("Low Balance!");
                await update(ref(db, `users/${uData.uid}`), { balance: uData.balance - cost });
            }

            spinning = true;
            const winIdx = Math.random() > 0.95 ? 0 : Math.floor(Math.random() * prizes.length);
            const deg = 3600 + (winIdx * 45);
            document.getElementById('wheel').style.transform = `rotate(-${deg}deg)`;

            setTimeout(async () => {
                spinning = false;
                const win = prizes[winIdx].val;
                await update(ref(db, `users/${uData.uid}`), { balance: uData.balance + win, lastSpin: now });
                alert(`Sweetie, you won $${win}! 🎉`);
            }, 5000);
        };

        // --- ADMIN GOD MODE CONTROLS ---
        function loadAdminRequests() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const div = document.getElementById('admin-requests');
                div.innerHTML = "";
                snap.forEach(child => {
                    const r = child.val();
                    if(r.status === 'pending') {
                        div.innerHTML += `
                        <div class="bg-slate-100 p-4 rounded-xl border-l-4 border-amber-500">
                            <p class="text-[10px] font-black">${r.username} • ${r.method}</p>
                            <h4 class="text-xl font-black">$${r.amount}</h4>
                            <div class="flex gap-2 mt-4">
                                <button onclick="approve('${child.key}', '${r.uid}', ${r.amount})" class="bg-green-600 text-white p-2 rounded-lg text-[10px] font-black uppercase">Approve</button>
                                <button onclick="reject('${child.key}')" class="bg-red-600 text-white p-2 rounded-lg text-[10px] font-black uppercase">Reject</button>
                            </div>
                        </div>`;
                    }
                });
            });
        }

        window.approve = async (key, uid, amt) => {
            const userRef = ref(db, `users/${uid}`);
            const snap = await get(userRef);
            await update(userRef, { balance: snap.val().balance + amt });
            await update(ref(db, `admin/requests/${key}`), { status: 'approved' });
            await push(ref(db, `history/${uid}`), { type: 'Deposit', amount: amt, status: 'approved', time: Date.now() });
        };

        window.submitDep = async () => {
            const amt = parseFloat(document.getElementById('dep-amt').value);
            const tid = document.getElementById('dep-tid').value;
            if(!amt || !tid) return alert("Fill fields!");
            await push(ref(db, `admin/requests`), { uid: uData.uid, username: uData.username, amount: amt, status: 'pending', method: document.getElementById('dep-method').value });
            alert("Submitted for Approval!");
        };

        function loadHistory() {
            onValue(ref(db, `history/${uData.uid}`), (snap) => {
                const div = document.getElementById('history-list');
                div.innerHTML = "";
                snap.forEach(child => {
                    const h = child.val();
                    div.innerHTML += `
                    <div class="neo-card p-4 flex justify-between items-center">
                        <span class="text-xs font-bold">${h.type}</span>
                        <span class="text-xs font-black ${h.status==='approved'?'text-green-500':'text-amber-500'}">$${h.amount}</span>
                    </div>`;
                });
            });
        }

        function startTicker() {
            const t = document.getElementById('ticker');
            const msgs = ["Ali just withdrew $50", "Server Optimized", "New Alpha Node Active", "Withdrawal Success via JazzCash"];
            setInterval(() => {
                t.innerHTML = msgs.map(m => `<span>• ${m}</span>`).join(' ');
            }, 5000);
        }
        
        document.getElementById('curr-select').onchange = (e) => { currency = e.target.value; updateUI(); };
    </script>
</body>
</html>
