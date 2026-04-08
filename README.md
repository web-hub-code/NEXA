<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA CLOUD | Next Gen Assets</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700;900&display=swap');
        body { font-family: 'Inter', sans-serif; background: #000; color: #fff; scroll-behavior: smooth; }
        
        /* High-End Glow Effects */
        .hero-glow { position: absolute; top: -10%; left: 50%; transform: translateX(-50%); width: 100%; height: 500px; background: radial-gradient(circle, rgba(99,102,241,0.15) 0%, rgba(0,0,0,0) 70%); z-index: -1; }
        .cloud-card { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.08); border-radius: 32px; transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .cloud-card:hover { border-color: rgba(99,102,241,0.5); transform: translateY(-5px); }
        
        /* Modern Button */
        .btn-primary { background: #fff; color: #000; font-weight: 800; border-radius: 16px; padding: 18px; transition: 0.3s; }
        .btn-primary:active { scale: 0.95; background: #6366f1; color: #fff; }
    </style>
</head>
<body class="pb-32">

    <div class="hero-glow"></div>

    <!-- Top Navigation -->
    <header class="p-6 flex justify-between items-center">
        <div class="flex items-center gap-2">
            <div class="w-8 h-8 bg-indigo-600 rounded-lg flex items-center justify-center rotate-45"><i class="fa-solid fa-cloud text-white -rotate-45 text-sm"></i></div>
            <span class="text-xl font-black tracking-tighter uppercase">Nexa<span class="text-indigo-500 italic">Cloud</span></span>
        </div>
        <div class="bg-indigo-500/10 px-4 py-2 rounded-full border border-indigo-500/20">
            <span class="text-[10px] font-bold text-indigo-400 uppercase tracking-widest">Balance: $2.50</span>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="p-6 text-center mt-4">
        <h1 class="text-4xl font-black leading-tight mb-4">Cloud Computing <br><span class="text-indigo-500">Earn Daily.</span></h1>
        <p class="text-slate-400 text-xs leading-relaxed px-4">Maximize your passive income with high-speed node clusters. Secure, decentralized, and 100% automated.</p>
    </section>

    <!-- Stats Row -->
    <div class="px-6 grid grid-cols-3 gap-4 mt-8">
        <div class="text-center">
            <h5 class="text-lg font-bold">12K+</h5>
            <p class="text-[8px] uppercase text-slate-500 font-bold">Active Nodes</p>
        </div>
        <div class="text-center border-x border-white/10">
            <h5 class="text-lg font-bold">$1.4M</h5>
            <p class="text-[8px] uppercase text-slate-500 font-bold">Total Paid</p>
        </div>
        <div class="text-center">
            <h5 class="text-lg font-bold">99.9%</h5>
            <p class="text-[8px] uppercase text-slate-500 font-bold">Uptime</p>
        </div>
    </div>

    <!-- Main Features (Nodes) -->
    <main class="p-6 space-y-6">
        
        <div class="cloud-card p-6">
            <div class="flex justify-between items-start mb-6">
                <div>
                    <h3 class="text-lg font-black italic uppercase">Standard Cluster</h3>
                    <p class="text-[10px] text-slate-500">Perfect for beginners</p>
                </div>
                <span class="text-indigo-500 font-black">$15.00</span>
            </div>
            
            <ul class="space-y-3 mb-8">
                <li class="flex items-center gap-3 text-[11px] font-medium text-slate-300"><i class="fa-solid fa-check text-green-500"></i> Daily Return: $0.75</li>
                <li class="flex items-center gap-3 text-[11px] font-medium text-slate-300"><i class="fa-solid fa-check text-green-500"></i> Cloud Hashrate: 1.2 TH/s</li>
                <li class="flex items-center gap-3 text-[11px] font-medium text-slate-300"><i class="fa-solid fa-check text-green-500"></i> 24/7 Monitoring</li>
            </ul>

            <button onclick="alert('Insufficient Balance! Please Top Up.')" class="btn-primary w-full text-[11px] uppercase tracking-[0.2em]">Deploy Node</button>
        </div>

        <!-- Secret Gamification Section -->
        <div class="cloud-card p-6 border-dashed border-2 border-indigo-500/30">
            <div class="flex items-center gap-4">
                <div class="w-12 h-12 bg-indigo-500 rounded-2xl flex items-center justify-center shadow-lg shadow-indigo-500/40">
                    <i class="fa-solid fa-gift text-xl"></i>
                </div>
                <div class="flex-1">
                    <h4 class="text-xs font-black uppercase">Daily Reward Wheel</h4>
                    <p class="text-[9px] text-slate-500 mt-1">Free spin for all VIP members</p>
                </div>
                <button class="bg-indigo-600 px-4 py-2 rounded-xl text-[10px] font-black uppercase">Spin</button>
            </div>
        </div>

    </main>

    <!-- Bottom Navigation (Floating Style) -->
    <div class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[90%] h-16 glass rounded-2xl flex justify-around items-center px-4 border border-white/10 shadow-2xl">
        <button class="text-indigo-500 text-lg"><i class="fa-solid fa-house-chimney"></i></button>
        <button class="text-slate-500 text-lg"><i class="fa-solid fa-chart-line"></i></button>
        <button class="text-slate-500 text-lg"><i class="fa-solid fa-wallet"></i></button>
        <button class="text-slate-500 text-lg"><i class="fa-solid fa-circle-user"></i></button>
    </div>

</body>
</html>
