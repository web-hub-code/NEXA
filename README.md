<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign App</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --accent: #0066ff; --bg: #fdfdfe; --text: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: var(--text); overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        .glass-panel { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(20px); border: 1px solid rgba(0, 0, 0, 0.05); border-radius: 30px; }
        .card-elite { background: linear-gradient(135deg, #0066ff 0%, #0044aa 100%); color: white; border-radius: 40px; box-shadow: 0 25px 50px -12px rgba(0, 102, 255, 0.3); }
        .tab-btn { transition: 0.3s; color: #94a3b8; }
        .tab-btn.active { color: var(--accent); transform: translateY(-3px); }
        .nexa-input { background: #f1f5f9; border-radius: 20px; padding: 18px; width: 100%; outline: none; font-weight: 600; border: 2px solid transparent; }
        .nexa-input:focus { border-color: var(--accent); background: white; }
        #god-ui { position: fixed; inset: 0; background: rgba(255, 255, 255, 0.98); z-index: 9999; display: none; padding: 30px; overflow-y: auto; }
        ::-webkit-scrollbar { display: none; }
        .hidden { display: none; }
    </style>
</head>
<body>

    <!-- ADMIN GOD MODE -->
    <div id="god-ui" class="animate__animated">
        <div class="flex justify-between items-center mb-10">
            <h2 class="font-bold text-3xl tracking-tighter text-blue-600 italic">GOD MODE</h2>
            <button onclick="toggleGodMode(false)" class="w-12 h-12 bg-red-50 text-red-500 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-4">
            <div class="p-6 bg-slate-50 rounded-[30px] border border-slate-100">
                <p class="text-[10px] text-gray-400 font-bold uppercase mb-4">Financial Override</p>
                <input type="text" id="adm-uid" placeholder="User UID" class="nexa-input mb-3">
                <input type="number" id="adm-bal" placeholder="New Balance ($)" class="nexa-input mb-3">
                <button onclick="adminEditBalance()" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black">UPDATE BALANCE</button>
            </div>
            <div class="p-6 bg-slate-50 rounded-[30px] border border-slate-100">
                <p class="text-[10px] text-gray-400 font-bold uppercase mb-4">Promo Factory</p>
                <input type="text" id="adm-p-code" placeholder="Promo Code" class="nexa-input mb-3">
                <input type="number" id="adm-p-amt" placeholder="Bonus Amount" class="nexa-input mb-3">
                <button onclick="adminAddPromo()" class="w-full bg-slate-900 text-white p-4 rounded-2xl font-black">CREATE PROMO</button>
            </div>
        </div>
    </div>

    <div class="max-w-md mx-auto min-h-screen px-6 py-8 relative">
        <!-- HEADER -->
        <header class="flex justify-between items-center mb-8">
            <div id="nexa-logo" class="flex items-center gap-3 cursor-pointer">
                <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-xl shadow-blue-200">
                    <i class="fa-solid fa-bolt-lightning text-xl"></i>
                </div>
                <span class="text-2xl font-black italic tracking-tighter">NEXA<span class="text-blue-600">.</span></span>
            </div>
            <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500 border-none"><i class="fa-solid fa-power-off text-sm"></i></button>
        </header>

        <!-- PAGE: HOME -->
        <main id="p-home" class="animate__animated animate__fadeIn">
            <div class="card-elite p-8 mb-8">
                <p class="text-[10px] font-bold opacity-70 uppercase tracking-[3px]">Total Portfolio</p>
                <h2 id="user-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                <div class="flex gap-4 mt-10">
                    <button onclick="showPage('deposit')" class="flex-1 bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-xl">Deposit</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/20 backdrop-blur-md py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest">Withdraw</button>
                </div>
            </div>

            <div class="glass-panel p-5 mb-8 flex items-center gap-4">
                <input type="text" id="promo-in" placeholder="PROMO CODE" class="bg-transparent flex-1 outline-none text-[10px] font-black uppercase tracking-widest">
                <button onclick="applyPromo()" class="text-blue-600 font-black text-[10px] uppercase">Apply</button>
            </div>

            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-6">Active Nodes</h3>
            <div id="nodes-grid" class="space-y-4 pb-32"></div>
        </main>

        <!-- PAGE: DEPOSIT -->
        <main id="p-deposit" class="hidden animate__animated animate__fadeIn">
            <h2 class="text-2xl font-black mb-6">Add Liquidity</h2>
            <div class="grid grid-cols-3 gap-3 mb-6">
                <button onclick="selectMethod('Easypaisa')" class="glass-panel p-4 text-center border-blue-200"><i class="fa-solid fa-mobile text-green-500 mb-2"></i><p class="text-[8px] font-bold">Easypaisa</p></button>
                <button onclick="selectMethod('JazzCash')" class="glass-panel p-4 text-center"><i class="fa-solid fa-bolt text-yellow-500 mb-2"></i><p class="text-[8px] font-bold">JazzCash</p></button>
                <button onclick="selectMethod('SadaPay')" class="glass-panel p-4 text-center"><i class="fa-solid fa-credit-card text-pink-500 mb-2"></i><p class="text-[8px] font-bold">SadaPay</p></button>
            </div>
            <div id="dep-area" class="hidden space-y-4">
                <div class="p-6 bg-blue-50 rounded-[30px] border border-blue-100">
                    <p class="text-[10px] text-blue-600 font-bold mb-1">RECIPIENT ACCOUNT (<span id="meth-name"></span>)</p>
                    <p class="text-xl font-bold">03379827882</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="nexa-input">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="nexa-input">
                <button onclick="submitAction('Deposit')" class="w-full bg-blue-600 text-white py-5 rounded-2xl font-black uppercase">Submit Proof</button>
            </div>
        </main>

        <!-- PAGE: WITHDRAW -->
        <main id="p-withdraw" class="hidden animate__animated animate__fadeIn">
            <h2 class="text-2xl font-black mb-6">Harvest Profit</h2>
            <div class="space-y-4">
                <div class="p-6 glass-panel"><p class="text-xs font-bold text-slate-400">Available</p><p id="wit-bal" class="text-3xl font-black text-blue-600">$0.00</p></div>
                <input type="number" id="wit-amt" placeholder="Amount to Withdraw" class="nexa-input">
                <input type="text" id="wit-acc" placeholder="Account Number" class="nexa-input">
                <button onclick="submitAction('Withdraw')" class="w-full bg-slate-900 text-white py-5 rounded-2xl font-black uppercase">Initialize Payout</button>
            </div>
        </main>

        <!-- DOCK -->
        <nav class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[90%] max-w-md glass-panel p-4 flex justify-around items-center z-[1000] shadow-2xl">
            <button onclick="showPage('home')" id="nav-home" class="tab-btn active"><i class="fa-solid fa-house-user text-xl"></i></button>
            <button onclick="showPage('deposit')" id="nav-deposit" class="tab-btn"><i class="fa-solid fa-wallet text-xl"></i></button>
            <button onclick="showPage('withdraw')" id="nav-withdraw" class="tab-btn"><i class="fa-solid fa-chart-line text-xl"></i></button>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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
        const uid = localStorage.getItem('nexa_uid');

        // --- NAVIGATION ---
        window.showPage = (id) => {
            ['home', 'deposit', 'withdraw'].forEach(p => document.getElementById('p-'+p).classList.add('hidden'));
            document.getElementById('p-'+id).classList.remove('hidden');
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            document.getElementById('nav-'+id)?.classList.add('active');
        };

        // --- AUTO-PLANS ---
        const initNodes = async () => {
            const snap = await get(ref(db, 'plans'));
            if(!snap.exists()) {
                const plans = {};
                for(let i=1; i<=15; i++) plans[`n${i}`] = { name: `NODE ${i}`, min: i*10, profit: (2 + i*0.5).toFixed(1) };
                for(let i=1; i<=5; i++) plans[`v${i}`] = { name: `VIP ${i}`, min: i*500, profit: (10 + i*3).toFixed(1) };
                await set(ref(db, 'plans'), plans);
            }
        };

        // --- CORE LOGIC ---
        async function start() {
            if(!uid) {
                const name = prompt("Enter Username sweetie:");
                if(name) {
                    const res = await signInAnonymously(auth);
                    await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0 });
                    localStorage.setItem('nexa_uid', res.user.uid);
                    location.reload();
                }
            } else {
                await initNodes();
                onValue(ref(db, `users/${uid}`), s => {
                    const b = s.val().balance.toFixed(2);
                    document.getElementById('user-bal').innerText = `$${b}`;
                    document.getElementById('wit-bal').innerText = `$${b}`;
                });
                onValue(ref(db, 'plans'), s => {
                    const grid = document.getElementById('nodes-grid');
                    grid.innerHTML = "";
                    s.forEach(p => {
                        const d = p.val();
                        grid.innerHTML += `<div class="glass-panel p-6 flex justify-between items-center animate__animated animate__fadeInUp">
                            <div><h4 class="text-[10px] font-black text-slate-400 uppercase">${d.name}</h4><p class="text-lg font-bold">${d.profit}% ROI</p></div>
                            <button onclick="alert('Stake Started!')" class="bg-blue-600 text-white px-5 py-3 rounded-2xl text-[9px] font-black uppercase">STAKE $${d.min}</button>
                        </div>`;
                    });
                });
            }
        }

        // --- PROMO ---
        window.applyPromo = async () => {
            const code = document.getElementById('promo-in').value.toUpperCase();
            const snap = await get(ref(db, `promos/${code}`));
            if(snap.exists() && !localStorage.getItem('p_'+code)) {
                const user = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: user.val().balance + snap.val().bonus });
                localStorage.setItem('p_'+code, true);
                alert("Bonus Added Sweetie!");
            } else { alert("Invalid Code!"); }
        };

        // --- ADMIN ---
        let taps = 0;
        document.getElementById('nexa-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("MASTER KEY:") === "NEXA786") toggleGodMode(true);
                taps = 0;
            }
            setTimeout(() => taps = 0, 2000);
        };
        window.toggleGodMode = (s) => document.getElementById('god-ui').style.display = s ? 'block' : 'none';
        window.adminEditBalance = async () => {
            const id = document.getElementById('adm-uid').value;
            const amt = document.getElementById('adm-bal').value;
            await update(ref(db, `users/${id}`), { balance: parseFloat(amt) });
            alert("Done!");
        };
        window.adminAddPromo = async () => {
            const c = document.getElementById('adm-p-code').value.toUpperCase();
            const b = document.getElementById('adm-p-amt').value;
            await set(ref(db, `promos/${c}`), { bonus: parseFloat(b) });
            alert("Promo Created!");
        };

        window.selectMethod = (m) => {
            document.getElementById('dep-area').classList.remove('hidden');
            document.getElementById('meth-name').innerText = m;
        };
        window.submitAction = (type) => { alert(type + " Request Sent Sweetie!"); showPage('home'); };
        window.logout = () => { localStorage.clear(); location.reload(); };

        start();
    </script>
</body>
</html>
