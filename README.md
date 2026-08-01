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
            padding: 60px 20px;
            text-align: center;
            cursor: pointer;
            user-select: none;
        }
        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        header p {
            font-size: 1.2rem;
            opacity: 0.9;
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
            max-width: 600px;
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

    <!-- Header acts as the secret tap trigger (Tap header 4 times quickly) -->
    <header id="secretTrigger">
        <h1>Solar Energy Solutions</h1>
        <p>Empowering Your Property with Clean, Renewable Power</p>
    </header>

    <div class="container">
        <div id="callStatusBadge">Status: Ready to Connect</div>
        <h2 class="section-title">Welcome to Our Consultation Portal</h2>
        <p>Discover how much you can save on your monthly utility bills with customized solar energy installations. Speak directly with our AI energy specialist, Suzanne Foster, right now or use our interactive tools below.</p>
        
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

        <!-- Interactive Solar Savings Calculator -->
        <div class="widget-box">
            <h3>⚡ Interactive Solar Savings Calculator</h3>
            <div class="form-group">
                <label for="monthlyBill">Enter Monthly Electricity Bill ($):</label>
                <input type="number" id="monthlyBill" placeholder="e.g. 200" oninput="calculateSavings()">
            </div>
            <div id="savingsResult" style="background: #e2e8f0; padding: 15px; border-radius: 6px; font-weight: bold; color: #1b4d3e; display: none;">
                Estimated Annual Savings: <span id="savedAmount" style="color: #27ae60; font-size: 1.2rem;">$0</span>
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
                    <input type="tel" id="wizPhone" placeholder="Phone Number / WhatsApp" required>
                </div>
                <button type="submit" class="submit-btn">Submit Qualified Lead</button>
            </form>
            <p id="wizardResponseMsg" style="margin-top: 10px; font-weight: bold; color: #2c7a5f; display: none;"></p>
        </div>
    </div>

    <!-- Live Social Proof Toast Notification -->
    <div id="toastNotification">🔔 Ahmed from Islamabad just requested a solar quote!</div>

    <!-- Secret Admin Panel Modal -->
    <div id="adminModal">
        <div class="admin-content">
            <span class="close-btn" id="closeAdmin">&times;</span>
            <h2 style="color: #1b4d3e; margin-bottom: 15px;">🔒 Secret Realtime Leads Panel</h2>
            <p style="font-size: 0.95rem; color: #555;">Live customer data collected from consultations & wizards:</p>
            <div id="leadsContainer">
                <p>Loading realtime leads from database...</p>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2026 Solar Energy Solutions. All rights reserved. Powered by Vapi AI & Firebase.
    </footer>

    <!-- Firebase, Calculator, Wizard, and Admin Logic -->
    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
      import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
      
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

      // Interactive Calculator Function
      window.calculateSavings = function() {
          const bill = parseFloat(document.getElementById("monthlyBill").value) || 0;
          const annualSavings = Math.round(bill * 12 * 0.75); // estimated 75% savings
          const resBox = document.getElementById("savingsResult");
          const savedSpan = document.getElementById("savedAmount");
          if (bill > 0) {
              resBox.style.display = "block";
              savedSpan.innerText = "$" + annualSavings.toLocaleString();
          } else {
              resBox.style.display = "none";
          }
      };

      // Multi-Step Wizard Submission
      const wizardForm = document.getElementById("wizardForm");
      const wizardMsg = document.getElementById("wizardResponseMsg");

      wizardForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const ownership = document.getElementById("ownership").value;
          const roofType = document.getElementById("roofType").value;
          const name = document.getElementById("wizName").value;
          const phone = document.getElementById("wizPhone").value;
          const timestamp = new Date().toLocaleString();

          const leadsRef = ref(db, 'leads');
          push(leadsRef, {
              name: name,
              phone: phone,
              bill: `Ownership: ${ownership}`,
              address: `Roof: ${roofType}`,
              timestamp: timestamp
          }).then(() => {
              wizardMsg.style.display = "block";
              wizardMsg.style.color = "#2c7a5f";
              wizardMsg.innerText = "Success! Your consultation profile is submitted.";
              wizardForm.reset();
          }).catch((error) => {
              wizardMsg.style.display = "block";
              wizardMsg.style.color = "red";
              wizardMsg.innerText = "Error: " + error.message;
          });
      });

      // Live Social Proof Toast Trigger Loop
      const toasts = [
          "🔔 Ali from Lahore just booked a solar consultation!",
          "🔔 Sara from Karachi estimated her solar savings!",
          "🔔 Bilal from Rawalpindi connected with Suzanne Foster!",
          "🔔 Usman from Islamabad just submitted a qualification form!"
      ];
      
      function showToast() {
          const toast = document.getElementById("toastNotification");
          const randomText = toasts[Math.floor(Math.random() * toasts.length)];
          toast.innerText = randomText;
          toast.style.display = "block";
          toast.style.opacity = "1";
          
          setTimeout(() => {
              toast.style.opacity = "0";
              setTimeout(() => { toast.style.display = "none"; }, 500);
          }, 4000);
      }
      setInterval(showToast, 12000); // Trigger every 12 seconds

      // 4-Tap Secret Trigger Logic with PIN 5426
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
              tapTimer = setTimeout(() => {
                  tapCount = 0;
              }, 600);
          }
      });

      closeBtn.addEventListener("click", () => {
          modal.style.display = "none";
      });

      window.addEventListener("click", (e) => {
          if (e.target === modal) {
              modal.style.display = "none";
          }
      });

      // Fetch Realtime Leads from Firebase RTDB
      function fetchRealtimeLeads() {
          const leadsRef = ref(db, 'leads');
          onValue(leadsRef, (snapshot) => {
              const data = snapshot.val();
              leadsContainer.innerHTML = "";
              
              if (!data) {
                  leadsContainer.innerHTML = "<p>No leads recorded yet.</p>";
                  return;
              }

              Object.keys(data).reverse().forEach(key => {
                  const lead = data[key];
                  const leadDiv = document.createElement("div");
                  leadDiv.className = "lead-item";
                  leadDiv.innerHTML = `
                      <strong>Name:</strong> ${lead.name || 'N/A'}<br>
                      <strong>Phone:</strong> ${lead.phone || 'N/A'}<br>
                      <strong>Bill Info:</strong> ${lead.bill || 'N/A'}<br>
                      <strong>Roof Details:</strong> ${lead.address || 'N/A'}<br>
                      <small style="color: #666;">Time: ${lead.timestamp || 'Recent'}</small>
                  `;
                  leadsContainer.appendChild(leadDiv);
              });
          }, (error) => {
              leadsContainer.innerHTML = `<p style="color: red;">Error loading leads: ${error.message}</p>`;
          });
      }
    </script>

    <!-- Vapi Web Widget SDK Script & Call Status Handlers -->
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
            offset: "40px",
            width: "300px",
            height: "500px",
            idle: {
              color: "#2c7a5f",
              type: "pill",
              title: "Talk with Suzanne",
              subtitle: "Solar Expert",
              icon: "https://unpkg.com/lucide-static@latest/icons/phone.svg"
            }
          }
        });

        // Listen to Vapi Call Events for Status Badge update
        setTimeout(() => {
            if (window.vapiSDK) {
                window.vapiSDK.on("call-start", () => {
                    const badge = document.getElementById("callStatusBadge");
                    badge.style.background = "#22c55e";
                    badge.style.color = "white";
                    badge.innerText = "Status: Connected with Suzanne Foster 🟢";
                });

                window.vapiSDK.on("call-end", () => {
                    const badge = document.getElementById("callStatusBadge");
                    badge.style.background = "#e2e8f0";
                    badge.style.color = "#333";
                    badge.innerText = "Status: Call Ended. Thank you!";
                });
            }
        }, 2000);
      });
    </script>
</body>
</html>
