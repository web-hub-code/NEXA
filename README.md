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
        :root { --primary: #2563eb; --neon: #00f2ff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; user-select: none; overflow-x: hidden; }
        
        /* Glassmorphism */
        .glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(25px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .card-main { background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%); color: white; border-radius: 35px; position: relative; overflow: hidden; }
        
        /* Admin Overlay */
        #admin-panel { position: fixed; inset: 0; background: rgba(15, 23, 42, 0.98); z-index: 2000; display: none; padding: 25px; overflow-y: auto; }
        .admin-card { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 25px; padding: 20px; transition: 0.3s; }
        .admin-card:active { transform: scale(0.98); background: rgba(255,255,255,0.1); }
        
        /* Neon Animations */
        .neon-pulse { animation: pulse-blue 2s infinite; }
        @keyframes pulse-blue { 0% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0.4); } 70% { box-shadow: 0 0 0 15px rgba(37, 99, 235, 0); } 100% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0); } }

        .dock { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); width: 92%; max-width: 450px; background: #0f172a; border-radius: 28px; padding: 12px; display: flex; justify-content: space-around; z-index: 1000; }
        .dock-item { color: #64748b; font-size: 10px; font-weight: 700; text-align: center; flex: 1; transition: 0.3s; }
        .dock-item.active { color: #3b82f6; transform: translateY(-5px); }
        .dock-item i { font-size: 22px; display: block; margin-bottom: 4px; }

        .input-field { background: white; border: 1px solid #e2e8f0; border-radius: 20px; padding: 18px; width: 100%; outline: none; font-weight: 600; }
        .btn-premium { background: linear-gradient(135deg, #2563eb, #7c3aed); color: white; border-radius: 20px; font-weight: 800; }
        .hidden { display: none; }
    </style>
</head>
<body>

    <!-- ADMIN GOD MODE OVERLAY -->
    <div id="admin-panel" class="animate__animated">
        <div class="flex justify-between items-center mb-8">
            <div>
                <h2 class="text-white text-3xl font-black italic tracking-tighter">GOD MODE<span class="text-blue-500">.</span></h2>
                <p class="text-blue-400 text-[10px] font-bold tracking-[3px] uppercase">Sovereign Control</p>
            </div>
            <button onclick="closeAdmin()" class="w-12 h-12 rounded-2xl bg-white/10 text-white flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
        </div>

        <div class="grid grid-cols-2 gap-4">
            <!-- Balance Hack -->
            <div onclick="adminEditBalance()" class="admin-card text-center">
                <i class="fa-solid fa-wand-magic-sparkles text-blue-400 text-3xl mb-3"></i>
                <h4 class="text-white text-xs font-bold uppercase">Edit Balance</h4>
            </div>
            <!-- Promo Factory -->
            <div onclick="adminAddPromo()" class="admin-card text-center">
                <i class="fa-solid fa-ticket text-purple-400 text-3xl mb-3"></i>
                <h4 class="text-white text-xs font-bold uppercase">Promo Factory</h4>
            </div>
            <!-- Node Injector -->
            <div onclick="adminAddNode()" class="admin-card text-center">
                <i class="fa-solid fa-microchip text-green-400 text-3xl mb-3"></i>
                <h4 class="text-white text-xs font-bold uppercase">Inject Node</h4>
            </div>
            <!-- System Purge -->
            <div onclick="adminSystemWipe()" class="admin-card text-center">
                <i class="fa-solid fa-skull text-red-500 text-3xl mb-3"></i>
                <h4 class="text-white text-xs font-bold uppercase">Purge Data</h4>
            </div>
        </div>

        <div class="mt-8 p-6 bg-blue-600/10 border border-blue-500/20 rounded-[30px]">
            <h4 class="text-blue-400 font-black text-xs mb-4 uppercase tracking-widest">Active System Logs</h4>
            <div id="admin-logs" class="text-[10px] font-mono text-gray-400 space-y-2">
                <p>> System initialized...</p>
                <p>> Waiting for master command...</p>
            </div>
        </div>
    </div>

    <div class="max-w-md mx-auto min-h-screen relative pb-32">
        <!-- HEADER -->
        <header class="glass sticky top-0 z-[500] px-6 py-5 flex justify-between items-center">
            <div class="flex items-center gap-2">
                <div id="god-trigger" class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-white font-black shadow-lg cursor-pointer neon-pulse">N</div>
                <h1 class="text-xl font-extrabold tracking-tighter italic">NEXA<span class="text-blue-600">.</span></h1>
            </div>
            <button onclick="logout()" id="logout-btn" class="hidden w-10 h-10 rounded-full bg-red-50 text-red-500 flex items-center justify-center border border-red-100"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <!-- DASHBOARD (Home Page) -->
        <div id="p-home" class="px-6 pt-6 animate__animated animate__fadeIn">
            <div class="card-main p-8 shadow-2xl">
                <p class="text-[10px] font-bold opacity-50 uppercase tracking-[2px]">Net Liquid Capital</p>
                <h2 id="user-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                <div class="flex gap-3 mt-8">
                    <button onclick="showPage('deposit')" class="flex-1 bg-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase">Stake</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/10 py-4 rounded-2xl text-[10px] font-black backdrop-blur-md uppercase">Harvest</button>
                </div>
                <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-blue-500 rounded-full blur-[80px] opacity-20"></div>
            </div>

            <div class="mt-8 glass p-5 rounded-[28px] shadow-sm flex items-center gap-3">
                <input type="text" id="promo-input" placeholder="Promo Code?" class="bg-transparent flex-1 outline-none font-bold text-xs">
                <button onclick="applyPromo()" class="bg-blue-600 text-white px-5 py-2 rounded-xl text-[10px] font-black uppercase">Apply</button>
            </div>

            <h3 class="font-black text-xl mt-10 mb-6 italic">Network Nodes</h3>
            <div id="nodes-list" class="space-y-4"></div>
        </div>

        <!-- OTHER SECTIONS (DEPOSIT, WITHDRAW) HIDDEN BY DEFAULT -->
        <div id="p-deposit" class="hidden px-6 pt-6"></div>
        <div id="p-withdraw" class="hidden px-6 pt-6"></div>

        <!-- DOCK -->
        <nav id="app-dock" class="hidden dock">
            <button onclick="showPage('home')" id="nav-home" class="dock-item active"><i class="fa-solid fa-house"></i>Home</button>
            <button onclick="showPage('deposit')" id="nav-deposit" class="dock-item"><i class="fa-solid fa-wallet"></i>Stake</button>
            <button onclick="showPage('withdraw')" id="nav-withdraw" class="dock-item"><i class="fa-solid fa-hand-holding-dollar"></i>Harvest</button>
            <button onclick="showPage('admin')" id="nav-admin" class="dock-item"><i class="fa-solid fa-gear"></i>Setup</button>
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

        // --- GOD MODE CORE ---
        let taps = 0;
        document.getElementById('god-trigger').onclick = () => {
            taps++;
            if(taps === 4) {
                const pass = prompt("Enter Master Key:");
                if(pass === "NEXA786") {
                    document.getElementById('admin-panel').style.display = 'block';
                    document.getElementById('admin-panel').classList.add('animate__fadeInUp');
                    logAdmin("Root Access Granted.");
                }
                taps = 0;
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.closeAdmin = () => {
            document.getElementById('admin-panel').classList.replace('animate__fadeInUp', 'animate__fadeOutDown');
            setTimeout(() => {
                document.getElementById('admin-panel').style.display = 'none';
                document.getElementById('admin-panel').classList.remove('animate__fadeOutDown');
            }, 500);
        };

        function logAdmin(msg) {
            const logs = document.getElementById('admin-logs');
            logs.innerHTML += `<p>> ${msg}</p>`;
            logs.scrollTop = logs.scrollHeight;
        }

        // --- ADMIN ACTIONS ---
        window.adminEditBalance = async () => {
            const target = prompt("Target User UID:");
            const amount = prompt("New Balance ($):");
            if(target && amount) {
                await update(ref(db, `users/${target}`), { balance: parseFloat(amount) });
                logAdmin(`Balance updated for ${target} to $${amount}`);
                alert("Done sweetie!");
            }
        };

        window.adminAddPromo = async () => {
            const code = prompt("New Promo Code:").toUpperCase();
            const bonus = prompt("Bonus Amount ($):");
            if(code && bonus) {
                await set(ref(db, `promos/${code}`), { bonus: parseFloat(bonus) });
                logAdmin(`Promo Code ${code} created with$${bonus} bonus.`);
                alert("Promo factory active sweetie!");
            }
        };

        window.adminAddNode = async () => {
            const name = prompt("Node Name:");
            const min = prompt("Min Stake ($):");
            const profit = prompt("Daily Profit (%):");
            if(name && min) {
                await push(ref(db, 'plans'), { name, min: parseFloat(min), profit: parseFloat(profit) });
                logAdmin(`New Node [${name}] injected into network.`);
            }
        };

        // --- CORE FUNCTIONALITY ---
        async function initApp() {
            if(!uid) {
                const user = prompt("Node Name sweetie?");
                if(user) {
                    const res = await signInAnonymously(auth);
                    await set(ref(db, `users/${res.user.uid}`), { username: user, balance: 0 });
                    localStorage.setItem('nexa_uid', res.user.uid);
                    location.reload();
                }
            } else {
                document.getElementById('app-dock').classList.remove('hidden');
                onValue(ref(db, `users/${uid}`), s => {
                    if(s.exists()) document.getElementById('user-bal').innerText = `$${s.val().balance.toFixed(2)}`;
                });
                onValue(ref(db, 'plans'), s => {
                    const list = document.getElementById('nodes-list');
                    list.innerHTML = "";
                    s.forEach(p => {
                        const d = p.val();
                        list.innerHTML += `<div class="glass p-5 rounded-[28px] flex justify-between items-center animate__animated animate__fadeInUp">
                            <div class="flex items-center gap-4">
                                <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-microchip"></i></div>
                                <div><h4 class="text-xs font-black uppercase text-gray-400">${d.name}</h4><p class="text-sm font-black">${d.profit}% Daily</p></div>
                            </div>
                            <button onclick="alert('Insufficient Funds!')" class="bg-slate-900 text-white px-5 py-2 rounded-xl text-[10px] font-black uppercase">Stake $${d.min}</button>
                        </div>`;
                    });
                });
            }
        }

        window.showPage = (id) => {
            alert(`Page ${id} is ready to be linked sweetie! Master Dashboard is Live.`);
        };

        initApp();
    </script>
</body>
</html>
