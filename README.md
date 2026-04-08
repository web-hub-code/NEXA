<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA ELITE | Global Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;900&display=swap');
        :root { --primary: #6366f1; --bg: #020617; }
        body { font-family: 'Outfit', sans-serif; background: var(--bg); color: #f8fafc; }
        
        .glass { background: rgba(15, 23, 42, 0.8); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.05); }
        .node-card { background: linear-gradient(145deg, #1e293b, #0f172a); border-radius: 24px; border: 1px solid rgba(255,255,255,0.03); }
        .mining-anim { animation: pulse-blue 2s infinite; }
        @keyframes pulse-blue { 0% { box-shadow: 0 0 0 0 rgba(99, 102, 241, 0.4); } 70% { box-shadow: 0 0 0 15px rgba(99, 102, 241, 0); } 100% { box-shadow: 0 0 0 0 rgba(99, 102, 241, 0); } }
        
        #wheel-container { position: relative; width: 280px; height: 280px; margin: auto; }
        #wheel { width: 100%; height: 100%; border-radius: 50%; transition: transform 5s cubic-bezier(0.15, 0, 0.15, 1); border: 8px solid #1e293b; }
        .wheel-segment { position: absolute; width: 50%; height: 50%; transform-origin: 100% 100%; display: flex; justify-content: center; align-items: flex-start; padding-top: 15px; font-weight: 800; font-size: 10px; color: white; }
    </style>
</head>
<body class="pb-32">

    <!-- Header Section -->
    <div class="p-6 flex justify-between items-center bg-slate-900/50 border-b border-white/5">
        <div>
            <h1 class="text-2xl font-black tracking-tighter italic">NEXA<span class="text-indigo-500">ELITE</span></h1>
            <div class="flex items-center gap-2 mt-1">
                <span class="w-2 h-2 bg-green-500 rounded-full animate-ping"></span>
                <span class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Server: HK-Active</span>
            </div>
        </div>
        <div class="text-right">
            <p class="text-[9px] font-black text-indigo-400 uppercase">Available Assets</p>
            <h2 id="user-bal" class="text-xl font-black text-white">$0.00</h2>
        </div>
    </div>

    <!-- Main Viewport -->
    <main id="app-content">
        
        <!-- HOME TAB (Mining Nodes) -->
        <div id="tab-home" class="tab-content p-5 space-y-6">
            <div class="flex items-center justify-between">
                <h3 class="font-black text-sm uppercase tracking-tighter">Mining Nodes <span class="text-indigo-500">(v4.0)</span></h3>
                <i class="fa-solid fa-microchip text-indigo-500 animate-pulse"></i>
            </div>

            <!-- Node 1 -->
            <div class="node-card p-5 relative overflow-hidden group">
                <div class="flex justify-between items-start mb-4">
                    <div>
                        <h4 class="font-black text-lg">Cluster V.1 <span class="text-[10px] bg-indigo-500/20 text-indigo-400 px-2 py-0.5 rounded ml-2 italic">STARTER</span></h4>
                        <p class="text-[10px] text-slate-400 mt-1">Daily Profit: $0.50 | 365 Days</p>
                    </div>
                    <div class="text-right">
                        <p class="text-xs font-black text-indigo-400">$10.00</p>
                        <p class="text-[8px] opacity-40 uppercase">Price</p>
                    </div>
                </div>
                <button onclick="buyNode('V.1', 10)" class="w-full bg-indigo-600 p-3 rounded-xl text-[11px] font-black uppercase tracking-widest hover:bg-indigo-500 transition-colors">Activate Node</button>
            </div>

            <!-- Node 2 -->
            <div class="node-card p-5 relative overflow-hidden border-t-2 border-amber-500/50">
                <div class="flex justify-between items-start mb-4">
                    <div>
                        <h4 class="font-black text-lg">Neon Core V.5 <span class="text-[10px] bg-amber-500/20 text-amber-500 px-2 py-0.5 rounded ml-2 italic">POPULAR</span></h4>
                        <p class="text-[10px] text-slate-400 mt-1">Daily Profit: $3.20 | 365 Days</p>
                    </div>
                    <div class="text-right">
                        <p class="text-xs font-black text-amber-500">$50.00</p>
                        <p class="text-[8px] opacity-40 uppercase">Price</p>
                    </div>
                </div>
                <button onclick="buyNode('V.5', 50)" class="w-full bg-amber-600 p-3 rounded-xl text-[11px] font-black uppercase tracking-widest">Activate Node</button>
            </div>

            <!-- Referral Empire Section -->
            <div class="p-6 glass rounded-3xl mt-10 border-dashed border-2 border-indigo-500/30">
                <div class="flex items-center gap-4 mb-4">
                    <div class="w-12 h-12 rounded-2xl bg-indigo-500/10 flex items-center justify-center text-indigo-400 text-xl"><i class="fa-solid fa-users-rays"></i></div>
                    <div>
                        <h4 class="font-bold text-xs">Affiliate Empire</h4>
                        <p class="text-[9px] text-slate-400">Invite friends and get 15% instant</p>
                    </div>
                </div>
                <div class="flex gap-2">
                    <div id="ref-code" class="flex-1 bg-black/40 p-3 rounded-xl text-xs font-mono text-indigo-300 border border-white/5">NEXA-WAIT...</div>
                    <button onclick="copyRef()" class="bg-white/5 px-4 rounded-xl text-[10px] font-bold uppercase">Copy</button>
                </div>
            </div>
        </div>

        <!-- SPIN TAB -->
        <div id="tab-spin" class="tab-content hidden p-6 text-center space-y-10">
            <div>
                <h2 class="text-2xl font-black italic">ELITE <span class="text-indigo-500 font-normal">SPIN</span></h2>
                <p class="text-[10px] text-slate-500 mt-1 uppercase tracking-widest">Provably Fair Algorithm</p>
            </div>
            
            <div id="wheel-container">
                <div class="absolute -top-6 left-1/2 -translate-x-1/2 z-50 text-indigo-500 text-4xl"><i class="fa-solid fa-sort-down"></i></div>
                <div id="wheel" class="relative overflow-hidden"></div>
            </div>

            <button onclick="handleSpin()" class="w-full bg-gradient-to-r from-indigo-600 to-purple-600 p-5 rounded-2xl font-black uppercase tracking-[0.3em] shadow-lg shadow-indigo-500/20">Spin Wheel ($0.50)</button>
        </div>

        <!-- ASSETS TAB -->
        <div id="tab-assets" class="tab-content hidden p-5 space-y-6">
            <div class="grid grid-cols-2 gap-4">
                <div onclick="switchTab('deposit')" class="node-card p-6 text-center group cursor-pointer">
                    <i class="fa-solid fa-arrow-down text-indigo-400 mb-2 text-xl group-hover:translate-y-1 transition-transform"></i>
                    <p class="text-[10px] font-black uppercase">Top Up</p>
                </div>
                <div onclick="switchTab('withdraw')" class="node-card p-6 text-center group cursor-pointer">
                    <i class="fa-solid fa-arrow-up text-purple-400 mb-2 text-xl group-hover:-translate-y-1 transition-transform"></i>
                    <p class="text-[10px] font-black uppercase">Payout</p>
                </div>
            </div>

            <div class="glass p-6 rounded-3xl space-y-4">
                <h4 class="text-xs font-black uppercase tracking-widest text-slate-500">Active Transactions</h4>
                <div id="history-list" class="space-y-3">
                    <p class="text-[10px] text-center opacity-30 italic">No recent movements...</p>
                </div>
            </div>
        </div>
    </main>

    <!-- Navigation Bar -->
    <nav class="fixed bottom-6 left-6 right-6 h-20 glass rounded-[2.5rem] flex justify-around items-center px-6 z-50 shadow-2xl">
        <button onclick="switchTab('home')" class="nav-btn text-indigo-500"><i class="fa-solid fa-house-chimney text-lg"></i></button>
        <button onclick="switchTab('spin')" class="nav-btn text-slate-500"><i class="fa-solid fa-dharmachakra text-lg"></i></button>
        <button onclick="switchTab('assets')" class="nav-btn text-slate-500"><i class="fa-solid fa-wallet text-lg"></i></button>
        <button onclick="openAdmin()" class="nav-btn text-slate-500"><i class="fa-solid fa-gear text-lg"></i></button>
    </nav>

    <script type="module">
        // --- PRECONFIGURED DATA ---
        const prizes = [
            { label: "$50", val: 50, col: "#6366f1" }, { label: "$0.01", val: 0.01, col: "#0f172a" },
            { label: "$5", val: 5, col: "#8b5cf6" }, { label: "$0.05", val: 0.05, col: "#020617" },
            { label: "MEGA", val: 100, col: "#f59e0b" }, { label: "MISS", val: 0, col: "#0f172a" },
            { label: "$1", val: 1, col: "#4f46e5" }, { label: "$0.02", val: 0.02, col: "#020617" }
        ];

        // Initialization
        window.onload = () => {
            initWheel();
            startFakeHype();
            // Simulating user data
            document.getElementById('ref-code').innerText = "NEXA-ELITE-" + Math.random().toString(36).substring(7).toUpperCase();
        };

        function initWheel() {
            const wheel = document.getElementById('wheel');
            wheel.innerHTML = prizes.map((p, i) => `
                <div class="wheel-segment" style="transform: rotate(${i*45}deg) skewY(-45deg); background: ${p.col};">
                    <span style="transform: rotate(-22deg) translateY(10px);">${p.label}</span>
                </div>
            `).join('');
        }

        window.switchTab = (tab) => {
            document.querySelectorAll('.tab-content').forEach(t => t.classList.add('hidden'));
            document.getElementById(`tab-${tab}`).classList.remove('hidden');
            // Logic to handle icon colors could be added here
        };

        window.buyNode = (version, price) => {
            alert(`Sweetie, is Node ${version} ko activate karne ke liye pehle wallet mein $${price} deposit karein! 😉`);
            switchTab('assets');
        };

        function startFakeHype() {
            setInterval(() => {
                const logs = ["Zeeshan won $1.00", "New Node V.1 Active", "Withdrawal Rs 1,200 Processed", "M.Ali joined via Link"];
                const list = document.getElementById('history-list');
                const log = logs[Math.floor(Math.random()*logs.length)];
                const html = `<div class="flex justify-between items-center text-[9px] bg-white/5 p-2 rounded-lg animate-fade-in border-l-2 border-indigo-500">
                    <span class="opacity-60">${log}</span>
                    <span class="text-indigo-400 font-bold">JUST NOW</span>
                </div>`;
                list.insertAdjacentHTML('afterbegin', html);
                if(list.children.length > 5) list.lastElementChild.remove();
            }, 8000);
        }

        window.copyRef = () => { alert("Elite Invite Link Copied! 💋"); };
    </script>
</body>
</html>
