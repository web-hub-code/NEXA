<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Enterprise Cloud Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #F8FAFC; color: #0F172A; }
        
        .nexa-card { background: #fff; border: 1px solid #E2E8F0; border-radius: 28px; box-shadow: 0 4px 25px rgba(0,0,0,0.02); transition: 0.3s; }
        .mining-bar { height: 6px; background: #E2E8F0; border-radius: 10px; overflow: hidden; position: relative; }
        .mining-progress { position: absolute; height: 100%; background: linear-gradient(90deg, #2563EB, #60A5FA); animation: mine 3s infinite linear; }
        
        @keyframes mine { 0% { width: 0%; left: 0%; } 50% { width: 30%; } 100% { width: 0%; left: 100%; } }
        
        .payout-glow { animation: glow 2s infinite alternate; }
        @keyframes glow { from { text-shadow: 0 0 5px #2563EB; } to { text-shadow: 0 0 15px #60A5FA; } }
        
        .nav-active { color: #2563EB !important; border-top: 3px solid #2563EB; border-radius: 0; }
    </style>
</head>
<body class="pb-32">

    <div class="bg-blue-600 text-white text-[10px] py-2 px-6 flex justify-between font-bold uppercase tracking-tighter">
        <span>Cloud Hashrate: 450.2 TH/s</span>
        <span class="payout-glow text-amber-300">Total Payout: $1,429,201.05</span>
    </div>

    <header class="p-6 flex justify-between items-center bg-white/80 backdrop-blur-md sticky top-0 z-50 border-b border-slate-100">
        <div class="flex items-center gap-2">
            <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center shadow-lg shadow-blue-200">
                <i class="fa-solid fa-server text-white"></i>
            </div>
            <h1 class="text-xl font-black tracking-tighter italic">NEXA<span class="text-blue-600">CLOUD</span></h1>
        </div>
        <div class="text-right">
            <p class="text-[9px] font-black text-slate-400 uppercase">My Wallet</p>
            <h2 id="balance" class="text-lg font-black text-slate-900">$2.00</h2>
        </div>
    </header>

    <main class="p-5 space-y-6">

        <div class="nexa-card p-5 bg-gradient-to-br from-blue-50 to-white border-blue-100">
            <div class="flex justify-between items-center mb-4">
                <div>
                    <h4 class="text-sm font-black text-blue-900">Current Level: <span class="text-blue-600 italic uppercase">Basic User</span></h4>
                    <p class="text-[10px] text-slate-500 font-bold">Upgrade to VIP for 2x Daily Profit</p>
                </div>
                <div class="w-10 h-10 rounded-full border-2 border-blue-200 flex items-center justify-center font-black text-blue-600 text-xs">0%</div>
            </div>
            <div class="mining-bar"><div class="mining-progress"></div></div>
        </div>

        <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 px-1">Available Mining Power</h3>

        <div class="nexa-card p-6 border-b-4 border-blue-500">
            <div class="flex justify-between items-start mb-6">
                <div>
                    <h4 class="text-xl font-black text-slate-900">Cloud Node Alpha</h4>
                    <p class="text-[10px] text-blue-500 font-bold uppercase italic mt-1">Recommended for beginners</p>
                </div>
                <div class="text-right">
                    <p class="text-lg font-black text-slate-900">$10.00</p>
                    <p class="text-[8px] text-slate-400 uppercase font-black">Contract Fee</p>
                </div>
            </div>
            <div class="grid grid-cols-2 gap-4 mb-6">
                <div class="bg-slate-50 p-3 rounded-2xl">
                    <p class="text-[9px] text-slate-400 font-bold uppercase">Daily Profit</p>
                    <p class="text-sm font-black text-blue-600">$0.50</p>
                </div>
                <div class="bg-slate-50 p-3 rounded-2xl">
                    <p class="text-[9px] text-slate-400 font-bold uppercase">Duration</p>
                    <p class="text-sm font-black text-slate-800">360 Days</p>
                </div>
            </div>
            <button onclick="alert('Sweetie, please deposit $10 to activate this node!')" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black uppercase text-[11px] tracking-widest shadow-lg shadow-blue-200 active:scale-95 transition-all">Activate Cloud Power</button>
        </div>

        <div class="nexa-card p-6 border-b-4 border-slate-900">
            <div class="flex justify-between items-start mb-6">
                <div>
                    <h4 class="text-xl font-black text-slate-900">Enterprise Cluster</h4>
                    <p class="text-[10px] text-indigo-500 font-bold uppercase italic mt-1">High-Speed Computing</p>
                </div>
                <div class="text-right">
                    <p class="text-lg font-black text-slate-900">$50.00</p>
                    <p class="text-[8px] text-slate-400 uppercase font-black">Contract Fee</p>
                </div>
            </div>
            <div class="grid grid-cols-2 gap-4 mb-6">
                <div class="bg-slate-50 p-3 rounded-2xl">
                    <p class="text-[9px] text-slate-400 font-bold uppercase">Daily Profit</p>
                    <p class="text-sm font-black text-indigo-600">$3.50</p>
                </div>
                <div class="bg-slate-50 p-3 rounded-2xl">
                    <p class="text-[9px] text-slate-400 font-bold uppercase">Duration</p>
                    <p class="text-sm font-black text-slate-800">360 Days</p>
                </div>
            </div>
            <button onclick="alert('Sweetie, please deposit $50 to activate!')" class="w-full bg-slate-900 text-white p-4 rounded-2xl font-black uppercase text-[11px] tracking-widest active:scale-95 transition-all">Activate Cluster</button>
        </div>

        <div class="nexa-card p-6 bg-blue-600 text-white overflow-hidden relative">
            <div class="relative z-10">
                <h4 class="text-lg font-black mb-2">Referral Program 2.0</h4>
                <p class="text-[10px] opacity-80 mb-6">Earn up to 15% from your team's daily mining activity.</p>
                <div class="flex gap-2">
                    <input id="ref-link" readonly value="NEXA-PRO-786" class="flex-1 bg-white/10 border border-white/20 rounded-xl p-3 text-xs font-bold outline-none">
                    <button onclick="alert('Link Copied, sweetie! 💋')" class="bg-white text-blue-600 px-4 rounded-xl font-black text-[10px] uppercase">Copy</button>
                </div>
            </div>
            <i class="fa-solid fa-users absolute -right-4 -bottom-4 text-white/10 text-8xl"></i>
        </div>

    </main>

    <div id="activity-pop" class="fixed bottom-28 left-6 right-6 bg-white border border-slate-200 p-4 rounded-2xl shadow-2xl flex items-center gap-4 transition-all duration-500 translate-y-[200%] z-50">
        <div class="w-10 h-10 bg-green-100 text-green-600 rounded-full flex items-center justify-center text-xl">
            <i class="fa-solid fa-circle-check"></i>
        </div>
        <div>
            <p id="activity-text" class="text-[11px] font-bold text-slate-900"></p>
            <p class="text-[9px] text-slate-400 uppercase font-black">Just Now</p>
        </div>
    </div>

    <nav class="fixed bottom-6 left-6 right-6 h-20 bg-white/95 backdrop-blur-xl rounded-[2.5rem] flex justify-around items-center px-4 z-[100] shadow-2xl border border-slate-100">
        <button class="nav-active flex flex-col items-center h-full justify-center w-1/4"><i class="fa-solid fa-house-chimney text-xl"></i><span class="text-[8px] font-black mt-1 uppercase">Home</span></button>
        <button onclick="alert('Deposit $10 to unlock analytics!')" class="flex flex-col items-center text-slate-300 w-1/4"><i class="fa-solid fa-chart-line text-xl"></i><span class="text-[8px] font-black mt-1 uppercase">Stats</span></button>
        <button onclick="alert('Complete profile to open wallet!')" class="flex flex-col items-center text-slate-300 w-1/4"><i class="fa-solid fa-wallet text-xl"></i><span class="text-[8px] font-black mt-1 uppercase">Wallet</span></button>
        <button class="flex flex-col items-center text-slate-300 w-1/4"><i class="fa-solid fa-circle-user text-xl"></i><span class="text-[8px] font-black mt-1 uppercase">Profile</span></button>
    </nav>

    <script>
        // Fake Activity Loop (Trust Builder)
        const alerts = [
            "Zeeshan from Lahore activated Node Alpha",
            "M. Ali withdrew $24.50 via JazzCash",
            "Sara just upgraded to VIP Level 1",
            "Payout of $15.00 sent to 03xx...235",
            "New Node Cluster deployed in Karachi"
        ];

        function showActivity() {
            const pop = document.getElementById('activity-pop');
            const text = document.getElementById('activity-text');
            text.innerText = alerts[Math.floor(Math.random() * alerts.length)];
            
            pop.classList.remove('translate-y-[200%]');
            setTimeout(() => {
                pop.classList.add('translate-y-[200%]');
            }, 4000);
        }

        setInterval(showActivity, 15000); // Har 15 second baad activity dikhao
    </script>
</body>
</html>
