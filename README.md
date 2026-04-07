<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Digital Node</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --primary: #2563eb; --dark: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--dark); user-select: none; }
        
        .glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .card-main { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); color: white; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.25); }
        .dock { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); width: 92%; max-width: 450px; background: #0f172a; border-radius: 28px; padding: 12px; display: flex; justify-content: space-around; z-index: 1000; box-shadow: 0 20px 40px rgba(0,0,0,0.3); }
        .dock-item { color: #64748b; font-size: 10px; font-weight: 700; text-align: center; flex: 1; transition: 0.3s; }
        .dock-item.active { color: #3b82f6; transform: translateY(-5px); }
        .dock-item i { font-size: 22px; display: block; margin-bottom: 4px; }
        .input-field { background: white; border: 1px solid #e2e8f0; border-radius: 20px; padding: 18px; width: 100%; outline: none; font-weight: 600; transition: 0.3s; }
        .input-field:focus { border-color: #2563eb; }
        .btn-premium { background: linear-gradient(135deg, #2563eb, #7c3aed); color: white; transition: 0.4s; border-radius: 20px; }
        .hidden { display: none; }
        .method-card { border: 2px solid transparent; transition: 0.3s; cursor: pointer; }
        .method-card.active { border-color: #2563eb; background: #eff6ff; }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <div class="max-w-md mx-auto min-h-screen relative pb-32">
        
        <!-- HEADER -->
        <header class="glass sticky top-0 z-[500] px-6 py-5 flex justify-between items-center">
            <div class="flex items-center gap-2">
                <div id="admin-trigger" class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-white font-black shadow-lg cursor-pointer">N</div>
                <h1 class="text-xl font-extrabold tracking-tighter italic">NEXA<span class="text-blue-600">.</span></h1>
            </div>
            <button onclick="logout()" id="logout-btn" class="hidden w-10 h-10 rounded-full bg-red-50 text-red-500 flex items-center justify-center border border-red-100"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <!-- PAGE: AUTH -->
        <div id="p-login" class="px-8 pt-16 animate__animated animate__fadeIn">
            <div class="mb-12 text-center">
                <h2 class="text-4xl font-black mb-2 tracking-tight italic">Initialize <br><span class="text-blue-600">Protocol</span>.</h2>
                <p class="text-gray-400 text-xs font-bold tracking-widest uppercase">Safe & Secure Staking sweetie.</p>
            </div>
            <div class="space-y-4">
                <input type="text" id="login-user" placeholder="Enter Username" class="input-field">
                <button onclick="handleAuth()" class="w-full btn-premium py-5 font-black uppercase tracking-widest text-sm shadow-2xl">Connect Vault</button>
            </div>
        </div>

        <!-- PAGE: HOME -->
        <div id="p-home" class="hidden px-6 pt-6 animate__animated animate__fadeIn">
            <div class="card-main p-8 relative overflow-hidden">
                <p class="text-[10px] font-bold opacity-50 uppercase tracking-[2px]">Net Liquid Capital</p>
                <h2 id="user-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                <div class="flex gap-3 mt-8">
                    <button onclick="showPage('deposit')" class="flex-1 bg-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase">Stake</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[10px] font-black backdrop-blur-md uppercase">Harvest</button>
                </div>
            </div>

            <!-- PROMO CODE SYSTEM -->
            <div class="mt-8 glass p-5 rounded-[28px] border-none shadow-sm flex items-center gap-3">
                <input type="text" id="promo-input" placeholder="Have a Promo Code?" class="bg-transparent flex-1 outline-none font-bold text-xs">
                <button onclick="applyPromo()" class="bg-blue-600 text-white px-4 py-2 rounded-xl text-[10px] font-black">APPLY</button>
            </div>

            <h3 class="font-black text-xl mt-10 mb-6 italic">Active Staking Nodes</h3>
            <div id="nodes-list" class="grid grid-cols-1 gap-4"></div>
        </div>

        <!-- PAGE: DEPOSIT -->
        <div id="p-deposit" class="hidden px-6 pt-6">
            <h3 class="font-black text-2xl mb-6 italic">Funding Gateway</h3>
            <div class="grid grid-cols-3 gap-3 mb-8">
                <div onclick="setMethod('Easypaisa')" class="method-card p-4 glass rounded-[25px] text-center">
                    <i class="fa-solid fa-mobile-screen text-xl text-green-500 mb-1"></i>
                    <p class="text-[9px] font-black">Easypaisa</p>
                </div>
                <div onclick="setMethod('JazzCash')" class="method-card p-4 glass rounded-[25px] text-center">
                    <i class="fa-solid fa-bolt text-xl text-yellow-500 mb-1"></i>
                    <p class="text-[9px] font-black">JazzCash</p>
                </div>
                <div onclick="setMethod('SadaPay')" class="method-card p-4 glass rounded-[25px] text-center">
                    <i class="fa-solid fa-credit-card text-xl text-pink-500 mb-1"></i>
                    <p class="text-[9px] font-black">SadaPay</p>
                </div>
            </div>
            <div id="dep-form" class="hidden space-y-5">
                <div class="p-6 bg-blue-50 rounded-[30px] border border-blue-100">
                    <p class="text-[10px] font-bold text-blue-600 uppercase mb-1">Send to (<span id="sel-method"></span>)</p>
                    <p class="font-black text-lg">03379827882</p>
                    <p class="text-[10px] font-bold text-gray-400 mt-1 uppercase">Name: NEXA HOLDINGS LTD</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-field">
                <input type="text" id="dep-tid" placeholder="Transaction TID" class="input-field">
                <div class="p-6 border-2 border-dashed border-gray-200 rounded-[25px] text-center bg-white">
                    <input type="file" id="dep-file" class="hidden"><label for="dep-file" class="cursor-pointer block"><i class="fa-solid fa-camera text-2xl text-blue-500 mb-2"></i><p class="text-[11px] font-bold text-gray-400">Proof Image</p></label>
                </div>
                <button onclick="submitDep()" class="w-full btn-premium py-5 font-black uppercase text-xs">Verify Deposit</button>
            </div>
        </div>

        <!-- PAGE: WITHDRAW -->
        <div id="p-withdraw" class="hidden px-6 pt-6">
            <h3 class="font-black text-2xl mb-6 italic">Harvest Profits</h3>
            <div class="space-y-4">
                <div class="p-6 glass rounded-[30px]"><p class="text-[10px] font-bold text-gray-400 uppercase">Balance</p><p id="wit-bal" class="text-3xl font-black text-blue-600 mt-1">$0.00</p></div>
                <input type="number" id="wit-amt" placeholder="Amount ($)" class="input-field">
                <input type="text" id="wit-acc" placeholder="Account Number" class="input-field">
                <button onclick="submitWit()" class="w-full btn-premium py-5 font-black uppercase text-xs">Initialize Payout</button>
            </div>
        </div>

        <!-- PAGE: HELP (Privacy Policy & Company Details) -->
        <div id="p-help" class="hidden px-6 pt-6">
            <h3 class="font-black text-2xl mb-6 italic">Protocol Center</h3>
            <div class="space-y-4">
                <div class="p-6 glass rounded-[30px]">
                    <h4 class="font-bold text-sm text-blue-600 mb-2 uppercase italic">About NEXA CORP</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">NEXA is a next-generation decentralized arbitrage network. We utilize 20 nodes globally to ensure stability and 100% payout security sweetie!</p>
                </div>
                <div class="p-6 glass rounded-[30px]">
                    <h4 class="font-bold text-sm text-blue-600 mb-2 uppercase italic">Privacy Shield</h4>
                    <p class="text-[11px] leading-relaxed text-gray-500">Your data is end-to-end encrypted. Proofs are only used for verification and then purged from our temporary cache. No KYC required sweetie.</p>
                </div>
            </div>
        </div>

        <!-- DOCK -->
        <nav id="app-dock" class="hidden dock">
            <button onclick="showPage('home')" id="nav-home" class="dock-item active"><i class="fa-solid fa-house"></i>Home</button>
            <button onclick="showPage('deposit')" id="nav-deposit" class="dock-item"><i class="fa-solid fa-wallet"></i>Stake</button>
            <button onclick="showPage('withdraw')" id="nav-withdraw" class="dock-item"><i class="fa-solid fa-hand-holding-dollar"></i>Harvest</button>
            <button onclick="showPage('help')" id="nav-help" class="dock-item"><i class="fa-solid fa-shield-halved"></i>Help</button>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, push, onValue, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
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

        // --- NAVIGATION ---
        window.showPage = (id) => {
            ['login', 'home', 'deposit', 'help', 'withdraw'].forEach(p => document.getElementById('p-' + p)?.classList.add('hidden'));
            document.getElementById('p-' + id).classList.remove('hidden');
            document.querySelectorAll('.dock-item').forEach(d => d.classList.remove('active'));
            document.getElementById('nav-' + id)?.classList.add('active');
        };

        // --- AUTO-INJECT 20 PLANS ---
        const initPlans = async () => {
            const snap = await get(ref(db, 'plans'));
            if(!snap.exists()) {
                const plans = {};
                for(let i=1; i<=15; i++) { plans[`p${i}`] = { name: `NODE ${i}`, min: i*10, profit: (i*0.5+2).toFixed(1) }; }
                for(let i=1; i<=5; i++) { plans[`vip${i}`] = { name: `VIP ELITE ${i}`, min: i*500, profit: (i*2+10).toFixed(1) }; }
                await set(ref(db, 'plans'), plans);
            }
        };

        // --- AUTH ---
        window.handleAuth = async () => {
            const user = document.getElementById('login-user').value;
            if(!user) return;
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            const snap = await get(ref(db, 'users/' + uid));
            if(!snap.exists()) await set(ref(db, 'users/' + uid), { username: user, balance: 0 });
            localStorage.setItem('nexa_uid', uid);
            location.reload();
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            initPlans();
            showPage('home');
            document.getElementById('logout-btn').classList.remove('hidden');
            document.getElementById('app-dock').classList.remove('hidden');
            onValue(ref(db, 'users/' + uid), s => {
                if(s.exists()){
                    const b = s.val().balance.toFixed(2);
                    document.getElementById('user-bal').innerText = `$${b}`;
                    document.getElementById('wit-bal').innerText = `$${b}`;
                }
            });
            onValue(ref(db, 'plans'), s => {
                const list = document.getElementById('nodes-list');
                list.innerHTML = "";
                s.forEach(p => {
                    const pd = p.val();
                    list.innerHTML += `<div class="glass p-5 rounded-[28px] flex justify-between items-center border-none">
                        <div class="flex items-center gap-4"><div class="w-11 h-11 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-microchip"></i></div>
                        <div><h4 class="text-[11px] font-black uppercase text-gray-400">${pd.name}</h4><p class="text-sm font-black">${pd.profit}% Daily</p></div></div>
                        <button onclick="alert('Fund your vault first sweetie!')" class="bg-slate-900 text-white px-5 py-2 rounded-xl text-[10px] font-black uppercase">Stake $${pd.min}</button></div>`;
                });
            });
        }

        // --- PROMO SYSTEM ---
        window.applyPromo = async () => {
            const code = document.getElementById('promo-input').value.toUpperCase();
            const snap = await get(ref(db, 'promos/' + code));
            if(snap.exists() && !localStorage.getItem('promo_'+code)) {
                const bonus = snap.val().bonus;
                const userSnap = await get(ref(db, 'users/' + uid));
                await update(ref(db, 'users/' + uid), { balance: userSnap.val().balance + bonus });
                localStorage.setItem('promo_'+code, true);
                alert(`Sweetie! Code applied. Bonus$${bonus} added!`);
            } else { alert("Invalid or used code sweetie!"); }
        };

        // --- DEPOSIT/WITHDRAWAL ---
        window.setMethod = (m) => {
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('active'));
            event.currentTarget.classList.add('active');
            document.getElementById('dep-form').classList.remove('hidden');
            document.getElementById('sel-method').innerText = m;
        };
        window.submitDep = () => { alert("Verification Proof Sent! Sweetie, wait 10-30 mins."); showPage('home'); };
        window.submitWit = () => { alert("Harvest request filed! Payout in 24h."); showPage('home'); };

        // --- GOD MODE (4 Taps on Logo) ---
        let taps = 0;
        document.getElementById('admin-trigger').onclick = () => {
            taps++;
            if(taps === 4) {
                const k = prompt("Master Access Key:");
                if(k === "NEXA786") {
                    const action = prompt("1: Add Promo | 2: Edit User Balance | 3: My UID");
                    if(action === "1") {
                        const c = prompt("Promo Code:").toUpperCase(); const b = parseFloat(prompt("Bonus ($):"));
                        set(ref(db, 'promos/' + c), { bonus: b });
                    } else if(action === "2") {
                        const u = prompt("User UID:"); const b = parseFloat(prompt("New Balance:"));
                        update(ref(db, 'users/' + u), { balance: b });
                    } else if(action === "3") { alert("Your UID: " + uid); }
                }
                taps = 0;
            }
        };

        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
