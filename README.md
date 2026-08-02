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
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f7f6;
            color: #333;
            line-height: 1.6;
        }
        header {
            background: linear-gradient(135deg, #1b4d3e, #2c7a5f);
            color: white;
            padding: 50px 20px;
            text-align: center;
            cursor: pointer;
            user-select: none;
            position: relative;
        }
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        /* Top Auth Bar */
        #authBar {
            position: absolute;
            top: 15px;
            right: 20px;
            background: rgba(255, 255, 255, 0.2);
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        #authBar button {
            background: white;
            color: #1b4d3e;
            border: none;
            padding: 5px 12px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
        }
        .container {
            max-width: 900px;
            margin: 40px auto;
            background: white;
            padding: 40px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }
        .section-title {
            color: #1b4d3e;
            font-size: 1.8rem;
            margin-bottom: 20px;
            border-bottom: 2px solid #2c7a5f;
            padding-bottom: 8px;
        }
        p {
            margin-bottom: 20px;
            font-size: 1.1rem;
        }
        /* Trust Badges Bar */
        .trust-bar {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            margin: 30px 0;
            text-align: center;
        }
        .trust-badge {
            background: #e8f5e9;
            border: 1px solid #c8e6c9;
            padding: 15px;
            border-radius: 8px;
            color: #1b4d3e;
            font-weight: bold;
            font-size: 0.95rem;
        }
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
            margin-bottom: 40px;
        }
        .feature-card {
            background: #f9fbfb;
            border: 1px solid #e2e8f0;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
        }
        .feature-card h3 {
            color: #2c7a5f;
            margin-bottom: 10px;
        }
        /* Modern Widgets Styling */
        .widget-box {
            background: #f1f5f9;
            padding: 25px;
            border-radius: 8px;
            border: 1px solid #cbd5e1;
            margin-top: 30px;
        }
        .widget-box h3 {
            color: #1b4d3e;
            margin-bottom: 15px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group input, .form-group select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 1rem;
        }
        .submit-btn {
            background: #2c7a5f;
            color: white;
            border: none;
            padding: 12px 20px;
            font-size: 1rem;
            border-radius: 6px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
        }
        .submit-btn:hover {
            background: #1b4d3e;
        }
        /* FAQ Accordion Styling */
        .faq-item {
            background: #fff;
            border: 1px solid #e2e8f0;
            margin-bottom: 10px;
            border-radius: 6px;
            overflow: hidden;
        }
        .faq-question {
            background: #f8fafc;
            padding: 15px;
            font-weight: bold;
            cursor: pointer;
            color: #1b4d3e;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .faq-answer {
            padding: 15px;
            display: none;
            color: #4b5563;
            background: #fff;
            border-top: 1px solid #e2e8f0;
        }
        /* Auth Modal Styling */
        #authModal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 9999;
            justify-content: center;
            align-items: center;
        }
        .auth-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 400px;
            text-align: center;
            position: relative;
        }
        .google-btn {
            background: #db4437;
            color: white;
            border: none;
            padding: 12px;
            width: 100%;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 15px;
        }
        .google-btn:hover {
            background: #c33d2e;
        }
        /* Status Badge */
        #callStatusBadge {
            display: inline-block;
            background: #e2e8f0;
            color: #333;
            padding: 6px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
            margin-bottom: 20px;
        }
        /* Vapi Voice Call Button */
        .vapi-btn {
            background: #27ae60;
            color: white;
            border: none;
            padding: 14px 25px;
            font-size: 1.1rem;
            border-radius: 30px;
            cursor: pointer;
            font-weight: bold;
            box-shadow: 0 4px 10px rgba(39, 174, 96, 0.3);
            display: inline-flex;
            align-items: center;
            gap: 10px;
            transition: background 0.3s ease;
        }
        .vapi-btn:hover {
            background: #219653;
        }
        .vapi-btn.active {
            background: #c0392b;
        }
        /* Toast Notification */
        #toastNotification {
            position: fixed;
            bottom: 20px;
            left: 20px;
            background: #1b4d3e;
            color: white;
            padding: 12px 20px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            font-size: 0.9rem;
            z-index: 999;
            display: none;
            transition: opacity 0.5s ease;
        }
        /* Secret Admin Modal Styling */
        #adminModal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 9999;
            justify-content: center;
            align-items: center;
        }
        .admin-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 700px;
            max-height: 80vh;
            overflow-y: auto;
            position: relative;
        }
        .close-btn {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }
        .lead-item {
            background: #f1f5f9;
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 6px;
            border-left: 4px solid #2c7a5f;
            font-size: 0.95rem;
        }
        footer {
            text-align: center;
            padding: 20px;
            color: #777;
            font-size: 0.9rem;
            margin-top: 40px;
        }
    </style>
