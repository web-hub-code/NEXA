<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA | Secure Access</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        body { background: radial-gradient(circle at center, #1e293b, #0f172a); min-height: 100vh; display: flex; align-items: center; justify-content: center; overflow: hidden; }
        .glass-card { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 2rem; }
        .input-glow:focus { box-shadow: 0 0 15px rgba(59, 130, 246, 0.5); border-color: #3b82f6; }
        .slide-up { animation: slideUp 0.8s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="text-white">

    <div class="glass-card p-8 w-full max-w-md mx-4 slide-up shadow-2xl">
        <div class="text-center mb-8">
            <h1 class="text-4xl font-black tracking-tighter text-blue-500 mb-2">NEXA</h1>
            <p class="text-gray-400" id="form-title">Enter your credentials to continue</p>
        </div>

        <!-- Form -->
        <form id="auth-form" class="space-y-5">
            <div id="name-field" class="hidden">
                <label class="text-sm text-gray-400 ml-2">Full Name</label>
                <input type="text" id="name" class="w-full bg-gray-900/50 border border-gray-700 rounded-xl px-4 py-3 outline-none input-glow transition" placeholder="John Doe">
            </div>

            <div>
                <label class="text-sm text-gray-400 ml-2">Email Address</label>
                <input type="email" id="email" required class="w-full bg-gray-900/50 border border-gray-700 rounded-xl px-4 py-3 outline-none input-glow transition" placeholder="name@nexa.com">
            </div>

            <div>
                <label class="text-sm text-gray-400 ml-2">Password</label>
                <input type="password" id="password" required class="w-full bg-gray-900/50 border border-gray-700 rounded-xl px-4 py-3 outline-none input-glow transition" placeholder="••••••••">
            </div>

            <button type="submit" id="submit-btn" class="w-full bg-blue-600 hover:bg-blue-500 py-4 rounded-xl font-bold shadow-lg shadow-blue-600/20 transition-all active:scale-95">
                Login to NEXA
            </button>
        </form>

        <div class="mt-8 text-center text-sm">
            <p class="text-gray-400">
                <span id="toggle-text">Don't have an account?</span> 
                <button onclick="toggleAuth()" class="text-blue-400 font-bold hover:underline ml-1" id="toggle-btn">Register Now</button>
            </p>
        </div>
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        let isLogin = true;

        window.toggleAuth = () => {
            isLogin = !isLogin;
            document.getElementById('name-field').classList.toggle('hidden');
            document.getElementById('form-title').innerText = isLogin ? 'Enter your credentials to continue' : 'Create your free investment account';
            document.getElementById('submit-btn').innerText = isLogin ? 'Login to NEXA' : 'Create Account';
            document.getElementById('toggle-text').innerText = isLogin ? "Don't have an account?" : "Already a member?";
            document.getElementById('toggle-btn').innerText = isLogin ? 'Register Now' : 'Login';
        };

        document.getElementById('auth-form').addEventListener('submit', async (e) => {
            e.preventDefault();
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const name = document.getElementById('name').value;

            try {
                if (isLogin) {
                    await signInWithEmailAndPassword(auth, email, password);
                    alert("Welcome to NEXA!");
                    window.location.href = "dashboard.html"; 
                } else {
                    const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                    const user = userCredential.user;
                    // User data in Realtime Database
                    await set(ref(db, 'users/' + user.uid), {
                        username: name,
                        email: email,
                        balance: 0,
                        joinedDate: new Date().toISOString()
                    });
                    alert("Account Created successfully!");
                    window.location.href = "dashboard.html";
                }
            } catch (error) {
                alert(error.message);
            }
        });
    </script>
</body>
</html>
# NEXA
NEXA NEXT CRYPTO WALLET
