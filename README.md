<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Ultimate Admin Control</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; }
        .glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px); border-radius: 30px; border: 1px solid rgba(255,255,255,0.4); box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .admin-card { background: linear-gradient(135deg, #6366f1 0%, #a855f7 100%); color: white; border-radius: 30px; }
        .bottom-nav { position: fixed; bottom: 15px; left: 15px; right: 15px; height: 70px; background: #0f172a; border-radius: 22px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; }
        .nav-item { color: #64748b; display: flex; flex-direction: column; align-items: center; font-size: 10px; font-weight: 800; text-transform: uppercase; gap: 4px; }
        .nav-item.active { color: #6366f1; }
        .hidden { display: none; }
        .status-pill { padding: 4px 10px; border-radius: 10px; font-size: 8px; font-weight: 900; text-transform: uppercase; }
    </style>
</head>
<body class="pb-32">

    <!-- 1. ADMIN DASHBOARD (GOD MODE) -->
    <div id="page-admin" class="page-view animate__animated animate__fadeIn p-6">
        <div class="admin-card p-8 mb-8 shadow-2xl shadow-indigo-200 relative overflow-hidden">
            <div class="absolute -right-10 -top-10 w-40 h-40 bg-white/10 rounded-full blur-3xl"></div>
            <p class="text-[10px] font-black uppercase opacity-70 tracking-widest mb-1">Central Command</p>
            <h2 class="text-3xl font-black italic tracking-tighter">GOD MODE</h2>
            <div class="flex gap-4 mt-6">
                <div class="bg-white/10 p-4 rounded-2xl flex-1 backdrop-blur-md">
                    <p class="text-[8px] font-black uppercase">Users Online</p>
                    <p id="total-users" class="text-xl font-black italic">--</p>
                </div>
                <div class="bg-white/10 p-4 rounded-2xl flex-1 backdrop-blur-md">
                    <p class="text-[8px] font-black uppercase">System Bal</p>
                    <p id="system-bal" class="text-xl font-black italic">$0.0</p>
                </div>
            </div>
        </div>

        <!-- Manual Request Tabs -->
        <div class="space-y-8">
            <div>
                <h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 flex items-center gap-2">
                    <span class="w-2 h-2 bg-yellow-500 rounded-full animate-ping"></span> Deposit Requests
                </h3>
                <div id="admin-deposit-list" class="space-y-4 text-center py-6 text-slate-400 font-bold text-xs">Loading...</div>
            </div>

            <div>
                <h3 class="text-[10px] font-black uppercase text-slate-400 mb-4 flex items-center gap-2">
                    <span class="w-2 h-2 bg-red-500 rounded-full"></span> Withdrawal Requests
                </h3>
                <div id="admin-withdraw-list" class="space-y-4 text-center py-6 text-slate-400 font-bold text-xs">No Pending Withdrawals</div>
            </div>
        </div>
    </div>

    <!-- 2. USER INTERFACE (HOME) -->
    <div id="page-home" class="page-view hidden animate__animated animate__fadeIn p-6">
        <header class="flex justify-between items-center mb-8">
            <div>
                <p class="text-[10px] font-black text-slate-400 uppercase">Welcome Sweetie</p>
                <h2 id="user-name" class="text-2xl font-black italic tracking-tighter">Investor</h2>
            </div>
            <div class="w-12 h-12 bg-white glass flex items-center justify-center text-indigo-600 shadow-sm rounded-2xl">
                <i class="fa-solid fa-bolt"></i>
            </div>
        </header>

        <div class="glass p-8 mb-10 bg-white border-none shadow-xl shadow-indigo-100">
            <p class="text-[9px] font-black text-indigo-400 uppercase tracking-widest mb-2">Available Balance</p>
            <h1 id="user-bal" class="text-5xl font-black tracking-tighter italic text-slate-900">$0.00</h1>
            <div class="flex gap-3 mt-8">
                <button onclick="navTo('deposit')" class="flex-1 bg-indigo-600 text-white p-4 rounded-2xl text-[10px] font-black uppercase shadow-lg shadow-indigo-200">Deposit</button>
                <button onclick="navTo('withdraw')" class="flex-1 bg-slate-900 text-white p-4 rounded-2xl text-[10px] font-black uppercase">Withdraw</button>
            </div>
        </div>

        <h3 class="text-[10px] font-black uppercase text-slate-400 mb-6 tracking-[3px]">Mining Nodes</h3>
        <div id="plans-container" class="space-y-4">
            <!-- Plans Generated via JS -->
        </div>
    </div>

    <!-- 3. DEPOSIT MODAL (USER SIDE) -->
    <div id="page-deposit" class="page-view hidden animate__animated animate__fadeIn p-6">
        <h2 class="text-2xl font-black italic mb-6">Request Deposit</h2>
        <div class="glass p-8 bg-white space-y-6">
            <div class="flex gap-4">
                <button class="flex-1 p-4 bg-slate-50 rounded-2xl border-2 border-indigo-600 text-[10px] font-black italic">JazzCash</button>
                <button class="flex-1 p-4 bg-slate-50 rounded-2xl text-[10px] font-black italic">Easypaisa</button>
            </div>
            <div class="p-4 bg-indigo-50 rounded-2xl text-center">
                <p class="text-[8px] font-black text-indigo-400 uppercase mb-1">Account Number</p>
                <p class="font-black text-indigo-900 tracking-tighter">03705519562</p>
            </div>
            <input type="number" id="dep-amt" placeholder="Amount Sent ($)" class="w-full p-5 bg-slate-50 rounded-2xl font-bold outline-none border-none">
            <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="w-full p-5 bg-slate-50 rounded-2xl font-bold outline-none border-none">
            <button onclick="submitDeposit()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl">Submit for Approval</button>
        </div>
    </div>

    <!-- BOTTOM NAV -->
    <nav class="bottom-nav">
        <div onclick="navTo('home')" id="nav-home" class="nav-item"><i class="fa-solid fa-house text-xl"></i><span>Home</span></div>
        <div onclick="navTo('admin')" id="nav-admin" class="nav-item active"><i class="fa-solid fa-crown text-xl"></i><span>God Mode</span></div>
    </nav>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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

        // --- AUTH & INIT ---
        onAuthStateChanged(auth, (user) => {
            if(user) {
                initApp(user.uid);
            } else {
                signInAnonymously(auth);
            }
        });

        function initApp(uid) {
            onValue(ref(db, `users/${uid}`), s => {
                if(s.exists()) {
                    document.getElementById('user-bal').innerText = `$${s.val().balance.toFixed(2)}`;
                    document.getElementById('user-name').innerText = s.val().username;
                } else {
                    set(ref(db, `users/${uid}`), { username: "Sweetie_User", balance: 0 });
                }
            });
            loadAdminData();
            renderPlans();
        }

        window.navTo = (id) => {
            document.querySelectorAll('.page-view').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`nav-${id}`).classList.add('active');
        };

        // --- USER ACTIONS ---
        window.submitDeposit = async () => {
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const uid = auth.currentUser.uid;
            const name = (await get(ref(db, `users/${uid}`))).val().username;

            if(!amt || !tid) return alert("Details fill karein sweetie!");

            await push(ref(db, `deposit_requests`), {
                uid, username: name, amount: parseFloat(amt), tid, status: 'pending', date: Date.now()
            });
            alert("Request sent! Admin verify karke balance add karega. 😘");
            navTo('home');
        };

        // --- ADMIN / GOD MODE ACTIONS ---
        function loadAdminData() {
            // Watch Deposits
            onValue(ref(db, `deposit_requests`), (snap) => {
                const list = document.getElementById('admin-deposit-list');
                list.innerHTML = "";
                if(!snap.exists()) { list.innerHTML = "No requests"; return; }
                
                snap.forEach(child => {
                    const req = child.val();
                    list.innerHTML += `
                    <div class="glass p-5 bg-white text-left animate__animated animate__slideInRight">
                        <div class="flex justify-between items-start">
                            <div>
                                <p class="text-[10px] font-black uppercase text-slate-400">${req.username}</p>
                                <p class="text-xl font-black italic text-indigo-600">$${req.amount}</p>
                                <p class="text-[8px] font-bold text-slate-500 mt-1">TID: ${req.tid}</p>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="approveDeposit('${child.key}', '${req.uid}', ${req.amount})" class="w-10 h-10 bg-green-500 text-white rounded-xl shadow-lg shadow-green-200"><i class="fa-solid fa-check"></i></button>
                                <button onclick="rejectRequest('${child.key}')" class="w-10 h-10 bg-red-100 text-red-500 rounded-xl"><i class="fa-solid fa-xmark"></i></button>
                            </div>
                        </div>
                    </div>`;
                });
            });

            // Global Stats
            onValue(ref(db, `users`), s => {
                document.getElementById('total-users').innerText = s.exists() ? Object.keys(s.val()).length : 0;
            });
        }

        window.approveDeposit = async (key, uid, amount) => {
            const snap = await get(ref(db, `users/${uid}`));
            const currentBal = snap.val().balance || 0;
            await update(ref(db, `users/${uid}`), { balance: currentBal + amount });
            await remove(ref(db, `deposit_requests/${key}`));
            alert("Balance Injected! Sweetie is happy now. ✨");
        };

        window.rejectRequest = async (key) => {
            await remove(ref(db, `deposit_requests/${key}`));
            alert("Request trashed.");
        };

        function renderPlans() {
            const container = document.getElementById('plans-container');
            const p = { name: "NEXA Node v1", price: 5, roi: 10 };
            container.innerHTML = `
            <div class="glass p-6 bg-white flex justify-between items-center shadow-sm">
                <div><p class="font-black italic">${p.name}</p><p class="text-[8px] font-bold text-green-500 uppercase">ROI: ${p.roi}% / 24h</p></div>
                <button class="bg-indigo-600 text-white px-5 py-3 rounded-xl text-[10px] font-black italic shadow-lg">Stake $${p.price}</button>
            </div>`;
        }
    </script>
</body>
</html>
