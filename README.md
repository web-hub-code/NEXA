<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Cloud Computing Platform</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background-color: #F8FAFC; 
            color: #0F172A; 
            margin: 0;
        }

        /* Cloud-Node Style Soft Cards */
        .nexa-card {
            background: #ffffff;
            border: 1px solid #E2E8F0;
            border-radius: 24px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.03);
            transition: all 0.3s ease;
        }
        .nexa-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.06);
            border-color: #CBD5E1;
        }

        /* Modern Blue Button */
        .btn-blue {
            background: #2563EB;
            color: white;
            font-weight: 700;
            border-radius: 16px;
            padding: 14px;
            text-align: center;
            display: block;
            width: 100%;
            transition: 0.3s;
            box-shadow: 0 4px 12px rgba(37, 99, 235, 0.2);
        }
        .btn-blue:active { scale: 0.96; background: #1D4ED8; }

        /* Fake Live Ticker */
        .ticker-wrap {
            background: #F1F5F9;
            padding: 8px 0;
            border-bottom: 1px solid #E2E8F0;
            overflow: hidden;
            font-size: 11px;
            font-weight: 600;
            color: #64748B;
        }
    </style>
</head>
<body class="pb-28">

    <!-- Top Info Ticker -->
    <div class="ticker-wrap text-center">
        <span class="inline-flex items-center gap-2">
            <span class="w-2 h-2 bg-green-500 rounded-full"></span>
            Global Cloud Network: ACTIVE • Total Nodes: 14,290 • Latest Payout: $42.50
        </span>
    </div>

    <!-- Header -->
    <header class="p-6 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-md z-50 border-b border-slate-100">
        <div class="flex items-center gap-2">
            <div class="w-9 h-9 bg-blue-600 rounded-xl flex items-center justify-center shadow-lg shadow-blue-200">
                <i class="fa-solid fa-cloud text-white text-sm"></i>
            </div>
            <h1 class="text-xl font-black tracking-tighter text-slate-900">NEXA<span class="text-blue-600 italic">CLOUD</span></h1>
        </div>
        <div class="text-right">
            <p class="text-[9px] font-extrabold text-slate-400 uppercase tracking-widest leading-none">Your Assets</p>
            <h2 class="text-lg font-black text-slate-900 mt-1">$0.00</h2>
        </div>
    </header>

    <main class="p-6 space-y-6">
        
        <!-- Hero Section -->
        <section class="text-center py-4">
            <h2 class="text-3xl font-black text-slate-900 leading-tight">Decentralized <br>Cloud Mining.</h2>
            <p class="text-slate-500 text-[13px] mt-2 px-4 font-medium">Earn automated rewards by deploying high-speed computational clusters.</p>
        </section>

        <!-- Stats Bento Grid -->
        <div class="grid grid-cols-2 gap-4">
            <div class="nexa-card p-5">
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Active Pool</p>
                <h4 class="text-xl font-black text-blue-600">$142.9K</h4>
            </div>
            <div class="nexa-card p-5">
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Global Users</p>
                <h4 class="text-xl font-black text-slate-900">8,500+</h4>
            </div>
        </div>

        <!-- Node Selection -->
        <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 pt-4 px-1">Available Clusters</h3>

        <!-- Node Card 1 -->
        <div class="nexa-card p-6 overflow-hidden relative">
            <div class="flex justify-between items-center mb-6">
                <div class="w-12 h-12 bg-blue-50 rounded-2xl flex items-center justify-center text-blue-600 text-xl">
                    <i class="fa-solid fa-bolt"></i>
                </div>
                <span class="text-[10px] font-black bg-blue-600/10 text-blue-600 px-3 py-1 rounded-full uppercase italic">Alpha v.1</span>
            </div>
            <h4 class="text-xl font-extrabold text-slate-900">Core Starter</h4>
            <div class="flex justify-between items-center mt-2 pb-6 border-b border-slate-50">
                <p class="text-xs font-semibold text-slate-500 italic">Profit: $0.75 / Day</p>
                <p class="text-lg font-black text-slate-900">$15.00</p>
            </div>
            <button onclick="alert('Sweetie, top up to activate your first node!')" class="btn-blue mt-6">Deploy Cluster</button>
        </div>

        <!-- Node Card 2 -->
        <div class="nexa-card p-6 border-l-4 border-indigo-500">
            <div class="flex justify-between items-center mb-6">
                <div class="w-12 h-12 bg-indigo-50 rounded-2xl flex items-center justify-center text-indigo-600 text-xl">
                    <i class="fa-solid fa-microchip"></i>
                </div>
                <span class="text-[10px] font-black bg-indigo-600/10 text-indigo-600 px-3 py-1 rounded-full uppercase italic">Pro v.5</span>
            </div>
            <h4 class="text-xl font-extrabold text-slate-900">Elite Computing</h4>
            <div class="flex justify-between items-center mt-2 pb-6 border-b border-slate-50">
                <p class="text-xs font-semibold text-slate-500 italic">Profit: $3.20 / Day</p>
                <p class="text-lg font-black text-slate-900">$50.00</p>
            </div>
            <button onclick="alert('Sweetie, top up to activate!')" class="btn-blue mt-6 bg-slate-900 shadow-slate-200">Deploy Cluster</button>
        </div>

    </main>

    <!-- Floating Navigation Bar -->
    <nav class="fixed bottom-6 left-6 right-6 h-20 bg-white/90 backdrop-blur-xl rounded-[2.5rem] flex justify-around items-center px-6 z-50 shadow-[0_20px_50px_rgba(0,0,0,0.1)] border border-slate-100">
        <button class="flex flex-col items-center text-blue-600"><i class="fa-solid fa-server text-xl"></i><span class="text-[9px] font-black mt-1 uppercase">Nodes</span></button>
        <button class="flex flex-col items-center text-slate-300"><i class="fa-solid fa-chart-pie text-xl"></i><span class="text-[9px] font-black mt-1 uppercase">Stats</span></button>
        <button class="flex flex-col items-center text-slate-300"><i class="fa-solid fa-wallet text-xl"></i><span class="text-[9px] font-black mt-1 uppercase">Wallet</span></button>
        <button class="flex flex-col items-center text-slate-300"><i class="fa-solid fa-circle-user text-xl"></i><span class="text-[9px] font-black mt-1 uppercase">User</span></button>
    </nav>

</body>
</html>
