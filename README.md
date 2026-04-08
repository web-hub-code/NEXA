<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GLOBAL | Wealth Management</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #F2F2F7; color: #1C1C1E; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.5); }
        .card-shadow { box-shadow: 0 10px 30px -5px rgba(0,0,0,0.03); border-radius: 30px; }
        .bank-card { background: linear-gradient(135deg, #1C1C1E 0%, #3A3A3C 100%); border-radius: 35px; color: white; box-shadow: 0 20px 40px -10px rgba(0,0,0,0.2); }
        .nav-active { color: #007AFF !important; }
        input { background: #E9E9EB !important; border-radius: 15px !important; padding: 15px !important; outline: none !important; border: none !important; }
        .ticker { animation: ticker 25s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
    </style>
</head>
<body class="pb-32">

    <!-- Auth Screen -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-20 h-20 bg-[#1C1C1E] rounded-[2rem] flex items-center justify-center text-white text-4xl mb-6 shadow-2xl">
            <i class="fa-solid fa-building-columns"></i>
        </div>
        <h1 class="text-3xl font-extrabold tracking-tighter">NEXA <span class="text-[#007AFF]">GLOBAL</span></h1>
        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[4px] mb-10">Institutional Grade</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Enter Your Name" class="w-full text-sm font-semibold">
            <input type="password" id="admin-key" placeholder="Security PIN (Optional)" class="w-full text-sm font-semibold">
            <button id="login-btn" class="w-full bg-[#007AFF] text-white p-5 rounded-2xl font-black uppercase text-[10px] tracking-widest active:scale-95 transition-all">Initialize Session</button>
        </div>
    </div>

    <!-- Main App -->
    <div id="app" class="hidden">
        <header class="p-6 flex justify-between items-center glass sticky top-0 z-50">
            <div>
                <p class="text-[9px] font-black text-[#007AFF] uppercase tracking-widest">Global Partner</p>
                <h3 id="display-name" class="text-xl font-extrabold tracking-tight">--</h3>
            </div>
            <button onclick="window.location.reload()" class="w-10 h-10 rounded-full glass flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <!-- Wallet Card -->
            <div class="bank-card p-8">
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest opacity-70">Total Liquidity</p>
                <h2 id="user-bal" class="text-4xl font-extrabold my-2">$0.00</h2>
                <div class="flex justify-between items-end mt-8">
                    <p class="text-xs font-bold text-blue-100">Status: <span class="text-green-400">Verified</span></p>
                    <button onclick="alert('Deposit System Coming Soon sweetie!')" class="bg-[#007AFF] px-6 py-2 rounded-xl text-[10px] font-black uppercase">Add Funds</button>
                </div>
            </div>

            <!-- Addictive Ticker -->
            <div class="glass py-2 overflow-hidden rounded-xl border border-slate-100">
                <div class="ticker flex gap-10 text-[9px] font-black uppercase text-slate-500">
                    <span>• @User_992 just earned $12.50</span>
                    <span class="text-green-600">• @Ayesha payout $50 success</span>
                    <span>• @King_Crypto activated Node V.5</span>
                </div>
            </div>

            <!-- Features -->
            <div class="grid grid-cols-2 gap-4">
                <div class="card-shadow bg-white p-6">
                    <i class="fa-solid fa-bolt-lightning text-[#007AFF] mb-3"></i>
                    <p class="text-[10px] font-black text-slate-400 uppercase">Active Rigs</p>
                    <h4 id="user-plans" class="text-xl font-black">0</h4>
                </div>
                <div class="card-shadow bg-white p-6">
                    <i class="fa-solid fa-chart-line text-green-500 mb-3"></i>
                    <p class="text-[10px] font-black text-slate-400 uppercase">Daily ROI</p>
                    <h4 class="text-xl font-black">+$0.00</h4>
                </div>
            </div>
        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-full flex justify-around items-center z-[100] shadow-2xl border border-slate-100 px-2">
            <div class="flex flex-col items-center text-[#007AFF]"><i class="fa-solid fa-house"></i><span class="text-[8px] font-bold uppercase mt-1">Home</span></div>
            <div class="flex flex-col items-center text-slate-400"><i class="fa-solid fa-microchip"></i><span class="text-[8px] font-bold uppercase mt-1">Rigs</span></div>
            <div class="flex flex-col items-center text-slate-400"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-bold uppercase mt-1">Wallet</span></div>
        </nav>
    </div>

    <!-- Firebase Script -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // Login Logic
        document.getElementById('login-btn').addEventListener('click', async () => {
            const name = document.getElementById('user-name').value.trim();
            const pin = document.getElementById('admin-key').value.trim();

            if (name.length < 3) return alert("Please enter your real name sweetie!");

            try {
                const res = await signInAnonymously(auth);
                const uid = res.user.uid;
                const userRef = ref(db, `users/${uid}`);
                const snap = await get(userRef);

                if (!snap.exists()) {
                    await set(userRef, {
                        username: name,
                        balance: 0,
                        plans: 0,
                        role: (pin === "sweetie786") ? "admin" : "user",
                        status: "active",
                        joined: Date.now()
                    });
                }
            } catch (err) {
                alert("Firebase Error: " + err.message);
            }
        });

        // Observer
        onAuthStateChanged(auth, (user) => {
            if (user) {
                onValue(ref(db, `users/${user.uid}`), (snap) => {
                    const data = snap.val();
                    if (data) {
                        document.getElementById('display-name').innerText = data.username;
                        document.getElementById('user-bal').innerText = `$${data.balance.toFixed(2)}`;
                        document.getElementById('user-plans').innerText = data.plans;
                        document.getElementById('auth-screen').classList.add('hidden');
                        document.getElementById('app').classList.remove('hidden');
                    }
                });
            }
        });
    </script>
</body>
</html>
