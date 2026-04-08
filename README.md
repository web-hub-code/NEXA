<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GOLD | Global Wealth Engine</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --accent: #635bff; --gold: #f59e0b; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #0f172a; color: #f8fafc; overflow-x: hidden; }
        
        /* Futuristic Glassmorphism */
        .glass-card { background: rgba(30, 41, 59, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.1); border-radius: 28px; }
        .premium-card { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); border: 1px solid rgba(99, 91, 255, 0.3); position: relative; overflow: hidden; }
        
        /* Animations */
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
        .animate-float { animation: float 3s ease-in-out infinite; }
        .page-transition { animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.98); } to { opacity: 1; transform: scale(1); } }
        
        /* Ticker Animation */
        .ticker-wrap { background: rgba(0,0,0,0.3); overflow: hidden; height: 30px; }
        .ticker { display: inline-block; white-space: nowrap; animation: ticker 20s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        .btn-glow { box-shadow: 0 0 15px rgba(99, 91, 255, 0.4); transition: 0.3s; }
        .btn-glow:active { transform: scale(0.95); }
        .nav-active { color: #635bff !important; filter: drop-shadow(0 0 5px #635bff); }
    </style>
</head>
<body class="pb-32">

    <!-- GLOBAL ANNOUNCEMENT TICKER -->
    <div class="ticker-wrap fixed top-0 left-0 right-0 z-[100] border-b border-white/5">
        <div class="ticker text-[10px] font-bold text-blue-400 py-1 uppercase tracking-widest" id="global-announcement">
            Welcome to Nexa Gold Global • Automated Mining Clusters are now Live • Join our official Telegram for Daily Rewards •
        </div>
    </div>

    <!-- AUTH SCREEN -->
    <div id="auth-screen" class="fixed inset-0 bg-[#0f172a] z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-24 h-24 premium-card flex items-center justify-center text-blue-500 text-5xl mb-8 animate-float">
            <i class="fa-solid fa-atom"></i>
        </div>
        <h1 class="text-3xl font-extrabold tracking-tighter">NEXA <span class="text-blue-500">ULTIMATE</span></h1>
        <p class="text-[9px] font-black text-slate-500 uppercase tracking-[6px] mb-12">Global Infrastructure</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Full Name" class="w-full p-5 glass-card bg-white/5 outline-none text-sm font-bold border-none">
            <input type="password" id="admin-key" placeholder="Security PIN" class="w-full p-5 glass-card bg-white/5 outline-none text-sm font-bold border-none">
            <button onclick="handleLogin()" class="w-full bg-blue-600 text-white p-5 rounded-3xl font-black uppercase text-[10px] tracking-widest btn-glow">Initialize Session</button>
        </div>
    </div>

    <div id="app" class="hidden pt-10">
        <!-- HEADER -->
        <header class="p-6 flex justify-between items-center">
            <div>
                <p class="text-[8px] font-black text-blue-500 uppercase tracking-widest">Active Partner</p>
                <h3 id="display-name" class="text-xl font-extrabold tracking-tight">--</h3>
            </div>
            <div class="flex gap-3">
                <div class="glass-card px-3 py-2 flex items-center gap-2 border-blue-500/30">
                    <i class="fa-brands fa-bitcoin text-yellow-500"></i>
                    <span id="btc-price" class="text-[10px] font-black text-slate-300">$64,231</span>
                </div>
                <button onclick="logout()" class="w-11 h-11 glass-card flex items-center justify-center text-red-500 border-red-500/20"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <!-- DASHBOARD -->
        <main id="page-home" class="page-content px-6 space-y-6 page-transition">
            <!-- LUXURY BANK CARD -->
            <div class="premium-card p-8 rounded-[40px] border-none shadow-2xl shadow-blue-900/20">
                <div class="flex justify-between items-start mb-12">
                    <div class="w-12 h-8 glass-card border-white/10 flex items-center justify-center"><div class="w-6 h-4 bg-yellow-600/50 rounded-sm"></div></div>
                    <img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Visa_Inc._logo.svg" class="h-4 opacity-50 grayscale invert">
                </div>
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Global Liquidity</p>
                <h2 id="user-bal" class="text-4xl font-extrabold my-2">$0.00</h2>
                <div class="flex justify-between items-end mt-12">
                    <p class="text-[10px] font-black text-blue-400">NEXA PRESTIGE</p>
                    <div class="flex gap-4">
                        <button onclick="nav('deposit')" class="text-[9px] font-black uppercase bg-white/10 px-4 py-2 rounded-lg">Add</button>
                        <button onclick="nav('withdraw')" class="text-[9px] font-black uppercase bg-blue-600 px-4 py-2 rounded-lg">Payout</button>
                    </div>
                </div>
            </div>

            <!-- QUICK FEATURES -->
            <div class="grid grid-cols-4 gap-4">
                <button onclick="openSpin()" class="flex flex-col items-center gap-2">
                    <div class="w-14 h-14 glass-card flex items-center justify-center text-amber-500 text-xl"><i class="fa-solid fa-dharmachakra"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Spin</span>
                </button>
                <button onclick="nav('team')" class="flex flex-col items-center gap-2">
                    <div class="w-14 h-14 glass-card flex items-center justify-center text-indigo-500 text-xl"><i class="fa-solid fa-users-rays"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Team</span>
                </button>
                <button onclick="openRedeem()" class="flex flex-col items-center gap-2">
                    <div class="w-14 h-14 glass-card flex items-center justify-center text-emerald-500 text-xl"><i class="fa-solid fa-ticket"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Promo</span>
                </button>
                <button onclick="nav('info')" class="flex flex-col items-center gap-2">
                    <div class="w-14 h-14 glass-card flex items-center justify-center text-slate-400 text-xl"><i class="fa-solid fa-shield-halved"></i></div>
                    <span class="text-[8px] font-black uppercase text-slate-400">Trust</span>
                </button>
            </div>

            <!-- LIVE STATS -->
            <div class="glass-card p-6 bg-gradient-to-r from-blue-900/20 to-transparent">
                <div class="flex justify-between items-center">
                    <div>
                        <p class="text-[9px] font-black text-slate-400 uppercase">Profit Accrued (24h)</p>
                        <h4 id="daily-earnings" class="text-xl font-extrabold text-emerald-500">+$0.00</h4>
                    </div>
                    <div class="text-right">
                        <p class="text-[9px] font-black text-slate-400 uppercase">Active Clusters</p>
                        <h4 id="active-plans" class="text-xl font-extrabold">0</h4>
                    </div>
                </div>
            </div>
        </main>

        <!-- NODES PAGE -->
        <main id="page-nodes" class="page-content hidden px-6 py-6 space-y-4 page-transition">
            <h2 class="text-2xl font-extrabold tracking-tight">Mining Clusters</h2>
            <div id="nodes-container" class="space-y-4 pb-20"></div>
        </main>

        <!-- TEAM PAGE -->
        <main id="page-team" class="page-content hidden px-6 py-6 space-y-6 page-transition">
            <h2 class="text-2xl font-extrabold tracking-tight">Affiliate Network</h2>
            <div class="grid grid-cols-3 gap-2">
                <div class="glass-card p-4 text-center border-blue-500/20"><p class="text-[8px] font-black text-slate-500">LVL 1</p><p id="t1" class="text-lg font-black">0</p></div>
                <div class="glass-card p-4 text-center border-indigo-500/20"><p class="text-[8px] font-black text-slate-500">LVL 2</p><p id="t2" class="text-lg font-black">0</p></div>
                <div class="glass-card p-4 text-center border-purple-500/20"><p class="text-[8px] font-black text-slate-500">LVL 3</p><p id="t3" class="text-lg font-black">0</p></div>
            </div>
            <div class="glass-card p-6"><p class="text-[10px] font-black text-slate-400 uppercase mb-2">Referral Link</p><div onclick="copyLink()" class="bg-black/30 p-4 rounded-xl text-[10px] font-mono break-all text-blue-400 border border-white/5" id="ref-link">https://nexagold.app/ref?id=...</div></div>
        </main>

        <!-- ADMIN COMMAND CENTER -->
        <main id="page-admin" class="page-content hidden px-6 py-6 space-y-6 page-transition">
            <h2 class="text-2xl font-extrabold text-red-500 tracking-tighter uppercase italic">Control Room</h2>
            
            <div class="glass-card p-5 space-y-4">
                <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Global Announcement</h3>
                <input id="ann-text" placeholder="Update news ticker..." class="w-full p-4 bg-white/5 rounded-xl text-xs font-bold border-none outline-none">
                <button onclick="setAnnouncement()" class="w-full bg-blue-600 text-white p-3 rounded-xl text-[10px] font-black uppercase">Publish News</button>
            </div>

            <div class="glass-card p-5 space-y-4">
                <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-widest">User Management (Ban/Edit)</h3>
                <input id="manage-uid" placeholder="Enter User UID" class="w-full p-4 bg-white/5 rounded-xl text-xs font-bold border-none outline-none">
                <div class="grid grid-cols-2 gap-2">
                    <button onclick="banUser()" class="bg-red-600 text-white p-3 rounded-xl text-[10px] font-black uppercase">Ban User</button>
                    <button onclick="unbanUser()" class="bg-green-600 text-white p-3 rounded-xl text-[10px] font-black uppercase">Unban User</button>
                </div>
                <input id="edit-bal" placeholder="Update Balance" class="w-full p-4 bg-white/5 rounded-xl text-xs font-bold border-none outline-none">
                <button onclick="updateUserBal()" class="w-full bg-slate-100 text-black p-3 rounded-xl text-[10px] font-black uppercase">Update Funds</button>
            </div>

            <div id="admin-req-list" class="space-y-4"></div>
        </main>

        <!-- NAVIGATION -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass-card border-white/10 flex justify-around items-center z-[100] shadow-2xl">
            <div onclick="nav('home')" class="nav-item flex flex-col items-center flex-1 text-slate-500" id="btn-home"><i class="fa-solid fa-house-chimney-window"></i><span class="text-[7px] font-black mt-1 uppercase">Bank</span></div>
            <div onclick="nav('nodes')" class="nav-item flex flex-col items-center flex-1 text-slate-500" id="btn-nodes"><i class="fa-solid fa-bolt-lightning"></i><span class="text-[7px] font-black mt-1 uppercase">Nodes</span></div>
            <div onclick="nav('team')" class="nav-item flex flex-col items-center flex-1 text-slate-500" id="btn-team"><i class="fa-solid fa-network-wired"></i><span class="text-[7px] font-black mt-1 uppercase">Network</span></div>
            <div onclick="nav('admin')" class="nav-item hidden flex flex-col items-center flex-1 text-red-500" id="btn-admin"><i class="fa-solid fa-microchip"></i><span class="text-[7px] font-black mt-1 uppercase">Root</span></div>
        </nav>
    </div>

    <!-- SPIN WHEEL MODAL -->
    <div id="spin-modal" class="hidden fixed inset-0 bg-black/90 backdrop-blur-xl z-[1000] flex items-center justify-center p-8">
        <div class="text-center space-y-8">
            <h3 class="text-2xl font-black uppercase tracking-tighter">Daily Lucky Spin</h3>
            <div id="wheel" class="w-64 h-64 border-8 border-blue-600 rounded-full flex items-center justify-center relative shadow-2xl shadow-blue-500/40">
                <i class="fa-solid fa-star text-4xl text-yellow-500"></i>
                <div class="absolute inset-0 border-4 border-dashed border-white/20 rounded-full animate-[spin_10s_linear_infinite]"></div>
            </div>
            <button onclick="startSpin()" class="bg-blue-600 text-white px-12 py-4 rounded-full font-black uppercase text-sm tracking-widest shadow-xl">Spin Now</button>
            <p onclick="document.getElementById('spin-modal').classList.add('hidden')" class="text-slate-500 text-[10px] font-bold uppercase cursor-pointer">Close</p>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // CONFIG (Replace with your actual keys)
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
        let userData = null, uid = "";

        // LOGIN SYSTEM
        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return alert("Full Name Required, Sweetie!");
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const s = await get(ref(db, `users/${uid}`));
            if(!s.exists()) {
                await set(ref(db, `users/${uid}`), { username: name, balance: 0, role: (key==="sweetie786"?"admin":"user"), status: 'active', joined: Date.now() });
            } else if(key==="sweetie786") {
                await update(ref(db, `users/${uid}`), { role: "admin" });
            }
            location.reload();
        };

        onAuthStateChanged(auth, u => {
            if(u) {
                uid = u.uid;
                onValue(ref(db, `users/${uid}`), s => {
                    userData = s.val();
                    if(!userData) return;
                    if(userData.status === 'banned') return document.body.innerHTML = "<div class='flex items-center justify-center h-screen bg-black text-red-500 font-black uppercase tracking-widest'>Your Account has been Banned.</div>";
                    
                    document.getElementById('display-name').innerText = userData.username;
                    document.getElementById('user-bal').innerText = `$${(userData.balance || 0).toFixed(2)}`;
                    document.getElementById('active-plans').innerText = userData.plans || 0;
                    document.getElementById('ref-link').innerText = `https://nexagold.app/ref?id=${uid}`;
                    if(userData.role === 'admin') document.getElementById('btn-admin').classList.remove('hidden');
                });
                syncGlobals(); loadNodes(); nav('home');
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // GLOBAL SYNC (ANNOUNCEMENTS & BTC)
        function syncGlobals() {
            onValue(ref(db, 'global/announcement'), s => {
                if(s.exists()) document.getElementById('global-announcement').innerText = s.val();
            });
            // Fake BTC Sync
            setInterval(() => {
                const p = 64000 + Math.random() * 500;
                document.getElementById('btc-price').innerText = `$${p.toLocaleString(undefined, {maximumFractionDigits:0})}`;
            }, 5000);
        }

        // NAVIGATION
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`btn-${id}`)?.classList.add('nav-active');
            if(id === 'admin') loadAdminRequests();
        };

        // NODES SYSTEM (20 NODES)
        window.loadNodes = () => {
            const con = document.getElementById('nodes-container'); con.innerHTML = "";
            for(let i=1; i<=20; i++) {
                const cost = i * 10;
                con.innerHTML += `
                <div class="glass-card p-6 flex justify-between items-center shadow-lg hover:border-blue-500/50 transition-all">
                    <div class="flex items-center gap-5">
                        <div class="w-14 h-14 bg-gradient-to-br from-blue-600 to-blue-900 rounded-2xl flex items-center justify-center text-2xl shadow-lg"><i class="fa-solid fa-server"></i></div>
                        <div>
                            <p class="text-[10px] font-black text-blue-400 uppercase tracking-widest">Nexa Cluster V.${i}</p>
                            <p class="text-[8px] font-bold text-slate-500 uppercase">Power: ${(i*3.2).toFixed(1)} TH/s | Daily: 2%</p>
                        </div>
                    </div>
                    <button onclick="buyPlan(${cost})" class="bg-blue-600 text-white px-6 py-3 rounded-xl text-[9px] font-black uppercase shadow-lg shadow-blue-500/20">$${cost}</button>
                </div>`;
            }
        };

        window.buyPlan = async (c) => {
            if(userData.balance < c) return alert("Insufficient Balance!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - c, plans: (userData.plans || 0) + 1 });
            alert("Deployment Successful!");
        };

        // LUCKY SPIN
        window.openSpin = () => document.getElementById('spin-modal').classList.remove('hidden');
        window.startSpin = async () => {
            const wheel = document.getElementById('wheel');
            wheel.style.transition = "transform 4s cubic-bezier(0.1, 0.7, 1.0, 0.1)";
            const deg = 1800 + Math.random() * 1000;
            wheel.style.transform = `rotate(${deg}deg)`;
            
            setTimeout(async () => {
                const win = (Math.random() * 0.5).toFixed(2);
                await update(ref(db, `users/${uid}`), { balance: (userData.balance || 0) + parseFloat(win) });
                alert(`Sweetie, you won $${win}! 🎉`);
                document.getElementById('spin-modal').classList.add('hidden');
                wheel.style.transform = `rotate(0deg)`; wheel.style.transition = "none";
            }, 4000);
        };

        // ADMIN CONTROLS
        window.setAnnouncement = () => {
            const txt = document.getElementById('ann-text').value;
            set(ref(db, 'global/announcement'), txt); alert("Global Update Live!");
        };

        window.banUser = () => {
            const target = document.getElementById('manage-uid').value;
            update(ref(db, `users/${target}`), { status: 'banned' }); alert("User Banned!");
        };

        window.unbanUser = () => {
            const target = document.getElementById('manage-uid').value;
            update(ref(db, `users/${target}`), { status: 'active' }); alert("User Restored!");
        };

        window.updateUserBal = () => {
            const target = document.getElementById('manage-uid').value;
            const amt = parseFloat(document.getElementById('edit-bal').value);
            update(ref(db, `users/${target}`), { balance: amt }); alert("Balance Updated!");
        };

        window.logout = () => signOut(auth).then(() => location.reload());
        window.copyLink = () => { navigator.clipboard.writeText(document.getElementById('ref-link').innerText); alert("Referral Link Copied!"); };

    </script>
</body>
</html>
