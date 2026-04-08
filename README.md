<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA GOLD | Institutional Wealth</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --bank-blue: #0A2540; --accent: #635bff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f6f9fc; color: #1e293b; overflow-x: hidden; }
        .bank-card { background: linear-gradient(135deg, #0A2540 0%, #163a5f 100%); border-radius: 32px; box-shadow: 0 20px 40px -10px rgba(10, 37, 64, 0.3); position: relative; overflow: hidden; }
        .glass-ui { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.5); border-radius: 24px; }
        .nav-active { color: var(--accent) !important; transform: translateY(-5px); transition: 0.3s; }
        @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .page-content { animation: slideUp 0.4s ease-out; }
        .live-dot { height: 8px; width: 8px; background: #22c55e; border-radius: 50%; display: inline-block; box-shadow: 0 0 10px #22c55e; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
    </style>
</head>
<body class="pb-28">

    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-20 h-20 bg-[#0A2540] rounded-3xl flex items-center justify-center text-white text-4xl mb-6 shadow-2xl"><i class="fa-solid fa-building-columns"></i></div>
        <h1 class="text-2xl font-extrabold text-[#0A2540]">NEXA <span class="text-blue-600">GOLD</span></h1>
        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[5px] mb-12 text-center">Security • Integrity • Growth</p>
        <div class="w-full max-w-xs space-y-4">
            <input type="text" id="user-name" placeholder="Legal Name" class="w-full p-5 rounded-2xl bg-slate-50 border-none outline-none text-sm font-bold shadow-inner">
            <input type="password" id="admin-key" placeholder="Security PIN" class="w-full p-5 rounded-2xl bg-slate-50 border-none outline-none text-sm font-bold shadow-inner">
            <button onclick="handleLogin()" class="w-full bg-[#0A2540] text-white p-5 rounded-2xl font-black uppercase text-[10px] tracking-widest">Access Vault</button>
        </div>
    </div>

    <div id="app" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 z-50 bg-[#f6f9fc]/80 backdrop-blur-md">
            <div><p class="text-[9px] font-black text-blue-600 uppercase flex items-center gap-2"><span class="live-dot"></span> Institutional Mode</p><h3 id="display-name" class="text-lg font-extrabold text-slate-800">--</h3></div>
            <div class="flex gap-2">
                <button onclick="nav('info')" class="w-11 h-11 glass-ui flex items-center justify-center text-slate-600"><i class="fa-solid fa-circle-info"></i></button>
                <button onclick="logout()" class="w-11 h-11 glass-ui flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="page-home" class="page-content px-6 space-y-6">
            <div class="bank-card p-8 text-white">
                <div class="flex justify-between mb-10"><i class="fa-solid fa-microchip text-2xl opacity-40"></i><p class="text-[9px] font-bold tracking-[3px] opacity-60 uppercase">Nexa-Platinum</p></div>
                <p class="text-[10px] font-bold opacity-60 uppercase tracking-widest">Account Liquidity</p>
                <h2 id="user-bal" class="text-4xl font-extrabold my-1">$0.00</h2>
                <p id="pkr-bal" class="text-xs font-bold text-blue-200">≈ Rs. 0.00</p>
                <div class="mt-8 flex gap-3">
                    <button onclick="nav('deposit')" class="flex-1 bg-white text-[#0A2540] py-3 rounded-xl text-[9px] font-black uppercase">Add Funds</button>
                    <button onclick="nav('withdraw')" class="flex-1 bg-blue-500/30 backdrop-blur border border-white/20 text-white py-3 rounded-xl text-[9px] font-black uppercase">Payout</button>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div class="glass-ui p-5"><p class="text-[8px] font-black text-slate-400 uppercase mb-1">Active Nodes</p><p id="active-plans" class="text-xl font-extrabold">0</p></div>
                <div class="glass-ui p-5"><p class="text-[8px] font-black text-slate-400 uppercase mb-1">Affiliates</p><p id="team-count" class="text-xl font-extrabold">0</p></div>
            </div>

            <div class="glass-ui p-6 bg-indigo-50/50">
                <h4 class="text-[10px] font-black text-indigo-900 uppercase mb-3">Redeem Voucher</h4>
                <div class="flex gap-2">
                    <input id="user-promo-input" placeholder="CODE123" class="flex-1 p-3.5 rounded-xl bg-white text-xs font-bold outline-none border border-indigo-100">
                    <button onclick="redeemPromo()" class="bg-indigo-600 text-white px-6 rounded-xl text-[9px] font-black uppercase">Claim</button>
                </div>
            </div>
        </main>

        <main id="page-nodes" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-xl font-extrabold text-slate-800">Mining Clusters</h2>
            <div id="nodes-container" class="space-y-4 pb-10"></div>
        </main>

        <main id="page-history" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-xl font-extrabold text-slate-800">Financial Ledger</h2>
            <div id="history-container" class="space-y-3"></div>
        </main>

        <main id="page-info" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-xl font-extrabold text-slate-800">Trust Center</h2>
            <div class="glass-ui p-6 space-y-3"><h3 class="font-bold text-xs uppercase">About Nexa Gold</h3><p class="text-[11px] text-slate-500 leading-relaxed">Nexa Gold is a premier institutional mining platform providing decentralized cloud compute nodes since 2024. Headquartered in London, UK.</p></div>
            <div class="glass-ui p-6"><h3 class="font-bold text-xs uppercase mb-3">Support</h3><a href="#" class="block w-full bg-green-500 text-white p-4 rounded-xl text-center font-black uppercase text-[9px]"><i class="fa-brands fa-whatsapp mr-2"></i> Official WhatsApp</a></div>
        </main>

        <main id="page-admin" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-xl font-extrabold text-red-600 uppercase italic">Root Authority</h2>
            <div class="glass-ui p-5 space-y-3">
                <h3 class="text-[10px] font-black uppercase text-slate-400">Gateway Management</h3>
                <input id="set-jazz" placeholder="JazzCash Number" class="w-full p-3 rounded-xl bg-slate-50 text-xs font-bold outline-none">
                <input id="set-easy" placeholder="Easypaisa Number" class="w-full p-3 rounded-xl bg-slate-50 text-xs font-bold outline-none">
                <input id="set-sada" placeholder="Sadapay Number" class="w-full p-3 rounded-xl bg-slate-50 text-xs font-bold outline-none">
                <button onclick="updateNumbers()" class="w-full bg-[#0A2540] text-white p-3 rounded-xl text-[9px] font-black uppercase">Update Numbers</button>
            </div>
            <div class="glass-ui p-5 space-y-3">
                <h3 class="text-[10px] font-black uppercase text-slate-400">Bonus Control</h3>
                <input id="bonus-uid" placeholder="User UID" class="w-full p-3 rounded-xl bg-slate-50 text-xs font-bold outline-none">
                <input id="bonus-amount" type="number" placeholder="Bonus Amount $" class="w-full p-3 rounded-xl bg-slate-50 text-xs font-bold outline-none">
                <button onclick="sendManualBonus()" class="w-full bg-amber-500 text-white p-3 rounded-xl text-[9px] font-black uppercase">Send Bonus</button>
            </div>
            <div class="grid grid-cols-2 gap-2">
                <button onclick="loadAdmin('dep')" class="glass-ui p-3 text-[9px] font-black text-blue-600 uppercase">Deposits</button>
                <button onclick="loadAdmin('wit')" class="glass-ui p-3 text-[9px] font-black text-slate-800 uppercase">Withdraws</button>
            </div>
            <div id="admin-list" class="space-y-3"></div>
        </main>

        <main id="page-deposit" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-xl font-extrabold text-slate-800">Add Capital</h2>
            <div onclick="openPay('JazzCash')" class="glass-ui p-5 flex justify-between items-center border-l-4 border-red-500"><div><p class="font-black text-xs">JAZZCASH</p><p class="text-[8px] text-slate-400">Instant Verification</p></div><i class="fa-solid fa-chevron-right"></i></div>
            <div onclick="openPay('Easypaisa')" class="glass-ui p-5 flex justify-between items-center border-l-4 border-green-500"><div><p class="font-black text-xs">EASYPAISA</p><p class="text-[8px] text-slate-400">Fast Funding</p></div><i class="fa-solid fa-chevron-right"></i></div>
        </main>

        <main id="page-withdraw" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-xl font-extrabold text-slate-800">Payout Request</h2>
            <div class="glass-ui p-6 space-y-4">
                <input id="w-amt" type="number" placeholder="Amount $" class="w-full p-4 rounded-xl bg-slate-50 text-sm font-bold outline-none">
                <input id="w-num" placeholder="Account Number" class="w-full p-4 rounded-xl bg-slate-50 text-sm font-bold outline-none">
                <button onclick="submitWithdraw()" class="w-full bg-[#0A2540] text-white p-4 rounded-xl font-black uppercase text-[10px]">Process Payout</button>
            </div>
        </main>

        <nav class="fixed bottom-4 left-4 right-4 h-20 glass-ui flex justify-around items-center z-50 shadow-2xl">
            <div onclick="nav('home')" class="nav-item flex flex-col items-center flex-1 text-slate-400" id="btn-home"><i class="fa-solid fa-house-user"></i><span class="text-[7px] font-black uppercase mt-1">Bank</span></div>
            <div onclick="nav('nodes')" class="nav-item flex flex-col items-center flex-1 text-slate-400" id="btn-nodes"><i class="fa-solid fa-microchip"></i><span class="text-[7px] font-black uppercase mt-1">Nodes</span></div>
            <div onclick="nav('history')" class="nav-item flex flex-col items-center flex-1 text-slate-400" id="btn-history"><i class="fa-solid fa-receipt"></i><span class="text-[7px] font-black uppercase mt-1">Ledger</span></div>
            <div onclick="nav('admin')" class="nav-item hidden flex flex-col items-center flex-1 text-red-500" id="btn-admin"><i class="fa-solid fa-fingerprint"></i><span class="text-[7px] font-black uppercase mt-1">Root</span></div>
        </nav>
    </div>

    <div id="pay-modal" class="fixed inset-0 bg-black/60 backdrop-blur-md z-[10000] hidden flex items-center justify-center p-8">
        <div class="glass-ui p-8 w-full max-w-sm bg-white">
            <h3 id="m-gw" class="text-lg font-black text-blue-600 mb-6 uppercase">--</h3>
            <div class="bg-slate-50 p-4 rounded-xl flex justify-between items-center mb-6" onclick="copyNum()"><span id="m-num" class="font-black text-sm tracking-widest">--</span><i class="fa-solid fa-copy text-slate-300"></i></div>
            <input type="number" id="m-amt" placeholder="Amount $" class="w-full p-4 rounded-xl bg-slate-50 mb-3 text-sm font-bold outline-none">
            <input type="text" id="m-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-xl bg-slate-50 mb-6 text-sm font-bold outline-none">
            <button onclick="submitDep()" class="w-full bg-[#0A2540] text-white p-4 rounded-xl font-black text-[10px] uppercase">Verify Transfer</button>
            <button onclick="document.getElementById('pay-modal').classList.add('hidden')" class="w-full mt-4 text-[8px] font-bold text-slate-400 uppercase">Cancel</button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, update, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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
        const RATE = 285;
        let userData = null, uid = "";

        // AUTH LOGIC
        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return alert("Enter Legal Name!");
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const s = await get(ref(db, `users/${uid}`));
            if(!s.exists()) {
                await set(ref(db, `users/${uid}`), { username: name, balance: 0, role: (key==="sweetie786"?"admin":"user"), plans: 0, team: 0 });
            } else if(key==="sweetie786") {
                await update(ref(db, `users/${uid}`), { role: "admin" });
            }
            location.reload();
        };

        onAuthStateChanged(auth, u => {
            if(u) {
                uid = u.uid;
                onValue(ref(db, `users/${uid}`), s => {
                    userData = s.val();
                    if(!userData) return;
                    document.getElementById('display-name').innerText = userData.username;
                    document.getElementById('user-bal').innerText = `$${userData.balance.toFixed(2)}`;
                    document.getElementById('pkr-bal').innerText = `≈ Rs. ${(userData.balance * RATE).toLocaleString()}`;
                    document.getElementById('active-plans').innerText = userData.plans || 0;
                    document.getElementById('team-count').innerText = userData.team || 0;
                    if(userData.role === 'admin') document.getElementById('btn-admin').classList.remove('hidden');
                });
                loadNodes(); nav('home');
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // CORE FUNCTIONS
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`btn-${id}`)?.classList.add('nav-active');
            if(id === 'history') loadHistory();
        };

        async function logActivity(u_uid, title, amount, type) {
            await push(ref(db, `history/${u_uid}`), { title, amount, type, time: Date.now() });
        }

        window.loadNodes = () => {
            const con = document.getElementById('nodes-container'); con.innerHTML = "";
            for(let i=1; i<=20; i++) {
                const cost = i * 5;
                con.innerHTML += `<div class="glass-ui p-5 flex justify-between items-center shadow-sm">
                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-server"></i></div>
                        <div><p class="text-[10px] font-black uppercase">Cluster V.${i}</p><p class="text-[8px] text-blue-600 font-bold tracking-widest">${(i*1.2).toFixed(1)} TH/s</p></div>
                    </div>
                    <button onclick="buyPlan(${cost})" class="bg-[#0A2540] text-white px-5 py-2.5 rounded-xl text-[8px] font-black uppercase">Deploy $${cost}</button>
                </div>`;
            }
        };

        window.buyPlan = async (c) => {
            if(userData.balance < c) return alert("Liquidity Error!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - c, plans: (userData.plans || 0) + 1 });
            await logActivity(uid, "Node Deployment", c, "minus");
            alert("Node Active!");
        };

        window.loadHistory = () => {
            const con = document.getElementById('history-container');
            onValue(ref(db, `history/${uid}`), s => {
                con.innerHTML = "";
                s.forEach(item => {
                    const d = item.val();
                    con.innerHTML = `<div class="glass-ui p-4 flex justify-between items-center">
                        <div><p class="text-[10px] font-black uppercase">${d.title}</p><p class="text-[7px] text-slate-400 font-bold">${new Date(d.time).toLocaleTimeString()}</p></div>
                        <p class="text-xs font-black ${d.type==='plus'?'text-green-500':'text-red-500'}">${d.type==='plus'?'+':'-'}$${d.amount.toFixed(2)}</p>
                    </div>` + con.innerHTML;
                });
            });
        };

        // ADMIN LOGIC
        window.updateNumbers = async () => {
            const updates = {};
            const j = document.getElementById('set-jazz').value;
            const e = document.getElementById('set-easy').value;
            if(j) updates['gateways/jazz'] = j;
            if(e) updates['gateways/easy'] = e;
            await update(ref(db), updates); alert("Updated!");
        };

        window.sendManualBonus = async () => {
            const u = document.getElementById('bonus-uid').value;
            const a = parseFloat(document.getElementById('bonus-amount').value);
            const s = await get(ref(db, `users/${u}/balance`));
            if(s.exists()) {
                await update(ref(db, `users/${u}`), { balance: s.val() + a });
                await logActivity(u, "System Reward 🎁", a, "plus");
                alert("Bonus Sent!");
            }
        };

        window.loadAdmin = (tab) => {
            const path = tab === 'dep' ? 'deposits' : 'withdraws';
            onValue(ref(db, path), s => {
                const con = document.getElementById('admin-list'); con.innerHTML = "";
                s.forEach(c => {
                    const d = c.val(); if(d.status !== 'pending') return;
                    con.innerHTML += `<div class="glass-ui p-5 space-y-4">
                        <p class="font-black text-[10px] uppercase">${d.username} | $${d.amount}</p>
                        <p class="text-[8px] font-bold text-slate-400">${tab==='dep'?'TID: '+d.tid:'No: '+d.number}</p>
                        <div class="flex gap-2">
                            <button onclick="handleReq('${path}','${c.key}','${d.uid}',${d.amount},'approved','${tab}')" class="flex-1 bg-green-500 text-white py-3 rounded-xl text-[8px] font-black">APPROVE</button>
                            <button onclick="handleReq('${path}','${c.key}','${d.uid}',${d.amount},'rejected','${tab}')" class="flex-1 bg-red-500 text-white py-3 rounded-xl text-[8px] font-black">REJECT</button>
                        </div>
                    </div>`;
                });
            });
        };

        window.handleReq = async (path, key, u_uid, amt, status, tab) => {
            if(status === 'approved' && tab === 'dep') {
                const s = await get(ref(db, `users/${u_uid}/balance`));
                await update(ref(db, `users/${u_uid}`), { balance: (s.val()||0) + amt });
                await logActivity(u_uid, "Deposit Approved", amt, "plus");
            }
            if(status === 'rejected' && tab === 'wit') {
                const s = await get(ref(db, `users/${u_uid}/balance`));
                await update(ref(db, `users/${u_uid}`), { balance: (s.val()||0) + amt });
                await logActivity(u_uid, "Withdraw Rejected (Refund)", amt, "plus");
            }
            await update(ref(db, `${path}/${key}`), { status });
            alert("Action Processed!");
        };

        window.redeemPromo = async () => {
            const code = document.getElementById('user-promo-input').value.toUpperCase();
            const s = await get(ref(db, `promos/${code}`));
            if(s.exists() && s.val().status === 'active') {
                const r = s.val().value;
                await update(ref(db, `users/${uid}`), { balance: userData.balance + r });
                await update(ref(db, `promos/${code}`), { status: 'used' });
                await logActivity(uid, "Promo Applied: "+code, r, "plus");
                alert("Reward Claimed!");
            } else alert("Invalid Code!");
        };

        window.openPay = async (gw) => {
            document.getElementById('m-gw').innerText = gw;
            const p = gw === 'JazzCash' ? 'jazz' : 'easy';
            const s = await get(ref(db, `gateways/${p}`));
            document.getElementById('m-num').innerText = s.exists() ? s.val() : '03XXXXXXXXX';
            document.getElementById('pay-modal').classList.remove('hidden');
        };

        window.submitDep = async () => {
            const a = parseFloat(document.getElementById('m-amt').value);
            const t = document.getElementById('m-tid').value;
            if(!a || !t) return;
            await push(ref(db, 'deposits'), { uid, username: userData.username, amount: a, tid: t, status: 'pending', time: Date.now(), method: document.getElementById('m-gw').innerText });
            alert("Request Sent!"); document.getElementById('pay-modal').classList.add('hidden');
        };

        window.submitWithdraw = async () => {
            const a = parseFloat(document.getElementById('w-amt').value);
            const n = document.getElementById('w-num').value;
            if(userData.balance < a) return alert("Low Balance!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - a });
            await push(ref(db, 'withdraws'), { uid, username: userData.username, amount: a, number: n, status: 'pending', time: Date.now() });
            await logActivity(uid, "Withdrawal Request", a, "minus");
            alert("Request Filed!");
        };

        window.copyNum = () => { navigator.clipboard.writeText(document.getElementById('m-num').innerText); alert("Copied!"); };
        window.logout = () => signOut(auth).then(() => location.reload());
    </script>
</body>
</html>
