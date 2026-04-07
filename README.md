<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign v5.0</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --accent: #0066ff; --bg: #f8fafc; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        .glass-panel { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.4); border-radius: 32px; }
        .card-elite { background: linear-gradient(145deg, #0052D1 0%, #001C48 100%); color: white; border-radius: 40px; box-shadow: 0 30px 60px -15px rgba(0, 82, 209, 0.4); overflow: hidden; }
        
        .nexa-input { background: #f1f5f9; border-radius: 20px; padding: 18px; width: 100%; outline: none; border: 2px solid transparent; transition: 0.3s; font-weight: 700; font-size: 14px; }
        .nexa-input:focus { border-color: var(--accent); background: white; box-shadow: 0 10px 20px rgba(0,0,0,0.05); }
        
        .hidden { display: none; }
        .tab-active { color: #0066ff !important; position: relative; }
        .tab-active::after { content: ''; position: absolute; bottom: -10px; left: 50%; transform: translateX(-50%); width: 6px; height: 6px; background: #0066ff; border-radius: 50%; }

        @keyframes scan { 0% { top: 0%; } 100% { top: 100%; } }
        .scan-line { position: absolute; width: 100%; height: 3px; background: #0066ff; box-shadow: 0 0 15px #0066ff; animation: scan 2s linear infinite; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. AUTH SCREEN (Modern Biometric Look) -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[20000] flex flex-col items-center justify-center p-8">
        <div class="w-20 h-20 bg-blue-600 rounded-[28px] flex items-center justify-center text-white text-3xl mb-12 shadow-2xl rotate-6 animate__animated animate__bounceIn">
            <i class="fa-solid fa-shield-halved"></i>
        </div>
        <h2 class="text-3xl font-black italic tracking-tighter mb-2">NEXA SECURE</h2>
        <p class="text-slate-400 text-xs font-bold uppercase tracking-widest mb-12 text-center leading-relaxed">Enter credentials to sync<br>with Sovereign Nodes</p>
        
        <div class="w-full space-y-4 max-w-xs">
            <div class="relative">
                <i class="fa-solid fa-user absolute left-5 top-1/2 -translate-y-1/2 text-slate-300"></i>
                <input type="text" id="login-user" placeholder="Node Username" class="nexa-input pl-14">
            </div>
            <div class="relative group cursor-pointer py-10 flex flex-col items-center" onclick="attemptLogin()">
                <div class="w-20 h-24 border-2 border-slate-200 rounded-2xl relative overflow-hidden flex items-center justify-center text-slate-200 text-4xl">
                    <i class="fa-solid fa-fingerprint"></i>
                    <div class="scan-line"></div>
                </div>
                <p class="mt-4 text-[10px] font-black text-blue-600 uppercase tracking-widest animate-pulse">Tap to Verify & Sync</p>
            </div>
        </div>
    </div>

    <!-- 2. MAIN APP CONTENT -->
    <div id="app-content" class="hidden">
        
        <!-- TOP TICKER -->
        <div class="bg-black text-[9px] py-2.5 font-bold uppercase tracking-[2px] text-blue-400 overflow-hidden whitespace-nowrap">
            <div class="inline-block animate-[ticker_60s_linear_infinite]">
                SYSTEM STATUS: <span class="text-green-500">OPTIMAL</span> • TOTAL RESERVES: $1,240,982.00 • NODE #092 SYNCED • RECENT HARVEST: $240.00 BY USER_928 • AES-256 ENCRYPTION ACTIVE •
            </div>
        </div>

        <div class="max-w-md mx-auto px-6 py-8">
            
            <!-- HEADER -->
            <header class="flex justify-between items-center mb-10">
                <div id="nexa-logo" class="flex items-center gap-4 cursor-pointer">
                    <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-xl shadow-blue-100"><i class="fa-solid fa-bolt-lightning text-xl"></i></div>
                    <div>
                        <h1 class="text-xl font-black italic tracking-tighter leading-none">NEXA.</h1>
                        <span class="text-[8px] font-black text-green-500 uppercase tracking-widest flex items-center gap-1">
                            <span class="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></span> Node Active
                        </span>
                    </div>
                </div>
                <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500 text-lg shadow-sm"><i class="fa-solid fa-power-off"></i></button>
            </header>

            <!-- DASHBOARD -->
            <main id="p-home" class="animate__animated animate__fadeIn">
                <div class="card-elite p-8 mb-8 relative">
                    <div class="flex justify-between items-start mb-8">
                        <div>
                            <p class="text-[9px] font-black opacity-60 uppercase tracking-[2px] mb-2">Portfolio Balance</p>
                            <h2 id="user-bal" class="text-5xl font-black tracking-tighter">$0.00</h2>
                        </div>
                        <div class="w-12 h-12 bg-white/10 rounded-full flex items-center justify-center backdrop-blur-xl border border-white/20">
                            <i class="fa-solid fa-gem text-blue-300"></i>
                        </div>
                    </div>
                    <div class="flex gap-4">
                        <button onclick="showPage('deposit')" class="flex-1 bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-2xl"><i class="fa-solid fa-plus-circle mr-2"></i>Stake</button>
                        <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest backdrop-blur-md"><i class="fa-solid fa-vault mr-2"></i>Harvest</button>
                    </div>
                    <!-- Fake Chart Line Decoration -->
                    <div class="absolute bottom-0 left-0 w-full opacity-20 pointer-events-none">
                        <svg viewBox="0 0 100 20" class="w-full h-12"><path d="M0,20 Q15,5 30,15 T60,5 T100,18" fill="none" stroke="white" stroke-width="1"/></svg>
                    </div>
                </div>

                <div class="flex gap-4 mb-10 overflow-x-auto pb-2 no-scrollbar">
                    <div class="glass-panel p-4 min-w-[140px] text-center border-b-4 border-blue-500">
                        <i class="fa-solid fa-link text-blue-600 mb-2"></i>
                        <p class="text-[8px] font-black text-slate-400 uppercase">Referral</p>
                        <p id="ref-id" class="text-[10px] font-bold text-slate-800 mt-1">---</p>
                    </div>
                    <div class="glass-panel p-4 min-w-[140px] text-center border-b-4 border-green-500">
                        <i class="fa-solid fa-shield-check text-green-500 mb-2"></i>
                        <p class="text-[8px] font-black text-slate-400 uppercase">Reserve Proof</p>
                        <p class="text-[10px] font-bold text-slate-800 mt-1">100% Solid</p>
                    </div>
                </div>

                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-6 flex items-center gap-3">
                    <i class="fa-solid fa-microchip text-blue-600"></i> Global Mining Nodes
                </h3>
                <div id="nodes-grid" class="space-y-4"></div>
            </main>

            <!-- DEPOSIT PAGE -->
            <main id="p-deposit" class="hidden animate__animated animate__fadeInUp">
                <h2 class="text-3xl font-black mb-8 italic">Node Liquidity</h2>
                <div id="method-selector" class="space-y-4">
                    <div onclick="selectMethod('Easypaisa', '03379827882')" class="glass-panel p-6 border-l-4 border-green-500 flex justify-between items-center cursor-pointer shadow-sm hover:shadow-md transition-all">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-green-50 text-green-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-money-bill-transfer text-xl"></i></div>
                            <div><p class="font-bold">Easypaisa</p><p class="text-[8px] text-slate-400 uppercase font-black">Instant Sync</p></div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-slate-200"></i>
                    </div>
                    <div onclick="selectMethod('JazzCash', '03705519562')" class="glass-panel p-6 border-l-4 border-yellow-500 flex justify-between items-center cursor-pointer shadow-sm hover:shadow-md transition-all">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-yellow-50 text-yellow-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-building-columns text-xl"></i></div>
                            <div><p class="font-bold">JazzCash</p><p class="text-[8px] text-slate-400 uppercase font-black">Instant Sync</p></div>
                        </div>
                        <i class="fa-solid fa-chevron-right text-slate-200"></i>
                    </div>
                </div>

                <div id="dep-form" class="hidden space-y-6 mt-4">
                    <div class="p-10 glass-panel bg-white text-center border-t-8 border-blue-600 shadow-2xl relative">
                        <div class="absolute -top-4 left-1/2 -translate-x-1/2 bg-blue-600 text-white px-4 py-1 rounded-full text-[8px] font-black uppercase">Official Wallet</div>
                        <p id="m-num-display" class="text-3xl font-black text-slate-800 tracking-widest mb-2"></p>
                        <p id="m-name-display" class="text-xs font-bold text-blue-600"></p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Stake Amount ($)" class="nexa-input">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="nexa-input">
                    <button onclick="submitManualRequest('Deposit')" class="w-full bg-blue-600 text-white p-6 rounded-3xl font-black uppercase text-xs tracking-[3px] shadow-2xl shadow-blue-200">Inject Liquidity</button>
                </div>
            </main>

            <!-- WITHDRAW PAGE -->
            <main id="p-withdraw" class="hidden animate__animated animate__fadeInUp">
                <h2 class="text-3xl font-black mb-8 italic">Harvest Gains</h2>
                <div class="space-y-6">
                    <div class="glass-panel p-10 text-center bg-white border-b-8 border-blue-600">
                        <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Claimable Rewards</p>
                        <p id="wit-bal-display" class="text-5xl font-black text-blue-600 tracking-tighter">$0.00</p>
                    </div>
                    <input type="number" id="wit-amt" placeholder="Amount to claim ($)" class="nexa-input">
                    <input type="text" id="wit-acc" placeholder="Account Details (Number)" class="nexa-input">
                    <select id="wit-meth" class="nexa-input bg-white font-bold">
                        <option>Easypaisa</option>
                        <option>JazzCash</option>
                        <option>SadaPay</option>
                    </select>
                    <button onclick="submitManualRequest('Withdraw')" class="w-full bg-slate-900 text-white p-6 rounded-3xl font-black uppercase text-xs tracking-[3px]">Process Payout</button>
                </div>
            </main>
        </div>

        <!-- NAV DOCK -->
        <nav class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[90%] max-w-sm glass-panel p-5 flex justify-around items-center z-[1000] shadow-2xl border-none">
            <button onclick="showPage('home')" id="n-home" class="text-slate-300 tab-active transition-all"><i class="fa-solid fa-layer-group text-2xl"></i></button>
            <button onclick="showPage('deposit')" id="n-deposit" class="text-slate-300 transition-all"><i class="fa-solid fa-circle-plus text-2xl"></i></button>
            <button onclick="showPage('withdraw')" id="n-withdraw" class="text-slate-300 transition-all"><i class="fa-solid fa-receipt text-2xl"></i></button>
        </nav>
    </div>

    <!-- GOD MODE PANEL -->
    <div id="god-ui" class="fixed inset-0 bg-white/95 backdrop-blur-2xl z-[50000] hidden p-10 overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="font-black text-2xl text-blue-600 italic uppercase">Master Control</h2>
            <button onclick="toggleGodMode(false)" class="text-red-500 text-4xl"><i class="fa-solid fa-circle-xmark"></i></button>
        </div>
        <div class="space-y-4">
            <p class="text-[10px] font-black text-slate-400">UID: <span id="my-uid-box" class="text-blue-600"></span></p>
            <input type="text" id="adm-uid" placeholder="Target User UID" class="nexa-input">
            <input type="number" id="adm-bal" placeholder="Set Balance ($)" class="nexa-input">
            <button onclick="adminEditBalance()" class="w-full bg-blue-600 text-white p-6 rounded-3xl font-black uppercase text-xs">Update Database</button>
        </div>
    </div>

    <!-- WHATSAPP SUPPORT -->
    <a href="https://wa.me/923379827882" class="fixed bottom-28 right-8 w-16 h-16 bg-green-500 text-white rounded-[24px] flex items-center justify-center shadow-2xl shadow-green-100 animate-bounce z-[1000]"><i class="fa-brands fa-whatsapp text-3xl"></i></a>

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

        window.showPage = (id) => {
            document.querySelectorAll('main').forEach(m => m.classList.add('hidden'));
            document.getElementById('p-'+id).classList.remove('hidden');
            document.querySelectorAll('nav button').forEach(b => b.classList.remove('tab-active'));
            document.getElementById('n-'+id).classList.add('tab-active');
            window.scrollTo(0,0);
        };

        window.selectMethod = (name, num) => {
            document.getElementById('method-selector').classList.add('hidden');
            document.getElementById('dep-form').classList.remove('hidden');
            document.getElementById('m-name-display').innerText = name;
            document.getElementById('m-num-display').innerText = num;
        };

        window.attemptLogin = async () => {
            const name = document.getElementById('login-user').value;
            if(!name) return alert("Enter Username Sweetie!");
            
            if(!uid) {
                const res = await signInAnonymously(auth);
                await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, ref: 'NX'+Math.floor(100+Math.random()*899) });
                localStorage.setItem('nexa_uid', res.user.uid);
            }
            document.getElementById('auth-screen').classList.add('animate__fadeOut');
            setTimeout(() => {
                document.getElementById('auth-screen').style.display = 'none';
                document.getElementById('app-content').classList.remove('hidden');
                initApp();
            }, 500);
        };

        window.submitManualRequest = async (type) => {
            const amt = type === 'Deposit' ? document.getElementById('dep-amt').value : document.getElementById('wit-amt').value;
            const extra = type === 'Deposit' ? document.getElementById('dep-tid').value : document.getElementById('wit-acc').value;
            if(!amt || !extra) return alert("Fill all fields sweetie!");

            await push(ref(db, `requests/${type}`), { uid: uid, amount: amt, info: extra, timestamp: Date.now() });
            alert(`Node verification in progress! Please wait.`);
            showPage('home');
        };

        function initApp() {
            document.getElementById('my-uid-box').innerText = uid;
            onValue(ref(db, `users/${uid}`), s => {
                const val = s.val().balance.toFixed(2);
                document.getElementById('user-bal').innerText = `$${val}`;
                document.getElementById('wit-bal-display').innerText = `$${val}`;
                document.getElementById('ref-id').innerText = s.val().ref;
            });

            const grid = document.getElementById('nodes-grid');
            grid.innerHTML = "";
            for(let i=1; i<=20; i++) {
                grid.innerHTML += `
                <div class="glass-panel p-6 animate__animated animate__fadeInUp" style="animation-delay: ${i*0.1}s">
                    <div class="flex justify-between items-center mb-4">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-microchip text-xl"></i></div>
                            <div><p class="text-[8px] font-black text-slate-400 uppercase tracking-widest">Node Alpha ${i}</p><p class="text-sm font-bold text-slate-800">${(1.5 + i*0.5).toFixed(1)}% ROI</p></div>
                        </div>
                        <button onclick="alert('Checking Node Capacity...')" class="bg-blue-600 text-white px-5 py-2.5 rounded-xl text-[9px] font-black uppercase">Stake $${i*20}</button>
                    </div>
                    <div class="w-full bg-slate-100 h-1 rounded-full overflow-hidden">
                        <div class="bg-blue-600 h-full animate-pulse" style="width: ${20 + (i*3)}%"></div>
                    </div>
                </div>`;
            }
        }

        // --- GOD MODE ---
        let taps = 0;
        document.getElementById('nexa-logo').onclick = () => {
            taps++;
            if(taps === 4) { if(prompt("MASTER KEY:") === "NEXA786") toggleGodMode(true); taps = 0; }
            setTimeout(() => taps = 0, 2000);
        };
        window.toggleGodMode = (v) => document.getElementById('god-ui').style.display = v ? 'block' : 'none';
        window.adminEditBalance = async () => {
            const target = document.getElementById('adm-uid').value;
            const bal = document.getElementById('adm-bal').value;
            await update(ref(db
