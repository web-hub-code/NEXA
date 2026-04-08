<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Premium Cloud Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        
        :root { --primary: #2563EB; --bg: #F8FAFC; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0F172A; -webkit-tap-highlight-color: transparent; }
        
        .nexa-card { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border: 1px solid rgba(226, 232, 240, 0.8); border-radius: 32px; box-shadow: 0 10px 40px -10px rgba(0,0,0,0.03); }
        .glass-header { background: rgba(248, 250, 252, 0.8); backdrop-filter: blur(12px); border-bottom: 1px solid rgba(226, 232, 240, 0.5); }
        .nav-btn { transition: 0.3s; color: #94A3B8; }
        .nav-active { color: var(--primary) !important; transform: translateY(-5px); }
        
        .mining-bar { height: 6px; background: #E2E8F0; border-radius: 20px; overflow: hidden; position: relative; }
        .mining-progress { position: absolute; height: 100%; background: linear-gradient(90deg, #2563EB, #7DD3FC); animation: flow 2s infinite linear; }
        @keyframes flow { 0% { width: 0%; left: 0%; } 50% { width: 50%; } 100% { width: 0%; left: 100%; } }
        
        .btn-primary { background: var(--primary); color: white; border-radius: 20px; font-weight: 800; font-size: 11px; text-transform: uppercase; letter-spacing: 1px; transition: 0.2s; box-shadow: 0 10px 25px -5px rgba(37, 99, 235, 0.4); }
        .btn-primary:active { transform: scale(0.95); }
    </style>

    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
      import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
      import { getDatabase, ref, set, get, update, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

      // --- Core Logic ---
      let adminClicks = 0;
      const ADMIN_KEY = "SWEETIE786";

      window.accessApp = async () => {
          try { await signInAnonymously(auth); } catch (e) { alert(e.message); }
      };

      onAuthStateChanged(auth, async (user) => {
          if (user) {
              document.getElementById('auth-screen').style.display = 'none';
              document.getElementById('app-screen').classList.remove('hidden');
              syncUserData(user.uid);
          } else {
              document.getElementById('auth-screen').style.display = 'flex';
          }
      });

      async function syncUserData(uid) {
          const userRef = ref(db, 'users/' + uid);
          const snap = await get(userRef);
          if(!snap.exists()) {
              await set(userRef, { balance: 5.00, history: [] }); // $5 Welcome Bonus
              logTx(uid, "Welcome Reward", 5.00, "plus");
          }
          onValue(userRef, (s) => {
              const data = s.val();
              document.querySelectorAll('.bal-val').forEach(el => el.innerText = "$" + data.balance.toFixed(2));
              renderHistory(data.history);
          });
      }

      async function logTx(uid, title, amt, type) {
          const histRef = ref(db, `users/${uid}/history`);
          push(histRef, { title, amt, type, time: new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'}) });
      }

      window.claimYield = async () => {
          const uid = auth.currentUser.uid;
          const snap = await get(ref(db, 'users/'+uid));
          const nb = snap.val().balance + 0.85;
          await update(ref(db, 'users/'+uid), { balance: nb });
          logTx(uid, "Node Yield", 0.85, "plus");
          alert("Yield Added Sweetie! 💋");
      };

      window.logoTrigger = () => {
          adminClicks++;
          if(adminClicks >= 5) {
              const k = prompt("Secret Key:");
              if(k === ADMIN_KEY) document.getElementById('admin-box').classList.remove('hidden');
              adminClicks = 0;
          }
      };

      // --- Admin Actions ---
      window.modUser = async () => {
          const id = prompt("User UID:");
          const amt = parseFloat(prompt("New Balance:"));
          if(id && !isNaN(amt)) {
              await update(ref(db, 'users/' + id), { balance: amt });
              alert("Done!");
          }
      };

      // --- Navigation ---
      window.showPage = (id) => {
          ['home','wallet','history'].forEach(p => document.getElementById('p-'+p).classList.add('hidden'));
          document.getElementById('p-'+id).classList.remove('hidden');
          document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('nav-active'));
          event.currentTarget.classList.add('nav-active');
      };

      function renderHistory(h) {
          const box = document.getElementById('hist-box');
          box.innerHTML = h ? "" : "<p class='text-center text-slate-400 py-10 text-xs font-bold'>NO TRANSACTIONS</p>";
          if(h) Object.values(h).reverse().forEach(t => {
              box.innerHTML += `
              <div class="flex justify-between items-center p-4 bg-white/50 rounded-2xl mb-3 border border-slate-100">
                  <div><p class="text-[11px] font-extrabold uppercase">${t.title}</p><p class="text-[9px] text-slate-400 font-bold">${t.time}</p></div>
                  <div class="font-black text-xs ${t.type==='plus'?'text-green-500':'text-red-500'}">${t.type==='plus'?'+':'-'}$${t.amt.toFixed(2)}</div>
              </div>`;
          });
      }
    </script>
</head>
<body class="pb-28">

    <!-- Splash/Auth Screen -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[9999] flex flex-col items-center justify-center p-8">
        <div class="w-24 h-24 bg-blue-600 rounded-[2.5rem] flex items-center justify-center shadow-2xl shadow-blue-200 mb-8 rotate-12">
            <i class="fa-solid fa-cloud text-white text-4xl -rotate-12"></i>
        </div>
        <h1 class="text-4xl font-black italic tracking-tighter">NEXA<span class="text-blue-600">.</span></h1>
        <p class="text-[10px] font-extrabold text-slate-400 uppercase tracking-[0.4em] mt-3 mb-12">Cloud Mining Protocol</p>
        <button onclick="accessApp()" class="w-full max-w-xs btn-primary py-5">Initialize Terminal</button>
    </div>

    <!-- Main Application -->
    <div id="app-screen" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 glass-header z-50">
            <div onclick="logoTrigger()" class="flex items-center gap-2">
                <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center shadow-lg"><i class="fa-solid fa-server text-white text-sm"></i></div>
                <h1 class="text-xl font-black italic tracking-tighter">NEXA</h1>
            </div>
            <div class="bg-white border border-slate-200 px-4 py-2 rounded-2xl">
                <p class="text-[8px] font-black text-slate-400 uppercase leading-none mb-1">Total Assets</p>
                <h2 class="bal-val text-sm font-black text-blue-600">$0.00</h2>
            </div>
        </header>

        <main class="p-5">
            <!-- Home Page -->
            <div id="p-home" class="space-y-6">
                <div class="nexa-card p-8 bg-gradient-to-br from-slate-900 to-slate-800 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <p class="text-[10px] font-black uppercase opacity-50 tracking-widest">Hashrate Power</p>
                        <h2 class="text-4xl font-black mt-2 mb-8 italic">45.2 <span class="text-xs font-normal opacity-40 uppercase tracking-normal">Ph/s Active</span></h2>
                        <button onclick="claimYield()" class="bg-blue-600 px-8 py-3 rounded-2xl font-black text-[10px] uppercase tracking-widest active:scale-95 transition-all">Claim Yield</button>
                    </div>
                    <i class="fa-solid fa-bolt-lightning absolute -right-6 -bottom-6 text-white/5 text-[10rem]"></i>
                </div>

                <div class="flex justify-between items-center px-1">
                    <h3 class="text-[10px] font-extrabold text-slate-400 uppercase tracking-widest">Infrastructure</h3>
                    <span class="text-[9px] font-black text-blue-600 uppercase">Live Stats <i class="fa-solid fa-circle text-[6px] ml-1 animate-pulse"></i></span>
                </div>

                <div class="nexa-card p-6">
                    <div class="flex justify-between items-start mb-6">
                        <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-microchip"></i></div>
                        <div class="text-right"><p class="text-xl font-black">$25.00</p><p class="text-[8px] font-black text-slate-400 uppercase">Per License</p></div>
                    </div>
                    <h4 class="text-lg font-black text-slate-900">Quantum Cluster v2</h4>
                    <p class="text-xs text-slate-500 mt-1 mb-6">Yield: <span class="text-blue-600 font-bold">$1.50 Daily</span> • Reliability: 99.9%</p>
                    <div class="mining-bar mb-6"><div class="mining-progress"></div></div>
                    <button onclick="alert('Insufficient Funds, sweetie! 💋')" class="w-full btn-primary py-4">Activate License</button>
                </div>
            </div>

            <!-- Wallet Page -->
            <div id="p-wallet" class="hidden space-y-6">
                <div class="nexa-card p-10 text-center bg-white border-2 border-blue-600/10">
                    <p class="text-xs font-black text-slate-400 uppercase tracking-[0.2em] mb-3">Available for Payout</p>
                    <h1 class="bal-val text-5xl font-black text-slate-900 tracking-tighter">$0.00</h1>
                    <div class="flex gap-4 mt-12">
                        <button onclick="alert('Contact Support for JazzCash/Easypaisa deposit details!')" class="flex-1 btn-primary py-4"><i class="fa-solid fa-plus mr-2"></i>Deposit</button>
                        <button onclick="alert('Min Payout: $10.00')" class="flex-1 bg-slate-100 text-slate-900 font-black text-[10px] uppercase rounded-2xl active:scale-95 transition-all">Withdraw</button>
                    </div>
                </div>
                <div class="nexa-card p-6 border-dashed border-2">
                    <h5 class="text-[10px] font-black uppercase text-slate-400 mb-2">Security Note</h5>
                    <p class="text-[11px] text-slate-500 leading-relaxed font-bold">Payouts are processed within 24 hours to your linked anonymous wallet address. Keep your UID safe.</p>
                </div>
            </div>

            <!-- History Page -->
            <div id="p-history" class="hidden space-y-6">
                <h3 class="text-[10px] font-extrabold text-slate-400 uppercase tracking-widest px-1">Ledger History</h3>
                <div id="hist-box">
                    <!-- Dynamic -->
                </div>
            </div>

            <!-- Secret Admin -->
            <div id="admin-box" class="hidden nexa-card p-6 border-red-500 border-2 mt-8">
                <h2 class="text-red-600 font-black text-center text-xs mb-4 uppercase">Master Terminal</h2>
                <button onclick="modUser()" class="w-full bg-red-600 text-white p-4 rounded-2xl font-black text-[10px] uppercase mb-2">Modify User Balance</button>
                <button onclick="document.getElementById('admin-box').classList.add('hidden')" class="w-full bg-slate-400 text-white p-2 rounded-xl font-black text-[10px] uppercase">Close</button>
            </div>
        </main>

        <!-- Navigation Bar -->
        <nav class="fixed bottom-8 left-8 right-8 h-20 nexa-card flex justify-around items-center px-6 z-50 border-none shadow-[0_20px_50px_rgba(0,0,0,0.1)]">
            <button onclick="showPage('home')" class="nav-btn nav-active flex flex-col items-center"><i class="fa-solid fa-server text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Nodes</span></button>
            <button onclick="showPage('wallet')" class="nav-btn flex flex-col items-center"><i class="fa-solid fa-wallet text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Assets</span></button>
            <button onclick="showPage('history')" class="nav-btn flex flex-col items-center"><i class="fa-solid fa-receipt text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Ledger</span></button>
        </nav>
    </div>

</body>
</html>
