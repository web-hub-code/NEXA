<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA | Premium Node Finance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        
        :root {
            --primary: #2563eb;
            --accent: #f43f5e;
            --bg: #ffffff;
            --surface: #f8fafc;
            --border: rgba(0,0,0,0.06);
        }

        body { 
            background: var(--bg); 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            color: #1e293b;
            overflow-x: hidden;
        }

        /* Modern Glassmorphism for Light Mode */
        .glass { 
            background: rgba(255, 255, 255, 0.7); 
            backdrop-filter: blur(20px); 
            border: 1px solid var(--border);
            box-shadow: 0 10px 30px -10px rgba(0,0,0,0.04);
        }

        .plan-card {
            background: #ffffff;
            border: 1px solid var(--border);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            border-radius: 24px;
        }

        .plan-card:hover {
            transform: translateY(-12px);
            box-shadow: 0 30px 60px -15px rgba(37, 99, 235, 0.15);
            border-color: var(--primary);
        }

        .btn-primary {
            background: linear-gradient(135deg, #2563eb, #3b82f6);
            color: white;
            transition: 0.3s;
        }

        .btn-primary:hover { transform: scale(1.02); filter: brightness(1.1); }

        .hidden { display: none; }

        /* Smooth Section Transitions */
        .section-fade { animation: fadeInUp 0.6s ease-out; }
        
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <!-- TOP NAVIGATION -->
    <nav class="glass sticky top-0 z-[100] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-8">
            <h1 id="logo" class="text-3xl font-black text-blue-600 cursor-pointer tracking-tighter animate__animated animate__fadeInLeft">NEXA</h1>
            <div class="hidden md:flex gap-6 text-[11px] uppercase tracking-widest font-bold opacity-60">
                <button onclick="showSec('home')" class="hover:text-blue-600 transition">Dashboard</button>
                <button onclick="showSec('about')" class="hover:text-blue-600 transition">Protocol</button>
                <button onclick="showSec('policy')" class="hover:text-blue-600 transition">Security</button>
            </div>
        </div>
        <div id="user-info" class="hidden flex items-center gap-6">
            <div class="text-right">
                <p class="text-[9px] font-bold opacity-40 uppercase">Net Liquidity</p>
                <p id="top-bal" class="text-blue-600 font-black">$0.00</p>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-red-50 text-red-500 flex items-center justify-center hover:bg-red-500 hover:text-white transition">
                <i class="fa-solid fa-power-off"></i>
            </button>
        </div>
    </nav>

    <!-- LOGIN SECTION -->
    <div id="auth-sec" class="min-h-[90vh] flex items-center justify-center p-6 bg-[radial-gradient(#e2e8f0_1px,transparent_1px)] [background-size:20px_20px]">
        <div class="glass p-12 rounded-[3rem] w-full max-w-md text-center animate__animated animate__zoomIn">
            <div class="w-20 h-20 bg-blue-600 rounded-3xl mx-auto mb-6 flex items-center justify-center shadow-2xl shadow-blue-200">
                <i class="fa-solid fa-shield-check text-3xl text-white"></i>
            </div>
            <h2 class="text-2xl font-black mb-2">Access Portal</h2>
            <p class="text-sm text-gray-400 mb-8 font-medium">Verified Encrypted Session</p>
            <form id="login-form" class="space-y-4 text-left">
                <div>
                    <label class="text-[10px] font-bold ml-2 text-gray-400 uppercase">Identity</label>
                    <input type="text" id="user-id" placeholder="Username" class="w-full p-4 rounded-2xl bg-gray-50 outline-none border border-transparent focus:border-blue-500 transition mt-1" required>
                </div>
                <div>
                    <label class="text-[10px] font-bold ml-2 text-gray-400 uppercase">Security Key</label>
                    <input type="password" id="user-key" placeholder="••••••••" class="w-full p-4 rounded-2xl bg-gray-50 outline-none border border-transparent focus:border-blue-500 transition mt-1" required>
                </div>
                <button class="w-full btn-primary py-5 rounded-2xl font-black uppercase tracking-widest mt-4 shadow-xl shadow-blue-100">Initialize Node</button>
            </form>
        </div>
    </div>

    <!-- MAIN DASHBOARD -->
    <div id="main-sec" class="hidden p-8 max-w-7xl mx-auto space-y-12">
        <header class="section-fade">
            <h2 class="text-4xl font-black tracking-tighter">Welcome, <span id="user-display" class="text-blue-600">Investor</span></h2>
            <p class="text-gray-400 font-medium">Operational Status: <span class="text-green-500">Active</span></p>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Balance Card -->
            <div class="glass p-10 rounded-[2.5rem] relative overflow-hidden bg-gradient-to-br from-white to-gray-50">
                <div class="absolute -right-10 -top-10 w-40 h-40 bg-blue-50 rounded-full blur-3xl opacity-50"></div>
                <p class="text-xs font-bold text-gray-400 uppercase tracking-widest">Available Balance</p>
                <h3 id="dash-bal" class="text-5xl font-black text-blue-600 mt-4 tracking-tighter">$0.00</h3>
                <div class="flex gap-4 mt-10">
                    <button onclick="openModal('dep-modal')" class="flex-1 btn-primary py-4 rounded-2xl font-bold text-sm">Deposit</button>
                    <button onclick="openModal('wit-modal')" class="flex-1 bg-gray-900 text-white py-4 rounded-2xl font-bold text-sm">Withdraw</button>
                </div>
            </div>

            <!-- History -->
            <div class="glass p-10 rounded-[2.5rem] lg:col-span-2">
                <div class="flex justify-between items-center mb-6">
                    <h4 class="font-black text-lg">Live Node Activity</h4>
                    <span class="text-[10px] bg-blue-50 text-blue-600 px-3 py-1 rounded-full font-bold">REAL-TIME</span>
                </div>
                <div id="history" class="space-y-4">
                    <div class="flex justify-between items-center p-4 bg-gray-50 rounded-2xl border border-dashed border-gray-200">
                        <p class="text-xs font-medium text-gray-400 italic">No node activity detected yet...</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Investment Section -->
        <div class="section-fade">
            <div class="flex justify-between items-end mb-8">
                <div>
                    <h3 class="text-2xl font-black">Available Nodes</h3>
                    <p class="text-sm text-gray-400">Nodes start from just $5.00</p>
                </div>
                <i class="fa-solid fa-sliders text-gray-300 text-xl cursor-pointer"></i>
            </div>
            <div id="plans-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8"></div>
        </div>
    </div>

    <!-- GOD MODE MODAL (ADMIN) -->
    <div id="admin-sec" class="hidden fixed inset-0 bg-white z-[300] p-10 overflow-y-auto animate__animated animate__slideInUp">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-12">
                <h1 class="text-3xl font-black uppercase italic">NEXA <span class="text-blue-600">GOD MODE</span></h1>
                <button onclick="location.reload()" class="w-12 h-12 bg-gray-100 rounded-full flex items-center justify-center text-xl hover:rotate-90 transition"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                <div class="p-10 border-2 border-blue-50 rounded-[3rem] space-y-6">
                    <h3 class="text-xl font-bold mb-4 flex items-center gap-2"><i class="fa-solid fa-plus-circle text-blue-600"></i> Forge New Node</h3>
                    <input type="text" id="p-name" placeholder="Node Alias (e.g. Alpha-7)" class="w-full p-4 rounded-2xl bg-gray-50 outline-none border border-gray-100">
                    <input type="number" id="p-min" placeholder="Min Stake ($5.00)" class="w-full p-4 rounded-2xl bg-gray-50 outline-none border border-gray-100">
                    <input type="number" id="p-profit" placeholder="Daily Yield %" class="w-full p-4 rounded-2xl bg-gray-50 outline-none border border-gray-100">
                    <button onclick="addPlan()" class="w-full btn-primary py-5 rounded-2xl font-black">PUBLISH TO MAINNET</button>
                    
                    <div id="admin-plans" class="mt-10 space-y-3 pt-6 border-t border-gray-50"></div>
                </div>

                <div class="space-y-6">
                    <h3 class="text-xl font-bold flex items-center gap-2"><i class="fa-solid fa-bell text-yellow-500"></i> Pending Verifications</h3>
                    <div id="admin-reqs" class="space-y-4"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- MODALS: DEPOSIT -->
    <div id="dep-modal" class="hidden fixed inset-0 bg-white/80 backdrop-blur-md z-[200] flex items-center justify-center p-6">
        <div class="bg-white p-10 rounded-[3rem] w-full max-w-md shadow-2xl border border-gray-100 animate__animated animate__fadeInUp">
            <h3 class="text-2xl font-black mb-6">Deposit Capital</h3>
            <div class="p-6 bg-blue-50 rounded-3xl mb-6">
                <p class="text-[10px] font-black text-blue-600 uppercase mb-2">Transfer Gateway</p>
                <p class="text-sm font-bold opacity-70">Easypaisa: 03379827882</p>
                <p class="text-sm font-bold opacity-70 mt-1">SadaPay: 03705519562</p>
            </div>
            <input type="number" id="d-amt" placeholder="Amount ($)" class="w-full p-4 rounded-2xl bg-gray-50 mb-4 outline-none border border-gray-100">
            <input type="text" id="d-tid" placeholder="TID Code" class="w-full p-4 rounded-2xl bg-gray-50 mb-6 outline-none border border-gray-100">
            <button onclick="submitDep()" class="w-full btn-primary py-5 rounded-2xl font-black uppercase">Verify Deposit</button>
            <button onclick="closeModals()" class="w-full mt-4 text-xs font-bold text-gray-300">DISMISS</button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get, push, onValue, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // --- CORE NAVIGATION ---
        window.showSec = (id) => {
            ['auth-sec', 'main-sec', 'about-sec', 'admin-sec'].forEach(s => {
                const el = document.getElementById(s);
                if(el) el.classList.add('hidden');
            });
            document.getElementById(id + (id==='home'?'main':'') + '-sec').classList.remove('hidden');
        };

        const uid = localStorage.getItem('nexa_uid');
        if(uid) {
            document.getElementById('auth-sec').classList.add('hidden');
            document.getElementById('main-sec').classList.remove('hidden');
            document.getElementById('user-info').classList.remove('hidden');
            
            onValue(ref(db, 'users/' + uid), s => {
                const d = s.val();
                if(d) {
                    document.getElementById('dash-bal').innerText = `$${d.balance.toFixed(2)}`;
                    document.getElementById('top-bal').innerText = `$${d.balance.toFixed(2)}`;
                    document.getElementById('user-display').innerText = d.username;
                }
            });

            onValue(ref(db, 'plans'), s => {
                const list = document.getElementById('plans-list');
                list.innerHTML = "";
                s.forEach(p => {
                    const pd = p.val();
                    list.innerHTML += `
                    <div class="plan-card p-8 text-center animate__animated animate__fadeIn">
                        <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl mx-auto mb-6 flex items-center justify-center">
                            <i class="fa-solid fa-bolt text-lg"></i>
                        </div>
                        <p class="text-[10px] font-black text-gray-300 uppercase tracking-widest">${pd.name}</p>
                        <h5 class="text-4xl font-black text-gray-900 my-2">${pd.profit}%</h5>
                        <p class="text-[11px] text-gray-400 font-medium mb-8">Daily Network Yield</p>
                        <button onclick="invest(${pd.min})" class="w-full py-4 bg-gray-900 text-white rounded-2xl text-[10px] font-black uppercase tracking-widest hover:bg-blue-600 transition">Stake $${pd.min}</button>
                    </div>`;
                });
            });
        }

        // --- AUTH ---
        document.getElementById('login-form').onsubmit = async (e) => {
            e.preventDefault();
            const res = await signInAnonymously(auth);
            const uid = res.user.uid;
            const user = document.getElementById('user-id').value;
            const snap = await get(ref(db, 'users/' + uid));
            if(!snap.exists()) await set(ref(db, 'users/' + uid), { username: user, balance: 0 });
            localStorage.setItem('nexa_uid', uid);
            location.reload();
        };

        // --- GOD MODE (ADMIN) ---
        let taps = 0;
        document.getElementById('logo').onclick = () => {
            taps++;
            if(taps === 4) {
                const k = prompt("Enter Master Access Key:");
                if(k === "NEXA786") {
                    showSec('admin');
                    loadAdminData();
                }
            }
            setTimeout(() => taps = 0, 2000);
        };

        window.addPlan = () => {
            const name = document.getElementById('p-name').value;
            const min = document.getElementById('p-min').value;
            const profit = document.getElementById('p-profit').value;
            if(name && min && profit) {
                push(ref(db, 'plans'), { name, min, profit });
                alert("Node plan published sweetie!");
            }
        };

        function loadAdminData() {
            onValue(ref(db, 'plans'), s => {
                const list = document.getElementById('admin-plans');
                list.innerHTML = "";
                s.forEach(p => {
                    list.innerHTML += `<div class="flex justify-between items-center bg-gray-50 p-4 rounded-2xl border border-gray-100">
                        <span class="font-bold text-sm">${p.val().name}</span>
                        <button onclick="removePlan('${p.key}')" class="text-red-500 text-xs font-black uppercase">Remove</button>
                    </div>`;
                });
            });

            onValue(ref(db, 'requests/deposits'), s => {
                const list = document.getElementById('admin-reqs');
                list.innerHTML = "";
                s.forEach(r => {
                    const rd = r.val();
                    list.innerHTML += `<div class="bg-blue-50 p-6 rounded-[2rem] border border-blue-100">
                        <p class="text-xs font-black text-blue-600 mb-2">User ID: ${rd.uid.substring(0,8)}</p>
                        <p class="text-lg font-bold">$${rd.amt} <span class="text-[10px] text-gray-400 font-normal">via TID: ${rd.tid}</span></p>
                        <div class="flex gap-2 mt-4">
                            <button onclick="approveDep('${r.key}', '${rd.uid}', ${rd.amt})" class="bg-blue-600 text-white px-6 py-2 rounded-xl text-[10px] font-black uppercase">Approve</button>
                            <button onclick="rejectReq('${r.key}')" class="text-red-500 px-4 py-2 text-[10px] font-bold">Reject</button>
                        </div>
                    </div>`;
                });
            });
        }

        window.approveDep = async (key, userId, amt) => {
            const uRef = ref(db, 'users/' + userId);
            const snap = await get(uRef);
            if(snap.exists()){
                const newBal = snap.val().balance + parseFloat(amt);
                await update(uRef, { balance: newBal });
                await remove(ref(db, `requests/deposits/${key}`));
                alert("Funded sweetie!");
            }
        };

        window.removePlan = (key) => remove(ref(db, 'plans/' + key));
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.openModal = (id) => document.getElementById(id).classList.remove('hidden');
        window.closeModals = () => document.getElementById('dep-modal').classList.add('hidden');
        window.submitDep = () => {
            const amt = document.getElementById('d-amt').value;
            const tid = document.getElementById('d-tid').value;
            if(amt && tid) {
                push(ref(db, 'requests/deposits'), { uid: localStorage.getItem('nexa_uid'), amt, tid });
                alert("Verification request sent sweetie!");
                closeModals();
            }
        };

        window.invest = (min) => alert(`Sweetie, staking system is checking your $${min} node capacity...`);

    </script>
</body>
</html>
