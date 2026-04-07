<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Digital Sovereign</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;500;700&family=Syncopate:wght@400;700&display=swap');
        
        :root { --accent: #3b82f6; --neon: #00f2ff; --bg: #05070a; }
        body { font-family: 'Space Grotesk', sans-serif; background: var(--bg); color: white; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        .font-sync { font-family: 'Syncopate', sans-serif; }

        /* Neumorphic Glass */
        .glass-panel { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 32px; }
        .neon-glow { box-shadow: 0 0 20px rgba(59, 130, 246, 0.5); }
        
        /* Premium Card */
        .card-elite { background: linear-gradient(160deg, #1e293b 0%, #05070a 100%); border: 1px solid rgba(255,255,255,0.1); position: relative; overflow: hidden; }
        .card-elite::before { content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%; background: radial-gradient(circle, rgba(59,130,246,0.1) 0%, transparent 70%); }

        /* Animated Tabs */
        .tab-btn { transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); opacity: 0.5; }
        .tab-btn.active { opacity: 1; transform: translateY(-5px); color: var(--neon); }

        /* Custom Inputs */
        .nexa-input { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 20px; padding: 20px; width: 100%; color: white; outline: none; transition: 0.3s; }
        .nexa-input:focus { border-color: var(--accent); background: rgba(255,255,255,0.08); }

        /* Admin Overlay */
        #god-ui { position: fixed; inset: 0; background: rgba(5,7,10,0.98); z-index: 9999; display: none; padding: 30px; border-top: 2px solid var(--accent); }
        .admin-stat { background: rgba(255,255,255,0.03); border-radius: 24px; padding: 20px; border-left: 4px solid var(--accent); }

        .hidden { display: none; }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <!-- GOD MODE OVERLAY -->
    <div id="god-ui" class="animate__animated">
        <div class="flex justify-between items-center mb-10">
            <h2 class="font-sync text-2xl font-bold tracking-tighter">GOD<span class="text-blue-500">MODE</span></h2>
            <button onclick="toggleGodMode(false)" class="w-12 h-12 glass-panel flex items-center justify-center text-red-400"><i class="fa-solid fa-power-off"></i></button>
        </div>

        <div class="space-y-6">
            <div class="admin-stat">
                <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-2">Network Control</p>
                <div class="grid grid-cols-2 gap-4">
                    <button onclick="adminEditBalance()" class="bg-blue-600/20 text-blue-400 p-4 rounded-2xl text-xs font-bold border border-blue-500/30">EDIT BALANCE</button>
                    <button onclick="adminAddPromo()" class="bg-purple-600/20 text-purple-400 p-4 rounded-2xl text-xs font-bold border border-purple-500/30">NEW PROMO</button>
                </div>
            </div>

            <div class="admin-stat">
                <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-2">Plan Injector</p>
                <button onclick="adminAddNode()" class="w-full bg-green-600/20 text-green-400 p-4 rounded-2xl text-xs font-bold border border-green-500/30">INJECT NEW NODE</button>
            </div>

            <div class="admin-stat">
                <p class="text-[10px] text-gray-500 uppercase tracking-widest mb-2">Live Console</p>
                <div id="console" class="font-mono text-[10px] text-blue-300 h-32 overflow-y-auto">
                    > System Kernel 5.0 Active...<br>
                    > Encryption Layer: Enabled...
                </div>
            </div>
        </div>
    </div>

    <div class="max-w-md mx-auto min-h-screen px-6 py-8 relative">
        
        <!-- TOP NAVIGATION -->
        <header class="flex justify-between items-center mb-10">
            <div id="nexa-logo" class="flex items-center gap-3 cursor-pointer">
                <div class="w-12 h-12 glass-panel flex items-center justify-center neon-glow">
                    <i class="fa-solid fa-atom text-blue-500 animate-spin-slow"></i>
                </div>
                <span class="font-sync text-lg font-bold tracking-tighter">NEXA<span class="text-blue-500">.</span></span>
            </div>
            <div class="flex gap-3">
                <button onclick="showPage('help')" class="w-12 h-12 glass-panel flex items-center justify-center"><i class="fa-solid fa-shield-halved text-xs text-gray-400"></i></button>
                <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500"><i class="fa-solid fa-right-from-bracket text-xs"></i></button>
            </div>
        </header>

        <!-- DASHBOARD SECTION -->
        <section id="sec-home" class="animate__animated animate__fadeIn">
            <div class="card-elite p-8 rounded-[40px] mb-8">
                <div class="relative z-10">
                    <div class="flex justify-between items-start mb-4">
                        <span class="text-[10px] font-bold text-gray-400 tracking-[4px] uppercase">Liquidity Pool</span>
                        <i class="fa-brands fa-nfc-directional text-blue-500"></i>
                    </div>
                    <h2 id="user-bal" class="text-5xl font-bold tracking-tighter mb-8">$0.00</h2>
                    <div class="flex gap-4">
                        <button onclick="showPage('deposit')" class="flex-1 bg-blue-600 py-4 rounded-2xl text-[10px] font-bold uppercase tracking-widest shadow-lg shadow-blue-500/20">Deposit</button>
                        <button onclick="showPage('withdraw')" class="flex-1 glass-panel py-4 rounded-2xl text-[10px] font-bold uppercase tracking-widest">Withdraw</button>
                    </div>
                </div>
            </div>

            <!-- PROMO WIDGET -->
            <div class="glass-panel p-5 mb-10 flex items-center gap-4">
                <div class="w-10 h-10 bg-blue-600/20 rounded-full flex items-center justify-center text-blue-500"><i class="fa-solid fa-tags text-xs"></i></div>
                <input type="text" id="promo-in" placeholder="Enter Promo" class="bg-transparent flex-1 outline-none text-xs font-bold uppercase tracking-widest">
                <button onclick="applyPromo()" class="text-blue-500 font-bold text-[10px] uppercase">Apply</button>
            </div>

            <div class="flex justify-between items-center mb-6">
                <h3 class="font-sync text-xs font-bold tracking-widest uppercase">Quantum Nodes</h3>
                <span class="text-[8px] px-3 py-1 bg-green-500/10 text-green-400 rounded-full font-bold">100% SECURE</span>
            </div>

            <!-- NODES CONTAINER -->
            <div id="nodes-grid" class="space-y-4 pb-24">
                <!-- Injected via JS -->
            </div>
        </section>

        <!-- DEPOSIT SECTION -->
        <section id="sec-deposit" class="hidden animate__animated animate__fadeInUp">
            <h2 class="font-sync text-xl font-bold mb-8 italic">Add <span class="text-blue-500">Liquidity</span></h2>
            <div class="space-y-6">
                <div class="grid grid-cols-3 gap-3">
                    <button onclick="setDepMethod('Easypaisa')" class="glass-panel p-6 text-center focus:border-blue-500">
                        <i class="fa-solid fa-mobile-button text-green-500 text-xl mb-2"></i>
                        <p class="text-[8px] font-bold uppercase">Easypaisa</p>
                    </button>
                    <button onclick="setDepMethod('JazzCash')" class="glass-panel p-6 text-center focus:border-blue-500">
                        <i class="fa-solid fa-bolt text-yellow-500 text-xl mb-2"></i>
                        <p class="text-[8px] font-bold uppercase">JazzCash</p>
                    </button>
                    <button onclick="setDepMethod('SadaPay')" class="glass-panel p-6 text-center focus:border-blue-500">
                        <i class="fa-solid fa-credit-card text-pink-500 text-xl mb-2"></i>
                        <p class="text-[8px] font-bold uppercase">SadaPay</p>
                    </button>
                </div>
                <div id="dep-form" class="hidden space-y-4">
                    <div class="glass-panel p-6 border-blue-500/30">
                        <p class="text-[10px] text-blue-400 font-bold mb-1">RECIPIENT ACCOUNT</p>
                        <p class="text-2xl font-bold tracking-widest mb-1">03379827882</p>
                        <p class="text-[10px] text-gray-500">NAME: NEXA CORP VENTURES</p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Stake Amount ($)" class="nexa-input">
                    <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="nexa-input">
                    <button onclick="submitDeposit()" class="w-full bg-blue-600 py-5 rounded-2xl font-bold text-xs uppercase tracking-widest shadow-xl">Confirm Staking</button>
                </div>
            </div>
        </section>

        <!-- NAVIGATION DOCK -->
        <nav class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[90%] max-w-md glass-panel p-3 flex justify-around items-center z-[1000] border-white/5">
            <button onclick="showPage('home')" class="tab-btn active"><i class="fa-solid fa-house-chimney text-xl"></i></button>
            <button onclick="showPage('deposit')" class="tab-btn"><i class="fa-solid fa-plus-minus text-xl"></i></button>
            <button onclick="showPage('withdraw')" class="tab-btn"><i class="fa-solid fa-hand-holding-dollar text-xl"></i></button>
            <button onclick="showPage('help')" class="tab-btn"><i class="fa-solid fa-info-circle text-xl"></i></button>
        </nav>

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

        // --- NAVIGATION ENGINE ---
        window.showPage = (id) => {
            document.querySelectorAll('section').forEach(s => s.classList.add('hidden'));
            document.getElementById('sec-' + id)?.classList.remove('hidden');
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            // Visual active state handling
        };

        // --- GOD MODE ENGINE ---
        let taps = 0;
        document.getElementById('nexa-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const p = prompt("Master Access Key:");
                if(p === "NEXA786") toggleGodMode(true);
                taps = 0;
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.toggleGodMode = (show) => {
            const ui = document.getElementById('god-ui');
            ui.style.display = show ? 'block' : 'none';
            if(show) ui.classList.add('animate__fadeInUp');
        };

        // --- ADMIN COMMANDS ---
        window.adminEditBalance = async () => {
            const id = prompt("User UID:");
            const bal = prompt("New Balance ($):");
            if(id && bal) {
                await update(ref(db, `users/${id}`), { balance: parseFloat(bal) });
                alert("Financial Matrix Updated sweetie!");
            }
        };

        window.adminAddPromo = async () => {
            const c = prompt("Code:").toUpperCase();
            const b = prompt("Bonus ($):");
            if(c && b) await set(ref(db, `promos/${c}`), { bonus: parseFloat(b) });
        };

        // --- CORE LOGIC ---
        async function initialize() {
            if(!uid) {
                const name = prompt("Enter Node Name sweetie:");
                if(name) {
                    const res = await signInAnonymously(auth);
                    await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0 });
                    localStorage.setItem('nexa_uid', res.user.uid);
                    location.reload();
                }
            } else {
                onValue(ref(db, `users/${uid}`), s => {
                    if(s.exists()) document.getElementById('user-bal').innerText = `$${s.val().balance.toFixed(2)}`;
                });
                
                // Load Nodes
                onValue(ref(db, 'plans'), s => {
                    const grid = document.getElementById('nodes-grid');
                    grid.innerHTML = "";
                    s.forEach(p => {
                        const d = p.val();
                        grid.innerHTML += `
                        <div class="glass-panel p-6 flex justify-between items-center animate__animated animate__fadeInUp">
                            <div class="flex items-center gap-4">
                                <div class="w-12 h-12 bg-blue-600/10 rounded-2xl flex items-center justify-center text-blue-500 shadow-inner">
                                    <i class="fa-solid fa-microchip text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="text-[10px] font-bold text-gray-500 uppercase tracking-widest">${d.name}</h4>
                                    <p class="text-sm font-bold text-blue-400">${d.profit}% Daily Yield</p>
                                </div>
                            </div>
                            <button class="bg-white/5 px-6 py-3 rounded-xl text-[10px] font-bold uppercase border border-white/10 hover:bg-blue-600 transition">Stake $${d.min}</button>
                        </div>`;
                    });
                });
            }
        }

        window.setDepMethod = (m) => {
            document.getElementById('dep-form').classList.remove('hidden');
            // Add focus visual
        };

        window.logout = () => { localStorage.clear(); location.reload(); };
        
        initialize();
    </script>
</body>
</html>
