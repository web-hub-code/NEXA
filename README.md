<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA CLOUD | Premium Mining Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --gold: #FACC15; --dark: #0F172A; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #0b0f1a; color: white; overflow-x: hidden; }
        
        /* Cloud-Node Specific Styling */
        .glass-card { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); border-radius: 28px; }
        .btn-premium { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 18px; transition: 0.3s; box-shadow: 0 10px 20px -5px rgba(37, 99, 235, 0.5); }
        .btn-premium:active { transform: scale(0.95); }
        .text-gradient { background: linear-gradient(to right, #60A5FA, #A78BFA); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        
        /* Live Popup Animation */
        #cloud-notif { position: fixed; top: 25px; left: 50%; transform: translateX(-50%) translateY(-200px); z-index: 9999; transition: 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275); width: 90%; max-width: 350px; }
        .notif-active { transform: translateX(-50%) translateY(0) !important; }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 0px; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .tab-content { animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // --- Data Arrays (30 Nodes) ---
        const usdNodes = Array.from({length: 15}, (_, i) => ({
            id: `U${i+1}`, name: `X-Cloud USD ${i+1}`, price: (i + 1) * 10, daily: ((i + 1) * 0.95).toFixed(2), total: ((i+1) * 0.95 * 360).toFixed(0)
        }));
        const pkrNodes = Array.from({length: 15}, (_, i) => ({
            id: `P${i+1}`, name: `Nexa PKR ${i+1}`, price: (i + 1) * 500, daily: ((i + 1) * 45).toFixed(0), total: ((i+1) * 45 * 360).toFixed(0)
        }));

        // --- Authentication Logic ---
        window.accessSystem = async (type) => {
            const user = document.getElementById('user-field').value;
            if(!user) return alert("Sweetie, enter your access ID! 💋");
            try {
                await signInAnonymously(auth);
                const uid = auth.currentUser.uid;
                const userRef = ref(db, 'users/' + uid);
                const snap = await get(userRef);
                if(type === 'reg' && !snap.exists()) {
                    await set(userRef, { username: user, balance: 2.0, pkr: 200, uid: uid, logs: [] });
                    localStorage.setItem('nexa_session', uid);
                    location.reload();
                } else if(type === 'log' && snap.exists()) {
                    localStorage.setItem('nexa_session', uid);
                    location.reload();
                } else { alert("ID Error or Account already exists!"); }
            } catch (e) { alert(e.message); }
        };

        window.onload = () => {
            const session = localStorage.getItem('nexa_session');
            if(session) {
                document.getElementById('welcome-screen').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                loadUserData(session);
                startPopups();
                renderNodes();
            }
        };

        function loadUserData(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                const d = s.val();
                document.getElementById('nav-user').innerText = d.username;
                document.getElementById('header-usd').innerText = "$" + d.balance.toFixed(2);
                document.getElementById('header-pkr').innerText = "Rs. " + d.pkr;
                document.getElementById('dash-bal').innerText = "$" + d.balance.toFixed(2);
            });
            onValue(ref(db, 'admin/settings'), (s) => { window.adminData = s.val(); });
        }

        function startPopups() {
            const names = ["Ahmad K.", "Sarah Ali", "Zain786", "User_99", "Someone from Dubai"];
            const amounts = ["$4,000", "Rs. 15,000", "$120", "Rs. 2,500", "$45,000"];
            setInterval(() => {
                const toast = document.getElementById('cloud-notif');
                document.getElementById('notif-user').innerText = names[Math.floor(Math.random()*names.length)];
                document.getElementById('notif-amt').innerText = amounts[Math.floor(Math.random()*amounts.length)];
                toast.classList.add('notif-active');
                setTimeout(() => toast.classList.remove('notif-active'), 5000);
            }, 12000);
        }

        function renderNodes() {
            const uWrap = document.getElementById('usd-grid');
            const pWrap = document.getElementById('pkr-grid');
            usdNodes.forEach(n => {
                uWrap.innerHTML += `<div class="glass-card p-6 border-b-2 border-blue-500">
                    <div class="flex justify-between items-start mb-4">
                        <p class="text-[10px] font-black uppercase text-blue-400">Premium Node</p>
                        <p class="text-xl font-black text-white">$${n.price}</p>
                    </div>
                    <h3 class="font-bold text-lg mb-4 italic">${n.name}</h3>
                    <div class="space-y-2 mb-6">
                        <div class="flex justify-between text-[10px] font-bold opacity-60"><span>DAILY PROFIT</span><span class="text-blue-400">$${n.daily}</span></div>
                        <div class="flex justify-between text-[10px] font-bold opacity-60"><span>TOTAL YIELD</span><span class="text-blue-400">$${n.total}</span></div>
                        <div class="flex justify-between text-[10px] font-bold opacity-60"><span>CONTRACT</span><span>360 DAYS</span></div>
                    </div>
                    <button onclick="switchTab('wallet')" class="w-full btn-premium py-4 text-[10px]">Buy Infrastructure</button>
                </div>`;
            });
            pkrNodes.forEach(n => {
                pWrap.innerHTML += `<div class="glass-card p-6 border-b-2 border-yellow-500">
                    <div class="flex justify-between items-start mb-4">
                        <p class="text-[10px] font-black uppercase text-yellow-400">Economy Node</p>
                        <p class="text-xl font-black text-white">Rs. ${n.price}</p>
                    </div>
                    <h3 class="font-bold text-lg mb-4 italic">${n.name}</h3>
                    <div class="space-y-2 mb-6">
                        <div class="flex justify-between text-[10px] font-bold opacity-60"><span>DAILY PROFIT</span><span class="text-yellow-400">Rs. ${n.daily}</span></div>
                        <div class="flex justify-between text-[10px] font-bold opacity-60"><span>TOTAL YIELD</span><span class="text-yellow-400">Rs. ${n.total}</span></div>
                        <div class="flex justify-between text-[10px] font-bold opacity-60"><span>CONTRACT</span><span>360 DAYS</span></div>
                    </div>
                    <button onclick="switchTab('wallet')" class="w-full bg-yellow-500 text-black font-black rounded-2xl py-4 text-[10px]">Buy Infrastructure</button>
                </div>`;
            });
        }

        window.openPay = (mode) => {
            const n = mode === 'jazz' ? window.adminData.jazz : window.adminData.easy;
            prompt(`Cloud Node Secure Deposit:\nMethod: ${mode.toUpperCase()}\nAccount: ${n}\n\nEnter Transaction ID:`, "");
        };

        window.switchTab = (tab) => {
            ['home', 'mine', 'wallet', 'info'].forEach(t => document.getElementById('sec-'+t).classList.add('hidden'));
            document.getElementById('sec-'+tab).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(i => i.style.color = '#94a3b8');
            event.currentTarget.style.color = '#2563EB';
        };
    </script>
</head>
<body class="pb-32">

    <!-- Notification -->
    <div id="cloud-notif" class="glass-card p-4 flex items-center gap-4 border-l-4 border-blue-500 shadow-2xl">
        <div class="w-10 h-10 bg-blue-500/20 text-blue-500 rounded-full flex items-center justify-center animate-pulse"><i class="fa-solid fa-check-double"></i></div>
        <div>
            <p id="notif-user" class="text-[10px] font-black text-slate-400 uppercase">...</p>
            <p class="text-xs font-black">Withdrawal success: <span id="notif-amt" class="text-blue-500">...</span></p>
        </div>
    </div>

    <!-- Login -->
    <div id="welcome-screen" class="fixed inset-0 bg-[#0b0f1a] z-[10000] p-10 flex flex-col justify-center">
        <div class="text-center mb-12">
            <div class="w-24 h-24 bg-gradient-to-tr from-blue-600 to-purple-600 rounded-[2.5rem] flex items-center justify-center mx-auto rotate-12 mb-6 shadow-2xl">
                <i class="fa-solid fa-cloud text-white text-4xl -rotate-12"></i>
            </div>
            <h1 class="text-4xl font-black italic text-gradient tracking-tighter">NEXA CLOUD</h1>
            <p class="text-[10px] font-black text-slate-500 mt-4 uppercase tracking-[0.4em]">Decentralized Enterprise</p>
        </div>
        <div class="space-y-4">
            <input id="user-field" type="text" placeholder="Enter Access Identity" class="w-full p-6 glass-card outline-none font-bold text-white text-center">
            <button onclick="accessSystem('log')" class="w-full btn-premium py-5 text-xs uppercase tracking-widest">Connect Terminal</button>
            <button onclick="accessSystem('reg')" class="w-full bg-white/5 border border-white/10 text-white py-5 rounded-2xl font-black text-[10px] uppercase">Initialize Account</button>
        </div>
    </div>

    <!-- Header -->
    <header class="p-6 flex justify-between items-center sticky top-0 bg-[#0b0f1a]/80 backdrop-blur-xl z-50 border-b border-white/5">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center text-white shadow-lg shadow-blue-500/30"><i class="fa-solid fa-bolt text-xs"></i></div>
            <span id="nav-user" class="font-black italic text-xs tracking-tight">...</span>
        </div>
        <div class="text-right">
            <p id="header-usd" class="text-blue-500 font-black leading-none">$0.00</p>
            <p id="header-pkr" class="text-[9px] font-bold text-slate-500 mt-1">Rs. 0</p>
        </div>
    </header>

    <main class="p-5">

        <!-- Home Tab -->
        <div id="sec-home" class="tab-content space-y-6">
            <div class="glass-card p-8 bg-gradient-to-br from-blue-900/40 to-transparent border-none">
                <h1 class="text-4xl font-black italic leading-none mb-4">Cloud<br><span class="text-gradient">Infrastructure</span></h1>
                <p class="text-[11px] font-bold text-slate-400 leading-relaxed mb-8">NEXA provides high-performance computing nodes for stable daily dividends. Deploy your nodes in seconds.</p>
                <div class="flex gap-4">
                    <button onclick="switchTab('mine')" class="btn-premium px-8 py-4 text-[10px]">Deploy Nodes</button>
                    <button onclick="switchTab('info')" class="bg-white/10 px-8 py-4 rounded-2xl text-[10px] font-black">Whitepaper</button>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div class="glass-card p-5">
                    <p class="text-[10px] font-black text-slate-500 uppercase mb-1">Live Users</p>
                    <h3 class="text-2xl font-black">42.8K</h3>
                </div>
                <div class="glass-card p-5">
                    <p class="text-[10px] font-black text-slate-500 uppercase mb-1">Nodes Active</p>
                    <h3 class="text-2xl font-black text-blue-500">1,240</h3>
                </div>
            </div>

            <div class="glass-card p-6">
                <h3 class="text-xs font-black uppercase text-blue-500 mb-4">Market Pulse</h3>
                <div class="space-y-4">
                    <div class="flex justify-between items-center"><span class="text-xs font-bold italic"><i class="fa-brands fa-bitcoin text-orange-500 mr-2"></i>Bitcoin</span><span class="text-xs font-black">$69,240.50</span></div>
                    <div class="flex justify-between items-center"><span class="text-xs font-bold italic"><i class="fa-brands fa-ethereum text-blue-400 mr-2"></i>Ethereum</span><span class="text-xs font-black">$3,812.10</span></div>
                </div>
            </div>
        </div>

        <!-- Nodes Tab (30 Nodes) -->
        <div id="sec-mine" class="tab-content hidden space-y-8">
            <div class="flex gap-3 overflow-x-auto no-scrollbar pb-2">
                <button class="bg-blue-600 text-white px-6 py-3 rounded-xl text-[10px] font-black uppercase flex-shrink-0">USD Nodes (15)</button>
                <button class="glass-card px-6 py-3 rounded-xl text-[10px] font-black uppercase flex-shrink-0">PKR Nodes (15)</button>
            </div>

            <h3 class="text-[10px] font-black uppercase text-slate-500 tracking-widest">Available Dollar Nodes</h3>
            <div id="usd-grid" class="space-y-4"></div>

            <h3 class="text-[10px] font-black uppercase text-slate-500 tracking-widest mt-12">Available PKR Nodes</h3>
            <div id="pkr-grid" class="space-y-4"></div>
        </div>

        <!-- Wallet Tab -->
        <div id="sec-wallet" class="tab-content hidden space-y-6">
            <div class="glass-card p-10 text-center bg-gradient-to-t from-blue-600/20 to-transparent">
                <p class="text-[10px] font-black text-blue-400 uppercase mb-2">Withdrawable Balance</p>
                <h1 id="dash-bal" class="text-5xl font-black">$0.00</h1>
                <div class="grid grid-cols-2 gap-4 mt-10">
                    <button onclick="openPay('jazz')" class="btn-premium py-4 text-[10px]">Deposit</button>
                    <button class="bg-white/10 py-4 rounded-2xl font-black text-[10px]">Withdraw</button>
                </div>
            </div>

            <div class="glass-card p-8">
                <h3 class="text-xs font-black uppercase mb-6 italic border-b border-white/5 pb-4">Secure Checkout</h3>
                <div class="space-y-4">
                    <input type="text" placeholder="Wallet Address / Number" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none text-xs font-bold">
                    <input type="number" placeholder="Enter Amount" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none text-xs font-bold">
                    <button class="w-full btn-premium py-5 text-[10px] uppercase tracking-widest">Process Withdrawal</button>
                </div>
            </div>
        </div>

        <!-- Info Tab -->
        <div id="sec-info" class="tab-content hidden space-y-6">
            <div class="glass-card p-6">
                <h2 class="text-xl font-black italic mb-4 text-gradient">About NEXA Shard</h2>
                <p class="text-[11px] text-slate-400 leading-relaxed font-bold">NEXA is a decentralized cloud mining protocol. We utilize Shard-Mining technology to distribute hashing power across 3,000 global servers, ensuring consistent yields even during market volatility.</p>
            </div>
            <div class="glass-card p-6 border-l-4 border-blue-500">
                <h3 class="text-xs font-black uppercase mb-3">24/7 Monitoring</h3>
                <p class="text-[10px] text-slate-500 font-bold">Our engineers monitor node health every millisecond. Your profits are guaranteed by our Liquidity Protection Fund (LPF).</p>
            </div>
            <div class="glass-card p-6 bg-blue-600/10">
                <h3 class="text-xs font-black uppercase mb-2">Referral Program</h3>
                <p class="text-[10px] font-bold">Earn 10% direct commission when your friends deploy their first node. Rewards are credited instantly.</p>
            </div>
        </div>

    </main>

    <!-- Nav Bar -->
    <nav class="fixed bottom-6 left-6 right-6 h-22 glass-card rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] border-t border-white/10 shadow-2xl">
        <button onclick="switchTab('home')" class="nav-icon text-blue-600 p-4"><i class="fa-solid fa-house"></i></button>
        <button onclick="switchTab('mine')" class="nav-icon p-4"><i class="fa-solid fa-server"></i></button>
        <button onclick="switchTab('wallet')" class="nav-icon p-4"><i class="fa-solid fa-wallet"></i></button>
        <button onclick="switchTab('info')" class="nav-icon p-4"><i class="fa-solid fa-shield-halved"></i></button>
    </nav>

</body>
</html>
