<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ULTIMATE | Verified Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --bg: #f8fafc; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; overflow-x: hidden; }
        .nexa-card { background: white; border: 1px solid #f1f5f9; border-radius: 28px; box-shadow: 0 10px 25px -5px rgba(0,0,0,0.02); }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #7C3AED); color: white; font-weight: 800; border-radius: 18px; transition: 0.3s; }
        .nav-icon { font-size: 20px; color: #cbd5e1; cursor: pointer; transition: 0.4s; }
        .active-tab { color: #2563EB !important; transform: translateY(-5px); }
        .hidden { display: none !important; }
        input { background: #f1f5f9 !important; border: 1px solid #e2e8f0 !important; border-radius: 16px; padding: 14px; font-weight: 700; width: 100%; outline: none; }
        .status-pill { padding: 4px 10px; border-radius: 10px; font-size: 9px; font-weight: 900; text-transform: uppercase; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
    </style>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        let uData = null;

        window.initAuth = async () => {
            const user = document.getElementById('u-field').value.trim();
            if(!user) return alert("Enter Terminal Name Sweetie! 💋");
            const uid = btoa(user.toLowerCase()).replace(/=/g, ""); 
            const uRef = ref(db, 'users/' + uid);
            const snap = await get(uRef);
            if(!snap.exists()) {
                await set(uRef, { username: user, balance: 0.0, pkr: 0, uid: uid, role: user.toLowerCase() === 'admin' ? 'admin' : 'user' });
            }
            localStorage.setItem('nexa_session', uid);
            location.reload();
        };

        window.onload = () => {
            const session = localStorage.getItem('nexa_session');
            if(session) {
                document.getElementById('auth-gate').classList.add('hidden');
                document.getElementById('main-ui').classList.remove('hidden');
                syncSession(session);
                renderNodes();
            }
        };

        function syncSession(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                uData = s.val();
                document.getElementById('nav-username').innerText = uData.username;
                document.getElementById('top-usd').innerText = "$" + (uData.balance || 0).toFixed(2);
                document.getElementById('top-pkr').innerText = "Rs. " + (uData.pkr || 0);
                if(uData.role === 'admin') {
                    document.getElementById('admin-trigger').classList.remove('hidden');
                    syncAdminHub();
                }
                loadHistory();
            });
        }

        window.renderNodes = () => {
            const box = document.getElementById('nodes-list');
            for(let i=1; i<=15; i++) {
                box.innerHTML += `<div class="nexa-card p-5 mb-4 border-l-4 border-blue-500 flex justify-between items-center">
                    <div><h4 class="text-xs font-black uppercase tracking-tighter">Nexa Core Node v.${i}</h4><p class="text-[9px] text-slate-400">Daily: $${(i*0.8).toFixed(2)}</p></div>
                    <div class="text-right"><p class="text-sm font-black text-blue-600">$${i*10}</p><button onclick="switchTab('wallet')" class="text-[8px] font-black uppercase text-slate-400">Deploy</button></div>
                </div>`;
            }
        };

        window.requestDeposit = () => {
            const amt = prompt("Enter Amount to Deposit (PKR):");
            const tid = prompt("Send to 03705519562 (EasyPaisa)\nEnter 11-Digit Transaction ID:");
            if(amt && tid) {
                push(ref(db, 'requests/deposits'), { uid: uData.uid, name: uData.username, amount: amt, tid: tid, status: 'pending', date: new Date().toLocaleDateString() });
                alert("Deposit Request Logged! Waiting for Admin verification sweetie. 💋");
            }
        };

        window.requestWithdraw = () => {
            const amt = prompt("Enter Withdrawal Amount (PKR):");
            const num = prompt("Your JazzCash/EasyPaisa Number:");
            if(amt && num) {
                if(uData.pkr < amt) return alert("Insufficient Balance!");
                push(ref(db, 'requests/withdraws'), { uid: uData.uid, name: uData.username, amount: amt, method: num, status: 'pending', date: new Date().toLocaleDateString() });
                alert("Withdrawal Request Sent! 💋");
            }
        };

        function loadHistory() {
            onValue(ref(db, 'requests/deposits'), (s) => {
                const box = document.getElementById('hist-box');
                box.innerHTML = "";
                const data = s.val();
                for(let k in data) {
                    if(data[k].uid === uData.uid) {
                        box.innerHTML += `<div class="nexa-card p-3 mb-2 flex justify-between items-center bg-slate-50/50">
                            <div><p class="text-[10px] font-black uppercase text-slate-600">Deposit</p><p class="text-[8px] text-slate-400">${data[k].date}</p></div>
                            <div class="text-right"><p class="text-[10px] font-bold">Rs. ${data[k].amount}</p><span class="status-pill ${data[k].status === 'pending' ? 'bg-amber-100 text-amber-600' : 'bg-green-100 text-green-600'}">${data[k].status}</span></div>
                        </div>`;
                    }
                }
            });
        }

        // --- ADMIN HUB ---
        function syncAdminHub() {
            onValue(ref(db, 'requests/deposits'), (s) => {
                const box = document.getElementById('admin-req-list');
                box.innerHTML = "";
                const data = s.val();
                for(let k in data) {
                    if(data[k].status === 'pending') {
                        box.innerHTML += `<div class="nexa-card p-4 mb-3 border-l-4 border-red-500 flex justify-between items-center">
                            <div><p class="text-[10px] font-black uppercase">${data[k].name}</p><p class="text-[9px] text-slate-500">Rs.${data[k].amount} | TID: ${data[k].tid}</p></div>
                            <button onclick="approveDeposit('${k}', '${data[k].uid}', ${data[k].amount})" class="btn-grad px-4 py-2 text-[9px]">APPROVE</button>
                        </div>`;
                    }
                }
            });
        }

        window.approveDeposit = async (rid, uid, amt) => {
            const uRef = ref(db, `users/${uid}`);
            const snap = await get(uRef);
            const current = snap.val().pkr || 0;
            await update(uRef, { pkr: current + parseInt(amt) });
            await update(ref(db, `requests/deposits/${rid}`), { status: 'approved' });
            alert("Funds Released! 💋");
        };

        window.switchTab = (t) => {
            ['home', 'mine', 'wallet', 'admin'].forEach(id => document.getElementById('sec-'+id).classList.add('hidden'));
            document.getElementById('sec-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(n => n.classList.remove('active-tab'));
            event.currentTarget.classList.add('active-tab');
        };

        window.logoutTerminal = () => { localStorage.clear(); location.reload(); };
    </script>
</head>
<body class="pb-28">

    <!-- Auth Gate -->
    <div id="auth-gate" class="fixed inset-0 bg-white z-[9999] flex flex-col justify-center p-10">
        <div class="text-center mb-10"><i class="fa-solid fa-gem text-blue-600 text-6xl mb-4"></i><h1 class="text-3xl font-black italic tracking-tighter text-slate-800">NEXA COMMAND</h1><p class="text-[9px] font-bold text-slate-400 uppercase tracking-[3px] mt-1">Lightweight Terminal</p></div>
        <input id="u-field" type="text" placeholder="Access Identity" class="mb-4 text-center text-lg">
        <button onclick="initAuth()" class="w-full btn-grad py-5 text-xs uppercase tracking-widest shadow-xl">Start Session</button>
    </div>

    <!-- Main UI -->
    <div id="main-ui" class="hidden">
        <header class="p-6 sticky top-0 bg-white/80 backdrop-blur-lg border-b border-slate-100 flex justify-between items-center z-50">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-lg"><i class="fa-solid fa-user-shield"></i></div>
                <div><h2 id="nav-username" class="text-xs font-black uppercase text-slate-800 leading-none mb-1">...</h2><button onclick="logoutTerminal()" class="text-[8px] font-black text-red-500 uppercase flex items-center gap-1"><i class="fa-solid fa-power-off"></i> Logout</button></div>
            </div>
            <div class="text-right"><p id="top-usd" class="text-blue-600 font-black text-xl leading-none">$0.00</p><p id="top-pkr" class="text-[9px] font-bold text-slate-400">Rs. 0</p></div>
        </header>

        <main class="p-5">
            <!-- Dashboard -->
            <div id="sec-home" class="space-y-6">
                <div class="nexa-card p-8 bg-gradient-to-br from-slate-900 to-blue-900 text-white border-none shadow-2xl mb-8 relative overflow-hidden">
                    <div class="relative z-10">
                        <h1 class="text-4xl font-black italic mb-2">Verified Hub.</h1>
                        <p class="text-[10px] font-bold opacity-70 mb-8 uppercase tracking-widest">Global Node Access Active</p>
                        <div class="flex gap-4">
                            <button onclick="requestDeposit()" class="bg-white text-blue-600 px-6 py-3 rounded-xl text-[10px] font-black uppercase shadow-lg">Load Balance</button>
                            <button onclick="requestWithdraw()" class="bg-white/10 border border-white/20 px-6 py-3 rounded-xl text-[10px] font-black uppercase">Payout</button>
                        </div>
                    </div>
                    <i class="fa-solid fa-satellite-dish absolute -bottom-4 -right-4 text-8xl opacity-10"></i>
                </div>
                <h3 class="text-xs font-black uppercase text-slate-400 italic mb-4 flex justify-between">Operation History <i class="fa-solid fa-bolt text-blue-500"></i></h3>
                <div id="hist-box" class="space-y-2"></div>
            </div>

            <!-- Nodes -->
            <div id="sec-mine" class="hidden"><div id="nodes-list"></div></div>

            <!-- Wallet -->
            <div id="sec-wallet" class="hidden">
                <div class="nexa-card p-10 text-center bg-blue-50/30 border-dashed border-2 border-blue-100">
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Net Worth</p>
                    <h1 class="text-5xl font-black text-slate-800">$0.00</h1>
                    <p class="text-[9px] font-bold text-blue-600 mt-4 uppercase">All nodes operating at 99.9% uptime 💋</p>
                </div>
            </div>

            <!-- Admin -->
            <div id="sec-admin" class="hidden space-y-6">
                <div class="nexa-card p-6 border-l-4 border-red-500 bg-red-50/20">
                    <h2 class="text-lg font-black italic text-red-600 uppercase">Commander Console</h2>
                    <p class="text-[10px] font-bold opacity-50 uppercase">Manual Verification Required</p>
                </div>
                <h3 class="text-xs font-black uppercase text-slate-400 italic">Pending Deposits</h3>
                <div id="admin-req-list" class="space-y-3"></div>
            </div>
        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 nexa-card rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] border-none shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon active-tab"><i class="fa-solid fa-house-user"></i></button>
            <button onclick="switchTab('mine')" class="nav-icon"><i class="fa-solid fa-cubes-stacked"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-chart-pie"></i></button>
            <button id="admin-trigger" onclick="switchTab('admin')" class="nav-icon hidden text-red-400"><i class="fa-solid fa-fingerprint"></i></button>
        </nav>
    </div>

</body>
</html>
