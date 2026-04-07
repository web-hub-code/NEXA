<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA | Join the Future</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&display=swap');
        
        body {
            font-family: 'Outfit', sans-serif;
            background: #020617;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Animated Colorful Background Shapes */
        .shape {
            position: absolute;
            filter: blur(80px);
            z-index: -1;
            border-radius: 50%;
            animation: move 10s infinite alternate;
        }
        .shape-1 { width: 300px; height: 300px; background: #3b82f6; top: -10%; left: -10%; }
        .shape-2 { width: 400px; height: 400px; background: #db2777; bottom: -10%; right: -10%; animation-delay: 2s; }
        
        @keyframes move {
            from { transform: translate(0, 0); }
            to { transform: translate(50px, 100px); }
        }

        .glass-box {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        .input-style {
            background: rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s ease;
        }

        .input-style:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 15px rgba(59, 130, 246, 0.3);
            outline: none;
        }

        .gradient-btn {
            background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 50%, #ec4899 100%);
            background-size: 200% auto;
            transition: 0.5s;
        }

        .gradient-btn:hover {
            background-position: right center;
            transform: translateY(-2px);
        }
    </style>
</head>
<body class="text-white p-4">

    <div class="shape shape-1"></div>
    <div class="shape shape-2"></div>

    <div class="glass-box w-full max-w-md p-8 rounded-[2.5rem] relative overflow-hidden">
        
        <!-- Header -->
        <div class="text-center mb-10">
            <h1 class="text-5xl font-extrabold tracking-tighter bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-pink-500 mb-2">NEXA</h1>
            <p id="status-text" class="text-gray-400 text-sm">Welcome back! Please login to your account.</p>
        </div>

        <!-- Form Section -->
        <form id="nexa-auth" class="space-y-4">
            <!-- Username (Hidden on Login) -->
            <div id="user-group" class="hidden transition-all duration-500">
                <div class="relative">
                    <i class="fa-solid fa-user absolute left-4 top-4 text-gray-500"></i>
                    <input type="text" id="username" class="input-style w-full pl-12 pr-4 py-3.5 rounded-2xl text-sm" placeholder="Full Name">
                </div>
            </div>

            <!-- Email -->
            <div class="relative">
                <i class="fa-solid fa-envelope absolute left-4 top-4 text-gray-500"></i>
                <input type="email" id="email" required class="input-style w-full pl-12 pr-4 py-3.5 rounded-2xl text-sm" placeholder="Email Address">
            </div>

            <!-- Password -->
            <div class="relative">
                <i class="fa-solid fa-lock absolute left-4 top-4 text-gray-500"></i>
                <input type="password" id="password" required class="input-style w-full pl-12 pr-4 py-3.5 rounded-2xl text-sm" placeholder="Password">
            </div>

            <!-- Submit Button -->
            <button type="submit" id="main-btn" class="gradient-btn w-full py-4 rounded-2xl font-bold text-lg shadow-xl shadow-blue-900/20">
                Login
            </button>
        </form>

        <!-- Footer Toggle -->
        <div class="mt-8 text-center">
            <p class="text-gray-500 text-sm">
                <span id="toggle-desc">Don't have an account?</span>
                <button onclick="switchMode()" id="toggle-link" class="text-blue-400 font-bold ml-1 hover:text-pink-400 transition">Create Account</button>
            </p>
        </div>

    </div>

    <!-- Firebase Logic -->
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

        window.switchMode = () => {
            isLogin = !isLogin;
            const userGroup = document.getElementById('user-group');
            const mainBtn = document.getElementById('main-btn');
            const statusText = document.getElementById('status-text');
            const toggleDesc = document.getElementById('toggle-desc');
            const toggleLink = document.getElementById('toggle-link');

            if(!isLogin) {
                userGroup.classList.remove('hidden');
                mainBtn.innerText = "Register Now";
                statusText.innerText = "Join NEXA and start earning today!";
                toggleDesc.innerText = "Already have an account?";
                toggleLink.innerText = "Login here";
            } else {
                userGroup.classList.add('hidden');
                mainBtn.innerText = "Login";
                statusText.innerText = "Welcome back! Please login to your account.";
                toggleDesc.innerText = "Don't have an account?";
                toggleLink.innerText = "Create Account";
            }
        };

        document.getElementById('nexa-auth').addEventListener('submit', async (e) => {
            e.preventDefault();
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const name = document.getElementById('username').value;

            try {
                if(isLogin) {
                    await signInWithEmailAndPassword(auth, email, password);
                    alert("Sweetie, Login Successful! Redirecting...");
                    window.location.href = "dashboard.html";
                } else {
                    const res = await createUserWithEmailAndPassword(auth, email, password);
                    await set(ref(db, 'users/' + res.user.uid), {
                        username: name,
                        email: email,
                        balance: 0,
                        plans: "None",
                        joined: new Date().toISOString()
                    });
                    alert("Account Created! Welcome to NEXA, sweetie.");
                    window.location.href = "dashboard.html";
                }
            } catch (err) {
                alert("Error: " + err.message);
            }
        });
    </script>
</body>
</html>
