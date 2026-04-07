<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | Sovereign Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(12px); border-radius: 24px; border: 1px solid rgba(255,255,255,0.3); }
        .neon-card { background: linear-gradient(135deg, #6366f1 0%, #a855f7 100%); color: white; border-radius: 30px; box-shadow: 0 20px 40px -10px rgba(99, 102, 241, 0.5); }
        .bottom-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; height: 70px; background: #1e293b; border-radius: 25px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; box-shadow: 0 15px 30px rgba(0,0,0,0.2); }
        .nav-item { color: #64748b; font-size: 20px; transition: 0.3s; cursor: pointer; }
        .nav-item.active { color: #818cf8; transform: translateY(-5px); }
        .fake-notif { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); z-index: 9999; width: 90%; max-width: 350px; pointer-events: none; }
        .hidden { display: none !important; }
        .timer-badge { background: rgba(0,0,0,0.1); padding: 4px 10px; border-radius: 8px; font-family: monospace; }
    </style>
</head>
<body class="pb-24">

    <!-- FAKE NOTIFICATION ENGINE -->
    <div id="notif-container" class="fake-notif"></div>

    <!-- AUTH MODULE -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9000] flex flex-col items-center justify-center p-8 text-center">
        <div onclick="adminTap()" class="w-20 h-20 bg-indigo-600 rounded-3xl flex items-center justify-center text-white text-3xl mb-6 shadow-xl">
            <i class="fa-solid fa-bolt"></i>
        </div>
        <h1 class="text-3xl font-extrabold tracking-tighter mb-2">NEXA <span class="text-indigo-600">PRO</span></h1>
        <p class="text-xs font-bold text-slate-400 uppercase tracking-[3px] mb-8">Cloud Mining Ecosystem</p>
        <input type="text" id="user-name" placeholder="Choose Nickname" class="w-full max-w-xs p-5 bg-slate-100 rounded-2xl border-none outline-none font-bold mb-4 focus:ring-2 ring-indigo-500">
        <button onclick="startApp()" class="w-full max-w-xs bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-2xl">Initialize Hub</button>
    </div>

    <!-- MAIN APP -->
    <div id="app" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-md z-50">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-indigo-50 rounded-xl flex items-center justify-center text-indigo-600 font-black">N</div>
                <div>
                    <h2 id="display-name" class="text-sm font-black italic">User</h2>
                    <p id="display-uid" class="text-[8px] text-slate-400 font-bold uppercase"></p>
                </div>
            </div>
            <button onclick="showAdmin()" id="admin-btn" class="hidden w-10 h-10 bg-red-50 text-red-500 rounded-xl"><i class="fa-solid fa-screwdriver-wrench"></i></button>
        </header>

        <main class="px-6">
            <!-- PAGE: HOME -->
            <div id="page-home" class="page-content animate__animated animate__fadeIn">
                <div class="neon-card p-8 mb-8 relative overflow-hidden">
                    <p class="text-[10px] font-bold opacity-80 uppercase tracking-widest mb-1">Available Liquidity</p>
                    <h2 id="user-bal" class="text-5xl font-black tracking-tighter mb-8">$0.00</h2>
                    <div class="flex gap-3">
                        <button onclick="nav('deposit')" class="flex-1 bg-white text-indigo-600 py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg">Deposit</button>
                        <button onclick="nav('withdraw')" class="flex-1 bg-white/20 py-4 rounded-2xl text-[10px] font-black uppercase backdrop-blur-sm">Withdraw</button>
                    </div>
                </div>

                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-[11px] font-black uppercase tracking-widest text-slate-400">Mining Clusters</h3>
                    <div class="flex gap-2 text-[10px] font-bold text-indigo-600"><i class="fa-solid fa-circle-dot animate-pulse"></i> LIVE</div>
                </div>

                <!-- PLANS CONTAINER -->
                <div id="plans-container" class="space-y-4"></div>
            </div>

            <!-- PAGE: DEPOSIT -->
            <div id="page-deposit" class="page-content hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">Top Up</h2>
                <div class="grid grid-cols-2 gap-4 mb-8">
                    <div onclick="openGateway('JazzCash','03705519562')" class="glass p-5 text-center active:scale-95 transition-all cursor-pointer">
                        <div class="w-12 h-12 bg-red-600 rounded-2xl mx-auto mb-3 flex items-center justify-center text-white font-black">JC</div>
                        <p class="font-black text-xs uppercase italic">JazzCash</p>
                    </div>
                    <div onclick="openGateway('Easypaisa','03379827882')" class="glass p-5 text-center active:scale-95 transition-all cursor-pointer">
                        <div class="w-12 h-12 bg-green-500 rounded-2xl mx-auto mb-3 flex items-center justify-center text-white font-black">EP</div>
                        <p class="font-black text-xs uppercase italic">Easypaisa</p>
                    </div>
                    <div onclick="openGateway('SadaPay','03379827882')" class="glass p-5 text-center active:scale-95 transition-all cursor-pointer">
                        <div class="w-12 h-12 bg-teal-400 rounded-2xl mx-auto mb-3 flex items-center justify-center text-white font-black">SP</div>
                        <p class="font-black text-xs uppercase italic">SadaPay</p>
                    </div>
                    <div class="glass p-5 text-center opacity-50 relative overflow-hidden">
                        <div class="w-12 h-12 bg-yellow-500 rounded-2xl mx-auto mb-3 flex items-center justify-center text-white font-black"><i class="fa-brands fa-bitcoin"></i></div>
                        <p class="font-black text-xs uppercase italic">Binance</p>
                        <div class="absolute inset-0 bg-black/40 flex items-center justify-center text-[8px] text-white font-black uppercase rotate-12">Coming Soon</div>
                    </div>
                </div>
            </div>

            <!-- PAGE: WITHDRAW -->
            <div id="page-withdraw" class="page-content hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black italic mb-6">Withdraw</h2>
                <div class="glass p-6 space-y-4">
                    <input type="number" id="wd-amt" placeholder="Amount ($5 Min)" class="w-full p-5 bg-slate-50 rounded-2xl font-bold outline-none">
                    <input type="text" id="wd-wallet" placeholder="Account Number" class="w-full p-5 bg-slate-50 rounded-2xl font-bold outline-none">
                    <button onclick="processWd()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs tracking-widest shadow-xl">Request Payout</button>
                </div>
            </div>

            <!-- PAGE: ADMIN -->
            <div id="page-admin" class="page-content hidden animate__animated animate__fadeIn">
                <div class="flex justify-between items-center mb-8">
                    <h2 class="text-3xl font-black italic text-red-500 tracking-tighter">ADMIN CORE</h2>
                    <button onclick="nav('home')" class="text-slate-400"><i class="fa-solid fa-circle-xmark text-2xl"></i></button>
                </div>
                
                <!-- ALL USERS SECTION -->
                <div class="mb-10">
                    <h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 ml-2 tracking-widest">Active Members</h3>
                    <div id="admin-user-list" class="space-y-3"></div>
                </div>

                <!-- DEPOSITS SECTION -->
                <div class="mb-10">
                    <h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 ml-2 tracking-widest">Pending Deposits</h3>
                    <div id="admin-dep-list" class="space-y-3"></div>
                </div>
            </div>
        </main>

        <nav class="bottom-nav">
            <div onclick="nav('home')" id="nav-home" class="nav-item active"><i class="fa-solid fa-house"></i></div>
            <div onclick="nav('deposit')" id="nav-deposit" class="nav-item"><i class="fa-solid fa-wallet"></i></div>
            <div onclick="nav('withdraw')" id="nav-withdraw" class="nav-item"><i class="fa-solid fa-arrow-up-right-from-square"></i></div>
            <div onclick="alert('Support: @AdminSweetie')" class="nav-item"><i class="fa-solid fa-headset"></i></div>
        </nav>
    </div>

    <!-- PAYMENT MODAL -->
    <div id="pay-modal" class="fixed inset-0 bg-black/80 z-[9999] hidden flex items-center justify-center p-6 backdrop-blur-md">
        <div class="glass p-8 bg-white w-full max-w-sm animate__animated animate__zoomIn">
            <h3 id="gw-name" class="text-2xl font-black italic mb-2">...</h3>
            <div class="bg-indigo-50 p-4 rounded-2xl mb-6 flex justify-between items-center">
                <span id="gw-num" class="font-black text-indigo-600 text-lg tracking-wider">0000000000</span>
                <i class="fa-solid fa-copy text-indigo-300"></i>
            </div>
            <input type="number" id="pay-amt" placeholder="Amount ($)" class="w-full p-4 bg-slate-50 rounded-xl font-bold mb-3 outline-none">
            <input type="text" id="pay-tid" placeholder="Transaction ID (TID)" class="w-full p-4 bg-slate-50 rounded-xl font-bold mb-6 outline-none">
            <button onclick="submitProof()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs">Submit to Admin</button>
            <button onclick="closeGateway()" class="w-full mt-4 text-slate-400 text-[10px] font-black uppercase tracking-widest">Cancel</button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // CONFIG (Check your Firebase Console)
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

        let currentUser = null;
        let isAdmin = false;

        // --- AUTH & LOGIN ---
        window.startApp = async () => {
            const name = document.getElementById('user-name').value || "Miner_" + Math.floor(Math.random()*999);
            const res = await signInAnonymously(auth);
            const userRef = ref(db, `users/${res.user.uid}`);
            const snapshot = await get(userRef);
            
            if(!snapshot.exists()) {
                await set(userRef, { username: name, balance: 0, role: 'user', joined: Date.now() });
            }
            location.reload();
        };

        onAuthStateChanged(auth, async (u) => {
            if(u) {
                currentUser = u;
                onValue(ref(db, `users/${u.uid}`), snap => {
                    const data = snap.val();
                    document.getElementById('display-name').innerText = data.username;
                    document.getElementById('display-uid').innerText = `UID: ${u.uid.substring(0,8)}`;
                    document.getElementById('user-bal').innerText = `$${(data.balance || 0).toFixed(2)}`;
                    if(data.role === 'admin') {
                        isAdmin = true;
                        document.getElementById('admin-btn').classList.remove('hidden');
                        loadAdminStats();
                    }
                });
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
                initPlans();
                startFakeNotifs();
            }
        });

        // --- NAVIGATION ---
        window.nav = (pageId) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${pageId}`).classList.remove('hidden');
            if(document.getElementById(`nav-${pageId}`)) document.getElementById(`nav-${pageId}`).classList.add('active');
        };

        // --- MINING PLANS ---
        const plans = [
            { id: 1, name: "Nano Core", price: 10, daily: 0.8, days: 30 },
            { id: 2, name: "Mega Flux", price: 50, daily: 4.5, days: 30 },
            { id: 3, name: "Giga Node", price: 100, daily: 10, days: 30 },
            { id: 4, name: "Tera Master", price: 500, daily: 55, days: 30 }
        ];

        function initPlans() {
            const con = document.getElementById('plans-container');
            con.innerHTML = plans.map(p => `
                <div class="glass p-6 bg-white border-none shadow-sm relative overflow-hidden">
                    <div class="flex justify-between items-start mb-4">
                        <div>
                            <h4 class="font-black text-lg italic">${p.name}</h4>
                            <p class="text-[10px] font-bold text-indigo-600 uppercase tracking-tighter">Price: $${p.price}</p>
                        </div>
                        <div class="timer-badge text-[10px] font-black text-slate-400">29D : 23H</div>
                    </div>
                    <div class="grid grid-cols-2 gap-4 mb-4">
                        <div class="bg-slate-50 p-3 rounded-xl">
                            <p class="text-[8px] font-black uppercase text-slate-400">Daily Profit</p>
                            <p class="text-sm font-black text-green-500">$${p.daily}</p>
                        </div>
                        <div class="bg-slate-50 p-3 rounded-xl">
                            <p class="text-[8px] font-black uppercase text-slate-400">Total ROI</p>
                            <p class="text-sm font-black text-slate-800">$${p.daily * p.days}</p>
                        </div>
                    </div>
                    <button onclick="buyPlan(${p.id}, ${p.price})" class="w-full bg-slate-900 text-white py-3 rounded-xl text-[10px] font-black uppercase">Activate Node</button>
                </div>
            `).join('');
        }

        // --- DEPOSIT SYSTEM ---
        window.openGateway = (name, num) => {
            document.getElementById('gw-name').innerText = name;
            document.getElementById('gw-num').innerText = num;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closeGateway = () => document.getElementById('pay-modal').classList.add('hidden');

        window.submitProof = async () => {
            const amt = parseFloat(document.getElementById('pay-amt').value);
            const tid = document.getElementById('pay-tid').value;
            if(!amt || !tid) return alert("Sweetie, TID aur Amount bharein!");

            await push(ref(db, 'deposits'), {
                uid: currentUser.uid,
                username: document.getElementById('display-name').innerText,
                amount: amt,
                tid: tid,
                method: document.getElementById('gw-name').innerText,
                status: 'pending',
                time: Date.now()
            });
            alert("Sent! Admin will verify sweetie. 😘");
            closeGateway();
        };

        // --- ADMIN CORE ---
        window.showAdmin = () => nav('admin');
        
        function loadAdminStats() {
            // All Users List
            onValue(ref(db, 'users'), snap => {
                const con = document.getElementById('admin-user-list'); con.innerHTML = "";
                snap.forEach(child => {
                    const u = child.val();
                    con.innerHTML += `
                        <div class="glass p-4 bg-white border-none flex justify-between items-center shadow-sm">
                            <div><p class="font-black text-xs italic">${u.username}</p><p class="text-[9px] text-indigo-500 font-bold">$${u.balance.toFixed(2)}</p></div>
                            <button onclick="deleteUser('${child.key}')" class="text-red-300 text-xs"><i class="fa-solid fa-trash"></i></button>
                        </div>`;
                });
            });

            // Pending Deposits
            onValue(ref(db, 'deposits'), snap => {
                const con = document.getElementById('admin-dep-list'); con.innerHTML = "";
                snap.forEach(child => {
                    const d = child.val();
                    con.innerHTML += `
                        <div class="glass p-5 bg-white border-none shadow-md">
                            <div class="flex justify-between mb-3">
                                <span class="text-[10px] font-black uppercase text-indigo-600">${d.method}</span>
                                <span class="text-[10px] font-black text-slate-400">${new Date(d.time).toLocaleTimeString()}</span>
                            </div>
                            <p class="font-black text-sm mb-1">${d.username} sent <span class="text-green-500">$${d.amount}</span></p>
                            <p class="text-[10px] font-mono font-bold bg-slate-100 p-2 rounded-lg mb-4 select-all italic">TID: ${d.tid}</p>
                            <div class="flex gap-2">
                                <button onclick="approveDep('${child.key}', '${d.uid}', ${d.amount})" class="flex-1 bg-green-500 text-white py-2 rounded-lg font-black text-[10px] uppercase">Approve</button>
                                <button onclick="rejectDep('${child.key}')" class="flex-1 bg-red-100 text-red-500 py-2 rounded-lg font-black text-[10px] uppercase">Reject</button>
                            </div>
                        </div>`;
                });
            });
        }

        window.approveDep = async (key, uid, amt) => {
            const userRef = ref(db, `users/${uid}`);
            const snap = await get(userRef);
            await update(userRef, { balance: (snap.val().balance || 0) + amt });
            await remove(ref(db, `deposits/${key}`));
            alert("Approved! Balance added.");
        };
        window.rejectDep = async (key) => { await remove(ref(db, `deposits/${key}`)); alert("Deposit Rejected!"); };

        // --- FAKE NOTIFICATIONS ---
        function startFakeNotifs() {
            const names = ["Zeeshan", "Ayesha", "John", "Kashif", "Sara", "Ali", "Fatima", "Rohan", "Priya", "Vikram"];
            const amounts = [10, 50, 100, 25, 500, 12, 80, 200, 45, 30];
            
            setInterval(() => {
                const n = names[Math.floor(Math.random()*names.length)];
                const a = amounts[Math.floor(Math.random()*amounts.length)];
                const type = Math.random() > 0.5 ? "Withdrew" : "Deposited";
                const color = type === "Withdrew" ? "text-red-500" : "text-green-500";
                
                const div = document.createElement('div');
                div.className = "glass p-4 bg-white/90 shadow-2xl mb-2 flex items-center gap-3 animate__animated animate__slideInDown";
                div.innerHTML = `<div class="w-8 h-8 bg-indigo-600 rounded-full flex items-center justify-center text-white text-[10px]"><i class="fa-solid fa-user"></i></div>
                                <div><p class="text-[10px] font-black">${n} just ${type} <span class="${color}">$${a}.00</span></p></div>`;
                
                document.getElementById('notif-container').appendChild(div);
                setTimeout(() => { div.classList.replace('animate__slideInDown', 'animate__fadeOutUp'); setTimeout(() => div.remove(), 500); }, 3000);
            }, 8000);
        }

        // --- ADMIN TRIGGER ---
        let taps = 0;
        window.adminTap = () => {
            taps++;
            if(taps === 5) {
                const pass = prompt("Admin Key?");
                if(pass === "786786") {
                    update(ref(db, `users/${currentUser.uid}`), { role: 'admin' });
                    alert("Admin Privileges Granted! 👑");
                    location.reload();
                }
                taps = 0;
            }
        };

    </script>
</body>
</html>
