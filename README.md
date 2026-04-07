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
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root { 
            --accent: #0066ff; 
            --bg: #fdfdfe; 
            --card: #ffffff;
            --text: #0f172a;
        }
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: var(--bg); 
            color: var(--text); 
            overflow-x: hidden; 
            -webkit-tap-highlight-color: transparent; 
        }

        /* Crystal Glassmorphism (Light) */
        .glass-panel { 
            background: rgba(255, 255, 255, 0.7); 
            backdrop-filter: blur(20px); 
            border: 1px solid rgba(0, 0, 0, 0.05); 
            border-radius: 30px; 
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.02);
        }
        
        /* Premium Soft Card */
        .card-elite { 
            background: linear-gradient(135deg, #0066ff 0%, #0044aa 100%); 
            color: white;
            border-radius: 40px; 
            position: relative; 
            overflow: hidden; 
            box-shadow: 0 25px 50px -12px rgba(0, 102, 255, 0.3);
        }

        .card-elite::after {
            content: ''; position: absolute; top: -20%; right: -10%; width: 150px; height: 150px;
            background: rgba(255,255,255,0.1); border-radius: 50%; blur: 40px;
        }

        /* Animated Navigation */
        .tab-btn { transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); color: #94a3b8; }
        .tab-btn.active { color: var(--accent); transform: translateY(-3px); }

        /* Modern Input Field */
        .nexa-input { 
            background: #f1f5f9; 
            border: 2px solid transparent; 
            border-radius: 24px; 
            padding: 20px; 
            width: 100%; 
            color: var(--text); 
            outline: none; 
            font-weight: 600;
            transition: 0.3s; 
        }
        .nexa-input:focus { border-color: var(--accent); background: white; box-shadow: 0 0 0 4px rgba(0, 102, 255, 0.05); }

        /* Admin UI Overlay (Crystal Dark) */
        #god-ui { 
            position: fixed; inset: 0; background: rgba(255, 255, 255, 0.98); 
            z-index: 9999; display: none; padding: 30px; 
        }
        .admin-stat { background: #f8fafc; border-radius: 28px; padding: 20px; border: 1px solid #e2e8f0; }

        .hidden { display: none; }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <!-- GOD MODE OVERLAY (Light Master) -->
    <div id="god-ui" class="animate__animated">
        <div class="flex justify-between items-center mb-10">
            <h2 class="font-bold text-3xl tracking-tighter text-blue-600 italic">GOD MODE</h2>
            <button onclick="toggleGodMode(false)" class="w-12 h-12 bg-red-50 text-red-500 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
        </div>

        <div class="space-y-6">
            <div class="admin-stat">
                <p class="text-[10px] text-gray-400 font-bold uppercase tracking-widest mb-4 text-center">System Override</p>
                <div class="grid grid-cols-2 gap-4">
                    <button onclick="adminEditBalance()" class="bg-blue-600 text-white p-5 rounded-3xl text-[10px] font-black uppercase shadow-lg shadow-blue-200">Edit Balance</button>
                    <button onclick="adminAddPromo()" class="bg-slate-900 text-white p-5 rounded-3xl text-[10px] font-black uppercase">Promo Factory</button>
                </div>
            </div>
            <button onclick="adminAddNode()" class="w-full bg-white border-2 border-dashed border-blue-200 p-6 rounded-[35px] text-blue-600 font-bold text-xs uppercase tracking-widest">+ Inject New Node</button>
        </div>
    </div>

    <div class="max-w-md mx-auto min-h-screen px-6 py-8 relative">
        
        <!-- HEADER -->
        <header class="flex justify-between items-center mb-8">
            <div id="nexa-logo" class="flex items-center gap-3">
                <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-xl shadow-blue-200">
                    <i class="fa-solid fa-bolt-lightning text-xl animate-pulse"></i>
                </div>
                <span class="text-2xl font-black italic tracking-tighter">NEXA<span class="text-blue-600">.</span></span>
            </div>
            <div class="flex gap-2">
                <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500 border-none"><i class="fa-solid fa-power-off text-sm"></i></button>
            </div>
        </header>

        <!-- DASHBOARD (Home) -->
        <section id="sec-home" class="animate__animated animate__fadeIn">
            <div class="card-elite p-8 mb-8">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold opacity-70 uppercase tracking-[3px]">Total Portfolio Value</p>
                    <h2 id="user-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                    <div class="flex gap-4 mt-10">
                        <button onclick="showPage('deposit')" class="flex-1 bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-xl">Deposit</button>
                        <button onclick="showPage('withdraw')" class="flex-1 bg-white/20 backdrop-blur-md py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest">Withdraw</button>
                    </div>
                </div>
            </div>

            <!-- PROMO WIDGET -->
            <div class="glass-panel p-5 mb-10 flex items-center gap-4">
                <div class="w-11 h-11 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-ticket-simple"></i></div>
                <input type="text" id="promo-in" placeholder="HAVE A PROMO CODE?" class="bg-transparent flex-1 outline-none text-[10px] font-black uppercase tracking-widest text-slate-400">
                <button onclick="applyPromo()" class="text-blue-600 font-black text-[10px] uppercase">Apply</button>
            </div>

            <div class="flex justify-between items-center mb-6 px-2">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Yield Generators</h3>
                <span class="text-[9px] font-bold text-green-500 bg-green-50 px-3 py-1 rounded-full border border-green-100">STABLE</span>
            </div>

            <!-- NODES GRID -->
            <div id="nodes-grid" class="space-y-4 pb-32">
                <!-- Data will be injected here -->
            </div>
        </section>

        <!-- FOOTER DOCK -->
        <nav class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[90%] max-w-md glass-panel p-4 flex justify-around items-center z-[1000] border-none shadow-2xl shadow-blue-100">
            <button onclick="showPage('home')" class="tab-btn active"><i class="fa-solid fa-house-user text-xl"></i></button>
            <button onclick="showPage('deposit')" class="tab-btn"><i class="fa-solid fa-wallet text-xl"></i></button>
            <button onclick="showPage('withdraw')" class="tab-btn"><i class="fa-solid fa-chart-line text-xl"></i></button>
            <button onclick="showPage('help')" class="tab-btn"><i class="fa-solid fa-circle-info text-xl"></i></button>
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

        // --- AUTH & INIT ---
        async function startSystem() {
            if(!uid) {
                const name = prompt("Identify yourself sweetie:");
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

                // Load Nodes (Light Theme Cards)
                onValue(ref(db, 'plans'), s => {
                    const grid = document.getElementById('nodes-grid');
                    grid.innerHTML = "";
                    s.forEach(p => {
                        const d = p.val();
                        grid.innerHTML += `
                        <div class="glass-panel p-6 flex justify-between items-center animate__animated animate__fadeInUp">
                            <div class="flex items-center gap-4">
                                <div class="w-14 h-14 bg-slate-50 border border-slate-100 rounded-3xl flex items-center justify-center text-blue-600 shadow-sm">
                                    <i class="fa-solid fa-server text-xl"></i>
                                </div>
                                <div>
                                    <h4 class="text-[10px] font-black text-slate-400 uppercase tracking-widest">${d.name}</h4>
                                    <p class="text-lg font-bold text-slate-800">${d.profit}% <span class="text-xs text-blue-500">Daily</span></p>
                                </div>
                            </div>
                            <button class="bg-blue-600 text-white px-6 py-3 rounded-2xl text-[10px] font-black uppercase shadow-lg shadow-blue-100">STAKE $${d.min}</button>
                        </div>`;
                    });
                });
            }
        }

        // --- GOD MODE (4 Taps on Logo) ---
        let taps = 0;
        document.getElementById('nexa-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const p = prompt("MASTER KEY:");
                if(p === "NEXA786") {
                    document.getElementById('god-ui').style.display = 'block';
                    document.getElementById('god-ui').classList.add('animate__fadeInUp');
                }
                taps = 0;
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.toggleGodMode = (show) => {
            document.getElementById('god-ui').style.display = show ? 'block' : 'none';
        };

        window.adminEditBalance = async () => {
            const id = prompt("User UID:");
            const amt = prompt("New Balance ($):");
            if(id && amt) await update(ref(db, `users/${id}`), { balance: parseFloat(amt) });
        };

        window.logout = () => { localStorage.clear(); location.reload(); };

        startSystem();
    </script>
</body>
</html>
