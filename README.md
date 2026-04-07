<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXA | Secure Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap');
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: #030712;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow-x: hidden;
        }

        /* Moving Gradient Background */
        .bg-animate {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at 20% 30%, #1e3a8a 0%, transparent 40%),
                        radial-gradient(circle at 80% 70%, #701a75 0%, transparent 40%);
            z-index: -1;
            filter: blur(50px);
            animation: moveBg 15s infinite alternate;
        }

        @keyframes moveBg {
            0% { transform: scale(1); }
            100% { transform: scale(1.1) translate(20px, 20px); }
        }

        .glass-card {
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 0 40px rgba(0, 0, 0, 0.5);
            border-radius: 2.5rem;
        }

        .input-box {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .input-box:focus-within {
            border-color: #3b82f6;
            box-shadow: 0 0 20px rgba(59, 130, 246, 0.2);
        }

        .btn-prime {
            background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 100%);
            transition: 0.3s;
        }

        .btn-prime:hover {
            box-shadow: 0 10px 25px rgba(59, 130, 246, 0.4);
            transform: translateY(-2px);
        }
    </style>
</head>
<body class="text-white p-6">

    <div class="bg-animate"></div>

    <div class="glass-card w-full max-w-md p-10 relative overflow-hidden">
        <!-- Logo Section -->
        <div class="text-center mb-10">
            <h1 class="text-4xl font-extrabold tracking-tighter bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-500">NEXA</h1>
            <p id="form-subtitle" class="text-gray-400 text-sm mt-2">Secure Anonymous Investment Protocol</p>
        </div>

        <form id="auth-form" class="space-y-5">
            <!-- Full Name (Only for Signup) -->
            <div id="name-container" class="input-box flex items-center rounded-2xl px-4 py-3">
                <i class="fa-solid fa-id-card text-gray-500 mr-3"></i>
                <input type="text" id="full-name" class="bg-transparent w-full outline-none text-sm" placeholder="Full Name">
            </div>

            <!-- Username -->
            <div class="input-box flex items-center rounded-2xl px-4 py-3">
                <i class="fa-solid fa-at text-gray-500 mr-3"></i>
                <input type="text" id="username" required class="bg-transparent w-full outline-none text-sm" placeholder="Username">
            </div>

            <!-- Private Access Key (Acts like Password for security feel) -->
            <div class="input-box flex items-center rounded-2xl px-4 py-3">
                <i class="fa-solid fa-key text-gray-500 mr-3"></i>
                <input type="password" id="access-key" required class="bg-transparent w-full outline-none text-sm" placeholder="Private Access Key">
            </div>

            <button type="submit" id="submit-btn" class="btn-prime w-full py-4 rounded-2xl font-bold tracking-wide uppercase text-sm shadow-lg">
                Create Secure Account
            </button>
        </form>

        <div class="mt-8 text-center text-sm">
            <p class="text-gray-500">
                <span id="toggle-text">Already have a NEXA ID?</span>
                <button onclick="toggleMode()" id="toggle-btn" class="text-blue-400 font-bold ml-1 hover:underline">Login</button>
            </p>
        </div>

        <!-- Security Badge -->
        <div class="mt-6 flex justify-center items-center gap-2 opacity-50">
            <i class="fa-solid fa-shield-halved text-xs text-green-400"></i>
            <span class="text-[10px] uppercase tracking-widest font-bold">End-to-End Encrypted</span>
        </div>
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, set, get } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        let isLogin = false;

        window.toggleMode = () => {
            isLogin = !isLogin;
            const nameField = document.getElementById('name-container');
            const submitBtn = document.getElementById('submit-btn');
            const toggleBtn = document.getElementById('toggle-btn');
            const toggleText = document.getElementById('toggle-text');

            if (isLogin) {
                nameField.style.display = 'none';
                submitBtn.innerText = 'Login to NEXA';
                toggleText.innerText = "Don't have an account?";
                toggleBtn.innerText = 'Sign Up';
            } else {
                nameField.style.display = 'flex';
                submitBtn.innerText = 'Create Secure Account';
                toggleText.innerText = "Already have a NEXA ID?";
                toggleBtn.innerText = 'Login';
            }
        };

        document.getElementById('auth-form').addEventListener('submit', async (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const fullName = document.getElementById('full-name').value;
            
            try {
                // Professional Loading Feel
                document.getElementById('submit-btn').innerText = "Verifying Protocol...";
                
                // Anonymous Authentication in Background
                const cred = await signInAnonymously(auth);
                const user = cred.user;

                // Check LocalStorage to link session
                localStorage.setItem('nexa_session', user.uid);
                localStorage.setItem('nexa_user', username);

                const userRef = ref(db, 'users/' + user.uid);
                const snapshot = await get(userRef);

                if (!snapshot.exists()) {
                    // Create Account in DB
                    await set(userRef, {
                        uid: user.uid,
                        username: username,
                        fullName: fullName || "NEXA Investor",
                        balance: 0,
                        status: "Verified",
                        joinedAt: new Date().toLocaleDateString()
                    });
                }

                alert(`Success sweetie! Account ${isLogin ? 'Verified' : 'Created'}.`);
                window.location.href = "dashboard.html";

            } catch (error) {
                alert("Security Protocol Failed: " + error.message);
                document.getElementById('submit-btn').innerText = isLogin ? "Login" : "Create Account";
            }
        });
    </script>
</body>
</html>
