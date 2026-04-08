<!DOCTYPE html>
<html lang="en" id="main-html" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    <title>NEXA GOLD | Global Node</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --bg: #010409; --card: #0d1117; --text: #f0f6fc; --border: #30363d; --accent: #3b82f6; }
        .light { --bg: #f8fafc; --card: #ffffff; --text: #0f172a; --border: #e2e8f0; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: var(--text); transition: 0.3s; padding-bottom: 100px; overflow-x: hidden; }
        .glass { background: var(--card); border: 1px solid var(--border); }
        .page { display: none; animation: slideUp 0.4s ease forwards; }
        .active-page { display: block; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .btn-prime { background: linear-gradient(135deg, #1e40af, #3b82f6); color: white; border-radius: 16px; font-weight: 800; transition: 0.2s; }
        .btn-prime:active { transform: scale(0.95); }
        input { background: var(--card); border: 1px solid var(--border); color: var(--text); padding: 14px; border-radius: 14px; width: 100%; outline: none; font-size: 13px; }
        .nav-active { color: var(--accent); transform: scale(1.1); opacity: 1 !important; }
        .animate-marquee { display: inline-block; animation: marquee 15s linear infinite; }
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        ::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <!-- Restricted Screen -->
    <div id="lock-screen" class="fixed inset-0 z-[1000000] bg-[var(--bg)] hidden flex flex-col items-center justify-center p-8 text-center">
        <div class="w-20 h-20 bg-red-500/20 rounded-full flex items-center justify-center mb-6 animate-pulse text-4xl">⚠️</div>
        <h1 id="lock-title" class="text-2xl font-black uppercase italic text-red-500 mb-2">Access Restricted</h1>
        <p id="lock-msg" class="text-[10px] font-bold opacity-60 uppercase tracking-widest leading-relaxed">Optimization in progress sweetie! 😘</p>
    </div>

    <!-- Top Navigation -->
    <header class="p-4 flex justify-between items-center sticky top-0 bg-[var(--bg)]/80 backdrop-blur-md border-b border-[var(--border)] z-[5000]">
        <div class="flex items-center gap-2">
            <div onclick="adminTap()" class="w-9 h-9 bg-blue-600 rounded-xl flex items-center justify-center font-black text-white italic shadow-lg">N</div>
            <span class="font-black text-xs uppercase tracking-tighter">NEXA <span class="text-blue-500">GOLD</span></span>
        </div>
        <div class="flex items-center gap-3">
            <button onclick="toggleTheme()" class="w-8 h-8 glass rounded-full flex items-center justify-center text-sm">🌓</button>
            <div id="top-bal" class="text-[10px] font-black bg-blue-600/10 text-blue-500 px-4 py-1.5 rounded-full border border-blue-500/20 italic">₨ 0</div>
        </div>
    </header>

    <!-- Auth Section -->
    <section id="auth-ui" class="fixed inset-0 z-[20000] bg-[var(--bg)] flex flex-col items-center justify-center p-8 text-center">
        <div class="w-16 h-16 bg-blue-600 rounded-[1.5rem] mb-6 flex items-center justify-center text-4xl font-black text-white italic shadow-2xl">N</div>
        <h1 class="text-2xl font-black italic tracking-tighter mb-8 uppercase text-[var(--text)]">Authorize Node</h1>
        <div class="w-full max-w-[300px] space-y-4">
            <input type="text" id="user-name" placeholder="Terminal ID" class="text-center font-bold">
            <input type="password" id="user-pass" placeholder="Access Key" class="text-center font-bold">
            <button onclick="login()" class="w-full p-4 btn-prime uppercase text-[10px] tracking-widest">Login 💋</button>
        </div>
    </section>

    <main id="app-ui" class="hidden p-4 space-y-6">
        <!-- Home Node -->
        <div id="p-home" class="page active-page space-y-6">
            <div class="bg-blue-600/5 border border-blue-500/10 p-2 rounded-xl overflow-hidden whitespace-nowrap">
                <p id="v-news" class="animate-marquee inline-block text-[8px] font-black uppercase text-blue-400 italic">
                    Welcome Sweetie! Minimum Deposit ₨ 200 | Secure Nodes Active 💋
                </p>
            </div>

            <div class="p-8 rounded-[2.5rem] bg-gradient-to-br from-blue-700 to-blue-900 text-white shadow-2xl relative overflow-hidden">
                <p class="text-[10px] font-black uppercase opacity-60 tracking-widest">Current Balance</p>
                <h2 class="text-4xl font-black tracking-tighter mt-1" id="v-bal">₨ 0.00</h2>
                <div class="mt-6 flex justify-between items-center bg-black/20 p-4 rounded-2xl backdrop-blur-md">
                    <span class="text-[8px] font-bold uppercase italic">Status: Online</span>
                    <button onclick="copyRef()" class="bg-white text-blue-800 px-4 py-2 rounded-xl text-[8px] font-black uppercase">Copy Invite</button>
                </div>
            </div>

            <div class="flex gap-2 p-1 bg-white/5 rounded-2xl">
                <button onclick="renderPlans('normal')" id="btn-normal" class="flex-1 p-3 rounded-xl bg-blue-600 text-white text-[9px] font-black uppercase">Standard Nodes</button>
                <button onclick="renderPlans('special')" id="btn-special" class="flex-1 p-3 rounded-xl text-[9px] font-black uppercase opacity-40">VIP Offers</button>
            </div>
            <div id="plans-grid" class="grid grid-cols-1 gap-4"></div>
        </div>

        <!-- Wallet Section -->
        <div id="p-wallet" class="page space-y-6">
            <h3 class="text-[10px] font-black uppercase opacity-40 text-center italic">Deposit Funds</h3>
            <div class="space-y-3">
                <div class="glass p-5 rounded-[2rem] border-l-4 border-red-600 flex justify-between items-center">
                    <div><p class="text-[8px] font-black text-red-500 uppercase">JazzCash</p><p class="text-lg font-black tracking-widest">03705519562</p></div>
                    <button onclick="copyText('03705519562')" class="text-[8px] bg-white/5 px-3 py-2 rounded-lg font-bold">COPY</button>
                </div>
                <div class="glass p-5 rounded-[2rem] border-l-4 border-green-500 flex justify-between items-center">
                    <div><p class="text-[8px] font-black text-green-500 uppercase">EasyPaisa</p><p class="text-lg font-black tracking-widest">03379827882</p></div>
                    <button onclick="copyText('03379827882')" class="text-[8px] bg-white/5 px-3 py-2 rounded-lg font-bold">COPY</button>
                </div>
            </div>
            <div class="glass p-6 rounded-[2.5rem] space-y-4">
                <input type="number" id="dep-amt" placeholder="Amount (₨)">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)">
                <button onclick="submitDep()" class="w-full p-4 btn-prime uppercase text-[10px] tracking-widest">Verify Deposit 💋</button>
            </div>
        </div>

        <!-- Logs Section -->
        <div id="p-history" class="page space-y-4">
            <h3 class="text-[10px] font-black uppercase opacity-40 italic tracking-widest text-center">Transaction Log</h3>
            <div id="history-list" class="space-y-3"></div>
        </div>
    </main>

    <!-- Bottom Navbar -->
    <nav id="bottom-nav" class="hidden fixed bottom-0 w-full glass border-t border-[var(--border)] p-4 flex justify-around items-center rounded-t-[2.5rem] z-[4000]">
        <button onclick="changePage('home')" id="n-home" class="nav-active opacity-40 flex flex-col items-center gap-1 px-4 py-2">🏠<span class="text-[7px] font-black">HOME</span></button>
        <button onclick="changePage('wallet')" id="n-wallet" class="opacity-40 flex flex-col items-center gap-1 px-4 py-2">📥<span class="text-[7px] font-black">DEPOSIT</span></button>
        <button onclick="changePage('history')" id="n-history" class="opacity-40 flex flex-col items-center gap-1 px-4 py-2">📜<span class="text-[7px] font-black">LOGS</span></button>
    </nav>

    <script>
        // Use your Firebase Config here
        const firebaseConfig = { apiKey: "AIzaSyDt3ChZHyDdtM4Ir1oXRZJUywcOiV30Wtg", authDomain: "investment-84f4e.firebaseapp.com", projectId: "investment-84f4e", storageBucket: "investment-84f4e.appspot.com", messagingSenderId: "975293889308", appId: "1:975293889308:web:6d034a99cc966c75ff58d9" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();
        let user = null; let tapCount = 0;

        const NORMAL_PLANS = Array.from({length: 20}, (_, i) => ({ name: `Nexa Node v${i+1}`, price: 200 + (i*500), profit: (3 + (i*0.2)).toFixed(1) }));
        const SPECIAL_PLANS = [{ name: "VIP Flash Node", price: 5000, profit: "15" }, { name: "Queen Choice", price: 10000, profit: "25" }];

        async function login() {
            const n = document.getElementById('user-name').value.trim().toLowerCase();
            const p = document.getElementById('user-pass').value.trim();
            if(!n || !p) return alert("Credentials please! 💋");
            const ref = db.collection("users").doc(n);
            const d = await ref.get();
            if(!d.exists) {
                await ref.set({ name: n, password: p, balance: 0, time: Date.now() });
                alert("Account Created Sweetie! 💋");
            } else {
                if(d.data().password !== p) return alert("Wrong Access Key!");
            }
            localStorage.setItem('nexa_user', n);
            location.reload();
        }

        function sync(n) {
            db.collection("users").doc(n).onSnapshot(d => {
                user = d.data();
                const bal = (user.balance || 0).toLocaleString();
                document.getElementById('v-bal').innerText = "₨ " + bal;
                document.getElementById('top-bal').innerText = "₨ " + bal;
            });
            db.collection("requests").where("user", "==", n).orderBy("time", "desc").onSnapshot(s => {
                const list = document.getElementById('history-list'); list.innerHTML = '';
                s.forEach(doc => {
                    const x = doc.data();
                    list.innerHTML += `<div class="glass p-4 rounded-2xl flex justify-between items-center text-[10px] font-black border-l-4 ${x.status==='approved'?'border-green-500':'border-yellow-500'}">
                        <div><p class="uppercase">${x.type}</p><p class="text-[7px] opacity-40">${new Date(x.time).toLocaleDateString()}</p></div>
                        <div class="text-right"><p>₨ ${x.amount}</p><p class="text-[7px] uppercase italic">${x.status}</p></div>
                    </div>`;
                });
            });
        }

        function renderPlans(cat) {
            const grid = document.getElementById('plans-grid');
            const data = cat === 'normal' ? NORMAL_PLANS : SPECIAL_PLANS;
            grid.innerHTML = '';
            data.forEach(p => {
                grid.innerHTML += `<div class="glass p-6 rounded-[2rem] border-l-4 border-blue-500">
                    <div class="flex justify-between items-center">
                        <div><p class="text-[10px] font-black uppercase italic">${p.name}</p><h3 class="text-xl font-black text-blue-500">₨ ${p.price}</h3></div>
                        <span class="bg-blue-600/10 text-blue-500 px-3 py-1 rounded-full text-[8px] font-black">${p.profit}% DAILY</span>
                    </div>
                    <button onclick="buyNode(${p.price})" class="w-full mt-4 btn-prime p-3 text-[9px] uppercase">Activate Node ⚡</button>
                </div>`;
            });
        }

        async function submitDep() {
            const a = document.getElementById('dep-amt').value; const t = document.getElementById('dep-tid').value;
            if(!a || !t) return alert("Fill all details! 💋");
            await db.collection("requests").add({ user: user.name, amount: parseInt(a), tid: t, type: "deposit", status: "pending", time: Date.now() });
            alert("Request Sent! Wait for approval sweetie. 💋");
        }

        function changePage(p) {
            document.querySelectorAll('.page').forEach(pg=>pg.classList.remove('active-page'));
            document.getElementById('p-'+p).classList.add('active-page');
            document.querySelectorAll('nav button').forEach(b => { b.classList.remove('nav-active'); b.classList.add('opacity-40'); });
            document.getElementById('n-'+p).classList.add('nav-active');
            document.getElementById('n-'+p).classList.remove('opacity-40');
        }

        function toggleTheme() { document.getElementById('main-html').classList.toggle('dark'); document.getElementById('main-html').classList.toggle('light'); }
        function copyText(t) { navigator.clipboard.writeText(t); alert("Copied! 💋"); }
        function adminTap() { tapCount++; if(tapCount >= 5) { const k = prompt("Secret Key:"); if(k==="mint786") alert("Admin Node Activated! (Check Firestore Dashboard)"); tapCount=0; } }

        window.onload = () => { 
            const saved = localStorage.getItem('nexa_user');
            if(saved) {
                document.getElementById('auth-ui').classList.add('hidden');
                document.getElementById('app-ui').classList.remove('hidden');
                document.getElementById('bottom-nav').classList.remove('hidden');
                sync(saved);
            }
            renderPlans('normal');
        }
    </script>
</body>
</html>
