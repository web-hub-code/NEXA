<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Solar Energy Solutions - Professional Consultation & Leads</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f8fafc;
            color: #1e293b;
            line-height: 1.6;
        }
        header {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            color: white;
            padding: 60px 20px;
            text-align: center;
            cursor: pointer;
            user-select: none;
            position: relative;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }
        header h1 {
            font-size: 2.75rem;
            margin-bottom: 12px;
            font-weight: 700;
            letter-spacing: -0.5px;
        }
        header p {
            font-size: 1.15rem;
            opacity: 0.85;
            font-weight: 300;
        }
        /* Top Auth Bar */
        #authBar {
            position: absolute;
            top: 20px;
            right: 25px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 8px 16px;
            border-radius: 30px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 12px;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }
        #authBar button {
            background: #10b981;
            color: white;
            border: none;
            padding: 6px 14px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: 600;
            transition: background 0.2s;
        }
        #authBar button:hover {
            background: #059669;
        }
        .container {
            max-width: 960px;
            margin: -30px auto 40px auto;
            background: white;
            padding: 40px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.05);
            position: relative;
            z-index: 10;
        }
        .section-title {
            color: #0f172a;
            font-size: 1.8rem;
            margin-bottom: 20px;
            font-weight: 600;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
        }
        p {
            margin-bottom: 20px;
            font-size: 1.05rem;
            color: #475569;
        }
        /* Modern Trust Badges */
        .trust-bar {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            margin: 30px 0;
            text-align: center;
        }
        .trust-badge {
            background: #f1f5f9;
            border: 1px solid #e2e8f0;
            padding: 16px;
            border-radius: 10px;
            color: #0f172a;
            font-weight: 600;
            font-size: 0.95rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
            margin-bottom: 40px;
        }
        .feature-card {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            padding: 24px;
            border-radius: 12px;
            text-align: center;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .feature-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.05);
        }
        .feature-card h3 {
            color: #0f172a;
            margin-bottom: 10px;
            font-size: 1.15rem;
        }
        /* Modernized Widgets Styling */
        .widget-box {
            background: #f8fafc;
            padding: 30px;
            border-radius: 12px;
            border: 1px solid #e2e8f0;
            margin-top: 30px;
        }
        .widget-box h3 {
            color: #0f172a;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }
        .form-group {
            margin-bottom: 18px;
        }
        .form-group label {
            display: block;
            margin-bottom: 6px;
            font-weight: 600;
            font-size: 0.95rem;
            color: #334155;
        }
        .form-group input, .form-group select {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 1rem;
            background: white;
            transition: border-color 0.2s, box-shadow 0.2s;
        }
        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: #10b981;
            box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.15);
        }
        .submit-btn {
            background: #10b981;
            color: white;
            border: none;
            padding: 14px 20px;
            font-size: 1rem;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-weight: 600;
            transition: background 0.2s;
        }
        .submit-btn:hover {
            background: #059669;
        }
        /* Modern AI Voice Hub Card */
        .ai-hub-card {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            color: white;
            padding: 30px;
            border-radius: 12px;
            margin-top: 30px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 8px 25px rgba(15, 23, 42, 0.15);
        }
        .ai-hub-card h3 {
            color: white;
            margin-bottom: 10px;
        }
        .ai-hub-card p {
            color: #cbd5e1;
        }
        .ai-actions-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }
        @media(max-width: 768px) {
            .ai-actions-grid {
                grid-template-columns: 1fr;
            }
        }
        /* FAQ Accordion */
        .faq-item {
            background: #fff;
            border: 1px solid #e2e8f0;
            margin-bottom: 10px;
            border-radius: 8px;
            overflow: hidden;
        }
        .faq-question {
            background: #fff;
            padding: 18px;
            font-weight: 600;
            cursor: pointer;
            color: #0f172a;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .faq-answer {
            padding: 18px;
            display: none;
            color: #475569;
            background: #f8fafc;
            border-top: 1px solid #e2e8f0;
        }
        /* Modals */
        #authModal, #adminModal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(15, 23, 42, 0.6);
            backdrop-filter: blur(5px);
            z-index: 9999;
            justify-content: center;
            align-items: center;
        }
        .auth-content, .admin-content {
            background: white;
            padding: 35px;
            border-radius: 16px;
            width: 90%;
            max-width: 500px;
            position: relative;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        .admin-content {
            max-width: 800px;
            max-height: 85vh;
            overflow-y: auto;
        }
        .close-btn {
            position: absolute;
            top: 20px;
            right: 25px;
            font-size: 1.5rem;
            cursor: pointer;
            color: #94a3b8;
            transition: color 0.2s;
        }
        .close-btn:hover {
            color: #0f172a;
        }
        .google-btn {
            background: #ef4444;
            color: white;
            border: none;
            padding: 12px;
            width: 100%;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            margin-top: 12px;
            transition: background 0.2s;
        }
        .google-btn:hover {
            background: #dc2626;
        }
        /* Status Badge */
        #callStatusBadge {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: #ecfdf5;
            color: #065f46;
            padding: 8px 16px;
            border-radius: 30px;
            font-size: 0.9rem;
            font-weight: 600;
            margin-bottom: 25px;
            border: 1px solid #a7f3d0;
        }
        /* Toast Notification */
        #toastNotification {
            position: fixed;
            bottom: 30px;
            left: 30px;
            background: #0f172a;
            color: white;
            padding: 14px 22px;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
            font-size: 0.95rem;
            z-index: 999;
            display: none;
            transition: opacity 0.4s ease;
            border: 1px solid rgba(255,255,255,0.1);
        }
        .lead-item {
            background: #f8fafc;
            padding: 16px;
            margin-bottom: 12px;
            border-radius: 8px;
            border-left: 4px solid #10b981;
            font-size: 0.95rem;
            border-top: 1px solid #e2e8f0;
            border-right: 1px solid #e2e8f0;
            border-bottom: 1px solid #e2e8f0;
        }
        footer {
            text-align: center;
            padding: 30px;
            color: #64748b;
            font-size: 0.9rem;
            margin-top: 40px;
            border-top: 1px solid #e2e8f0;
        }
    </style>
