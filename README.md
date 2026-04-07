<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA | Ultimate Investment Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #020617; color: white; overflow-x: hidden; }
        .glass { background: rgba(15, 23, 42, 0.7); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .neon-border { box-shadow: 0 0 20px rgba(59, 130, 246, 0.2); border: 1px solid rgba(59, 130, 246, 0.5); }
        .hidden { display: none; }
        .plan-card { background: rgba(255, 255, 255, 0.03); border-radius: 20px; transition: 0.3s; border: 1px solid rgba(255, 255, 255, 0.05); }
        .plan-card:hover { transform: translateY(-5px); border-color: #3b82f6; }
        input, select { background: rgba(0,0,0,0.3) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; }
    </style>
</head>
<body>

    <!-- SECTION 1: AUTHENTICATION (LOGIN/SIGNUP) -->
    <div id="auth-page" class="min-h-screen flex items-center justify-center p-6">
        <div class="glass w-full max-w-md p-8 rounded-[2.5rem] text-center">
            <h1 id="logo" class="text-5xl font-black tracking-tighter bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-pink-500 mb-2 cursor-pointer">NEXA</h1>
            <p id="auth-subtitle" class="text-gray-400 text-sm mb-8">Secure Anonymous Investment Protocol</p>
            
            <form id="auth-form" class="space-y-4">
                <input type="text" id="reg-name" class="w-full p-4 rounded-2xl outline-none hidden" placeholder="Full Name">
                <input type="text" id="auth-user" required class="w-full p-4 rounded-2xl outline-none" placeholder="Username">
                <input type="password" id="auth-key" required class="w-full p-4 rounded-2xl outline-none" placeholder="Secret Access Key">
                <button type="submit" id="auth-btn" class="w-full bg-blue-600 py-4 rounded-2xl font-bold uppercase tracking-widest shadow-lg">Enter NEXA</button>
            </form>
            <p class="mt-6 text-sm text-gray-500">
                <span id="toggle-text">Don't have an account?</span>
                <button onclick="toggleAuth()" id="toggle-btn" class="text-blue-400 font-bold ml-1">Create One</button>
            </p>
        </div>
    </div>

    <!-- SECTION 2: MAIN DASHBOARD -->
    <div id="dashboard-page" class="hidden min-h-screen">
        <nav class="glass sticky top-0 z-50 p-4 flex justify-between items-center px-8">
            <h2 class="text-2xl font-black text-blue-500">NEXA</h2>
            <div class="flex gap-6 items-center">
                <div class="text-right"><p class="text-[10px] text-gray-500">BALANCE</p><p id="user-bal" class="text-green-400 font-bold">$0.00</p></div>
                <button onclick="logout()" class="text-gray-500 hover:text-white"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </nav>

        <main class="max-w-7xl mx-auto p-6 space-y-10">
            <!-- Stats -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="glass p-6 rounded-3xl">
                    <p class="text-gray-400 text-sm">Welcome back, <span id="user-display" class="text-white font-bold">...</span></p>
                    <div class="flex gap-2 mt-4">
                        <button onclick="openModal('deposit-modal')" class="bg-blue-600 px-6 py-2 rounded-xl text-sm font-bold">Deposit</button>
                        <button onclick="openModal('withdraw-modal')" class="bg-white/5 border border-white/10 px-6 py-2 rounded-xl text-sm font-bold">Withdraw</button>
                    </div>
                </div>
                <div class="glass p-6 rounded-3xl flex flex-col justify-center">
                    <p class="text-[10px] text-gray-500 uppercase tracking-widest font-bold">Referral Link</p>
                    <p id="ref-link" class="text-blue-400 text-xs mt-1 truncate">Loading...</p>
                </div>
            </div>

            <!-- Plans -->
            <h3 class="text-2xl font-black">Investment <span class="text-blue-500">Plans</span></h3>
            <div id="plans-container" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6"></div>
        </main>
    </div>

    <!-- SECTION 3: MODALS (DEPOSIT/WITHDRAW) -->
    <div id="deposit-modal" class="hidden fixed inset-0 bg-black/90 z-[100] flex items-center justify-center p-6">
        <div class="glass w-full max-w-md p-8 rounded-3xl">
            <h3 class="text-2xl font-bold mb-4 text-blue-400">Deposit Funds</h3>
            <p class="text-xs text-gray-400 mb-4 font-mono">Easypaisa: 03379827882<br>JazzCash/SadaPay: 03705519562</p>
            <form id="dep-form" class="space-y-4">
                <input type="number" id="d-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl outline-none" required>
                <input type="text" id="d-tid" placeholder="TID Number" class="w-full p-4 rounded-xl outline-none" required>
                <button type="submit" class="w-full bg-blue-600 py-4 rounded-xl font-bold">Submit Deposit</button>
                <button type="button" onclick="closeModals()" class="w-full text-gray-500 text-sm mt-2">Cancel</button>
            </form>
        </div>
    </div>

    <div id="withdraw-modal" class="hidden fixed inset-0 bg-black/90 z-[100] flex items-center justify-center p-6">
        <div class="glass w-full max-w-md p-8 rounded-3xl">
            <h3 class="text-2xl font-bold mb-4 text-pink-500">Withdraw Funds</h3>
            <form id="wit-form" class="space-y-4">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl outline-none" required>
                <select id="w-meth" class="w-full p-4 rounded-xl outline-none">
                    <option>Easypaisa</option><option>JazzCash</option><option>SadaPay</option>
                </select>
                <input type="text" id="w-acc" placeholder="Account Number" class="w-full p-4 rounded-xl outline-none" required>
                <button type="submit" class="w-full bg-pink-600 py-4 rounded-xl font-bold">Request Withdrawal</button>
                <button type="button" onclick="closeModals()" class="w-full text-gray-500 text-sm mt-2">Cancel</button>
            </form>
        </div>
    </div>

    <!-- FIREBASE LOGIC -->
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

        // --- AUTH LOGIC ---
        let isLogin = true;
        window.toggleAuth = () => {
            isLogin = !isLogin;
            document.getElementById('reg-name').classList.toggle('hidden');
            document.getElementById('auth-btn').innerText = isLogin ? 'Enter NEXA' : 'Create Account';
            document.getElementById('toggle-btn').innerText = isLogin ? 'Create One' : 'Login';
        };

        // Secret Admin Tap
        let taps = 0;
        document.getElementById('logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const key = prompt("Admin Key?");
                if(key === "NEXA786") alert("Admin access granted! (Redirecting to Panel...)");
            }
            setTimeout(() => taps = 0, 2000);
        };

        document.getElementById('auth-form').onsubmit = async (e) => {
            e.preventDefault();
            const user = document.getElementById('auth-user').value;
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            
            const userRef = ref(db, 'users/' + uid);
            const snap = await get(userRef);
            
            if(!snap.exists()) {
                await set(userRef, { username: user, balance: 0, joined: new Date().getTime() });
            }
            
            localStorage.setItem('nexa_uid', uid);
            showDashboard(uid);
        };

        function showDashboard(uid) {
            document.getElementById('auth-page').classList.add('hidden');
            document.getElementById('dashboard-page').classList.remove('hidden');
            
            onValue(ref(db, 'users/' + uid), (snap) => {
                const data = snap.val();
                document.getElementById('user-bal').innerText = `$${data.balance.toFixed(2)}`;
                document.getElementById('user-display').innerText = data.username;
                document.getElementById('ref-link').innerText = `https://nexa.com/join?id=${uid.substring(0,6)}`;
            });
            renderPlans();
        }

        function renderPlans() {
            const container = document.getElementById('plans-container');
            container.innerHTML = "";
            for(let i=1; i<=20; i++) {
                const cost = 200 + (i*50);
                const profit = 10 + (i*2);
                container.innerHTML += `
                    <div class="plan-card p-6 text-center">
                        <p class="text-[10px] text-blue-400 font-bold">PLAN ${i}</p>
                        <h4 class="text-3xl font-black my-2">${profit}%</h4>
                        <p class="text-xs text-gray-500 mb-4">Daily Profit</p>
                        <div class="bg-white/5 py-2 rounded-lg mb-4 text-sm font-bold">$${cost}</div>
                        <button onclick="alert('Balance insufficient sweetie!')" class="w-full py-2 bg-blue-600 rounded-lg text-xs font-bold uppercase">Invest</button>
                    </div>
                `;
            }
        }

        // --- TRANSACTION LOGIC ---
        window.openModal = (id) => document.getElementById(id).classList.remove('hidden');
        window.closeModals = () => {
            document.getElementById('deposit-modal').classList.add('hidden');
            document.getElementById('withdraw-modal').classList.add('hidden');
        };

        document.getElementById('dep-form').onsubmit = async (e) => {
            e.preventDefault();
            const uid = localStorage.getItem('nexa_uid');
            const amt = document.getElementById('d-amt').value;
            const tid = document.getElementById('d-tid').value;
            await push(ref(db, 'requests/deposits'), { uid, amt, tid, status: 'pending' });
            alert("Deposit request sent sweetie!");
            closeModals();
        };

        window.logout = () => { localStorage.clear(); location.reload(); };

        // Auto-load session
        const saved = localStorage.getItem('nexa_uid');
        if(saved) showDashboard(saved);
    </script>
</body>
</html>
