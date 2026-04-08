<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ELITE | Premium Investment</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;500;700&display=swap');
        :root { --primary: #6366f1; --accent: #a855f7; --bg: #030712; }
        body { font-family: 'Space Grotesk', sans-serif; background: var(--bg); color: #f3f4f6; overflow-x: hidden; }
        
        /* Modern Glass UI */
        .glass-card { background: rgba(31, 41, 55, 0.5); backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,0.1); border-radius: 28px; }
        .neon-glow { box-shadow: 0 0 20px rgba(99, 102, 241, 0.3); }
        .gradient-text { background: linear-gradient(to right, #818cf8, #c084fc); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        
        /* Attractive Spin Wheel */
        #wheel-container { position: relative; width: 300px; height: 300px; margin: 0 auto; border: 10px solid #1f2937; border-radius: 50%; box-shadow: 0 0 40px rgba(0,0,0,0.5), inset 0 0 20px rgba(255,255,255,0.05); }
        #wheel { width: 100%; height: 100%; border-radius: 50%; transition: transform 5s cubic-bezier(0.15, 0, 0.15, 1); position: relative; overflow: hidden; }
        .wheel-segment { position: absolute; width: 50%; height: 50%; transform-origin: 100% 100%; display: flex; justify-content: center; align-items: flex-start; padding-top: 20px; font-weight: 700; color: white; border: 1px solid rgba(0,0,0,0.1); }
        #wheel-pointer { position: absolute; top: -15px; left: 50%; transform: translateX(-50%); z-index: 50; filter: drop-shadow(0 5px 10px rgba(0,0,0,0.5)); color: #fbbf24; font-size: 40px; }
        
        .tab-btn.active { color: #818cf8; position: relative; }
        .tab-btn.active::after { content: ''; position: absolute; bottom: -10px; left: 25%; width: 50%; height: 3px; background: #818cf8; border-radius: 10px; }
    </style>
</head>
<body class="pb-32">

    <!-- Top Status Bar -->
    <div class="p-4 flex justify-between items-center glass-card m-4 mt-6 neon-glow">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-600 to-purple-600 flex items-center justify-center font-bold text-white shadow-lg">N</div>
            <div>
                <h4 id="display-name" class="text-sm font-bold">Investo_User</h4>
                <div class="flex items-center gap-1"><span class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></span><span class="text-[8px] uppercase tracking-tighter opacity-60">Verified VIP 1</span></div>
            </div>
        </div>
        <div class="text-right">
            <p class="text-[9px] uppercase font-bold opacity-50">Global Balance</p>
            <h2 id="user-bal" class="text-lg font-black gradient-text">$0.00</h2>
        </div>
    </div>

    <!-- Main Content -->
    <div id="main-app">
        
        <!-- HOME TAB -->
        <div id="tab-home" class="tab-content p-5 space-y-6">
            <!-- Jackpot Counter -->
            <div class="text-center py-4">
                <p class="text-[10px] font-bold text-indigo-400 uppercase tracking-[0.2em]">Current Reward Pool</p>
                <h1 class="text-4xl font-black italic">$148,290.<span class="text-sm">92</span></h1>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div class="glass-card p-5 text-center border-b-4 border-indigo-500" onclick="switchTab('wallet')">
                    <i class="fa-solid fa-arrow-down-long text-indigo-400 mb-2"></i>
                    <p class="text-[10px] font-bold uppercase">Deposit</p>
                </div>
                <div class="glass-card p-5 text-center border-b-4 border-purple-500" onclick="switchTab('wallet')">
                    <i class="fa-solid fa-paper-plane text-purple-400 mb-2"></i>
                    <p class="text-[10px] font-bold uppercase">Withdraw</p>
                </div>
            </div>

            <!-- Referral Link Box -->
            <div class="glass-card p-6 bg-gradient-to-r from-indigo-900/20 to-transparent">
                <h3 class="text-xs font-bold mb-3 uppercase tracking-wider text-indigo-300">Affiliate Network</h3>
                <div class="flex items-center gap-3 bg-black/40 p-3 rounded-2xl border border-white/5">
                    <code id="ref-code" class="flex-1 text-xs font-bold text-indigo-400 tracking-widest">NEXA-786X</code>
                    <button onclick="copyRef()" class="text-[10px] font-black uppercase text-indigo-300">Copy</button>
                </div>
                <p class="text-[9px] mt-3 opacity-50 italic">Get 10% from every deposit your friends make, sweetie!</p>
            </div>
        </div>

        <!-- SPIN TAB (Modern Casino Design) -->
        <div id="tab-spin" class="tab-content hidden p-5 text-center">
            <div class="mb-10">
                <h2 class="text-2xl font-black italic uppercase">Mega <span class="text-amber-400">Wheel</span></h2>
                <p class="text-[10px] opacity-60">Spin the wheel to unlock your daily fortune</p>
            </div>

            <div id="wheel-container">
                <div id="wheel-pointer"><i class="fa-solid fa-location-arrow fa-rotate-180"></i></div>
                <div id="wheel"></div>
                <div class="absolute inset-0 m-auto w-12 h-12 bg-white rounded-full shadow-2xl flex items-center justify-center z-40 border-4 border-gray-800">
                    <div class="w-3 h-3 bg-indigo-600 rounded-full animate-ping"></div>
                </div>
            </div>

            <button onclick="handleSpin()" id="spin-btn" class="w-full mt-12 bg-gradient-to-r from-indigo-600 to-purple-600 p-5 rounded-3xl font-black uppercase tracking-[0.2em] shadow-lg shadow-indigo-500/20 active:scale-95 transition-all">
                Execute Spin ($0.50)
            </button>
        </div>

        <!-- WALLET TAB -->
        <div id="tab-wallet" class="tab-content hidden p-5 space-y-6">
            <div class="glass-card p-6 border-l-4 border-indigo-500">
                <h4 class="text-xs font-black uppercase text-indigo-400 mb-4">Secure Deposit</h4>
                <div class="grid grid-cols-2 gap-2 mb-4">
                    <div class="bg-black/40 p-3 rounded-xl border border-white/5">
                        <p class="text-[8px] opacity-50">SadaPay/JazzCash</p>
                        <p class="text-[10px] font-bold">03705519562</p>
                    </div>
                    <div class="bg-black/40 p-3 rounded-xl border border-white/5">
                        <p class="text-[8px] opacity-50">EasyPaisa</p>
                        <p class="text-[10px] font-bold">03379827882</p>
                    </div>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount in USD" class="mb-3 block w-full bg-zinc-900 border-none rounded-xl p-4 text-sm">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="mb-4 block w-full bg-zinc-900 border-none rounded-xl p-4 text-sm">
                <button onclick="submitDep()" class="w-full bg-indigo-600 p-4 rounded-2xl font-black uppercase text-xs tracking-widest">Verify Payment</button>
            </div>
            
            <div id="history-list" class="space-y-3">
                <!-- Fake history will go here -->
            </div>
        </div>

    </div>

    <!-- Bottom Navigation -->
    <nav class="fixed bottom-6 left-6 right-6 h-20 glass-card flex justify-around items-center px-4 z-50">
        <button onclick="switchTab('home')" class="tab-btn flex flex-col items-center text-zinc-500 active"><i class="fa-solid fa-grid-2 text-xl"></i><span class="text-[8px] font-bold mt-1 uppercase">Vault</span></button>
        <button onclick="switchTab('spin')" class="tab-btn flex flex-col items-center text-zinc-500"><i class="fa-solid fa-circle-dot text-xl"></i><span class="text-[8px] font-bold mt-1 uppercase">Wheel</span></button>
        <button onclick="switchTab('wallet')" class="tab-btn flex flex-col items-center text-zinc-500"><i class="fa-solid fa-wallet text-xl"></i><span class="text-[8px] font-bold mt-1 uppercase">Assets</span></button>
    </nav>

    <script type="module">
        // --- LOGIC STARTS HERE ---
        const prizes = [
            { label: "$50", color: "#6366f1", val: 50 }, { label: "$0.01", color: "#1f2937", val: 0.01 },
            { label: "$5", color: "#8b5cf6", val: 5 }, { label: "$0.05", color: "#111827", val: 0.05 },
            { label: "JACKPOT", color: "#fbbf24", val: 100 }, { label: "$0.00", color: "#1f2937", val: 0 },
            { label: "$1", color: "#4f46e5", val: 1 }, { label: "$0.02", color: "#111827", val: 0.02 }
        ];

        function initWheel() {
            const wheel = document.getElementById('wheel');
            wheel.innerHTML = prizes.map((p, i) => `
                <div class="wheel-segment" style="transform: rotate(${i*45}deg) skewY(-45deg); background: ${p.color};">
                    <span style="transform: rotate(-22deg) translateY(10px); display: block;">${p.label}</span>
                </div>
            `).join('');
        }

        window.switchTab = (tab) => {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active', 'text-indigo-400'));
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
            event.currentTarget.classList.add('active', 'text-indigo-400');
        };

        // Initialize Wheel
        initWheel();

        // Fake Trust Ticker
        setInterval(() => {
            const names = ["Ayesha", "Hamza", "Sidra", "Khan_786", "M.Nazim"];
            const name = names[Math.floor(Math.random()*names.length)];
            const amt = (Math.random()*5000).toFixed(0);
            const list = document.getElementById('history-list');
            const item = `<div class="glass-card p-3 flex justify-between items-center animate-bounce text-[10px] border-l-2 border-green-500">
                <span class="opacity-60">${name} withdrawn via JazzCash</span>
                <span class="font-bold text-green-400">+Rs ${amt}</span>
            </div>`;
            list.insertAdjacentHTML('afterbegin', item);
            if(list.children.length > 4) list.lastElementChild.remove();
        }, 10000);

        window.copyRef = () => { alert("Empire Link Copied, sweetie! 💋"); };
    </script>
</body>
</html>
