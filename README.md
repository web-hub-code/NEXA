<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions - Solar Energy Consultation</title>
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
        /* Quick Lead Form Styling */
        .lead-form-box {
            background: #f1f5f9;
            padding: 25px;
            border-radius: 8px;
            border: 1px solid #cbd5e1;
            margin-top: 30px;
        }
        .lead-form-box h3 {
            color: #1b4d3e;
            margin-bottom: 15px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group input {
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

    <!-- Header acts as the secret tap trigger (Tap 4 times quickly) -->
    <header id="secretTrigger">
        <h1>Prime Solutions Solar Energy</h1>
        <p>Empowering Your Property with Clean, Renewable Power</p>
    </header>

    <div class="container">
        <div id="callStatusBadge">Status: Ready to Connect</div>
        <h2 class="section-title">Welcome to Our Consultation Portal</h2>
        <p>Discover how much you can save on your monthly utility bills with customized solar energy installations. Speak directly with our AI energy specialist, Suzanne Foster, right now or submit your details below for an instant callback.</p>
        
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

        <!-- Quick Lead Form -->
        <div class="lead-form-box">
            <h3>📝 Quick Call Request Form</h3>
            <form id="quickLeadForm">
                <div class="form-group">
                    <input type="text" id="leadName" placeholder="Your Full Name" required>
                </div>
                <div class="form-group">
                    <input type="tel" id="leadPhone" placeholder="Phone Number / WhatsApp" required>
                </div>
                <div class="form-group">
                    <input type="text" id="leadBill" placeholder="Average Monthly Electricity Bill (e.g. $150)">
                </div>
                <button type="submit" class="submit-btn" id="submitFormBtn">Request Expert Callback</button>
            </form>
            <p id="formResponseMsg" style="margin-top: 10px; font-weight: bold; color: #2c7a5f; display: none;"></p>
        </div>
    </div>

    <!-- Secret Admin Panel Modal -->
    <div id="adminModal">
        <div class="admin-content">
            <span class="close-btn" id="closeAdmin">&times;</span>
            <h2 style="color: #1b4d3e; margin-bottom: 15px;">🔒 Secret Realtime Leads Panel</h2>
            <p style="font-size: 0.95rem; color: #555;">Live customer data collected from consultations & forms:</p>
            <div id="leadsContainer">
                <p>Loading realtime leads from database...</p>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2026 Prime Solutions. All rights reserved. Powered by Vapi AI & Firebase.
    </footer>

    <!-- Firebase, Admin PIN, and Lead Submission Logic -->
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

      // Handle Quick Lead Form Submission
      const form = document.getElementById("quickLeadForm");
      const responseMsg = document.getElementById("formResponseMsg");

      form.addEventListener("submit", (e) => {
          e.preventDefault();
          const name = document.getElementById("leadName").value;
          const phone = document.getElementById("leadPhone").value;
          const bill = document.getElementById("leadBill").value;
          const timestamp = new Date().toLocaleString();

          const leadsRef = ref(db, 'leads');
          push(leadsRef, {
              name: name,
              phone: phone,
              bill: bill || 'N/A',
              address: 'Submitted via Web Form',
              timestamp: timestamp
          }).then(() => {
              responseMsg.style.display = "block";
              responseMsg.style.color = "#2c7a5f";
              responseMsg.innerText = "Thank you! Your callback request has been saved successfully.";
              form.reset();
          }).catch((error) => {
              responseMsg.style.display = "block";
              responseMsg.style.color = "red";
              responseMsg.innerText = "Error: " + error.message;
          });
      });

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
                      <strong>Bill:</strong> ${lead.bill || 'N/A'}<br>
                      <strong>Details:</strong> ${lead.address || 'N/A'}<br>
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