</head>
<body>

    <!-- Header acts as secret trigger (Tap 4 times quickly) -->
    <header id="secretTrigger">
        <div id="authBar">
            <span id="userDisplay">Guest</span>
            <button id="authBtn">Login</button>
        </div>
        <h1>Solar Energy Solutions</h1>
        <p>Empowering Your Property with Clean, Renewable Power</p>
    </header>

    <div class="container">
        <div id="callStatusBadge">Status: Ready to Connect</div>
        <h2 class="section-title">Welcome to Our Consultation Portal</h2>
        <p>Discover how much you can save on your monthly utility bills with customized solar energy installations. Speak directly with our AI energy specialist, Suzanne Foster, right now or use our interactive tools below.</p>
        
        <!-- Vapi AI Voice Widget Section -->
        <div class="widget-box" style="text-align: center; background: #e8f5e9; border-color: #c8e6c9;">
            <h3>🎙️ Talk Live with Suzanne Foster (AI Energy Specialist)</h3>
            <p style="font-size: 1rem; margin-bottom: 15px;">Have questions about solar panels, federal tax credits, or financing? Tap below to start a live voice conversation instantly.</p>
            <button id="vapiCallBtn" class="vapi-btn">📞 Start Voice Call</button>
        </div>

        <!-- Trust Badges Bar -->
        <div class="trust-bar">
            <div class="trust-badge">🛡️ 25-Year Performance Warranty</div>
            <div class="trust-badge">⚡ 0-Down Financing Options</div>
            <div class="trust-badge">👷 100% Certified Solar Experts</div>
        </div>

        <div class="features">
            <div class="feature-card">
                <h3>Instant Eligibility</h3>
                <p>Quick assessment of your roof space and electricity consumption.</p>
            </div>
            <div class="feature-card">
                <h3>Tailored Savings</h3>
                <p>Learn about customized solar packages designed for your home.</p>
            </div>
            <div class="feature-card">
                <h3>Expert Callback</h3>
                <p>Connect with a senior solar consultant at your convenience.</p>
            </div>
        </div>

        <!-- Interactive Solar Savings & ROI Calculator -->
        <div class="widget-box">
            <h3>⚡ Interactive Solar Savings & ROI Calculator</h3>
            <div class="form-group">
                <label for="monthlyBill">Enter Monthly Electricity Bill ($):</label>
                <input type="number" id="monthlyBill" placeholder="e.g. 200" oninput="calculateSavings()">
            </div>
            <div id="savingsResult" style="background: #e2e8f0; padding: 15px; border-radius: 6px; font-weight: bold; color: #1b4d3e; display: none;">
                Estimated Annual Savings: <span id="savedAmount" style="color: #27ae60; font-size: 1.2rem;">$0</span><br>
                Estimated System Payback Period: <span id="paybackPeriod" style="color: #1b4d3e;">3.2 Years</span>
            </div>
        </div>

        <!-- Multi-Step Lead Qualification Wizard -->
        <div class="widget-box" style="margin-top: 30px;">
            <h3>📋 Multi-Step Solar Qualification Wizard</h3>
            <form id="wizardForm">
                <div class="form-group">
                    <label>Do you own your property?</label>
                    <select id="ownership" required>
                        <option value="">Select option</option>
                        <option value="Yes - Owner">Yes, I own it</option>
                        <option value="No - Renter">No, I rent</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Roof Type / Sunlight Exposure:</label>
                    <select id="roofType" required>
                        <option value="">Select roof type</option>
                        <option value="Excellent - Full Sun">Excellent (Full Sun)</option>
                        <option value="Good - Partial Shade">Good (Partial Shade)</option>
                    </select>
                </div>
                <div class="form-group">
                    <input type="text" id="wizName" placeholder="Your Full Name" required>
                </div>
                <div class="form-group">
                    <input type="tel" id="wizPhone" placeholder="Phone Number" required>
                </div>
                <button type="submit" class="submit-btn">Submit Qualified Lead</button>
            </form>
            <p id="wizardResponseMsg" style="margin-top: 10px; font-weight: bold; color: #2c7a5f; display: none;"></p>
        </div>

        <!-- FAQ Accordion Section -->
        <div class="widget-box" style="margin-top: 30px;">
            <h3>❓ Frequently Asked Questions</h3>
            <div class="faq-item">
                <div class="faq-question">How long do solar panels take to install? <span>+</span></div>
                <div class="faq-answer">Standard residential installations typically take between 1 to 3 days depending on system size and roof complexity.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">Will my solar panels work during a power outage? <span>+</span></div>
                <div class="faq-answer">Grid-tied systems shut down during outages for safety unless paired with a battery storage backup system.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">How much maintenance do solar panels require? <span>+</span></div>
                <div class="faq-answer">Solar panels require very minimal maintenance—usually just an occasional rinse once or twice a year to remove dust.</div>
            </div>
        </div>
    </div>

    <!-- Live Social Proof Toast Notification -->
    <div id="toastNotification">🔔 Michael from California just requested a solar quote!</div>

    <!-- Login / Sign-up Modal -->
    <div id="authModal">
        <div class="auth-content">
            <span class="close-btn" id="closeAuth">&times;</span>
            <h2 style="color: #1b4d3e; margin-bottom: 15px;">Account Access</h2>
            <form id="emailAuthForm">
                <div class="form-group">
                    <input type="email" id="authEmail" placeholder="Email Address" required>
                </div>
                <div class="form-group">
                    <input type="password" id="authPassword" placeholder="Password" required>
                </div>
                <button type="submit" class="submit-btn" id="emailAuthBtn">Login / Sign Up</button>
            </form>
            <p style="margin: 15px 0 5px 0; font-size: 0.9rem; color: #666;">OR</p>
            <button class="google-btn" id="googleLoginBtn">Sign in with Google</button>
            <p id="authErrorMsg" style="margin-top: 10px; color: red; font-size: 0.9rem; display: none;"></p>
        </div>
    </div>

    <!-- Secret Admin Panel Modal -->
    <div id="adminModal">
        <div class="admin-content">
            <span class="close-btn" id="closeAdmin">&times;</span>
            <h2 style="color: #1b4d3e; margin-bottom: 15px;">🔒 Secret Realtime Leads & Call Logs Panel</h2>
            <p style="font-size: 0.95rem; color: #555;">Live customer data from Wizards & Suzanne Call Logs:</p>
            <div id="leadsContainer">
                <p>Loading realtime records from database...</p>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2026 Solar Energy Solutions. All rights reserved. Powered by Vapi AI & Firebase.
    </footer>

    <!-- Vapi Web SDK Script -->
    <script src="https://cdn.jsdelivr.net/gh/VapiAI/html-script-tag@latest/dist/assets/index.js"></script>

    <!-- Firebase SDKs, Auth, DB, and Logic -->
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
              signOut(auth).then(() => {
                  alert("Logged out successfully.");
              });
          } else {
              authModal.style.display = "flex";
          }
      });

      closeAuth.addEventListener("click", () => {
          authModal.style.display = "none";
      });

      document.getElementById("googleLoginBtn").addEventListener("click", () => {
          signInWithPopup(auth, googleProvider)
              .then(() => {
                  authModal.style.display = "none";
              })
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
              .then(() => {
                  authModal.style.display = "none";
              })
              .catch(() => {
                  createUserWithEmailAndPassword(auth, email, password)
                      .then(() => {
                          authModal.style.display = "none";
                      })
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
              document.querySelectorAll(".faq-question span").forEach(span => span.innerText = "+");
              if (!isOpen) {
                  answer.style.display = "block";
                  item.querySelector("span").innerText = "-";
              }
          });
      });

      const wizardForm = document.getElementById("wizardForm");
      wizardForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const leadData = {
              ownership: document.getElementById("ownership").value,
              roofType: document.getElementById("roofType").value,
              name: document.getElementById("wizName").value,
              phone: document.getElementById("wizPhone").value,
              user: currentUserEmail,
              timestamp: new Date().toISOString()
          };

          push(ref(db, 'solar_leads'), leadData)
              .then(() => {
                  const msg = document.getElementById("wizardResponseMsg");
                  msg.style.display = "block";
                  msg.innerText = "Success! Your consultation request has been saved.";
                  wizardForm.reset();
              })
              .catch((err) => {
                  alert("Error saving lead: " + err.message);
              });
      });

      // Vapi AI Integration Setup with Enhanced Debugging & Error Handling
      const vapiPublicKey = "e0ffb174-f51f-418d-93e3-93ea7f72810b";
      const vapiAssistantId = "1fce054b-91d4-4d60-9f39-9af04c51279a";

      window.addEventListener("load", () => {
          const statusBadge = document.getElementById("callStatusBadge");
          const customCallBtn = document.getElementById("vapiCallBtn");

          if (window.vapiSDK) {
              try {
                  window.vapiInstance = window.vapiSDK.run({
                      apiKey: vapiPublicKey,
                      assistant: vapiAssistantId,
                      config: {
                          position: "bottom-right",
                          buttonColor: "#27ae60",
                          pulseColor: "#2ecc71"
                      }
                  });

                  window.vapiInstance.on("call-start", () => {
                      statusBadge.innerText = "Status: Connected with Suzanne Foster 🎙️";
                      statusBadge.style.background = "#d4edda";
                      statusBadge.style.color = "#155724";
                      customCallBtn.innerText = "🔴 End Voice Call";
                      customCallBtn.classList.add("active");
                      
                      push(ref(db, 'call_logs'), {
                          action: "Call Started",
                          user: currentUserEmail,
                          timestamp: new Date().toISOString()
                      });
                  });

                  window.vapiInstance.on("call-end", () => {
                      statusBadge.innerText = "Status: Ready to Connect";
                      statusBadge.style.background = "#e2e8f0";
                      statusBadge.style.color = "#333";
                      customCallBtn.innerText = "📞 Start Voice Call";
                      customCallBtn.classList.remove("active");

                      push(ref(db, 'call_logs'), {
                          action: "Call Ended",
                          user: currentUserEmail,
                          timestamp: new Date().toISOString()
                      });
                  });

                  window.vapiInstance.on("error", (e) => {
                      console.error("Vapi Error Event:", e);
                      statusBadge.innerText = "Status: Connection Error (Check Mic / Keys)";
                      statusBadge.style.background = "#f8d7da";
                      statusBadge.style.color = "#721c24";
                      customCallBtn.innerText = "📞 Start Voice Call";
                      customCallBtn.classList.remove("active");
                  });

                  customCallBtn.addEventListener("click", async () => {
                      // Request explicit mic permission first
                      try {
                          await navigator.mediaDevices.getUserMedia({ audio: true });
                      } catch (micErr) {
                          alert("Microphone permission is required to speak with Suzanne. Please allow mic access in your browser settings.");
                          return;
                      }

                      if (customCallBtn.classList.contains("active")) {
                          window.vapiInstance.stop();
                      } else {
                          statusBadge.innerText = "Status: Connecting to Suzanne...";
                          window.vapiInstance.start();
                      }
                  });

              } catch (initErr) {
                  console.error("Vapi Init Exception:", initErr);
                  statusBadge.innerText = "Status: Vapi Initialization Failed";
              }
          } else {
              statusBadge.innerText = "Status: SDK Failed to Load";
          }
      });

      let tapCount = 0;
      let tapTimer = null;
      const secretTrigger = document.getElementById("secretTrigger");
      const adminModal = document.getElementById("adminModal");
      const closeAdmin = document.getElementById("closeAdmin");

      secretTrigger.addEventListener("click", () => {
          tapCount++;
          clearTimeout(tapTimer);
          tapTimer = setTimeout(() => {
              tapCount = 0;
          }, 600);

          if (tapCount === 4) {
              tapCount = 0;
              adminModal.style.display = "flex";
              loadAdminData();
          }
      });

      closeAdmin.addEventListener("click", () => {
          adminModal.style.display = "none";
      });

      function loadAdminData() {
          const container = document.getElementById("leadsContainer");
          container.innerHTML = "<p>Loading records...</p>";

          onValue(ref(db, 'solar_leads'), (snapshot) => {
              const leads = snapshot.val();
              let html = "<h4 style='color:#1b4d3e; margin-bottom:10px;'>Qualified Leads:</h4>";
              if (leads) {
                  Object.values(leads).reverse().forEach(lead => {
                      html += `<div class="lead-item"><strong>${lead.name}</strong> (${lead.phone}) - Owner: ${lead.ownership}, Roof: ${lead.roofType} [User: ${lead.user}]<br><small style="color:#777;">${new Date(lead.timestamp).toLocaleString()}</small></div>`;
                  });
              } else {
                  html += "<p>No leads found yet.</p>";
              }

              onValue(ref(db, 'call_logs'), (callSnapshot) => {
                  const calls = callSnapshot.val();
                  html += "<h4 style='color:#1b4d3e; margin: 15px 0 10px 0;'>Vapi Call Logs:</h4>";
                  if (calls) {
                      Object.values(calls).reverse().forEach(call => {
                          html += `<div class="lead-item" style="border-left-color: #27ae60;"><strong>${call.action}</strong> - User: ${call.user}<br><small style="color:#777;">${new Date(call.timestamp).toLocaleString()}</small></div>`;
                      });
                  } else {
                      html += "<p>No call logs found yet.</p>";
                  }
                  container.innerHTML = html;
              }, { onlyOnce: true });

          }, { onlyOnce: true });
      }

      const toasts = [
          "🔔 Michael from California just requested a solar quote!",
          "⚡ Emily from Texas calculated $1,400 in annual savings!",
          "🎙️ A visitor just finished a voice consultation with Suzanne!",
          "🛡️ David from Florida secured a 25-year warranty package!"
      ];
      let toastIndex = 0;
      const toastEl = document.getElementById("toastNotification");

      setInterval(() => {
          toastEl.innerText = toasts[toastIndex];
          toastEl.style.display = "block";
          toastEl.style.opacity = "1";
          setTimeout(() => {
              toastEl.style.opacity = "0";
              setTimeout(() => { toastEl.style.display = "none"; }, 500);
          }, 4000);
          toastIndex = (toastIndex + 1) % toasts.length;
      }, 10000);
    </script>
</body>
</html>
