<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA NODES | High-Yield Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --primary: #2563eb; --bg: #F8FAFC; --card: #FFFFFF; --text: #1E293B; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: var(--text); -webkit-tap-highlight-color: transparent; }
        .trust-card { background: var(--card); border-radius: 24px; border: 1px solid rgba(0,0,0,0.05); box-shadow: 0 10px 25px -5px rgba(0,0,0,0.05); }
        .btn-primary { background: var(--primary); color: white; box-shadow: 0 4px 12px rgba(37,99,235,0.2); transition: 0.3s; }
        .btn-primary:active { transform: scale(0.96); }
        .nav-active { color: var(--primary) !important; border-top: 3px solid var(--primary); }
        input, select { background: #F1F5F9 !important; border: 1px solid #E2E8F0 !important; color: #1E293B !important; }
        .status-badge { padding: 2px 8px; border-radius: 100px; font-size: 7px; font-weight: 900; text-transform: uppercase; }
    </style>
</head>
<body class="pb-24">

    <!-- LOGIN / AUTH -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-16 h-16 bg-blue-600 rounded-2xl flex items-center justify-center text-white text-3xl mb-4 shadow-xl shadow-blue-200"><i class="fa-solid fa-server"></i></div>
        <h1 class="text-xl font-extrabold tracking-tight mb-2">NEXA <span class="text-blue-600">NODES</span></h1>
        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest mb-8 text-center">Institutional Mining Interface</p>
        <div class="w-full max-w-xs space-y-3">
            <input type="text" id="user-name" placeholder="Full Member Name" class="w-full p-4 rounded-xl outline-none text-sm font-semibold">
            <input type="password" id="admin-key" placeholder="Security Key (Optional)" class="w-full p-4 rounded-xl outline-none text-sm font-semibold">
            <button onclick="handleLogin()" class="w-full btn-primary p-4 rounded-xl font-bold uppercase text-[10px] tracking-widest">Access Secure Dashboard</button>
        </div>
    </div>

    <!-- MAIN APP -->
    <div id="app" class="hidden">
        
        <header class="p-6 flex justify-between items-center bg-white/90 backdrop-blur-md sticky top-0 z-50 border-b border-slate-100">
            <div>
                <h3 id="display-name" class="text-sm font-extrabold text-slate-800">--</h3>
                <p class="text-[8px] font-black text-blue-600 uppercase tracking-widest"><i class="fa-solid fa-circle-check mr-1"></i> Verified Operator</p>
            </div>
            <button onclick="logout()" class="w-10 h-10 bg-slate-50 text-slate-400 rounded-full flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <!-- PAGE: HOME -->
        <main id="page-home" class="page-content px-6 py-6 space-y-6">
            <div class="trust-card p-8 text-center border-t-[6px] border-blue-600 relative overflow-hidden">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[3px] mb-2">Portfolio Valuation</p>
                <h2 id="user-bal" class="text-4xl font-extrabold text-slate-900">$0.00</h2>
                <p id="pkr-bal" class="text-xs font-bold text-blue-500 mt-1 italic">≈ Rs. 0.00</p>
                <div class="flex gap-3 mt-6">
                    <button onclick="nav('deposit')" class="flex-1 btn-primary py-3 rounded-xl text-[9px] font-black uppercase">Add Funds</button>
                    <button onclick="nav('withdraw')" class="flex-1 bg-slate-900 text-white py-3 rounded-xl text-[9px] font-black uppercase">Payout</button>
                </div>
            </div>

            <!-- ANALYTICS -->
            <div class="grid grid-cols-2 gap-4">
                <div class="trust-card p-5">
                    <i class="fa-solid fa-microchip text-blue-600 text-xs mb-2"></i>
                    <p class="text-[8px] font-bold text-slate-400 uppercase">Active Rigs</p>
                    <p id="active-plans" class="text-xl font-extrabold">0</p>
                </div>
                <div class="trust-card p-5">
                    <i class="fa-solid fa-users text-blue-600 text-xs mb-2"></i>
                    <p class="text-[8px] font-bold text-slate-400 uppercase">Team Size</p>
                    <p id="team-count" class="text-xl font-extrabold">0</p>
                </div>
            </div>

            <!-- PROMO CLAIM -->
            <div class="trust-card p-5 border-l-4 border-amber-400">
                <p class="text-[9px] font-extrabold uppercase text-slate-500 mb-3">Claim Incentive Bonus</p>
                <div class="flex gap-2">
                    <input id="promo-input" placeholder="Promo Code (e.g. GOLD214)" class="flex-1 p-3 rounded-lg text-[10px] uppercase font-bold outline-none">
                    <button onclick="submitPromo()" class="bg-amber-400 text-black px-4 rounded-lg text-[9px] font-black uppercase">Submit</button>
                </div>
                <p id="promo-msg" class="text-[7px] mt-2 font-black text-blue-500 uppercase tracking-tighter"></p>
            </div>

            <!-- INVITE -->
            <div class="trust-card p-5">
                <p class="text-[9px] font-extrabold uppercase text-slate-500 mb-2">Partnership ID</p>
                <div class="flex gap-2 items-center bg-slate-50 p-2 rounded-lg">
                    <input id="ref-link" readonly value="..." class="flex-1 bg-transparent text-[9px] font-bold text-blue-600 border-none outline-none">
                    <button onclick="copyRef()" class="text-slate-400 px-2"><i class="fa-solid fa-copy"></i></button>
                </div>
            </div>
        </main>

        <!-- PAGE: NODES (15+5) -->
        <main id="page-nodes" class="page-content hidden px-6 py-6 space-y-4">
            <h2 class="text-lg font-extrabold uppercase tracking-tighter">Mining Infrastructure</h2>
            <div id="nodes-container" class="space-y-3 pb-10"></div>
        </main>

        <!-- PAGE: WITHDRAW -->
        <main id="page-withdraw" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-lg font-extrabold uppercase tracking-tighter">Liquidity Payout</h2>
            <div class="trust-card p-6 space-y-4">
                <select id="w-method" class="w-full p-4 rounded-xl outline-none text-xs font-bold">
                    <option value="JazzCash">JazzCash</option>
                    <option value="Easypaisa">Easypaisa</option>
                </select>
                <input type="text" id="w-num" placeholder="Account Number" class="w-full p-4 rounded-xl outline-none text-xs font-bold">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl outline-none text-xs font-bold">
                <button onclick="submitWithdraw()" class="w-full btn-primary p-4 rounded-xl font-bold uppercase text-[9px]">Initiate Withdrawal</button>
            </div>
        </main>

        <!-- PAGE: LEGAL / ABOUT -->
        <main id="page-info" class="page-content hidden px-6 py-6 space-y-6 pb-24">
            <h2 class="text-lg font-extrabold uppercase tracking-tighter">Corporate Compliance</h2>
            <div class="trust-card p-6 space-y-6 text-[10px] leading-relaxed text-slate-600">
                <section>
                    <h4 class="text-slate-900 font-extrabold mb-1 uppercase tracking-widest">Mission Statement</h4>
                    <p>Nexa Nodes provides high-performance computing power to global blockchain networks, allowing retail investors to earn stable daily yields.</p>
                </section>
                <section>
                    <h4 class="text-slate-900 font-extrabold mb-1 uppercase tracking-widest">Privacy Protocol</h4>
                    <p>Humara platform 256-bit encryption use karta hai. Aapki banking info aur private data kabhi store ya share nahi hota.</p>
                </section>
                <section>
                    <h4 class="text-slate-900 font-extrabold mb-1 uppercase tracking-widest">Standard Terms</h4>
                    <ul class="list-disc ml-4 space-y-1">
                        <li>Withdrawal processing: 1-12 Business Hours.</li>
                        <li>Strict KYC: One account per person only.</li>
                        <li>Min Withdrawal: $1 (285 PKR).</li>
                    </ul>
                </section>
                <a href="https://chat.whatsapp.com/EbfTbr66JQLFEmjnxrReE3" class="block w-full bg-green-500 text-white p-4 rounded-xl text-center font-bold uppercase text-[9px]">
                    <i class="fa-brands fa-whatsapp text-lg mr-2"></i> Official Support Group
                </a>
            </div>
        </main>

        <!-- PAGE: ADMIN -->
        <main id="page-admin" class="page-content hidden px-6 py-6 space-y-6">
            <h2 class="text-lg font-extrabold text-red-600 uppercase">Administrator Hub</h2>
            <div class="flex flex-wrap gap-2">
                <button onclick="loadAdmin('dep')" class="bg-blue-600 text-white px-4 py-2 rounded-lg text-[8px] font-black">DEPOSITS</button>
                <button onclick="loadAdmin('wit')" class="bg-slate-800 text-white px-4 py-2 rounded-lg text-[8px] font-black">PAYOUTS</button>
                <button onclick="loadAdminPromo()" class="bg-amber-500 text-white px-4 py-2 rounded-lg text-[8px] font-black">PROMO REQS</button>
                <button onclick="loadUsers()" class="bg-indigo-600 text-white px-4 py-2 rounded-lg text-[8px] font-black">BONUSES</button>
            </div>
            <div id="admin-list" class="space-y-4"></div>
        </main>

        <!-- NAVIGATION -->
        <nav class="fixed bottom-0 left-0 right-0 h-20 bg-white border-t border-slate-100 flex justify-around items-center z-50 px-2">
            <div onclick="nav('home')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-home"><i class="fa-solid fa-house"></i><span class="text-[8px] font-black mt-1 uppercase">Home</span></div>
            <div onclick="nav('nodes')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-nodes"><i class="fa-solid fa-microchip"></i><span class="text-[8px] font-black mt-1 uppercase">Nodes</span></div>
            <div onclick="nav('withdraw')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-withdraw"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-black mt-1 uppercase">Cash</span></div>
            <div onclick="nav('info')" class="nav-item flex flex-col items-center flex-1 py-3 text-slate-400" id="btn-info"><i class="fa-solid fa-shield-halved"></i><span class="text-[8px] font-black mt-1 uppercase">Legal</span></div>
            <div onclick="nav('admin')" class="nav-item hidden flex flex-col items-center flex-1 py-3 text-red-500" id="btn-admin"><i class="fa-solid fa-user-gear"></i><span class="text-[8px] font-black mt-1 uppercase">Admin</span></div>
        </nav>
    </div>

    <!-- PAYMENT MODAL -->
    <div id="pay-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-[10000] hidden flex items-center justify-center p-6">
        <div class="trust-card p-8 w-full max-w-sm">
            <h3 id="m-gw" class="text-lg font-extrabold text-blue-600 mb-2 uppercase">--</h3>
            <p id="m-num" class="bg-slate-50 p-4 rounded-xl font-bold text-slate-900 text-center tracking-widest text-lg mb-6 border border-slate-100" onclick="copyNum()">--</p>
            <div class="space-y-3">
                <input type="number" id="m-amt" placeholder="Amount ($)" class="w-full p-4 rounded-xl outline-none text-xs font-bold">
                <input type="text" id="m-tid" placeholder="Transaction ID (TID)" class="w-full p-4 rounded-xl outline-none text-xs font-bold">
                <button onclick="submitDep()" class="w-full btn-primary p-4 rounded-xl font-bold uppercase text-[9px]">Confirm Funding</button>
                <button onclick="closeModal()" class="w-full text-slate-400 text-[8px] font-bold uppercase mt-2">Cancel</button>
            </div>
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

        // AUTH
        window.handleLogin = async () => {
            const name = document.getElementById('user-name').value;
            const key = document.getElementById('admin-key').value;
            if(!name) return alert("Sweetie, enter your name!");
            const res = await signInAnonymously(auth);
            uid = res.user.uid;
            const s = await get(ref(db, `users/${uid}`));
            if(!s.exists()) {
                await set(ref(db, `users/${uid}`), { username: name, balance: 0, role: (key==="sweetie786"?"admin":"user"), joined: Date.now(), plans: 0, team: 0 });
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
                    document.getElementById('display-name').innerText = userData.username;
                    document.getElementById('user-bal').innerText = `$${(userData.balance || 0).toFixed(2)}`;
                    document.getElementById('pkr-bal').innerText = `≈ Rs. ${(userData.balance * RATE).toLocaleString()}`;
                    document.getElementById('active-plans').innerText = userData.plans || 0;
                    document.getElementById('team-count').innerText = userData.team || 0;
                    document.getElementById('ref-link').value = `https://nexanodes.com/reg?id=${uid}`;
                    if(userData.role === 'admin') document.getElementById('btn-admin').classList.remove('hidden');
                });
                loadNodes(); nav('home');
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('app').classList.remove('hidden');
            }
        });

        // CORE NAV
        window.nav = (id) => {
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            document.getElementById(`page-${id}`).classList.remove('hidden');
            document.getElementById(`btn-${id}`)?.classList.add('nav-active');
        };

        // NODES SYSTEM (15 Tiers + 5 VIP)
        function loadNodes() {
            const con = document.getElementById('nodes-container');
            con.innerHTML = "";
            for(let i=1; i<=15; i++) con.innerHTML += createNode(`Quantum Node v.${i}`, i*5, 'blue');
            [200, 500, 1000, 2500, 5000].forEach((c, idx) => con.innerHTML += createNode(`Institutional Rig VIP ${idx+1}`, c, 'indigo'));
        }
        function createNode(n, c, col) {
            return `<div class="trust-card p-4 flex justify-between items-center border-l-4 border-${col}-600">
                <div><p class="text-[9px] font-black text-slate-800 uppercase">${n}</p><p class="text-[8px] text-slate-400 font-bold">$${c} • Rs. ${c*RATE}</p></div>
                <button onclick="buyPlan(${c})" class="bg-blue-50 text-blue-600 px-4 py-2 rounded-lg text-[8px] font-black border border-blue-100 uppercase">Deploy</button>
            </div>`;
        }
        window.buyPlan = async (c) => {
            if(userData.balance < c) return alert("Sweetie, balance low hai!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - c, plans: (userData.plans || 0) + 1 });
            alert("Rig Deployment Successful!");
        };

        // PROMO REQUEST SYSTEM (Manual)
        window.submitPromo = async () => {
            const code = document.getElementById('promo-input').value.trim().toUpperCase();
            if(!code) return alert("Sweetie, code to likho!");
            await push(ref(db, 'promo_requests'), { uid, username: userData.username, code, status: 'pending', time: Date.now() });
            document.getElementById('promo-msg').innerText = "Request Logged. Waiting for Admin Approval... ⏳";
            document.getElementById('promo-input').value = "";
        };

        // FUNDING & PAYOUTS
        window.openPay = (gw, n) => { document.getElementById('m-gw').innerText = gw; document.getElementById('m-num').innerText = n; document.getElementById('pay-modal').classList.remove('hidden'); };
        window.closeModal = () => document.getElementById('pay-modal').classList.add('hidden');
        window.submitDep = async () => {
            const a = parseFloat(document.getElementById('m-amt').value);
            const t = document.getElementById('m-tid').value;
            if(!a || !t) return alert("Fill all details!");
            await push(ref(db, 'deposits'), { uid, username: userData.username, amount: a, tid: t, method: document.getElementById('m-gw').innerText, status: 'pending' });
            alert("Funding request submitted!"); closeModal();
        };
        window.submitWithdraw = async () => {
            const a = parseFloat(document.getElementById('w-amt').value);
            const n = document.getElementById('w-num').value;
            const m = document.getElementById('w-method').value;
            if(userData.balance < a || a < 1) return alert("Insufficient Liquidity!");
            await update(ref(db, `users/${uid}`), { balance: userData.balance - a });
            await push(ref(db, 'withdraws'), { uid, username: userData.username, amount: a, number: n, method: m, status: 'pending' });
            alert("Withdrawal Logged!");
        };

        // ADMIN FUNCTIONS
        window.loadAdmin = (tab) => {
            const path = tab === 'dep' ? 'deposits' : 'withdraws';
            onValue(ref(db, path), s => {
                const con = document.getElementById('admin-list'); con.innerHTML = "";
                s.forEach(c => {
                    const d = c.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `<div class="trust-card p-4 text-[9px] bg-slate-50 border-none">
                            <p class="font-black text-slate-800 uppercase">${d.username} | <span class="text-blue-600">$${d.amount}</span></p>
                            <p class="text-slate-400 mb-3 tracking-tighter">${tab==='dep'?'TID: '+d.tid : 'Number: '+d.number}</p>
                            <button onclick="approveAction('${path}', '${c.key}', '${d.uid}', ${d.amount}, '${tab}')" class="w-full btn-primary py-2 rounded-lg font-black">Approve</button>
                        </div>`;
                    }
                });
            });
        };

        window.loadAdminPromo = () => {
            onValue(ref(db, 'promo_requests'), s => {
                const con = document.getElementById('admin-list'); con.innerHTML = "";
                s.forEach(c => {
                    const d = c.val();
                    if(d.status === 'pending') {
                        con.innerHTML += `<div class="trust-card p-4 text-[9px]">
                            <p class="font-black text-slate-800 uppercase">${d.username} is claiming: <span class="text-amber-600">${d.code}</span></p>
                            <div class="flex gap-2 mt-3">
                                <input id="b-amt-${c.key}" type="number" placeholder="Enter $ Bonus" class="flex-1 p-2 rounded text-[9px] border border-slate-200 outline-none">
                                <button onclick="approvePromo('${c.key}', '${d.uid}')" class="bg-green-600 text-white px-4 rounded-lg font-black">Verify</button>
                            </div>
                        </div>`;
                    }
                });
            });
        };

        window.approvePromo = async (key, u_uid) => {
            const amt = parseFloat(document.getElementById(`b-amt-${key}`).value);
            if(!amt) return alert("Set reward first!");
            const uSnap = await get(ref(db, `users/${u_uid}`));
            await update(ref(db, `users/${u_uid}`), { balance: (uSnap.val().balance || 0) + amt });
            await update(ref(db, `promo_requests/${key}`), { status: 'approved' });
            alert("Bonus Issued!");
        };

        window.loadUsers = () => {
            onValue(ref(db, 'users'), s => {
                const con = document.getElementById('admin-list'); con.innerHTML = "<p class='text-[8px] font-black uppercase text-slate-400 mb-2'>Member Directory (Direct Bonus)</p>";
                s.forEach(u => {
                    const user = u.val();
                    con.innerHTML += `<div class="trust-card p-4 flex justify-between items-center text-[9px]">
                        <div><p class="font-black">${user.username}</p><p class="text-[7px] text-slate-400 select-all">${u.key}</p></div>
                        <button onclick="directBonus('${u.key}')" class="bg-blue-600 text-white px-3 py-1 rounded font-bold">Gift</button>
                    </div>`;
                });
            });
        };

        window.directBonus = async (u_uid) => {
            const amt = parseFloat(prompt("Enter Bonus Amount ($):"));
            if(!amt) return;
            const snap = await get(ref(db, `users/${u_uid}/balance`));
            await update(ref(db, `users/${u_uid}`), { balance: (snap.val() || 0) + amt });
            alert("Bonus Sent!");
        };

        window.approveAction = async (path, key, u_uid, amt, tab) => {
            if(tab === 'dep') {
                const snap = await get(ref(db, `users/${u_uid}/balance`));
                await update(ref(db, `users/${u_uid}`), { balance: (snap.val() || 0) + amt });
            }
            await update(ref(db, `${path}/${key}`), { status: 'approved' });
            alert("Verified!");
        };

        window.copyRef = () => { navigator.clipboard.writeText(document.getElementById('ref-link').value); alert("Link Copied!"); };
        window.copyNum = () => { navigator.clipboard.writeText(document.getElementById('m-num').innerText); alert("Copied!"); };
        window.logout = () => signOut(auth).then(() => location.reload());
    </script>

    <!-- DEPOSIT TRIGGERS (In Deposit Page) -->
    <script>
        // Manually handling Deposit Gateway selections
        document.getElementById('page-deposit').innerHTML = `
            <h2 class="text-lg font-extrabold uppercase px-6 py-6 tracking-tighter">Funding Hub</h2>
            <div class="px-6 space-y-4">
                <div onclick="openPay('JazzCash','03705519562')" class="trust-card p-6 flex justify-between items-center border-l-[6px] border-red-500">
                    <div><p class="text-[10px] font-black uppercase">JazzCash Official</p><p class="text-[8px] text-slate-400">Institutional Merchant</p></div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="openPay('Easypaisa','03332637235')" class="trust-card p-6 flex justify-between items-center border-l-[6px] border-green-500">
                    <div><p class="text-[10px] font-black uppercase">Easypaisa Fast</p><p class="text-[8px] text-slate-400">Automated Gateway</p></div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
            </div>
        `;
    </script>
</body>
</html>
