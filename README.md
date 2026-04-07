<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA Mobile</title>
    <link rel="manifest" href="data:application/json;base64,ewogICJuYW1lIjogIk5FWEEgUHJvIiwKICAic2hvcnRfbmFtZSI6ICJORVhBIiwKICAic3RhcnRfdXJsIjogIi4iLAogICJkaXNwbGF5IjogInN0YW5kYWxvbmUiLAogICJiYWNrZ3JvdW5kX2NvbG9yIjogIiNmZmZmZmYiLAogICJ0aGVtZV9jb2xvciI6ICIjMjU2M2ViIiwKICAiaWNvbnMiOiBbCiAgICB7CiAgICAgICJzcmMiOiAiaHR0cHM6Ly9jZG4taWNvbnMtcG5nLmZsaXRpY29uLmNvbS81MTIvMjg2Ny8yODY3MzA0LnBuZyIsCiAgICAgICJzaXplcyI6ICI1MTJ4NTEyIiwKICAgICAgInR5cGUiOiAiaW1hZ2UvcG5nIgogICAgfQogIF0KfQ==">
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: #f8fafc; 
            -webkit-tap-highlight-color: transparent;
            user-select: none;
        }

        /* App UI Optimization */
        .app-container { max-width: 500px; margin: 0 auto; min-height: 100vh; background: white; position: relative; padding-bottom: 80px; }
        
        .bottom-nav {
            position: fixed; bottom: 0; left: 50%; transform: translateX(-50%);
            width: 100%; max-width: 500px; background: rgba(255,255,255,0.9);
            backdrop-filter: blur(20px); border-top: 1px solid rgba(0,0,0,0.05);
            display: flex; justify-content: space-around; padding: 15px 0; z-index: 1000;
        }

        .nav-item { text-align: center; color: #94a3b8; font-size: 10px; font-weight: 700; flex: 1; }
        .nav-item.active { color: #2563eb; }
        .nav-item i { font-size: 18px; display: block; margin-bottom: 4px; }

        .card-gradient { background: linear-gradient(135deg, #2563eb, #7c3aed); color: white; border-radius: 30px; }
        
        .node-card { border: 1px solid #f1f5f9; border-radius: 24px; transition: 0.2s; background: white; }
        .node-card:active { transform: scale(0.95); background: #f8fafc; }

        .hidden { display: none; }
    </style>
</head>
<body>

    <div class="app-container shadow-2xl">
        
        <header class="px-6 py-6 flex justify-between items-center bg-white sticky top-0 z-50">
            <h1 id="logo" class="text-2xl font-extrabold text-blue-600 tracking-tighter">NEXA</h1>
            <div id="auth-controls" class="hidden flex gap-3">
                <button onclick="logout()" class="w-10 h-10 rounded-full bg-gray-50 flex items-center justify-center text-gray-400">
                    <i class="fa-solid fa-power-off text-sm"></i>
                </button>
            </div>
        </header>

        <div id="page-login" class="px-8 pt-10 animate-fade">
            <div class="text-center mb-10">
                <div class="w-16 h-16 bg-blue-600 rounded-2xl mx-auto mb-4 flex items-center justify-center shadow-lg shadow-blue-200">
                    <i class="fa-solid fa-fingerprint text-white text-3xl"></i>
                </div>
                <h2 class="text-2xl font-extrabold">Welcome Back</h2>
                <p class="text-gray-400 text-sm">Sign in to your secure node</p>
            </div>
            <form id="login-form" class="space-y-4">
                <input type="text" id="user-id" placeholder="Username" class="w-full p-4 rounded-2xl bg-gray-50 border-none outline-none focus:ring-2 ring-blue-100 transition" required>
                <input type="password" id="user-key" placeholder="Access Key" class="w-full p-4 rounded-2xl bg-gray-50 border-none outline-none focus:ring-2 ring-blue-100 transition" required>
                <button class="w-full bg-blue-600 text-white py-4 rounded-2xl font-bold shadow-xl shadow-blue-100">Login to Dashboard</button>
            </form>
        </div>

        <div id="page-home" class="hidden px-6 space-y-6">
            <div class="card-gradient p-8 shadow-xl relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-xs opacity-80 font-bold uppercase tracking-widest">Total Assets</p>
                    <h2 id="dash-bal" class="text-4xl font-black mt-2">$0.00</h2>
                    <div class="flex gap-3 mt-6">
                        <button onclick="showPage('deposit')" class="bg-white/20 px-5 py-2 rounded-xl text-xs font-bold backdrop-blur-md">Deposit</button>
                        <button onclick="showPage('withdraw')" class="bg-white text-blue-600 px-5 py-2 rounded-xl text-xs font-bold">Withdraw</button>
                    </div>
                </div>
                <i class="fa-solid fa-circle-nodes absolute -right-4 -bottom-4 text-8xl opacity-10"></i>
            </div>

            <div class="flex justify-between items-center">
                <h3 class="font-extrabold text-gray-800">Mining Nodes</h3>
                <span class="text-[10px] font-bold text-blue-600 bg-blue-50 px-3 py-1 rounded-full uppercase">Live</span>
            </div>
            
            <div id="plans-list" class="grid grid-cols-2 gap-4">
                </div>
        </div>

        <div id="page-about" class="hidden px-8 pt-6 space-y-4">
            <h2 class="text-xl font-bold">About NEXA Protocol</h2>
            <div class="bg-blue-50 p-6 rounded-3xl text-sm leading-relaxed text-blue-800">
                NEXA is a high-performance node network. We provide secure liquidity solutions for digital assets.
            </div>
            <div class="space-y-2">
                <div class="p-4 bg-gray-50 rounded-2xl flex items-center gap-4">
                    <i class="fa-solid fa-shield-heart text-blue-500"></i>
                    <span class="text-sm font-bold">Encrypted Security</span>
                </div>
                <div class="p-4 bg-gray-50 rounded-2xl flex items-center gap-4">
                    <i class="fa-solid fa-bolt text-yellow-500"></i>
                    <span class="text-sm font-bold">Instant Payouts</span>
                </div>
            </div>
        </div>

        <nav id="app-nav" class="hidden bottom-nav">
            <button onclick="showPage('home')" class="nav-item active" id="nav-home">
                <i class="fa-solid fa-house"></i>Home
            </button>
            <button onclick="showPage('about')" class="nav-item" id="nav-about">
                <i class="fa-solid fa-circle-info"></i>About
            </button>
            <button onclick="showPage('history')" class="nav-item" id="nav-history">
                <i class="fa-solid fa-receipt"></i>History
            </button>
            <button onclick="showPage('policy')" class="nav-item" id="nav-policy">
                <i class="fa-solid fa-user-shield"></i>Policy
            </button>
        </nav>

    </div>

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
            document.querySelectorAll('[id^="page-"]').forEach(p => p.classList.add('hidden'));
            document.getElementById('page-' + id).classList.remove('hidden');
            
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            const activeNav = document.getElementById('nav-' + id);
            if(activeNav) activeNav.classList.add('active');
        };

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

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            document.getElementById('page-login').classList.add('hidden');
            document.getElementById('page-home').classList.remove('hidden');
            document.getElementById('app-nav').classList.remove('hidden');
            document.getElementById('auth-controls').classList.remove('hidden');

            onValue(ref(db, 'users/' + uid), s => {
                const d = s.val();
                if(d) document.getElementById('dash-bal').innerText = `$${d.balance.toFixed(2)}`;
            });

            // Auto Generate Plans $5 onwards
            onValue(ref(db, 'plans'), s => {
                const list = document.getElementById('plans-list');
                list.innerHTML = "";
                s.forEach(p => {
                    const pd = p.val();
                    list.innerHTML += `
                    <div class="node-card p-5 text-center shadow-sm">
                        <div class="text-blue-600 mb-2"><i class="fa-solid fa-microchip"></i></div>
                        <p class="text-[9px] font-bold text-gray-400 uppercase tracking-tighter">${pd.name}</p>
                        <h4 class="text-xl font-black text-gray-800">${pd.profit}%</h4>
                        <button onclick="invest(${pd.min})" class="mt-4 w-full py-2 bg-blue-50 text-blue-600 rounded-xl text-[10px] font-bold">STAKE $${pd.min}</button>
                    </div>`;
                });
            });
        }

        // --- GOD MODE ---
        let taps = 0;
        document.getElementById('logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const key = prompt("Admin Key:");
                if(key === "NEXA786") alert("God Mode Activated sweetie!");
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.logout = () => { localStorage.clear(); location.reload(); };

    </script>
</body>
</html>
