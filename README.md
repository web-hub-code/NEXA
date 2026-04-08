<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Premium Cloud Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #F8FAFC; color: #0F172A; overflow-x: hidden; }
        .nexa-card { background: #fff; border: 1px solid #E2E8F0; border-radius: 24px; transition: 0.3s; }
        .glass-nav { background: rgba(255,255,255,0.8); backdrop-filter: blur(20px); border-top: 1px solid #E2E8F0; }
        .hidden { display: none !important; }
        .nav-active { color: #2563EB !important; }
        .status-pulse { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
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

      // --- Global Variables ---
      let clickCount = 0;
      const ADMIN_KEY = "SWEETIE786";

      // --- Auth ---
      window.startApp = async () => {
          try { await signInAnonymously(auth); } catch (e) { alert(e.message); }
      };

      onAuthStateChanged(auth, async (user) => {
          if (user) {
              document.getElementById('auth-screen').classList.add('hidden');
              document.getElementById('main-app').classList.remove('hidden');
              loadUserData(user.uid);
          } else {
              document.getElementById('auth-screen').classList.remove('hidden');
          }
      });

      async function loadUserData(uid) {
          const userRef = ref(db, 'users/' + uid);
          const snap = await get(userRef);
          if(!snap.exists()) {
              await set(userRef, { balance: 2.00, history: [] });
              addHistory(uid, "Welcome Bonus", 2.00, "plus");
          }
          onValue(userRef, (s) => {
              const data = s.val();
              document.getElementById('user-bal').innerText = "$" + data.balance.toFixed(2);
              document.getElementById('wallet-bal').innerText = "$" + data.balance.toFixed(2);
              renderHistory(data.history);
          });
      }

      // --- Database Helpers ---
      async function addHistory(uid, title, amt, type) {
          const histRef = ref(db, `users/${uid}/history`);
          push(histRef, { title, amt, type, date: new Date().toLocaleString() });
      }

      function renderHistory(history) {
          const container = document.getElementById('history-list');
          container.innerHTML = "";
          if(!history) return container.innerHTML = "<p class='text-center text-slate-400 py-4 text-xs'>No Transactions</p>";
          Object.values(history).reverse().forEach(item => {
              container.innerHTML += `
                <div class="flex justify-between items-center p-3 bg-slate-50 rounded-xl mb-2">
                    <div>
                        <p class="text-[11px] font-bold">${item.title}</p>
                        <p class="text-[9px] text-slate-400">${item.date}</p>
                    </div>
                    <span class="text-xs font-black ${item.type === 'plus' ? 'text-green-500' : 'text-red-500'}">
                        ${item.type === 'plus' ? '+' : '-'}$${item.amt.toFixed(2)}
                    </span>
                </div>`;
          });
      }

      // --- Admin Logic ---
      window.logoClick = () => {
          clickCount++;
          if(clickCount >= 5) {
              const key = prompt("Enter Secret Admin Key, sweetie:");
              if(key === ADMIN_KEY) {
                  document.getElementById('admin-panel').classList.remove('hidden');
                  clickCount = 0;
              } else { alert("Wrong Key!"); clickCount = 0; }
          }
      };

      window.updateBalance = async () => {
          const targetUid = prompt("Enter User UID (from Firebase):");
          const newAmt = parseFloat(prompt("Enter New Balance:"));
          if(targetUid && newAmt) {
              await update(ref(db, 'users/' + targetUid), { balance: newAmt });
              alert("Balance Updated!");
          }
      };

      // --- UI Controllers ---
      window.switchTab = (tab) => {
          const sections = ['home', 'wallet', 'history'];
          sections.forEach(s => document.getElementById(s+'-section').classList.add('hidden'));
          document.getElementById(tab+'-section').classList.remove('hidden');
          const btns = document.querySelectorAll('.nav-btn');
          btns.forEach(b => b.classList.remove('text-blue-600'));
          event.currentTarget.classList.add('text-blue-600');
      };

      window.claimYield = async () => {
          const uid = auth.currentUser.uid;
          const snap = await get(ref(db, 'users/'+uid));
          const newBal = snap.val().balance + 0.50;
          await update(ref(db, 'users/'+uid), { balance: newBal });
          addHistory(uid, "Daily Yield", 0.50, "plus");
          alert("Yield Claimed! +$0.50 💋");
      }
    </script>
</head>
<body class="pb-24">

    <!-- Auth -->
    <div id="auth-screen" class="fixed inset-0 bg-white z-[2000] flex flex-col items-center justify-center p-10">
        <div class="w-20 h-20 bg-blue-600 rounded-[2rem] flex items-center justify-center shadow-xl mb-6 rotate-12">
            <i class="fa-solid fa-cloud text-white text-3xl -rotate-12"></i>
        </div>
        <h1 class="text-3xl font-black italic tracking-tighter mb-10">NEXA<span class="text-blue-600 text-4xl">.</span></h1>
        <button onclick="startApp()" class="w-full bg-blue-600 text-white py-5 rounded-3xl font-black uppercase tracking-widest shadow-lg shadow-blue-100 active:scale-95 transition-all">Connect to Cluster</button>
        <p class="mt-6 text-[10px] text-slate-400 font-bold uppercase tracking-widest">Protocol v4.0.2 Locked</p>
    </div>

    <!-- Main App -->
    <div id="main-app" class="hidden">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-lg z-50">
            <div onclick="logoClick()" class="flex items-center gap-2 cursor-pointer">
                <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center"><i class="fa-solid fa-server text-white text-[10px]"></i></div>
                <h1 class="font-black italic tracking-tighter">NEXA</h1>
            </div>
            <div class="flex items-center gap-2 bg-slate-50 px-3 py-2 rounded-xl">
                <span class="status-pulse"></span>
                <span id="user-bal" class="text-sm font-black text-blue-600">$0.00</span>
            </div>
        </header>

        <!-- Tabs Container -->
        <main class="p-5">
            
            <!-- Home Section -->
            <div id="home-section" class="space-y-6">
                <div class="nexa-card p-6 bg-gradient-to-br from-blue-600 to-indigo-700 text-white overflow-hidden relative">
                    <p class="text-[10px] font-black uppercase opacity-60">Total Hashrate</p>
                    <h2 class="text-3xl font-black mt-1 mb-6">452.9 <span class="text-sm font-normal opacity-50">TH/s</span></h2>
                    <button onclick="claimYield()" class="bg-white text-blue-600 px-6 py-3 rounded-2xl font-black text-[10px] uppercase shadow-lg">Claim Daily Yield</button>
                    <i class="fa-solid fa-bolt-lightning absolute -right-4 -bottom-4 text-white/10 text-9xl"></i>
                </div>

                <h3 class="text-[10px] font-black uppercase text-slate-400 tracking-widest px-1">Mining Nodes</h3>
                <div class="nexa-card p-5">
                    <div class="flex justify-between items-center mb-6">
                        <div class="w-10 h-10 bg-blue-50 text-blue-600 rounded-xl flex items-center justify-center"><i class="fa-solid fa-microchip"></i></div>
                        <span class="text-sm font-black">$20.00</span>
                    </div>
                    <h4 class="font-black text-slate-900">Alpha Core Cluster</h4>
                    <p class="text-[10px] text-slate-500 mt-1 mb-6">Profit: $1.20 Daily • 365 Days</p>
                    <button onclick="alert('Insufficient Balance, sweetie! Please Deposit.')" class="w-full bg-slate-900 text-white py-4 rounded-2xl font-black text-[10px] uppercase tracking-widest">Activate Node</button>
                </div>
            </div>

            <!-- Wallet Section -->
            <div id="wallet-section" class="hidden space-y-6">
                <div class="nexa-card p-8 bg-slate-900 text-white text-center relative overflow-hidden">
                    <p class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-2">Available Balance</p>
                    <h1 id="wallet-bal" class="text-5xl font-black">$0.00</h1>
                    <div class="flex gap-3 mt-10 relative z-10">
                        <button onclick="alert('Contact Admin for Deposit Address')" class="flex-1 bg-blue-600 p-4 rounded-2xl font-black text-[10px] uppercase"><i class="fa-solid fa-plus mr-2"></i>Deposit</button>
                        <button onclick="alert('Min withdrawal $10.00')" class="flex-1 bg-white/10 border border-white/10 p-4 rounded-2xl font-black text-[10px] uppercase"><i class="fa-solid fa-arrow-up-from-bracket mr-2"></i>Withdraw</button>
                    </div>
                    <i class="fa-solid fa-wallet absolute -left-10 -bottom-10 text-white/5 text-[12rem]"></i>
                </div>
            </div>

            <!-- History Section -->
            <div id="history-section" class="hidden space-y-6">
                <h3 class="text-[10px] font-black uppercase text-slate-400 tracking-widest px-1">Transaction History</h3>
                <div id="history-list" class="nexa-card p-4">
                    <!-- Loaded via JS -->
                </div>
            </div>

            <!-- Secret Admin Panel (Hidden) -->
            <div id="admin-panel" class="hidden nexa-card p-6 border-2 border-dashed border-red-500 bg-red-50/50 mt-10">
                <h3 class="text-red-600 font-black text-center mb-4 uppercase">Secret Admin Menu</h3>
                <button onclick="updateBalance()" class="w-full bg-red-600 text-white p-4 rounded-xl font-black text-xs mb-2">Change User Balance</button>
                <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="w-full bg-slate-400 text-white p-2 rounded-xl font-black text-[10px]">Close</button>
            </div>

        </main>

        <!-- Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 glass-nav rounded-[2.5rem] flex justify-around items-center px-6 z-50 shadow-2xl">
            <button onclick="switchTab('home')" class="nav-btn text-blue-600 flex flex-col items-center"><i class="fa-solid fa-server text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Nodes</span></button>
            <button onclick="switchTab('wallet')" class="nav-btn text-slate-400 flex flex-col items-center"><i class="fa-solid fa-wallet text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Wallet</span></button>
            <button onclick="switchTab('history')" class="nav-btn text-slate-400 flex flex-col items-center"><i class="fa-solid fa-clock-rotate-left text-xl"></i><span class="text-[8px] font-black uppercase mt-1">History</span></button>
        </nav>
    </div>

</body>
</html>
