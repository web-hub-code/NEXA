<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Cloud Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #F8FAFC; color: #0F172A; }
        .nexa-card { background: #fff; border: 1px solid #E2E8F0; border-radius: 28px; transition: 0.3s; }
        .auth-screen { position: fixed; inset: 0; background: white; z-index: 1000; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 2rem; }
        .hidden { display: none !important; }
        .nav-active { color: #2563EB !important; border-top: 3px solid #2563EB; border-radius: 0; }
    </style>

    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
      import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
      import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

      // --- Anonymous Login Function ---
      window.startEarning = async () => {
          try {
              await signInAnonymously(auth);
          } catch (err) { 
              console.error(err);
              alert("Error: " + err.message); 
          }
      };

      // --- Data Monitoring ---
      onAuthStateChanged(auth, async (user) => {
          if (user) {
              document.getElementById('auth-section').classList.add('hidden');
              document.getElementById('main-app').classList.remove('hidden');

              const userRef = ref(db, 'users/' + user.uid);
              const snapshot = await get(userRef);

              if (!snapshot.exists()) {
                  // Pehli baar aane wale user ko bonus dena
                  await set(userRef, {
                      balance: 2.00,
                      uid: user.uid,
                      joinedAt: new Date().toISOString()
                  });
              }

              // Real-time balance update
              onValue(userRef, (snap) => {
                  const data = snap.val();
                  if(data) {
                      document.getElementById('balance-display').innerText = "$" + data.balance.toFixed(2);
                      document.getElementById('user-id-display').innerText = "ID: " + user.uid.substring(0, 8);
                  }
              });
          } else {
              document.getElementById('auth-section').classList.remove('hidden');
              document.getElementById('main-app').classList.add('hidden');
          }
      });

      // Bonus Logic
      window.claimBonus = async () => {
          const user = auth.currentUser;
          const userRef = ref(db, 'users/' + user.uid);
          const snapshot = await get(userRef);
          let currentBal = snapshot.val().balance;
          await update(userRef, { balance: currentBal + 0.10 });
          alert("Daily Yield Claimed, sweetie! 💋");
      };
    </script>
</head>
<body class="pb-32">

    <div id="auth-section" class="auth-screen text-center">
        <div class="w-24 h-24 bg-blue-600 rounded-[2.5rem] flex items-center justify-center shadow-2xl shadow-blue-200 mb-8 rotate-12">
            <i class="fa-solid fa-cloud text-white text-4xl -rotate-12"></i>
        </div>
        <h1 class="text-4xl font-black italic tracking-tighter text-slate-900">NEXA<span class="text-blue-600">CLOUD</span></h1>
        <p class="text-slate-400 text-[10px] font-bold uppercase tracking-[0.3em] mt-4 mb-12">Anonymous Mining Protocol</p>
        
        <button onclick="startEarning()" class="w-full max-w-xs bg-blue-600 text-white p-5 rounded-3xl font-black uppercase tracking-widest shadow-xl active:scale-95 transition-all">
            Access Dashboard
        </button>
        <p class="text-[10px] text-slate-400 mt-6 px-10">No registration required. Your data is linked to this device.</p>
    </div>

    <div id="main-app" class="hidden">
        <header class="p-6 flex justify-between items-center bg-white border-b border-slate-100 sticky top-0 z-50">
            <div class="flex items-center gap-2">
                <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center shadow-lg shadow-blue-100">
                    <i class="fa-solid fa-server text-white text-sm"></i>
                </div>
                <h1 class="text-xl font-black italic tracking-tighter">NEXA</h1>
            </div>
            <div class="text-right">
                <p id="user-id-display" class="text-[8px] font-black text-slate-400 uppercase mb-1">ID: LOADING</p>
                <h2 id="balance-display" class="text-xl font-black text-blue-600">$0.00</h2>
            </div>
        </header>

        <main class="p-5 space-y-6">
            <div class="nexa-card p-6 border-b-8 border-blue-600">
                <h3 class="text-xl font-black mb-2">Alpha Node Cluster</h3>
                <p class="text-xs text-slate-500 mb-6">Automated cloud mining active. Earn daily rewards safely.</p>
                <div class="bg-blue-50 p-4 rounded-2xl flex justify-between items-center mb-6">
                    <span class="text-[10px] font-black uppercase text-blue-600">Daily Yield</span>
                    <span class="font-black">$0.75 / Day</span>
                </div>
                <button onclick="claimBonus()" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black uppercase text-[10px] tracking-widest shadow-lg">Claim Rewards</button>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div class="nexa-card p-5 text-center">
                    <p class="text-[9px] font-black text-slate-400 uppercase mb-1">Global Hashrate</p>
                    <h4 class="text-lg font-black italic">850 TH/s</h4>
                </div>
                <div class="nexa-card p-5 text-center">
                    <p class="text-[9px] font-black text-slate-400 uppercase mb-1">Active Users</p>
                    <h4 class="text-lg font-black italic">14.2K+</h4>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 bg-white shadow-[0_20px_50px_rgba(0,0,0,0.1)] rounded-[2.5rem] border border-slate-100 flex justify-around items-center px-4">
            <button class="text-blue-600 flex flex-col items-center"><i class="fa-solid fa-layer-group text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Mining</span></button>
            <button onclick="alert('Wallet features coming soon!')" class="text-slate-300 flex flex-col items-center"><i class="fa-solid fa-wallet text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Assets</span></button>
            <button onclick="alert('Team features coming soon!')" class="text-slate-300 flex flex-col items-center"><i class="fa-solid fa-users text-xl"></i><span class="text-[8px] font-black uppercase mt-1">Network</span></button>
        </nav>
    </div>

</body>
</html>
