<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GLOBAL | The God-Mode Empire</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --primary: #007AFF; --bg: #09090B; --card: #18181B; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #FAFAFA; overflow-x: hidden; }
        .glass { background: rgba(24, 24, 27, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); }
        .neo-card { background: var(--card); border-radius: 24px; border: 1px solid rgba(255,255,255,0.05); }
        .accent-btn { background: linear-gradient(135deg, #007AFF 0%, #00C6FF 100%); transition: 0.3s; }
        .hidden { display: none; }
        input, select { background: #27272A !important; border: 1px solid #3F3F46 !important; color: white !important; border-radius: 12px !important; padding: 12px !important; outline: none; width: 100%; }
        #wheel { transition: transform 5s cubic-bezier(0.15, 0, 0.15, 1); border: 8px solid #27272A; border-radius: 50%; }
        .wheel-segment { position: absolute; width: 50%; height: 50%; transform-origin: 100% 100%; display: flex; justify-content: center; align-items: flex-start; padding-top: 15px; font-size: 9px; font-weight: 900; }
        @keyframes pulse-green { 0% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.4); } 70% { box-shadow: 0 0 0 10px rgba(16, 185, 129, 0); } 100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); } }
        .trust-pulse { animation: pulse-green 2s infinite; }
    </style>
</head>
<body class="pb-28">

    <!-- Global Ticker -->
    <div class="fixed top-0 w-full z-[60] bg-blue-600/10 py-1 border-b border-blue-500/20 overflow-hidden">
        <div id="ticker" class="whitespace-nowrap flex gap-10 text-[9px] font-black uppercase text-blue-400">
            <span>• Loading Global Markets...</span>
        </div>
    </div>

    <!-- Auth Screen -->
    <div id="auth-screen" class="fixed inset-0 bg-[#09090B] z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-20 h-20 accent-btn rounded-[2.5rem] flex items-center justify-center text-3xl mb-6 shadow-2xl"><i class="fa-solid fa-crown"></i></div>
        <h1 class="text-3xl font-black mb-10 tracking-tighter italic">NEXA <span class="text-[#007AFF]">GLOBAL</span></h1>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Enter Full Name">
            <input type="text" id="refer-input" placeholder="Referral ID (Optional)" class="text-center">
            <button id="login-btn" class="w-full accent-btn p-4 rounded-xl font-black uppercase text-[11px] tracking-widest">Initialize Access</button>
        </div>
    </div>

    <!-- GOD MODE ADMIN (SHIFT + A) -->
    <div id="admin-panel" class="hidden fixed inset-0 bg-white text-black z-[10000] p-6 overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b-2 pb-4 border-red-600">
            <h2 class="text-2xl font-black text-red-600 italic uppercase tracking-tighter">God Mode Control</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div id="admin-requests" class="space-y-4">
            <p class="text-slate-400 text-center italic">Checking for new victims, sweetie...</p>
        </div>
    </div>

    <!-- Main App -->
    <div id="main-app" class="hidden pt-12">
        <header class="p-6 flex justify-between items-center">
            <div>
                <p class="text-[9px] font-bold text-blue-500 uppercase tracking-widest">Imperial Partner</p>
                <h3 id="display-name" class="text-xl font-black tracking-tight">--</h3>
            </div>
            <select id="curr-select" class="!p-1 !w-24 !text-[10px] bg-transparent border-none">
                <option value="USD">USD ($)</option>
                <option value="PKR">PKR (Rs)</option>
            </select>
        </header>

        <!-- Home Tab -->
        <div id="tab-home" class="tab-content p-6 space-y-6">
            <div class="neo-card p-8 accent-btn relative overflow-hidden shadow-2xl">
                <p class="text-[10px] font-bold uppercase opacity-80 tracking-widest">Global Liquidity</p>
                <h1 id="user-bal" class="text-5xl font-black my-2">$0.00</h1>
                <div class="flex gap-2 mt-8">
                    <button onclick="switchTab('wallet')" class="flex-1 bg-white/20 p-3 rounded-xl text-[10px] font-black uppercase">Deposit</button>
                    <button onclick="switchTab('wallet')" class="flex-1 bg-black/20 p-3 rounded-xl text-[10px] font-black uppercase">Withdraw</button>
                </div>
            </div>

            <!-- Referral Card -->
            <div class="neo-card p-6 border-l-4 border-purple-500">
                <div class="flex justify-between items-center mb-2">
                    <h4 class="text-xs font-black uppercase text-purple-400">Referral ID</h4>
                    <span id="ref-id-display" class="text-xs font-mono font-bold text-white">NEXA-XXXX</span>
                </div>
                <button onclick="copyRef()" class="w-full bg-purple-600/20 text-purple-400 p-2 rounded-lg text-[9px] font-black uppercase border border-purple-500/30">Copy Invite Link</button>
            </div>
        </div>

        <!-- Spin Tab -->
        <div id="tab-spin" class="tab-content hidden p-6 text-center">
            <h2 class="text-2xl font-black mb-8 italic">Neon <span class="text-amber-400">Jackpot</span></h2>
            <div class="relative w-64 h-64 mx-auto mb-10">
                <div class="absolute -top-4 left-1/2 -translate-x-1/2 z-50 text-amber-400 text-3xl"><i class="fa-solid fa-caret-down"></i></div>
                <div id="wheel" class="relative w-full h-full overflow-hidden shadow-[0_0_50px_rgba(251,191,36,0.2)]"></div>
            </div>
            <button onclick="handleSpin()" id="spin-btn" class="w-full accent-btn p-5 rounded-2xl font-black uppercase text-[11px] shadow-xl active:scale-95 transition-all">Try My Luck ($0.50)</button>
        </div>

        <!-- Wallet Tab -->
        <div id="tab-wallet" class="tab-content hidden p-6 space-y-6">
            <div class="neo-card p-6 space-y-4">
                <h4 class="text-xs font-black uppercase text-blue-500">Deposit Hub</h4>
                <div class="space-y-1 text-[10px] bg-black/20 p-3 rounded-xl">
                    <div class="flex justify-between"><span>JazzCash / SadaPay:</span> <b class="text-white">03705519562</b></div>
                    <div class="flex justify-between"><span>EasyPaisa:</span> <b class="text-white">03379827882</b></div>
                </div>
                <select id="dep-method">
                    <option value="JazzCash">JazzCash</option>
                    <option value="SadaPay">SadaPay</option>
                    <option value="EasyPaisa">EasyPaisa</option>
                    <option value="Binance">Binance (USDT)</option>
                </select>
                <input type="number" id="dep-amt" placeholder="Amount (USD)">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)">
                <button onclick="submitDep()" class="w-full accent-btn p-4 rounded-xl font-black text-[10px] uppercase">Submit Deposit</button>
            </div>

            <div class="neo-card p-6 space-y-4 border-l-4 border-red-500">
                <h4 class="text-xs font-black uppercase text-red-500">Withdraw Hub</h4>
                <input type="number" id="wit-amt" placeholder="Withdraw Amount">
                <input type="text" id="wit-acc" placeholder="Account Number">
                <button onclick="submitWit()" class="w-full bg-zinc-800 p-4 rounded-xl font-black text-[10px] uppercase">Withdraw Funds</button>
            </div>

            <div id="history-list" class="space-y-2"></div>
        </div>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2rem] flex justify-around items-center px-4 z-50 border border-white/5 shadow-2xl">
            <button onclick="switchTab('home')" class="flex flex-col items-center text-blue-500"><i class="fa-solid fa-house"></i><span class="text-[8px] font-black mt-1 uppercase">Home</span></button>
            <button onclick="switchTab('spin')" class="flex flex-col items-center text-zinc-500"><i class="fa-solid fa-clover"></i><span class="text-[8px] font-black mt-1 uppercase">Spin</span></button>
            <button onclick="switchTab('wallet')" class="flex flex-col items-center text-zinc-500"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-black mt-1 uppercase">Wallet</span></button>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        const PKR_RATE = 285;

        // --- AUTH & INITIALIZATION ---
        document.getElementById('login-btn').onclick = async () => {
            const name = document.getElementById('user-name').value;
            const referBy = document.getElementById('refer-input').value;
            if(name.length < 3) return alert("Enter your name, sweetie!");
            const res = await signInAnonymously(auth);
            await set(ref(db, `users/${res.user.uid}`), {
                uid: res.user.uid, username: name, balance: 2, nodes: 0, lastSpin: 0, referredBy: referBy || null
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
                startTrustEngine();
            }
        });

        function updateUI() {
            const displayBal = currency === 'USD' ? uData.balance : uData.balance * PKR_RATE;
            document.getElementById('user-bal').innerText = (currency === 'USD' ? '$' : 'Rs ') + displayBal.toLocaleString(undefined, {minimumFractionDigits: 2});
            document.getElementById('display-name').innerText = uData.username;
            document.getElementById('ref-id-display').innerText = `NEXA-${uData.uid.substring(0, 6).toUpperCase()}`;
        }

        window.switchTab = (tab) => {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
        };

        // --- SPIN LOGIC (RIGGED FOR LOOT) ---
        const prizes = [
            { label: "$100", val: 100, color: "#FB4444" }, { label: "$0.01", val: 0.01, color: "#18181B" },
            { label: "$5", val: 5, color: "#007AFF" }, { label: "$0.05", val: 0.05, color: "#18181B" },
            { label: "JACKPOT", val: 50, color: "#F59E0B" }, { label: "TRY AGAIN", val: 0, color: "#000" },
            { label: "$1", val: 1, color: "#10B981" }, { label: "$0.02", val: 0.02, color: "#18181B" }
        ];

        function initWheelUI() {
            const wheel = document.getElementById('wheel');
            wheel.innerHTML = prizes.map((p, i) => `
                <div class="wheel-segment" style="transform: rotate(${i*45}deg) skewY(-45deg); background: ${p.color};">
                    <div style="transform: rotate(-22deg) translateY(5px); color: ${p.color==='#18181B'?'#555':'white'};">${p.label}</div>
                </div>`).join('');
        }

        let isSpinning = false;
        window.handleSpin = async () => {
            if(isSpinning) return;
            const now = Date.now();
            if((now - (uData.lastSpin || 0)) < 86400000) {
                if(!confirm("Free spin used! Pay $0.50 to spin again?")) return;
                if(uData.balance < 0.50) return alert("Insufficient balance, sweetie!");
                await update(ref(db, `users/${uData.uid}`), { balance: uData.balance - 0.50 });
            }

            isSpinning = true;
            // Rigging: High win only if luck > 98%
            const winIdx = Math.random() > 0.98 ? 0 : Math.random() > 0.5 ? 5 : 1; 
            const deg = 3600 + (winIdx * 45);
            document.getElementById('wheel').style.transform = `rotate(-${deg}deg)`;

            setTimeout(async () => {
                isSpinning = false;
                const win = prizes[winIdx].val;
                await update(ref(db, `users/${uData.uid}`), { balance: uData.balance + win, lastSpin: now });
                alert(`Sweetie! You won $${win}! 🎉`);
            }, 5000);
        };

        // --- WALLET LOGIC ---
        window.submitDep = async () => {
            const amt = parseFloat(document.getElementById('dep-amt').value);
            const tid = document.getElementById('dep-tid').value;
            if(!amt || !tid) return alert("Enter details!");
            await push(ref(db, `admin/requests`), { 
                uid: uData.uid, username: uData.username, amount: amt, status: 'pending', type: 'Deposit', tid: tid, method: document.getElementById('dep-method').value, time: Date.now() 
            });
            alert("Deposit Submitted! Admin will verify soon.");
        };

        window.submitWit = async () => {
            const amt = parseFloat(document.getElementById('wit-amt').value);
            if(uData.balance < amt) return alert("Low balance!");
            if(uData.balance < 10) return alert("Min withdraw $10!");
            await push(ref(db, `admin/requests`), { 
                uid: uData.uid, username: uData.username, amount: amt, status: 'pending', type: 'Withdrawal', account: document.getElementById('wit-acc').value, time: Date.now() 
            });
            alert("Withdrawal Pending!");
        };

        // --- ADMIN GOD MODE ---
        window.loadAdminRequests = () => {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const div = document.getElementById('admin-requests');
                div.innerHTML = "";
                snap.forEach(child => {
                    const r = child.val();
                    if(r.status === 'pending') {
                        div.innerHTML += `
                        <div class="bg-slate-100 p-4 rounded-xl border-l-4 border-amber-500 shadow-md">
                            <p class="text-[10px] font-black uppercase text-slate-500">${r.type} - ${r.username}</p>
                            <h4 class="text-xl font-black">$${r.amount}</h4>
                            <p class="text-[9px] font-mono">${r.tid || r.account}</p>
                            <div class="flex gap-2 mt-4">
                                <button onclick="approveReq('${child.key}', '${r.uid}', ${r.amount}, '${r.type}')" class="flex-1 bg-green-600 text-white p-2 rounded-lg text-[10px] font-black uppercase">Approve</button>
                                <button onclick="rejectReq('${child.key}')" class="flex-1 bg-red-600 text-white p-2 rounded-lg text-[10px] font-black uppercase">Reject</button>
                            </div>
                        </div>`;
                    }
                });
            });
        };

        window.approveReq = async (key, uid, amt, type) => {
            const userRef = ref(db, `users/${uid}`);
            const userSnap = await get(userRef);
            const currentBal = userSnap.val().balance || 0;
            const newBal = type === 'Deposit' ? currentBal + amt : currentBal - amt;
            
            await update(userRef, { balance: newBal });
            await update(ref(db, `admin/requests/${key}`), { status: 'approved' });
            
            // Referral Commission (10%)
            if(type === 'Deposit' && userSnap.val().referredBy) {
                const inviterId = userSnap.val().referredBy.replace('NEXA-', '').toLowerCase();
                // (Note: Simplified refer logic for single file)
            }
            alert("Action Successful!");
        };

        // --- TRUST & ADDICTION ENGINE ---
        function startTrustEngine() {
            const ticker = document.getElementById('ticker');
            const msgs = ["Ali (Multan) withdrawn Rs 4,500", "New Deposit of $100 via EasyPaisa", "Zoya just won $50 in Spin!", "System Upgrade Complete"];
            setInterval(() => {
                ticker.innerHTML = msgs.map(m => `<span>• ${m}</span>`).join(' ');
            }, 5000);
        }

        document.getElementById('curr-select').onchange = (e) => { currency = e.target.value; updateUI(); };
        window.copyRef = () => { alert("Invite Link Copied! Send to friends, sweetie!"); };
    </script>
</body>
</html>
