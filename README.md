<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXA | Cloud Mining Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
    
    <!-- Firebase SDKs -->
    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
      import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
      import { getDatabase, ref, set, get, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

      // Aapki Firebase Configuration
      const firebaseConfig = {
        apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
        authDomain: "verbose-6c008.firebaseapp.com",
        databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
        projectId: "verbose-6c008",
        storageBucket: "verbose-6c008.firebasestorage.app",
        messagingSenderId: "867100945312",
        appId: "1:867100945312:web:315dfb48fb34496cee12c5"
      };

      // Initialize Firebase
      const app = initializeApp(firebaseConfig);
      const auth = getAuth(app);
      const db = getDatabase(app);

      // --- Auth Functions ---
      window.handleSignup = async () => {
          const email = document.getElementById('sig-email').value;
          const pass = document.getElementById('sig-pass').value;
          try {
              const res = await createUserWithEmailAndPassword(auth, email, pass);
              // Naya user bante hi database mein balance 0 set karna
              await set(ref(db, 'users/' + res.user.uid), {
                  balance: 2.00, // Welcome Bonus
                  email: email,
                  role: "user"
              });
              alert("Account Created, sweetie! 💋");
          } catch (err) { alert(err.message); }
      };

      window.handleLogin = async () => {
          const email = document.getElementById('log-email').value;
          const pass = document.getElementById('log-pass').value;
          try {
              await signInWithEmailAndPassword(auth, email, pass);
          } catch (err) { alert("Invalid credentials, sweetie!"); }
      };

      window.handleLogout = () => signOut(auth);

      // Real-time State Change
      onAuthStateChanged(auth, async (user) => {
          if (user) {
              document.getElementById('auth-section').classList.add('hidden');
              document.getElementById('main-app').classList.remove('hidden');
              // Fetch Balance from DB
              const snapshot = await get(ref(db, 'users/' + user.uid));
              if(snapshot.exists()) {
                  document.getElementById('balance-display').innerText = "$" + snapshot.val().balance.toFixed(2);
              }
          } else {
              document.getElementById('auth-section').classList.remove('hidden');
              document.getElementById('main-app').classList.add('hidden');
          }
      });
    </script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #F8FAFC; color: #0F172A; }
        .nexa-card { background: #fff; border: 1px solid #E2E8F0; border-radius: 28px; }
        .auth-screen { position: fixed; inset: 0; background: white; z-index: 1000; display: flex; flex-direction: column; padding: 2rem; }
        .hidden { display: none !important; }
        .nav-active { color: #2563EB !important; border-top: 3px solid #2563EB; border-radius: 0; }
    </style>
</head>
<body class="pb-32">

    <!-- AUTH SECTION -->
    <div id="auth-section" class="auth-screen">
        <div class="mt-10 mb-10 text-center">
            <div class="w-16 h-16 bg-blue-600 rounded-3xl mx-auto flex items-center justify-center shadow-xl mb-4 rotate-12">
                <i class="fa-solid fa-cloud text-white text-3xl -rotate-12"></i>
            </div>
            <h1 class="text-3xl font-black italic">NEXA<span class="text-blue-600">CLOUD</span></h1>
        </div>

        <div id="login-form" class="space-y-4">
            <input type="email" id="log-email" placeholder="Email" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none">
            <input type="password" id="log-pass" placeholder="Password" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none">
            <button onclick="handleLogin()" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black uppercase tracking-widest">Login</button>
            <p class="text-center text-xs font-bold text-slate-500">New here? <span class="text-blue-600" onclick="document.getElementById('login-form').classList.add('hidden'); document.getElementById('signup-form').classList.remove('hidden')">Create Account</span></p>
        </div>

        <div id="signup-form" class="space-y-4 hidden">
            <input type="email" id="sig-email" placeholder="Email" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none">
            <input type="password" id="sig-pass" placeholder="Password" class="w-full bg-slate-50 border border-slate-200 p-4 rounded-2xl outline-none">
            <button onclick="handleSignup()" class="w-full bg-blue-600 text-white p-4 rounded-2xl font-black uppercase tracking-widest">Sign Up</button>
            <p class="text-center text-xs font-bold text-slate-500">Already a member? <span class="text-blue-600" onclick="document.getElementById('signup-form').classList.add('hidden'); document.getElementById('login-form').classList.remove('hidden')">Login</span></p>
        </div>
    </div>

    <!-- APP SECTION -->
    <div id="main-app" class="hidden">
        <header class="p-6 flex justify-between items-center bg-white border-b border-slate-100 sticky top-0 z-50">
            <div class="flex items-center gap-2">
                <div class="w-10 h-10 bg-blue-600 rounded-xl flex items-center justify-center shadow-lg">
                    <i class="fa-solid fa-server text-white text-sm"></i>
                </div>
                <h1 class="text-xl font-black tracking-tighter italic">NEXA<span class="text-blue-600">CLOUD</span></h1>
            </div>
            <div class="text-right">
                <p class="text-[9px] font-black text-slate-400 uppercase">Balance</p>
                <h2 id="balance-display" class="text-lg font-black text-slate-900">$0.00</h2>
            </div>
        </header>

        <main class="p-5 space-y-6">
            <!-- Node Section -->
            <div class="nexa-card p-6 border-b-4 border-blue-600">
                <div class="flex justify-between items-start mb-4">
                    <h3 class="text-xl font-black">Cloud Cluster V.1</h3>
                    <span class="text-blue-600 font-black">$10.00</span>
                </div>
                <p class="text-xs text-slate-500 mb-6 font-medium">Earn $0.50 daily for 360 days. Secure enterprise computing.</p>
                <button onclick="alert('Deposit $10 to activate, sweetie!')" class="w-full bg-slate-900 text-white p-4 rounded-2xl font-black uppercase text-[10px] tracking-widest">Buy Now</button>
            </div>
        </main>

        <nav class="fixed bottom-6 left-6 right-6 h-20 bg-white shadow-2xl rounded-[2.5rem] border border-slate-100 flex justify-around items-center px-4">
            <button class="flex flex-col items-center text-blue-600"><i class="fa-solid fa-house"></i><span class="text-[8px] font-black uppercase mt-1">Home</span></button>
            <button onclick="handleLogout()" class="flex flex-col items-center text-slate-400"><i class="fa-solid fa-right-from-bracket"></i><span class="text-[8px] font-black uppercase mt-1">Logout</span></button>
        </nav>
    </div>

</body>
</html>
