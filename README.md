<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Cloud Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;900&display=swap');
        :root { --accent: #2563EB; --dark: #0F172A; }
        body { font-family: 'Outfit', sans-serif; background: #F1F5F9; color: var(--dark); }
        .glass-card { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); border-radius: 30px; border: 1px solid rgba(255,255,255,0.5); box-shadow: 0 20px 50px -15px rgba(0,0,0,0.05); }
        .input-box { background: #F8FAFC; border: 1px solid #E2E8F0; padding: 16px; border-radius: 18px; width: 100%; font-weight: 600; outline: none; transition: 0.3s; }
        .input-box:focus { border-color: var(--accent); ring: 2px var(--accent); }
        .tab-btn { color: #94A3B8; font-weight: 800; font-size: 10px; text-transform: uppercase; transition: 0.3s; }
        .tab-active { color: var(--accent); transform: translateY(-3px); }
        .node-badge { background: linear-gradient(90deg, #2563EB, #60A5FA); color: white; padding: 4px 12px; border-radius: 10px; font-size: 10px; font-weight: 900; }
        .hidden { display: none !important; }
    </style>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, update, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // --- State Management ---
        let currentUser = JSON.parse(localStorage.getItem('nexa_user')) || null;
        let adminClicks = 0;

        window.handleAuth = async (type) => {
            const user = document.getElementById('auth-user').value;
            if(!user) return alert("Please enter username, sweetie!");
            
            try {
                await signInAnonymously(auth);
                const uid = auth.currentUser.uid;
                const userRef = ref(db, 'users/' + uid);
                const snap = await get(userRef);

                if(type === 'signup' && !snap.exists()) {
                    const userData = { username: user, balance: 0.00, pkr_balance: 0, uid: uid };
                    await set(userRef, userData);
                    localStorage.setItem('nexa_user', JSON.stringify(userData));
                    location.reload();
                } else if (type === 'login' && snap.exists()) {
                    localStorage.setItem('nexa_user', JSON.stringify(snap.val()));
                    location.reload();
                } else {
                    alert("Account issue! Check username.");
                }
            } catch (e) { alert(e.message); }
        };

        onAuthStateChanged(auth, (user) => {
            if (user && currentUser) {
                document.getElementById('auth-page').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                syncData(user.uid);
            }
        });

        function syncData(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                const data = s.val();
                document.getElementById('disp-user').innerText = data.username;
                document.getElementById('disp-bal-usd').innerText = "$" + data.balance.toFixed(2);
                document.getElementById('disp-bal-pkr').innerText = "Rs. " + data.pkr_balance;
            });
            // Fetch Admin Numbers
            onValue(ref(db, 'admin/settings'), (s) => {
                const settings = s.val() || { jazz: "03705519562", easy: "03379827882", sada: "03705519562" };
                window.adminNumbers = settings;
            });
        }

        window.openDeposit = (method) => {
            const num = method === 'jazz' ? window.adminNumbers.jazz : (method === 'easy' ? window.adminNumbers.easy : window.adminNumbers.sada);
            prompt(`Send Payment to ${method.toUpperCase()} Number:\n\n${num}\n\nThen send screenshot to Admin. Enter Transaction ID here:`, "");
        };

        window.triggerAdmin = () => {
            adminClicks++;
            if(adminClicks >= 5) {
                const p = prompt("Enter Secret Key:");
                if(p === "SWEETIE786") document.getElementById('admin-modal').classList.remove('hidden');
                adminClicks = 0;
            }
        };

        window.updateNumbers = async () => {
            const j = document.getElementById('adm-jazz').value;
            const e = document.getElementById('adm-easy').value;
            await update(ref(db, 'admin/settings'), { jazz: j, easy: e });
            alert("Numbers Updated Successfully! 💋");
        };

        window.switchPage = (p) => {
            ['home','wallet','history'].forEach(id => document.getElementById('pg-'+id).classList.add('hidden'));
            document.getElementById('pg-'+p).classList.remove('hidden');
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('tab-active'));
            event.currentTarget.classList.add('tab-active');
        };
    </script>
</head>
<body class="pb-32">

    <!-- Login/Signup -->
    <div id="auth-page" class="fixed inset-0 bg-white z-[9999] flex flex-col p-8 justify-center">
        <div class="mb-12 text-center">
            <div class="w-20 h-20 bg-blue-600 rounded-3xl mx-auto flex items-center justify-center rotate-12 mb-6">
                <i class="fa-solid fa-bolt text-white text-3xl -rotate-12"></i>
            </div>
            <h1 class="text-4xl font-black italic tracking-tighter">NEXA PRO</h1>
            <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest mt-2">Next Gen Mining Terminal</p>
        </div>
        <div class="space-y-4">
            <input id="auth-user" type="text" placeholder="Choose Username" class="input-box">
            <button onclick="handleAuth('login')" class="w-full bg-slate-900 text-white py-5 rounded-2xl font-black text-xs uppercase tracking-widest">Login to Account</button>
            <button onclick="handleAuth('signup')" class="w-full bg-blue-600 text-white py-5 rounded-2xl font-black text-xs uppercase tracking-widest shadow-xl shadow-blue-100">Create New Account</button>
        </div>
    </div>

    <!-- Main App -->
    <div id="main-app" class="hidden">
        <header class="p-6 flex justify-between items-center bg-white/80 backdrop-blur-md sticky top-0 z-50">
            <div onclick="triggerAdmin()" class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-lg shadow-blue-200">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <div>
                    <h2 id="disp-user" class="text-sm font-black italic leading-none">...</h2>
                    <p class="text-[8px] font-bold text-slate-400 uppercase tracking-tighter mt-1">Status: Platinum User</p>
                </div>
            </div>
            <div class="text-right">
                <h3 id="disp-bal-usd" class="text-blue-600 font-black text-lg leading-none">$0.00</h3>
                <p id="disp-bal-pkr" class="text-[10px] font-bold text-slate-400 mt-1">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <!-- Dashboard -->
            <div id="pg-home" class="space-y-6">
                <!-- Promo Card -->
                <div class="glass-card p-8 bg-slate-900 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <span class="node-badge">LIVE NODES</span>
                        <h1 class="text-4xl font-black mt-4 mb-8">15+5 <span class="text-xs font-normal opacity-50 uppercase tracking-widest">Power Active</span></h1>
                        <button onclick="alert('Claimed! 💋')" class="bg-blue-600 px-8 py-3 rounded-xl font-black text-[10px] uppercase">Claim Rewards</button>
                    </div>
                    <i class="fa-solid fa-atom absolute -right-10 -bottom-10 text-white/5 text-[15rem] animate-spin-slow"></i>
                </div>

                <!-- Premium Dollar Nodes -->
                <h3 class="text-[10px] font-black uppercase text-slate-400 tracking-widest px-2">Premium Dollar Nodes ($)</h3>
                <div class="grid grid-cols-1 gap-4">
                    <div class="glass-card p-6">
                        <div class="flex justify-between items-center mb-6">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-microchip"></i></div>
                            <span class="text-xl font-black">$5.00</span>
                        </div>
                        <h4 class="font-black">Alpha Cloud Node</h4>
                        <p class="text-[10px] text-slate-400 font-bold mb-6 italic">Daily Profit: $0.35 | 360 Days</p>
                        <button class="w-full py-4 bg-slate-900 text-white rounded-2xl font-black text-[10px] uppercase">Activate Node</button>
                    </div>
                </div>

                <!-- Economy PKR Nodes -->
                <h3 class="text-[10px] font-black uppercase text-slate-400 tracking-widest px-2 mt-8">Economy PKR Nodes (Rs.)</h3>
                <div class="grid grid-cols-1 gap-4">
                    <div class="glass-card p-6 border-l-4 border-blue-600">
                        <div class="flex justify-between items-center mb-6">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-server"></i></div>
                            <span class="text-xl font-black">Rs. 250</span>
                        </div>
                        <h4 class="font-black">Starter PKR Node</h4>
                        <p class="text-[10px] text-slate-400 font-bold mb-6 italic">Daily Profit: Rs. 15 | 360 Days</p>
                        <button class="w-full py-4 bg-blue-600 text-white rounded-2xl font-black text-[10px] uppercase">Buy Now</button>
                    </div>
                </div>
            </div>

            <!-- Wallet -->
            <div id="pg-wallet" class="hidden space-y-6">
                <div class="glass-card p-6">
                    <h3 class="font-black mb-4">Deposit Assets</h3>
                    <div class="grid grid-cols-2 gap-3">
                        <button onclick="openDeposit('jazz')" class="p-4 bg-slate-50 rounded-2xl border flex flex-col items-center gap-2">
                            <i class="fa-solid fa-phone text-green-500"></i>
                            <span class="text-[10px] font-black uppercase">JazzCash</span>
                        </button>
                        <button onclick="openDeposit('easy')" class="p-4 bg-slate-50 rounded-2xl border flex flex-col items-center gap-2">
                            <i class="fa-solid fa-wallet text-blue-500"></i>
                            <span class="text-[10px] font-black uppercase">EasyPaisa</span>
                        </button>
                        <button onclick="openDeposit('sada')" class="p-4 bg-slate-50 rounded-2xl border flex flex-col items-center gap-2">
                            <i class="fa-solid fa-credit-card text-teal-500"></i>
                            <span class="text-[10px] font-black uppercase">Sadapay</span>
                        </button>
                        <div class="p-4 bg-slate-100 rounded-2xl border opacity-50 flex flex-col items-center gap-2 cursor-not-allowed">
                            <i class="fa-brands fa-bitcoin text-orange-500"></i>
                            <span class="text-[10px] font-black uppercase">Binance Soon</span>
                        </div>
                    </div>
                </div>

                <div class="glass-card p-6">
                    <h3 class="font-black mb-4 italic text-blue-600">Withdraw Funds</h3>
                    <div class="space-y-3">
                        <input type="text" placeholder="Account Title (Username)" class="input-box">
                        <input type="number" placeholder="Withdraw Amount" class="input-box">
                        <input type="text" placeholder="JazzCash/EasyPaisa Number" class="input-box">
                        <button class="w-full bg-slate-900 text-white py-5 rounded-2xl font-black text-xs uppercase">Submit Request</button>
                    </div>
                </div>
            </div>
        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-8 left-8 right-8 h-20 glass-card border-none flex justify-around items-center px-6 z-50 shadow-2xl">
            <button onclick="switchPage('home')" class="tab-btn tab-active flex flex-col items-center">
                <i class="fa-solid fa-house-chimney text-xl"></i>
                <span class="mt-1">Dash</span>
            </button>
            <button onclick="switchPage('wallet')" class="tab-btn flex flex-col items-center">
                <i class="fa-solid fa-wallet text-xl"></i>
                <span class="mt-1">Wallet</span>
            </button>
            <button onclick="switchPage('history')" class="tab-btn flex flex-col items-center">
                <i class="fa-solid fa-clock-rotate-left text-xl"></i>
                <span class="mt-1">Log</span>
            </button>
        </nav>

        <!-- Admin Modal -->
        <div id="admin-modal" class="fixed inset-0 bg-black/80 z-[10000] p-6 hidden overflow-y-auto">
            <div class="bg-white rounded-[40px] p-8 max-w-md mx-auto">
                <h2 class="text-red-600 font-black text-xl mb-6 uppercase italic">Admin Terminal</h2>
                <div class="space-y-4">
                    <label class="text-[10px] font-black uppercase text-slate-400">JazzCash / SadaPay Number</label>
                    <input id="adm-jazz" type="text" value="03705519562" class="input-box">
                    <label class="text-[10px] font-black uppercase text-slate-400">EasyPaisa Number</label>
                    <input id="adm-easy" type="text" value="03379827882" class="input-box">
                    <button onclick="updateNumbers()" class="w-full bg-red-600 text-white py-4 rounded-xl font-black text-xs">UPDATE SYSTEM NUMBERS</button>
                    <button onclick="document.getElementById('admin-modal').classList.add('hidden')" class="w-full bg-slate-200 py-3 rounded-xl font-black text-[10px]">EXIT TERMINAL</button>
                </div>
            </div>
        </div>
    </div>

</body>
</html>
