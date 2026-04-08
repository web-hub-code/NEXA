<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Next-Gen Cloud Mining</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #F8FAFC; color: #0F172A; }
        .nexa-card { background: #fff; border: 1px solid #E2E8F0; border-radius: 28px; transition: 0.3s; }
        .nexa-card:active { transform: scale(0.98); }
        .auth-screen { position: fixed; inset: 0; background: white; z-index: 1000; display: flex; flex-direction: column; padding: 2rem; overflow-y: auto; }
        .hidden { display: none !important; }
        .nav-active { color: #2563EB !important; border-top: 3px solid #2563EB; border-radius: 0; }
        .status-dot { width: 8px; height: 8px; border-radius: 50%; display: inline-block; margin-right: 5px; background: #22c55e; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
        /* Professional Progress Bar */
        .progress-container { height: 6px; background: #F1F5F9; border-radius: 10px; overflow: hidden; }
        .progress-bar { height: 100%; background: linear-gradient(90deg, #2563EB, #60A5FA); width: 0%; transition: width 0.5s; }
    </style>

    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
      import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
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

      // --- Authentication ---
      window.handleSignup = async () => {
          const email = document.getElementById('sig-email').value;
          const pass = document.getElementById('sig-pass').value;
          if(!email || !pass) return alert("Fill all fields, sweetie!");
          try {
              const res = await createUserWithEmailAndPassword(auth, email, pass);
              await set(ref(db, 'users/' + res.user.uid), {
                  balance: 2.00,
                  email: email,
                  joinedAt: new Date().toISOString(),
                  nodes: 0
              });
              alert("Welcome to the NEXA Family! 💋");
          } catch (err) { alert(err.message); }
      };

      window.handleLogin = async () => {
          const email = document.getElementById('log-email').value;
          const pass = document.getElementById('log-pass').value;
          try { await signInWithEmailAndPassword(auth, email, pass); } 
          catch (err) { alert("Wrong details, sweetie!"); }
      };

      window.handleLogout = () => signOut(auth);

      // --- Data Sync ---
      onAuthStateChanged(auth, (user) => {
          if (user) {
              document.getElementById('auth-section').classList.add('hidden');
              document.getElementById('main-app').classList.remove('hidden');
              onValue(ref(db, 'users/' + user.uid), (snapshot) => {
                  const data = snapshot.val();
                  if(data) {
                      document.getElementById('balance-display').innerText = "$" + data.balance.toFixed(2);
                      document.getElementById('wallet-bal').innerText = "$" + data.balance.toFixed(2);
                      document.getElementById('user-email').innerText = data.email;
                  }
              });
          } else {
              document.getElementById('auth-section').classList.remove('hidden');
              document.getElementById('main-app').classList.add('hidden');
          }
      });

      // --- Functional Features ---
      window.claimBonus = async () => {
          const user = auth.currentUser;
          const snapshot = await get(ref(db, 'users/' + user.uid));
          let currentBal = snapshot.val().balance;
          await update(ref(db, 'users/' + user.uid), { balance: currentBal + 0.10 });
          alert("Daily Yield Claimed! +$0.10 💎");
      };
    </script>
</head>
<body class="pb-32">

    <!-- 1. AUTH SCREENS -->
    <div id="auth-section" class="auth-screen">
        <div class="mt-20 text-center">
            <div class="w-20 h-20 bg-blue-600 rounded-[2rem] mx-auto flex items-center justify-center shadow-2xl shadow-blue-200 mb-6 rotate-12">
                <i class="fa-solid fa-cloud text-white text-4xl -rotate-12"></i>
            </div>
            <h1 class="text-4xl font-black italic tracking-tighter">NEXA<span class="text-blue-600">CLOUD</span></h1>
            <p class="text-slate-400 text-[10px] font-bold uppercase tracking-[0.3em] mt-3">Advanced Mining Protocol</p>
        </div>

        <div id="login-form" class="mt-12 space-y-4">
            <input type="email" id="log-email" placeholder="Professional Email" class="w-full bg-slate-50 border border-slate-200 p-5 rounded-3xl outline-none focus:border-blue-500 transition-all">
            <input type="password" id="log-pass" placeholder="Password" class="w-full bg-slate-50 border border-slate-200 p-5 rounded-3xl outline-none focus:border-blue-500 transition-all">
            <button onclick="handleLogin()" class="w-full bg-blue-600 text-white p-5 rounded-3xl font-black uppercase tracking-widest shadow-xl">Secure Login</button>
            <p class="text-center text-xs font-bold text-slate-400">New Investor? <span class="text-blue-600 cursor-pointer" onclick="document.getElementById('login-form').classList.add('hidden'); document.getElementById('signup-form').classList.remove('hidden')">Create Account</span></p>
        </div>

        <div id="signup-form" class="mt-12 space-y-4 hidden">
            <input type="email" id="sig-email" placeholder="Email Address" class="w-full bg-slate-50 border border-slate-200 p-5 rounded-3xl outline-none focus:border-blue-500 transition-all">
            <input type="password" id="sig-pass" placeholder="Choose Password" class="w-full bg-slate-50 border border-slate-200 p-5 rounded-3xl outline-none focus:border-blue-500 transition-all">
            <button onclick="handleSignup()" class="w-full bg-blue-600 text-white p-5 rounded-3xl font-black uppercase tracking-widest shadow-xl">Start Earning</button>
            <p class="text-center text-xs font-bold text-slate-400">Already a member? <span class="text-blue-600 cursor-pointer" onclick="document.getElementById('signup-form').classList.add('hidden'); document.getElementById('login-form').classList.remove('hidden')">Back to Login</span></p>
        </div>
    </div>

    <!-- 2. MAIN APP -->
    <div id="main-app" class="hidden">
        <!-- Sticky Header -->
        <header class="p-6 flex justify-between items-center bg-white/90 backdrop-blur-lg sticky top-0 z-50 border-b border-slate-100">
            <div class="flex items-center gap-2">
                <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center shadow-lg"><i class="fa-solid fa-cloud text-white text-sm"></i></div>
                <h1 class="text-xl font-black italic">NEXA</h1>
            </div>
            <div class="bg-blue-50 px-4 py-2 rounded-2xl border border-blue-100">
                <h2 id="balance-display" class="text-lg font-black text-blue-600">$0.00</h2>
            </div>
        </header>

        <main class="p-5 space-y-6">
            
            <!-- Global Stats (Cloud Node Style) -->
            <div class="grid grid-cols-2 gap-4">
                <div class="nexa-card p-5">
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest">Active Nodes</p>
                    <h3 class="text-xl font-black">12,492 <span class="status-dot"></span></h3>
                </div>
                <div class="nexa-card p-5">
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest">Network Power</p>
                    <h3 class="text-xl font-black text-blue-600">850 TH/s</h3>
                </div>
            </div>

            <!-- Tabs Content -->
            <div id="tab-home" class="space-y-6">
                <!-- Daily Reward -->
                <div class="nexa-card p-6 bg-gradient-to-br from-blue-600 to-indigo-800 text-white relative overflow-hidden">
                    <h4 class="text-xs font-black uppercase opacity-70">Daily Node Maintenance</h4>
                    <p class="text-xl font-bold mt-1 mb-6">Claim Your Yield Bonus</p>
                    <button onclick="claimBonus()" class="bg-white text-blue-600 px-8 py-3 rounded-2xl font-black text-[10px] uppercase shadow-xl active:scale-90 transition-all">Claim Now</button>
                    <i class="fa-solid fa-bolt absolute -right-4 -bottom-4 text-white/10 text-9xl"></i>
                </div>

                <!-- Product Cards (Unlimited Style) -->
                <h3 class="text-xs font-black uppercase text-slate-400 px-1 tracking-widest">Available Infrastructure</h3>
                
                <div class="nexa-card p-6 border-b-8 border-blue-600">
                    <div class="flex justify-between items-center mb-6">
                        <div class="p-3 bg-blue-50 rounded-2xl text-blue-600 text-xl"><i class="fa-solid fa-microchip"></i></div>
                        <div class="text-right">
                            <p class="text-lg font-black">$15.00</p>
                            <span class="text-[8px] bg-green-100 text-green-600 px-2 py-1 rounded font-black uppercase tracking-tighter italic">Low Risk</span>
                        </div>
                    </div>
                    <h4 class="text-lg font-black">Core Node Cluster v.1</h4>
                    <p class="text-xs text-slate-500 mt-1 mb-6">Daily Return: <span class="text-blue-600 font-bold">$0.75</span> • Duration: 365 Days</p>
                    <div class="progress-container mb-6"><div class="progress-bar" style="width: 45%;"></div></div>
                    <button onclick="alert('Sweetie, deposit $15 to initiate this node!')" class="w-full bg-slate-900 text-white p-4 rounded-[1.5rem] font-black uppercase text-[10px] tracking-widest">Deploy Infrastructure</button>
                </div>
            </div>

            <!-- Wallet Tab (Unlimited Control) -->
            <div id="tab-wallet" class="hidden space-y-6">
                <div class="nexa-card p-8 bg-slate-900 text-white text-center">
                    <p class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-2">Available for Withdrawal</p>
                    <h1 id="wallet-bal" class="text-5xl font-black">$0.00</h1>
                    <div class="flex gap-4 mt-10">
                        <button onclick="alert('Join Official Telegram for Deposit Address')" class="flex-1 bg-blue-600 p-4 rounded-2xl font-black text-[10px] uppercase tracking-widest">Deposit</button>
                        <button onclick="alert('Minimum withdrawal: $10.00')" class="flex-1 bg-white/10 border border-white/10 p-4 rounded-2xl font-black text-[10px] uppercase tracking-widest">Withdraw</button>
                    </div>
                </div>
                <div class="nexa-card p-6">
                    <h5 class="font-black text-xs uppercase text-slate-400 mb-4">Transaction History</h5>
                    <div class="text-center py-10">
                        <i class="fa-solid fa-receipt text-3xl text-slate-100"></i>
                        <p class="text-[10px] text-slate-400 mt-2 font-bold uppercase">No records found yet</p>
                    </div>
                </div>
            </div>

            <!-- Profile/Team Tab -->
            <div id="tab-profile" class="hidden space-y-6">
                <div class="nexa-card p-6 text-center">
                    <div class="w-20 h-20 bg-slate-100 rounded-full mx-auto flex items-center justify-center text-slate-400 text-3xl mb-4"><i class="fa-solid fa-user-secret"></i></div>
                    <h4 id="user-email" class="font-black text-slate-900">Loading...</h4>
                    <p class="text-[10px] text-blue-600 font-bold uppercase tracking-widest mt-1">Verified Investor</p>
                </div>
                <div class="nexa-card p-6">
                    <h5 class="font-black text-xs uppercase mb-4">Affiliate Program</h5>
                    <div class="flex items-center gap-4 bg-slate-50 p-4 rounded-2xl">
                        <div class="flex-1 overflow-hidden">
                            <p class="text-[9px] text-slate-400 uppercase font-black">Invite Code</p>
                            <p class="text-sm font-black text-slate-900 truncate">NEXA-REF-786-PRO</p>
                        </div>
                        <button onclick="alert('Link Copied!')" class="bg-blue-600 text-white px-4 py-2 rounded-xl text-[10px] font-black">COPY</button>
                    </div>
                </div>
            </div>

        </main>

        <!-- Dynamic Navigation -->
        <nav class="fixed bottom-6 left-6 right-6 h-20 bg-white/90 backdrop-blur-xl rounded-[2.5rem] border border-slate-100 shadow-[0_25px_60px_rgba(0,0,0,0.1)] flex justify-around items-center px-4 z-50">
            <button onclick="switchTab('home')" class="nav-btn flex flex-col items-center nav-active w-1/4"><i class="fa-solid fa-layer-group"></i><span class="text-[8px] font-black mt-1 uppercase tracking-tighter">Mining</span></button>
            <button onclick="switchTab('wallet')" class="nav-btn flex flex-col items-center text-slate-400 w-1/4"><i class="fa-solid fa-wallet"></i><span class="text-[8px] font-black mt-1 uppercase tracking-tighter">Assets</span></button>
            <button onclick="switchTab('profile')" class="nav-btn flex flex-col items-center text-slate-400 w-1/4"><i class="fa-solid fa-users"></i><span class="text-[8px] font-black mt-1 uppercase tracking-tighter">Team</span></button>
            <button onclick="handleLogout()" class="flex flex-col items-center text-slate-400 w-1/4"><i class="fa-solid fa-door-open"></i><span class="text-[8px] font-black mt-1 uppercase tracking-tighter">Exit</span></button>
        </nav>
    </div>

    <script>
        // Tab Switcher Logic
        function switchTab(tabId) {
            const tabs = ['tab-home', 'tab-wallet', 'tab-profile'];
            tabs.forEach(t => document.getElementById(t).classList.add('hidden'));
            document.getElementById('tab-'+tabId).classList.remove('hidden');
            
            // UI Update
            const btns = document.querySelectorAll('.nav-btn');
            btns.forEach(b => b.classList.remove('nav-active', 'text-blue-600'));
            btns.forEach(b => b.classList.add('text-slate-400'));
            event.currentTarget.classList.add('nav-active', 'text-blue-600');
        }
    </script>
</body>
</html>