</head>
<body>

    <!-- Header (Tap 4 times quickly for secret admin panel) -->
    <header id="secretTrigger">
        <div id="authBar">
            <span id="userDisplay">Guest</span>
            <button id="authBtn">Login</button>
        </div>
        <h1>Solar Energy Solutions</h1>
        <p>Empowering Your Property with Clean, Intelligent Renewable Power</p>
    </header>

    <div class="container">
        <div id="callStatusBadge">
            <span style="width: 8px; height: 8px; background: #10b981; border-radius: 50%; display: inline-block;"></span>
            AI Assistant Suzanne Ready
        </div>
        
        <h2 class="section-title">Comprehensive Solar Consultation Hub</h2>
        <p>Speak directly with our advanced AI voice expert <strong>Suzanne Foster</strong> using the modern widget at the bottom-right, or complete our comprehensive A-to-Z qualifying questionnaire below to get your precise customized proposal instantly.</p>
        
        <!-- Trust Badges Bar -->
        <div class="trust-bar">
            <div class="trust-badge">🛡️ 25-Year Warranty</div>
            <div class="trust-badge">⚡ 0-Down Financing</div>
            <div class="trust-badge">👷 100% Certified Engineers</div>
        </div>

        <div class="features">
            <div class="feature-card">
                <h3>A-to-Z Qualification</h3>
                <p>Complete data capture for roof orientation, shading, and power needs.</p>
            </div>
            <div class="feature-card">
                <h3>Real-time AI Sync</h3>
                <p>Seamlessly syncs voice conversations and form entries directly to admin dashboard.</p>
            </div>
            <div class="feature-card">
                <h3>Instant ROI Forecast</h3>
                <p>Accurate estimation of annual savings and payback duration.</p>
            </div>
        </div>

        <!-- Modern AI Voice Call Session & A-to-Z Qualification Hub -->
        <div class="ai-hub-card">
            <h3>🎙️ Modern AI Voice & Live Qualification Sync</h3>
            <p style="font-size: 0.95rem; margin-bottom: 15px;">Talk with Suzanne via the floating voice widget, then instantly log your live A-to-Z qualifying parameters to the central database.</p>
            
            <div class="ai-actions-grid">
                <div>
                    <label style="color: #cbd5e1; font-size: 0.85rem; margin-bottom: 5px; display:block;">Voice Session Status:</label>
                    <input type="text" id="aiSessionNotes" placeholder="e.g. Discussed 10kW system & roof shade" style="background: rgba(255,255,255,0.1); border: 1px solid rgba(255,255,255,0.2); color: white;">
                </div>
                <div style="display: flex; align-items: flex-end;">
                    <button type="button" class="submit-btn" id="logAiCallBtn" style="background: #10b981; height: 46px;">Sync Voice Consultation Data</button>
                </div>
            </div>
            <p id="aiLogMsg" style="margin-top: 12px; font-weight: 600; color: #34d399; font-size: 0.9rem; display: none;"></p>
        </div>

        <!-- Interactive Solar Savings & ROI Calculator -->
        <div class="widget-box">
            <h3>⚡ Interactive Solar Savings & ROI Calculator</h3>
            <div class="form-group">
                <label for="monthlyBill">Enter Monthly Electricity Bill ($):</label>
                <input type="number" id="monthlyBill" placeholder="e.g. 250" oninput="calculateSavings()">
            </div>
            <div id="savingsResult" style="background: #e2e8f0; padding: 18px; border-radius: 8px; font-weight: bold; color: #0f172a; display: none;">
                Estimated Annual Savings: <span id="savedAmount" style="color: #059669; font-size: 1.25rem;">$0</span><br>
                Estimated System Payback Period: <span id="paybackPeriod" style="color: #0f172a;">3.1 Years</span>
            </div>
        </div>

        <!-- Comprehensive A-to-Z Qualifying Questionnaire Wizard -->
        <div class="widget-box" style="margin-top: 30px;">
            <h3>📋 Complete A-to-Z Solar Qualifying Questionnaire</h3>
            <p style="font-size: 0.9rem; color: #64748b; margin-bottom: 20px;">Provide complete details so our engineers and AI specialist Suzanne can prepare your exact system configuration.</p>
            
            <form id="wizardForm">
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <div class="form-group">
                        <label>1. Property Ownership Status:</label>
                        <select id="ownership" required>
                            <option value="">Select option</option>
                            <option value="Yes - Homeowner">Yes, I own the property</option>
                            <option value="No - Renter">No, I rent</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>2. Roof Type & Condition:</label>
                        <select id="roofType" required>
                            <option value="">Select roof type</option>
                            <option value="Shingle - Excellent Sun">Asphalt Shingle (Full Sun)</option>
                            <option value="Tile - Partial Shade">Tile Roof (Partial Shade)</option>
                            <option value="Metal - Flat / Sloped">Metal Roof</option>
                        </select>
                    </div>
                </div>

                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <div class="form-group">
                        <label>3. Average Monthly Power Bill:</label>
                        <select id="billRange" required>
                            <option value="">Select range</option>
                            <option value="$100 - $200">$100 - $200 / month</option>
                            <option value="$200 - $400">$200 - $400 / month</option>
                            <option value="$400+">$400+ / month</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>4. Primary Energy Goal:</label>
                        <select id="energyGoal" required>
                            <option value="">Select primary goal</option>
                            <option value="Max Bill Reduction">Maximum Bill Reduction</option>
                            <option value="Battery Backup Protection">Backup Protection (Outages)</option>
                            <option value="Complete Energy Independence">Complete Off-Grid Independence</option>
                        </select>
                    </div>
                </div>

                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <div class="form-group">
                        <label>5. Full Name:</label>
                        <input type="text" id="wizName" placeholder="Enter your full name" required>
                    </div>
                    <div class="form-group">
                        <label>6. Phone / WhatsApp Number:</label>
                        <input type="tel" id="wizPhone" placeholder="e.g. +92 300 1234567" required>
                    </div>
                </div>

                <div class="form-group">
                    <label>7. Property Address / City:</label>
                    <input type="text" id="wizAddress" placeholder="Enter city or street address" required>
                </div>

                <button type="submit" class="submit-btn" style="margin-top: 10px;">Submit A-to-Z Qualification Profile</button>
            </form>
            <p id="wizardResponseMsg" style="margin-top: 12px; font-weight: 600; color: #10b981; display: none;"></p>
        </div>

        <!-- FAQ Accordion Section -->
        <div class="widget-box" style="margin-top: 30px;">
            <h3>❓ Frequently Asked Questions</h3>
            <div class="faq-item">
                <div class="faq-question">How long do solar panel installations take? <span>+</span></div>
                <div class="faq-answer">Standard residential installations typically take between 1 to 3 days depending on system capacity and roof layout.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">Will my system function during grid power outages? <span>+</span></div>
                <div class="faq-answer">Grid-tied systems automatically shut down during blackouts for safety unless paired with an integrated battery backup solution.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">What kind of maintenance is required? <span>+</span></div>
                <div class="faq-answer">Solar setups require very minimal upkeep—typically just an occasional annual rinse to remove dust or debris.</div>
            </div>
        </div>
    </div>

    <!-- Live Social Proof Toast Notification -->
    <div id="toastNotification">🔔 Ahmed from Islamabad just completed a solar qualification wizard!</div>

    <!-- Login / Sign-up Modal -->
    <div id="authModal">
        <div class="auth-content">
            <span class="close-btn" id="closeAuth">&times;</span>
            <h2 style="color: #0f172a; margin-bottom: 20px;">Account Access</h2>
            <form id="emailAuthForm">
                <div class="form-group">
                    <input type="email" id="authEmail" placeholder="Email Address" required>
                </div>
                <div class="form-group">
                    <input type="password" id="authPassword" placeholder="Password" required>
                </div>
                <button type="submit" class="submit-btn" id="emailAuthBtn">Login / Sign Up</button>
            </form>
            <p style="margin: 20px 0 10px 0; font-size: 0.9rem; color: #64748b; text-align: center;">OR</p>
            <button class="google-btn" id="googleLoginBtn">Sign in with Google</button>
            <p id="authErrorMsg" style="margin-top: 12px; color: #ef4444; font-size: 0.9rem; display: none; text-align: center;"></p>
        </div>
    </div>

    <!-- Secret Admin Panel Modal -->
    <div id="adminModal">
        <div class="admin-content">
            <span class="close-btn" id="closeAdmin">&times;</span>
            <h2 style="color: #0f172a; margin-bottom: 10px;">🔒 Realtime A-to-Z Leads & AI Voice Logs</h2>
            <p style="font-size: 0.95rem; color: #64748b; margin-bottom: 20px;">Live synchronized customer parameters and consultation transcripts:</p>
            <div id="leadsContainer">
                <p>Loading realtime records from database...</p>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2026 Solar Energy Solutions. All rights reserved. Powered by Vapi AI & Firebase.
    </footer>

    <!-- Firebase SDKs & Core Logic -->
    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
      import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
      import { getAuth, signInWithPopup, GoogleAuthProvider, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
      
      const firebaseConfig = {
        apiKey: "AIzaSyCSD1O9tV7xDZu_kljq-0NMhA2DqtW5quE",
        authDomain: "live-chat-b810c.firebaseapp.com",
        databaseURL: "https://live-chat-b810c-default-rtdb.firebaseio.com",
        projectId: "live-chat-b810c",
        storageBucket: "live-chat-b810c.firebasestorage.app",
        messagingSenderId: "555058795334",
        appId: "1:555058795334:web:f668887409800c32970b47"
      };

      const app = initializeApp(firebaseConfig);
      const db = getDatabase(app);
      const auth = getAuth(app);
      const googleProvider = new GoogleAuthProvider();

      let currentUserEmail = "Guest";

      onAuthStateChanged(auth, (user) => {
          const userDisplay = document.getElementById("userDisplay");
          const authBtn = document.getElementById("authBtn");
          if (user) {
              currentUserEmail = user.email || user.displayName || "User";
              userDisplay.innerText = currentUserEmail.split('@')[0];
              authBtn.innerText = "Logout";
          } else {
              currentUserEmail = "Guest";
              userDisplay.innerText = "Guest";
              authBtn.innerText = "Login";
          }
      });

      const authModal = document.getElementById("authModal");
      const authBtn = document.getElementById("authBtn");
      const closeAuth = document.getElementById("closeAuth");

      authBtn.addEventListener("click", (e) => {
          e.stopPropagation();
          if (auth.currentUser) {
              signOut(auth).then(() => { alert("Logged out successfully."); });
          } else {
              authModal.style.display = "flex";
          }
      });

      closeAuth.addEventListener("click", () => { authModal.style.display = "none"; });

      document.getElementById("googleLoginBtn").addEventListener("click", () => {
          signInWithPopup(auth, googleProvider)
              .then(() => { authModal.style.display = "none"; })
              .catch((error) => {
                  document.getElementById("authErrorMsg").style.display = "block";
                  document.getElementById("authErrorMsg").innerText = error.message;
              });
      });

      const emailAuthForm = document.getElementById("emailAuthForm");
      emailAuthForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const email = document.getElementById("authEmail").value;
          const password = document.getElementById("authPassword").value;
          const errorMsg = document.getElementById("authErrorMsg");

          signInWithEmailAndPassword(auth, email, password)
              .then(() => { authModal.style.display = "none"; })
              .catch(() => {
                  createUserWithEmailAndPassword(auth, email, password)
                      .then(() => { authModal.style.display = "none"; })
                      .catch((err) => {
                          errorMsg.style.display = "block";
                          errorMsg.innerText = err.message;
                      });
              });
      });

      window.calculateSavings = function() {
          const bill = parseFloat(document.getElementById("monthlyBill").value) || 0;
          const annualSavings = Math.round(bill * 12 * 0.75); 
          const resBox = document.getElementById("savingsResult");
          const savedSpan = document.getElementById("savedAmount");
          const paybackSpan = document.getElementById("paybackPeriod");
          if (bill > 0) {
              resBox.style.display = "block";
              savedSpan.innerText = "$" + annualSavings.toLocaleString();
              let payback = ( (bill * 12 * 3.5) / annualSavings ).toFixed(1);
              paybackSpan.innerText = payback + " Years";
          } else {
              resBox.style.display = "none";
          }
      };

      document.querySelectorAll(".faq-question").forEach(item => {
          item.addEventListener("click", () => {
              const answer = item.nextElementSibling;
              const isOpen = answer.style.display === "block";
              document.querySelectorAll(".faq-answer").forEach(ans => ans.style.display = "none");
              answer.style.display = isOpen ? "none" : "block";
          });
      });

      // A-to-Z Questionnaire Wizard Submission
      const wizardForm = document.getElementById("wizardForm");
      const wizardMsg = document.getElementById("wizardResponseMsg");

      wizardForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const ownership = document.getElementById("ownership").value;
          const roofType = document.getElementById("roofType").value;
          const billRange = document.getElementById("billRange").value;
          const energyGoal = document.getElementById("energyGoal").value;
          const name = document.getElementById("wizName").value;
          const phone = document.getElementById("wizPhone").value;
          const address = document.getElementById("wizAddress").value;
          const timestamp = new Date().toLocaleString();

          const leadsRef = ref(db, 'leads');
          push(leadsRef, {
              type: "A-to-Z Qualification Wizard",
              user: currentUserEmail,
              name: name,
              phone: phone,
              ownership: ownership,
              roofType: roofType,
              billRange: billRange,
              energyGoal: energyGoal,
              address: address,
              timestamp: timestamp
          }).then(() => {
              wizardMsg.style.display = "block";
              wizardMsg.innerText = "Success! Your A-to-Z qualification profile has been saved.";
              wizardForm.reset();
              setTimeout(() => { wizardMsg.style.display = "none"; }, 5000);
          }).catch((error) => {
              alert("Error: " + error.message);
          });
      });

      // AI Voice Call Sync Button Handler
      const logAiCallBtn = document.getElementById("logAiCallBtn");
      const aiLogMsg = document.getElementById("aiLogMsg");
      const aiSessionNotes = document.getElementById("aiSessionNotes");

      logAiCallBtn.addEventListener("click", () => {
          const timestamp = new Date().toLocaleString();
          const notes = aiSessionNotes.value || "Completed voice consultation with Suzanne";
          const leadsRef = ref(db, 'leads');
          
          push(leadsRef, {
              type: "Suzanne AI Voice Consultation",
              user: currentUserEmail,
              name: currentUserEmail,
              phone: "Live Voice Call Hub",
              ownership: "Captured via AI Voice",
              roofType: "Assessed by Suzanne",
              billRange: "Discussed on Call",
              energyGoal: notes,
              address: "Voice Session Widget",
              timestamp: timestamp
          }).then(() => {
              aiLogMsg.style.display = "block";
              aiLogMsg.innerText = "✅ Voice session and qualifying notes synced to admin database!";
              aiSessionNotes.value = "";
              setTimeout(() => { aiLogMsg.style.display = "none"; }, 4000);
          }).catch((err) => {
              alert("Error syncing session: " + err.message);
          });
      });

      const toasts = [
          "🔔 Ali from Lahore completed the A-to-Z solar wizard!",
          "🔔 Sara from Karachi connected with Suzanne Foster!",
          "🔔 Bilal from Rawalpindi submitted system requirements!",
          "🔔 Usman from Islamabad checked estimated solar ROI!"
      ];
      
      function showToast() {
          const toast = document.getElementById("toastNotification");
          toast.innerText = toasts[Math.floor(Math.random() * toasts.length)];
          toast.style.display = "block";
          toast.style.opacity = "1";
          setTimeout(() => {
              toast.style.opacity = "0";
              setTimeout(() => { toast.style.display = "none"; }, 500);
          }, 4000);
      }
      setInterval(showToast, 13000);

      // Secret Admin Panel 4-Tap Trigger with PIN 5426
      let tapCount = 0;
      let tapTimer = null;
      const trigger = document.getElementById("secretTrigger");
      const modal = document.getElementById("adminModal");
      const closeBtn = document.getElementById("closeAdmin");
      const leadsContainer = document.getElementById("leadsContainer");

      trigger.addEventListener("click", () => {
          tapCount++;
          clearTimeout(tapTimer);
          if (tapCount === 4) {
              tapCount = 0;
              let enteredPin = prompt("Enter Secret Admin PIN:");
              if (enteredPin === "5426") {
                  modal.style.display = "flex";
                  fetchRealtimeLeads();
              } else if (enteredPin !== null) {
                  alert("Incorrect Secret PIN!");
              }
          } else {
              tapTimer = setTimeout(() => { tapCount = 0; }, 600);
          }
      });

      closeBtn.addEventListener("click", () => { modal.style.display = "none"; });
      window.addEventListener("click", (e) => { e.target === modal && (modal.style.display = "none"); });

      function fetchRealtimeLeads() {
          const leadsRef = ref(db, 'leads');
          onValue(leadsRef, (snapshot) => {
              const data = snapshot.val();
              leadsContainer.innerHTML = "";
              if (!data) {
                  leadsContainer.innerHTML = "<p>No records found yet.</p>";
                  return;
              }

              Object.keys(data).reverse().forEach(key => {
                  const item = data[key];
                  const leadDiv = document.createElement("div");
                  leadDiv.className = "lead-item";
                  leadDiv.innerHTML = `
                      <span style="background: #e2e8f0; color: #0f172a; padding: 3px 10px; border-radius: 4px; font-size: 0.8rem; font-weight: 700;">${item.type || 'Record'}</span><br><br>
                      <strong>User Account:</strong> ${item.user || 'Guest'}<br>
                      <strong>Name:</strong> ${item.name || 'N/A'}<br>
                      <strong>Phone:</strong> ${item.phone || 'N/A'}<br>
                      <strong>Ownership:</strong> ${item.ownership || 'N/A'}<br>
                      <strong>Roof Type:</strong> ${item.roofType || 'N/A'}<br>
                      <strong>Bill / Range:</strong> ${item.billRange || 'N/A'}<br>
                      <strong>Energy Goal / Notes:</strong> ${item.energyGoal || 'N/A'}<br>
                      <strong>Address:</strong> ${item.address || 'N/A'}<br>
                      <small style="color: #64748b;">Timestamp: ${item.timestamp || 'Recent'}</small>
                  `;
                  leadsContainer.appendChild(leadDiv);
              });
          }, (error) => {
              leadsContainer.innerHTML = `<p style="color: red;">Error loading records: ${error.message}</p>`;
          });
      }
    </script>

    <!-- Vapi Web Widget SDK Script -->
    <script
      src="https://cdn.jsdelivr.net/gh/VapiAI/html-script-tag@latest/dist/assets/index.js"
      defer
    ></script>
    <script>
      window.addEventListener("DOMContentLoaded", () => {
        window.vapiSDK.run({
          apiKey: "e0ffb174-f51f-418d-87c9-93ea7f72810b",
          assistant: "1fce054b-91d4-4d60-9f39-9af04c51279a",
          config: {
            position: "bottom-right",
            offset: "30px",
            width: "320px",
            height: "520px",
            idle: {
              color: "#10b981",
              type: "pill",
              title: "Talk with Suzanne",
              subtitle: "Solar Expert",
              icon: "https://unpkg.com/lucide-static@latest/icons/phone.svg"
            }
          }
        });
      });
    </script>
</body>
</html>
