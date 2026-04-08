<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Cloud Mining Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #F8FAFC; color: #0F172A; overflow-x: hidden; }
        .nexa-card { background: #fff; border: 1px solid #E2E8F0; border-radius: 28px; box-shadow: 0 4px 25px rgba(0,0,0,0.02); }
        .auth-screen { position: fixed; inset: 0; background: white; z-index: 1000; display: flex; flex-direction: column; padding: 2rem; }
        .hidden { display: none !important; }
        .nav-active { color: #2563EB !important; border-top: 3px solid #2563EB; border-radius: 0; }
        .mining-anim { height: 4px; background: #E2E8F0; border-radius: 10px; overflow: hidden; position: relative; }
        .mining-progress { position: absolute; height: 100%; background: #2563EB; animation: mine 2s infinite linear; }
        @keyframes mine { 0% { width: 0%; left: 0%; } 50% { width: 40%; } 100% { width: 0%; left: 100%; } }
    </style>
</head>
<body class="pb-32">

    <!-- AUTHENTICATION SCREENS -->
    <div id="auth-section" class="auth-screen">
        <div class="mt-10 mb-10 text-center">
            <div class="w-16 h-16 bg-blue-600 rounded-3xl mx-auto flex items-center justify-center shadow-xl shadow-blue-200 mb-4 rotate-12">
                <i class="fa-solid fa-cloud text-white text-3xl -rotate-12"></i>
            </div>
            <h1 class="text-3xl font-black tracking-tighter italic">NEXA<span class="text-blue-600">CLOUD</span></h1>
            <p class="text-slate-400 text-xs font-bold uppercase tracking-widest mt-2">Enterprise Mining Access</p>
        </div>

        <!-- Login Form -->
        <div id="login-form" class="space-y-4">
            <input type="email" id="log-email" placeholder="Email Address" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none focus:border-blue-500 transition-all">
            <input type="password" id="log-pass" placeholder="Password" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none focus:border-blue-500 transition-all">
            <button onclick="handleAuth('login')" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black uppercase tracking-widest shadow-lg">Login</button>
            <p class="text-center text-xs font-bold text-slate-500">Don't have an account? <span class="text-blue-600 cursor-pointer" onclick="toggleAuth()">Sign Up</span></p>
        </div>

        <!-- Signup Form -->
        <div id="signup-form" class="space-y-4 hidden">
            <input type="text" id="sig-name" placeholder="Full Name" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none focus:border-blue-500 transition-all">
            <input type="email" id="sig-email" placeholder="Email Address" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none focus:border-blue-500 transition-all">
            <input type="password" id="sig-pass" placeholder="Create Password" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none focus:border-blue-500 transition-all">
            <button onclick="handleAuth('signup')" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black uppercase tracking-widest shadow-lg">Create Account</button>
            <p class="text-center text-xs font-bold text-slate-500">Already a member? <span class="text-blue-600 cursor-pointer" onclick="toggleAuth()">Login</span></p>
        </div>
    </div>

    <!-- MAIN APP CONTENT -->
    <div id="main-app" class="hidden">
        <header class="p-6 flex justify-between items-center bg-white border-b border-slate-100 sticky top-0 z-50">
            <div class="flex items-center gap-2">
                <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center shadow-lg shadow-blue-100">
                    <i class="fa-solid fa-server text-white text-sm"></i>
                </div>
                <h1 class="text-xl font-black tracking-tighter">NEXA<span class="text-blue-600">CLOUD</span></h1>
            </div>
            <div class="text-right">
                <p class="text-[9px] font-black text-slate-400 uppercase">Available</p>
                <h2 id="balance-display" class="text-lg font-black text-slate-900">$2.00</h2>
            </div>
        </header>

        <main class="p-5 space-y-6">
            <!-- Daily Bonus -->
            <div class="nexa-card p-5 bg-gradient-to-r from-blue-600 to-indigo-700 text-white relative overflow-hidden">
                <div class="relative z-10">
                    <h4 class="text-xs font-black uppercase opacity-80">Daily Node Yield</h4>
                    <p class="text-lg font-bold mb-4">Claim $0.15 Bonus</p>
                    <button id="claim-btn" onclick="claimDaily()" class="bg-white text-blue-600 px-6 py-2 rounded-full font-black text-[10px] uppercase">Claim Now</button>
                </div>
                <i class="fa-solid fa-gift absolute -right-2 -bottom-2 text-white/10 text-7xl"></i>
            </div>

            <!-- Tabs Container -->
            <div id="tab-home" class="space-y-6">
                <h3 class="text-[11px] font-black uppercase tracking-widest text-slate-400 flex justify-between">
                    Mining Clusters <span>Live <i class="fa-solid fa-circle text-[6px] text-green-500 animate-pulse"></i></span>
                </h3>
                
                <!-- Node 1 -->
                <div class="nexa-card p-6">
                    <div class="flex justify-between items-start mb-6">
                        <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-bolt"></i></div>
                        <div class="text-right"><p class="text-xl font-black text-slate-900">$10.00</p><p class="text-[8px] font-bold text-slate-400 uppercase">Per Year</p></div>
                    </div>
                    <h4 class="font-black text-lg">Cloud Alpha v.1</h4>
                    <p class="text-[11px] text-slate-500 mb-4">Daily Profit: $0.50 • Power: 1.2 TH/s</p>
                    <div class="mining-anim mb-6"><div class="mining-progress"></div></div>
                    <button onclick="goToWallet()" class="w-full bg-slate-900 text-white p-4 rounded-2xl font-black uppercase text-[10px] tracking-widest shadow-xl">Activate Node</button>
                </div>
            </div>

            <div id="tab-team" class="hidden space-y-6 text-center">
                <div class="nexa-card p-8">
                    <i class="fa-solid fa-users-viewfinder text-5xl text-blue-600 mb-4"></i>
                    <h2 class="text-2xl font-black text-slate-900">Affiliate Team</h2>
                    <p class="text-xs text-slate-500 mt-2 mb-6 px-6">Earn 10% from every deposit your friends make. Grow your cloud network together!</p>
                    <div class="bg-slate-50 p-4 rounded-2xl border border-dashed border-slate-300">
                        <p class="text-[10px] font-bold text-slate-400 uppercase mb-2">Your Invite Code</p>
                        <p class="text-lg font-black text-blue-600">NEXA-786-PRO</p>
                    </div>
                </div>
            </div>

            <div id="tab-wallet" class="hidden space-y-6">
                <div class="nexa-card p-6 bg-slate-900 text-white">
                    <p class="text-[10px] font-bold text-slate-400 uppercase">Total Assets</p>
                    <h1 class="text-4xl font-black mt-1">$2.00</h1>
                    <div class="flex gap-4 mt-6">
                        <button onclick="alert('Scan JazzCash/EasyPaisa QR in group!')" class="flex-1 bg-blue-600 p-3 rounded-xl font-black text-[10px] uppercase">Deposit</button>
                        <button onclick="alert('Min withdrawal $10.00')" class="flex-1 bg-white/10 p-3 rounded-xl font-black text-[10px] uppercase border border-white/10">Withdraw</button>
                    </div>
                </div>
            </div>
        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 bg-white shadow-2xl rounded-[2.5rem] border border-slate-100 flex justify-around items-center px-4 z-50">
            <button onclick="switchTab('home')" class="flex flex-col items-center nav-active h-full justify-center w-1/4"><i class="fa-solid fa-server"></i><span class="text-[8px] font-black uppercase mt-1">Nodes</span></button>
            <button onclick="switchTab('team')" class="flex flex-col items-center text-slate-400 h-full justify-center w-1/4"><i class="fa-solid fa-users"></i><span class="text-[8px] font-black uppercase mt-1">Team</span></button>
            <button onclick="switchTab('wallet')" class="flex flex-col items-center text-slate-400 h-full justify-center w-1/4"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-black uppercase mt-1">Wallet</span></button>
            <button onclick="handleLogout()" class="flex flex-col items-center text-slate-400 h-full justify-center w-1/4"><i class="fa-solid fa-right-from-bracket"></i><span class="text-[8px] font-black uppercase mt-1">Exit</span></button>
        </nav>
    </div>

    <script>
        // AUTHENTICATION LOGIC (Dummy Version)
        function toggleAuth() {
            document.getElementById('login-form').classList.toggle('hidden');
            document.getElementById('signup-form').classList.toggle('hidden');
        }

        function handleAuth(type) {
            // Sweetie, yahan hum fake login karwa rahe hain abhi
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');
            alert(`Sweetie, Welcome to Nexa! You are now logged in. 💋`);
        }

        function handleLogout() {
            document.getElementById('auth-section').classList.remove('hidden');
            document.getElementById('main-app').classList.add('hidden');
        }

        // TAB SYSTEM
        function switchTab(tab) {
            document.getElementById('tab-home').classList.add('hidden');
            document.getElementById('tab-team').classList.add('hidden');
            document.getElementById('tab-wallet').classList.add('hidden');
            document.getElementById('tab-'+tab).classList.remove('hidden');
            
            // UI Active State
            const buttons = document.querySelectorAll('nav button');
            buttons.forEach(btn => btn.classList.remove('nav-active', 'text-blue-600'));
            buttons.forEach(btn => btn.classList.add('text-slate-400'));
            event.currentTarget.classList.add('nav-active', 'text-blue-600');
        }

        function claimDaily() {
            const btn = document.getElementById('claim-btn');
            btn.innerText = "Claimed!";
            btn.classList.add('bg-slate-300', 'text-slate-500');
            btn.disabled = true;
            document.getElementById('balance-display').innerText = "$2.15";
            alert("Sweetie, $0.15 added to your balance! 👑");
        }

        function goToWallet() {
            switchTab('wallet');
            alert("Please deposit $10 to activate Alpha v.1 Cluster.");
        }
    </script>
</body>
</html>
