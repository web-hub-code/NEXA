<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Solar Energy Solutions - Next-Gen Professional Consultation Portal</title>
    <!-- Chart.js for Interactive Savings Graph -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- html2pdf for PDF Quote Generation -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0fdf4;
            color: #1e293b;
            line-height: 1.6;
        }
        header {
            background: linear-gradient(135deg, #065f46, #047857, #10b981);
            color: white;
            padding: 50px 15px;
            text-align: center;
            cursor: pointer;
            user-select: none;
            position: relative;
            box-shadow: 0 4px 20px rgba(6, 95, 70, 0.2);
        }
        header h1 {
            font-size: 2.3rem;
            margin-bottom: 10px;
            letter-spacing: -0.5px;
        }
        header p {
            font-size: 1.1rem;
            opacity: 0.95;
        }
        #authBar {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            padding: 6px 12px;
            border-radius: 30px;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 8px;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        #authBar button {
            background: white;
            color: #065f46;
            border: none;
            padding: 4px 10px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        #authBar button:hover {
            background: #e2e8f0;
        }
        .container {
            max-width: 950px;
            margin: -20px 15px 40px 15px;
            background: white;
            padding: 25px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.06);
            position: relative;
        }
        @media(min-width: 768px) {
            .container {
                margin: -30px auto 40px auto;
                padding: 45px;
            }
            header {
                padding: 60px 20px;
            }
            header h1 {
                font-size: 2.8rem;
            }
            header p {
                font-size: 1.25rem;
            }
        }
        .live-badge {
            display: inline-block;
            background: #dcfce7;
            color: #166534;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-bottom: 20px;
            border: 1px solid #bbf7d0;
            text-align: center;
        }
        .section-title {
            color: #065f46;
            font-size: 1.6rem;
            margin-bottom: 20px;
            border-bottom: 2px solid #a7f3d0;
            padding-bottom: 8px;
        }
        @media(min-width: 768px) {
            .section-title {
                font-size: 1.9rem;
            }
        }
        p {
            margin-bottom: 20px;
            font-size: 1rem;
            color: #475569;
        }
        @media(min-width: 768px) {
            p {
                font-size: 1.1rem;
            }
        }
        .trust-bar {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
            margin: 25px 0;
            text-align: center;
        }
        @media(min-width: 600px) {
            .trust-bar {
                grid-template-columns: repeat(3, 1fr);
            }
        }
        .trust-badge {
            background: #f0fdf4;
            border: 1px solid #bbf7d0;
            padding: 15px;
            border-radius: 10px;
            color: #065f46;
            font-weight: bold;
            font-size: 0.9rem;
            box-shadow: 0 2px 5px rgba(0,0,0,0.02);
        }
        .features {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
            margin-top: 25px;
            margin-bottom: 35px;
        }
        @media(min-width: 600px) {
            .features {
                grid-template-columns: repeat(3, 1fr);
            }
        }
        .feature-card {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            transition: transform 0.3s;
        }
        .feature-card:hover {
            transform: translateY(-3px);
            border-color: #10b981;
        }
        .feature-card h3 {
            color: #047857;
            margin-bottom: 8px;
            font-size: 1.1rem;
        }
        .widget-box {
            background: #f8fafc;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid #e2e8f0;
            margin-top: 25px;
        }
        @media(min-width: 768px) {
            .widget-box {
                padding: 30px;
            }
        }
        .widget-box h3 {
            color: #065f46;
            margin-bottom: 15px;
            font-size: 1.3rem;
        }
        
        /* Ultra-Modern Voice Assistant Call Box */
        .voice-call-box {
            background: linear-gradient(135deg, #022c22, #064e3b, #065f46);
            color: white;
            padding: 30px 20px;
            border-radius: 16px;
            text-align: center;
            position: relative;
            overflow: hidden;
            box-shadow: 0 12px 30px rgba(6, 95, 70, 0.25);
            border: 1px solid #10b981;
            margin-top: 25px;
        }
        @media(min-width: 768px) {
            .voice-call-box {
                padding: 45px 30px;
            }
        }
        .voice-pulse-ring {
            width: 70px;
            height: 70px;
            background: rgba(16, 185, 129, 0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px auto;
            animation: pulseGlow 2s infinite;
            border: 2px solid #34d399;
        }
        .voice-pulse-inner {
            width: 45px;
            height: 45px;
            background: #10b981;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.3rem;
            box-shadow: 0 0 20px #34d399;
        }
        @keyframes pulseGlow {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(52, 211, 153, 0.6); }
            70% { transform: scale(1.1); box-shadow: 0 0 0 15px rgba(52, 211, 153, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(52, 211, 153, 0); }
        }
        .voice-call-btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            background: linear-gradient(135deg, #10b981, #059669);
            color: white;
            padding: 14px 28px;
            border-radius: 40px;
            text-decoration: none;
            font-weight: bold;
            font-size: 1.05rem;
            box-shadow: 0 6px 20px rgba(16, 185, 129, 0.4);
            transition: all 0.3s ease;
            border: 1px solid #6ee7b7;
            width: 100%;
            max-width: 320px;
        }
        @media(min-width: 600px) {
            .voice-call-btn {
                width: auto;
                padding: 16px 36px;
                font-size: 1.15rem;
            }
        }
        .voice-call-btn:hover {
            transform: translateY(-2px);
            background: linear-gradient(135deg, #059669, #047857);
            box-shadow: 0 8px 25px rgba(16, 185, 129, 0.6);
        }

        .form-group {
            margin-bottom: 18px;
        }
        .form-group label {
            display: block;
            margin-bottom: 6px;
            font-weight: 600;
            color: #334155;
            font-size: 0.95rem;
        }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            transition: border-color 0.3s;
            background: #fff;
        }
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            border-color: #10b981;
            box-shadow: 0 0 0 3px rgba(16, 185, 129, 0.1);
        }
        .form-row {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }
        @media(min-width: 600px) {
            .form-row {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        .submit-btn, .action-btn {
            background: linear-gradient(135deg, #059669, #047857);
            color: white;
            border: none;
            padding: 14px 20px;
            font-size: 1.05rem;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 4px 12px rgba(5, 150, 105, 0.2);
            transition: opacity 0.3s;
            display: inline-block;
            text-align: center;
            text-decoration: none;
        }
        .submit-btn:hover, .action-btn:hover {
            opacity: 0.9;
        }
        .faq-item {
            background: #fff;
            border: 1px solid #e2e8f0;
            margin-bottom: 10px;
            border-radius: 8px;
            overflow: hidden;
        }
        .faq-question {
            background: #f8fafc;
            padding: 14px 18px;
            font-weight: bold;
            cursor: pointer;
            color: #065f46;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.95rem;
        }
        .faq-answer {
            padding: 14px 18px;
            display: none;
            color: #475569;
            background: #fff;
            border-top: 1px solid #e2e8f0;
            font-size: 0.95rem;
        }
        #authModal, #adminModal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.6);
            backdrop-filter: blur(4px);
            z-index: 9999;
            justify-content: center;
            align-items: center;
            padding: 15px;
        }
        .auth-content, .admin-content {
            background: white;
            padding: 25px;
            border-radius: 14px;
            width: 100%;
            max-width: 450px;
            text-align: center;
            position: relative;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        .admin-content {
            max-width: 750px;
            max-height: 85vh;
            overflow-y: auto;
            text-align: left;
        }
        .google-btn {
            background: #ef4444;
            color: white;
            border: none;
            padding: 12px;
            width: 100%;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        #toastNotification {
            position: fixed;
            bottom: 20px;
            left: 15px;
            right: 15px;
            background: #065f46;
            color: white;
            padding: 12px 18px;
            border-radius: 10px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.15);
            font-size: 0.85rem;
            z-index: 999;
            display: none;
            transition: opacity 0.5s ease;
            border-left: 5px solid #34d399;
            text-align: center;
        }
        @media(min-width: 600px) {
            #toastNotification {
                left: 25px;
                right: auto;
                font-size: 0.95rem;
                max-width: 400px;
                text-align: left;
            }
        }
        .close-btn {
            position: absolute;
            top: 15px;
            right: 18px;
            font-size: 1.5rem;
            cursor: pointer;
            color: #94a3b8;
            transition: color 0.2s;
        }
        .close-btn:hover {
            color: #1e293b;
        }
        .lead-item, .msg-item {
            background: #f1f5f9;
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 8px;
            border-left: 4px solid #10b981;
            font-size: 0.9rem;
        }
        .admin-tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 15px;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
            overflow-x: auto;
        }
        .tab-btn {
            background: #e2e8f0;
            border: none;
            padding: 8px 14px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            color: #475569;
            white-space: nowrap;
        }
        .tab-btn.active {
            background: #065f46;
            color: white;
        }
        
        /* Floating Real-Time AI Live Chat Widget */
        #chatWidget {
            position: fixed;
            bottom: 25px;
            right: 25px;
            z-index: 9998;
        }
        #chatToggleBtn {
            background: #059669;
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            border: none;
            font-size: 1.6rem;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(5, 150, 105, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.3s;
        }
        #chatToggleBtn:hover {
            transform: scale(1.05);
        }
        #chatBoxContainer {
            display: none;
            position: absolute;
            bottom: 75px;
            right: 0;
            width: 320px;
            max-width: 90vw;
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            border: 1px solid #cbd5e1;
            overflow: hidden;
            flex-direction: column;
        }
        #chatHeader {
            background: #065f46;
            color: white;
            padding: 12px 15px;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.95rem;
        }
        #chatBody {
            height: 250px;
            overflow-y: auto;
            padding: 12px;
            background: #f8fafc;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .chat-msg {
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 0.85rem;
            max-width: 80%;
        }
        .chat-msg.bot {
            background: #e2e8f0;
            color: #1e293b;
            align-self: flex-start;
        }
        .chat-msg.user {
            background: #059669;
            color: white;
            align-self: flex-end;
        }
        #chatFooter {
            display: flex;
            padding: 10px;
            background: white;
            border-top: 1px solid #e2e8f0;
        }
        #chatInput {
            flex: 1;
            padding: 8px 12px;
            border: 1px solid #cbd5e1;
            border-radius: 6px;
            outline: none;
            font-size: 0.85rem;
        }
        #chatSendBtn {
            background: #059669;
            color: white;
            border: none;
            padding: 8px 14px;
            margin-left: 6px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
        }

        footer {
            text-align: center;
            padding: 20px;
            color: #64748b;
            font-size: 0.85rem;
            margin-top: 30px;
            border-top: 1px solid #e2e8f0;
        }
    </style>
</head>
<body>

    <header id="secretTrigger">
        <div id="authBar">
            <span id="userDisplay">Guest</span>
            <button id="authBtn">Login</button>
        </div>
        <h1>Solar Energy Solutions</h1>
        <p>Empowering Your Property with Clean, Next-Gen Renewable Power</p>
    </header>

    <div class="container" id="pdfReportContent">
        <div class="live-badge">🟢 <span id="visitorCount">1</span> Active Visitors Online &nbsp;|&nbsp; ⚡ AI Powered & Verified Portal</div>
        
        <h2 class="section-title">Welcome to Our Advanced Consultation Portal</h2>
        <p>Discover precisely how much you can save on your monthly utility bills with customized solar installations. Speak directly with our AI energy specialist, <b>Suzanne Foster</b>, right now or use our interactive financial and consultation tools below.</p>
        
        <!-- Fully Responsive Ultra-Modern Voice Assistant Call Box -->
        <div class="voice-call-box">
            <div class="voice-pulse-ring">
                <div class="voice-pulse-inner">🎙️</div>
            </div>
            <h3 style="color: #ffffff; margin-bottom: 8px; font-size: 1.3rem;">Talk Live with Suzanne Foster</h3>
            <p style="color: #a7f3d0; font-size: 0.95rem; margin-bottom: 20px; max-width: 550px; margin-left: auto; margin-right: auto;">Experience an ultra-realistic, real-time voice consultation with our expert AI specialist. Tap below to launch the secure voice session instantly:</p>
            
            <a href="https://vapi.ai?assistantId=1fce054b-91d4-4d60-9f39-9af04c51279a" target="_blank" class="voice-call-btn">
                <span>📞 Start Secure Voice Call</span>
            </a>
        </div>

        <div class="trust-bar" style="margin-top: 30px;">
            <div class="trust-badge">🛡️ 25-Year Performance Warranty</div>
            <div class="trust-badge">⚡ 0-Down Flexible Financing</div>
            <div class="trust-badge">👷 100% Certified Solar Experts</div>
        </div>

        <div class="features">
            <div class="feature-card">
                <h3>Instant Eligibility</h3>
                <p>Quick smart assessment of your roof space and electricity consumption profile.</p>
            </div>
            <div class="feature-card">
                <h3>Tailored Savings</h3>
                <p>Learn about customized high-efficiency solar packages designed for your property.</p>
            </div>
            <div class="feature-card">
                <h3>Expert Callback</h3>
                <p>Connect instantly with a senior renewable energy consultant at your convenience.</p>
            </div>
        </div>

        <!-- Advanced Solar Savings Calculator & Chart & PDF Report -->
        <div class="widget-box">
            <h3>⚡ Advanced Solar Savings & ROI Calculator</h3>
            <div class="form-group">
                <label for="monthlyBill">Enter Monthly Electricity Bill ($):</label>
                <input type="number" id="monthlyBill" placeholder="e.g. 250" oninput="calculateSavings()">
            </div>
            <div id="savingsResult" style="background: #e2e8f0; padding: 15px; border-radius: 8px; font-weight: bold; color: #065f46; display: none; font-size: 0.95rem;">
                Estimated Annual Savings: <span id="savedAmount" style="color: #059669; font-size: 1.2rem;">$0</span><br>
                Estimated System Size Needed: <span id="systemSize" style="color: #1e293b;">6.5 kW</span><br>
                Estimated System Payback Period: <span id="paybackPeriod" style="color: #1e293b;">3.1 Years</span>
                
                <!-- Interactive Savings Graph Canvas -->
                <div style="margin-top: 20px; background: white; padding: 10px; border-radius: 8px;">
                    <canvas id="savingsChart" width="400" height="200"></canvas>
                </div>

                <!-- PDF Quote Download Button -->
                <button onclick="downloadPDFReport()" class="action-btn" style="margin-top: 15px; background: #0284c7;">📥 Download Official PDF Estimate Report</button>
            </div>
        </div>

        <!-- AI Solar Panel Roof Image Scanner Simulator -->
        <div class="widget-box" style="margin-top: 25px;">
            <h3>🛰️ AI Roof Space & Panel Scanner</h3>
            <p style="font-size: 0.9rem; margin-bottom: 12px;">Upload a photo of your roof to simulate AI spatial analysis for panel capacity:</p>
            <div class="form-group">
                <input type="file" id="roofImageInput" accept="image/*" onchange="scanRoofImage()">
            </div>
            <div id="scanResultMsg" style="background: #e2e8f0; padding: 12px; border-radius: 8px; font-size: 0.9rem; font-weight: bold; color: #065f46; display: none;"></div>
        </div>

        <!-- Interactive Booking Calendar System -->
        <div class="widget-box" style="margin-top: 25px;">
            <h3>📅 Book Site Inspection / Expert Appointment</h3>
            <form id="bookingForm">
                <div class="form-row">
                    <div class="form-group">
                        <label>Select Preferred Date:</label>
                        <input type="date" id="bookDate" required>
                    </div>
                    <div class="form-group">
                        <label>Select Time Slot:</label>
                        <select id="bookTime" required>
                            <option value="">Choose time slot</option>
                            <option value="10:00 AM - 12:00 PM">10:00 AM - 12:00 PM</option>
                            <option value="02:00 PM - 04:00 PM">02:00 PM - 04:00 PM</option>
                            <option value="04:00 PM - 06:00 PM">04:00 PM - 06:00 PM</option>
                        </select>
                    </div>
                </div>
                <button type="submit" class="submit-btn" style="background: #10b981;">Confirm Appointment Booking</button>
            </form>
            <p id="bookingResponseMsg" style="margin-top: 10px; font-weight: bold; color: #059669; display: none; font-size: 0.95rem;"></p>
        </div>

        <!-- Advanced Comprehensive Solar Qualification Wizard -->
        <div class="widget-box" style="margin-top: 25px;">
            <h3>📋 Comprehensive Solar Qualification Wizard</h3>
            <p style="font-size: 0.9rem; margin-bottom: 15px;">Complete the details below to check your full eligibility for zero-down solar installation programs:</p>
            <form id="wizardForm">
                <div class="form-row">
                    <div class="form-group">
                        <label>First Name:</label>
                        <input type="text" id="wizFirstName" placeholder="e.g. John" required>
                    </div>
                    <div class="form-group">
                        <label>Last Name:</label>
                        <input type="text" id="wizLastName" placeholder="e.g. Smith" required>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>Are you the homeowner?</label>
                        <select id="wizHomeowner" required>
                            <option value="">Select option</option>
                            <option value="Yes">Yes</option>
                            <option value="No">No</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Average Monthly Electric Bill ($):</label>
                        <input type="number" id="wizMonthlyBill" placeholder="e.g. 200" required>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>Electric Provider Name:</label>
                        <input type="text" id="wizElectricProvider" placeholder="e.g. Pacific Gas & Electric" required>
                    </div>
                    <div class="form-group">
                        <label>Estimated Credit Score:</label>
                        <select id="wizCreditScore" required>
                            <option value="">Select credit bracket</option>
                            <option value="Excellent (740+)">Excellent (740+)</option>
                            <option value="Good (700-739)">Good (700-739)</option>
                            <option value="Fair (650-699)">Fair (650-699)</option>
                            <option value="Below 650">Below 650</option>
                        </select>
                    </div>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>Annual Household Income:</label>
                        <select id="wizIncome" required>
                            <option value="">Select income level</option>
                            <option value="Less than $35,000">Less than $35,000</option>
                            <option value="More than $35,000">More than $35,000</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Phone Number:</label>
                        <input type="tel" id="wizPhone" placeholder="e.g. +1 555-0198" required>
                    </div>
                </div>

                <div class="form-group">
                    <label>Street Address:</label>
                    <input type="text" id="wizStreet" placeholder="e.g. 123 Sunshine Blvd" required>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label>City:</label>
                        <input type="text" id="wizCity" placeholder="e.g. Los Angeles" required>
                    </div>
                    <div class="form-group">
                        <label>State & Zip Code:</label>
                        <input type="text" id="wizStateZip" placeholder="e.g. CA, 90001" required>
                    </div>
                </div>

                <button type="submit" class="submit-btn">Submit Qualified Lead</button>
            </form>
            <p id="wizardResponseMsg" style="margin-top: 12px; font-weight: bold; color: #059669; display: none; font-size: 0.95rem;"></p>
        </div>

        <!-- Direct Live Customer Support Message Box -->
        <div class="widget-box" style="margin-top: 25px;">
            <h3>💬 Direct Customer Support & Inquiry Box</h3>
            <p style="font-size: 0.9rem; margin-bottom: 12px;">Have custom questions? Drop a message below and our support team will respond quickly.</p>
            <form id="supportForm">
                <div class="form-group">
                    <textarea id="supportMsgText" rows="3" placeholder="Type your message or custom inquiry here..." required></textarea>
                </div>
                <button type="submit" class="submit-btn" style="background: #0284c7;">Send Support Message</button>
            </form>
            <p id="supportResponseMsg" style="margin-top: 10px; font-weight: bold; color: #0284c7; display: none; font-size: 0.95rem;"></p>
        </div>

        <!-- FAQs -->
        <div class="widget-box" style="margin-top: 25px;">
            <h3>❓ Frequently Asked Questions</h3>
            <div class="faq-item">
                <div class="faq-question">How long do solar panels take to install? <span>+</span></div>
                <div class="faq-answer">Standard residential installations typically take between 1 to 3 days depending on system size and roof complexity.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">Will my solar panels work during a power outage? <span>+</span></div>
                <div class="faq-answer">Grid-tied systems shut down during outages for safety unless paired with a modern battery storage backup system.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">How much maintenance do solar panels require? <span>+</span></div>
                <div class="faq-answer">Solar panels require very minimal maintenance—usually just an occasional rinse once or twice a year to remove dust.</div>
            </div>
        </div>
    </div>

    <!-- Floating Real-Time AI Live Chat Widget -->
    <div id="chatWidget">
        <button id="chatToggleBtn" onclick="toggleChatWindow()">💬</button>
        <div id="chatBoxContainer">
            <div id="chatHeader">
                <span>AI Support Assistant</span>
                <span style="cursor: pointer;" onclick="toggleChatWindow()">&times;</span>
            </div>
            <div id="chatBody">
                <div class="chat-msg bot">Hello sweetie! How can I help you with solar solutions today?</div>
            </div>
            <div id="chatFooter">
                <input type="text" id="chatInput" placeholder="Type a message..." onkeypress="handleChatKey(event)">
                <button id="chatSendBtn" onclick="sendChatMessage()">Send</button>
            </div>
        </div>
    </div>

    <div id="toastNotification">🔔 Michael from California just requested a solar quote!</div>

    <!-- Auth Modal -->
    <div id="authModal">
        <div class="auth-content">
            <span class="close-btn" id="closeAuth">&times;</span>
            <h2 style="color: #065f46; margin-bottom: 15px; font-size: 1.4rem;">Account Access</h2>
            <form id="emailAuthForm">
                <div class="form-group" style="text-align: left;">
                    <input type="email" id="authEmail" placeholder="Email Address" required>
                </div>
                <div class="form-group" style="text-align: left;">
                    <input type="password" id="authPassword" placeholder="Password" required>
                </div>
                <button type="submit" class="submit-btn" id="emailAuthBtn">Login / Sign Up</button>
            </form>
            <p style="margin: 15px 0 5px 0; font-size: 0.85rem; color: #64748b;">OR</p>
            <button class="google-btn" id="googleLoginBtn">Sign in with Google</button>
            <p id="authErrorMsg" style="margin-top: 10px; color: #ef4444; font-size: 0.85rem; display: none;"></p>
        </div>
    </div>

    <!-- Admin Leads & Support Messages Modal -->
    <div id="adminModal">
        <div class="admin-content">
            <span class="close-btn" id="closeAdmin">&times;</span>
            <h2 style="color: #065f46; margin-bottom: 8px; font-size: 1.3rem;">🔒 Secret Admin Control Panel</h2>
            <p style="font-size: 0.85rem; color: #64748b; margin-bottom: 15px;">Manage customer submissions and real-time portal telemetry:</p>
            
            <div class="admin-tabs">
                <button class="tab-btn active" onclick="switchAdminTab('leads')">Qualified Leads</button>
                <button class="tab-btn" onclick="switchAdminTab('messages')">Support Messages</button>
            </div>

            <div id="adminLeadsTab">
                <div id="leadsContainer">
                    <p>Loading records from database...</p>
                </div>
            </div>

            <div id="adminMessagesTab" style="display: none;">
                <div id="messagesContainer">
                    <p>Loading messages...</p>
                </div>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2026 Solar Energy Solutions. All rights reserved. Powered by Vapi AI & Firebase.
    </footer>

    <!-- Official Vapi SDK Widget Script -->
    <script src="https://cdn.jsdelivr.net/gh/VapiAI/html-script-tag@latest/dist/assets/index.js"></script>
    <script>
      window.addEventListener("DOMContentLoaded", () => {
        try {
          window.vapiSDK.run({
            apiKey: "e0ffb174-f51f-418d-87c9-93ea7f72810b",
            assistant: "1fce054b-91d4-4d60-9f39-9af04c51279a",
            config: {
              position: "bottom-right",
              buttonColor: "#059669",
            }
          });
        } catch(e) {
          console.log("Vapi SDK widget fallback mode.");
        }
      });
    </script>

    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
      import { getDatabase, ref, push, onValue, set, onDisconnect } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
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

      // Realtime Active Visitor Presence Counter
      const visitorRef = ref(db, 'active_visitors/' + Math.random().toString(36).substring(2));
      set(visitorRef, true);
      onDisconnect(visitorRef).remove();

      onValue(ref(db, 'active_visitors'), (snapshot) => {
          const count = snapshot.val() ? Object.keys(snapshot.val()).length : 1;
          document.getElementById("visitorCount").innerText = count;
      });

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

      let myChart = null;
      window.calculateSavings = function() {
          const bill = parseFloat(document.getElementById("monthlyBill").value) || 0;
          const annualSavings = Math.round(bill * 12 * 0.78); 
          const systemKw = (bill / 35).toFixed(1);
          const resBox = document.getElementById("savingsResult");
          const savedSpan = document.getElementById("savedAmount");
          const systemSpan = document.getElementById("systemSize");
          const paybackSpan = document.getElementById("paybackPeriod");
          if (bill > 0) {
              resBox.style.display = "block";
              savedSpan.innerText = "$" + annualSavings.toLocaleString();
              systemSpan.innerText = systemKw + " kW";
              let payback = ( (bill * 12 * 3.2) / annualSavings ).toFixed(1);
              paybackSpan.innerText = payback + " Years";

              // Render Chart.js Graph
              const ctx = document.getElementById('savingsChart').getContext('2d');
              let years = [5, 10, 15, 20, 25];
              let cumulativeSavings = years.map(y => annualSavings * y);
              
              if(myChart) myChart.destroy();
              myChart = new Chart(ctx, {
                  type: 'bar',
                  data: {
                      labels: years.map(y => y + ' Years'),
                      datasets: [{
                          label: 'Cumulative Savings ($)',
                          data: cumulativeSavings,
                          backgroundColor: '#059669',
                          borderRadius: 6
                      }]
                  },
                  options: {
                      responsive: true,
                      plugins: { legend: { display: false } }
                  }
              });

          } else {
              resBox.style.display = "none";
          }
      };

      window.downloadPDFReport = function() {
          const element = document.getElementById('pdfReportContent');
          const opt = {
              margin:       10,
              filename:     'Solar_Estimation_Report.pdf',
              image:        { type: 'jpeg', quality: 0.98 },
              html2canvas:  { scale: 2 },
              jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
          };
          html2pdf().from(element).save();
      };

      window.scanRoofImage = function() {
          const fileInput = document.getElementById("roofImageInput");
          const resMsg = document.getElementById("scanResultMsg");
          if(fileInput.files && fileInput.files[0]) {
              resMsg.style.display = "block";
              resMsg.innerHTML = "🛰️ Scanning roof geometry... <br>✅ Analysis Complete: Estimated optimal capacity is **7.2 kW** (Approx. 18 high-efficiency panels fit with full sun exposure).";
          }
      };

      const bookingForm = document.getElementById("bookingForm");
      bookingForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const bookingData = {
              date: document.getElementById("bookDate").value,
              time: document.getElementById("bookTime").value,
              user: currentUserEmail,
              timestamp: new Date().toISOString()
          };

          push(ref(db, 'site_bookings'), bookingData)
              .then(() => {
                  const msg = document.getElementById("bookingResponseMsg");
                  msg.style.display = "block";
                  msg.innerText = "Appointment booked successfully! Our technician will confirm shortly.";
                  bookingForm.reset();
              })
              .catch((err) => {
                  alert("Error booking appointment: " + err.message);
              });
      });

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
              firstName: document.getElementById("wizFirstName").value,
              lastName: document.getElementById("wizLastName").value,
              homeowner: document.getElementById("wizHomeowner").value,
              monthlyBill: document.getElementById("wizMonthlyBill").value,
              electricProvider: document.getElementById("wizElectricProvider").value,
              creditScore: document.getElementById("wizCreditScore").value,
              householdIncome: document.getElementById("wizIncome").value,
              phone: document.getElementById("wizPhone").value,
              street: document.getElementById("wizStreet").value,
              city: document.getElementById("wizCity").value,
              stateZip: document.getElementById("wizStateZip").value,
              user: currentUserEmail,
              timestamp: new Date().toISOString()
          };

          push(ref(db, 'solar_leads'), leadData)
              .then(() => {
                  const msg = document.getElementById("wizardResponseMsg");
                  msg.style.display = "block";
                  msg.innerText = "Success! Your comprehensive consultation request has been saved.";
                  wizardForm.reset();
              })
              .catch((err) => {
                  alert("Error saving lead: " + err.message);
              });
      });

      const supportForm = document.getElementById("supportForm");
      supportForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const supportData = {
              message: document.getElementById("supportMsgText").value,
              user: currentUserEmail,
              timestamp: new Date().toISOString()
          };

          push(ref(db, 'support_messages'), supportData)
              .then(() => {
                  const msg = document.getElementById("supportResponseMsg");
                  msg.style.display = "block";
                  msg.innerText = "Message sent successfully! Our support team will contact you.";
                  supportForm.reset();
              })
              .catch((err) => {
                  alert("Error: " + err.message);
              });
      });

      // Floating Live Chat Logic
      window.toggleChatWindow = function() {
          const chatBox = document.getElementById("chatBoxContainer");
          chatBox.style.display = chatBox.style.display === "flex" ? "none" : "flex";
      };

      window.handleChatKey = function(e) {
          if (e.key === "Enter") sendChatMessage();
      };

      window.sendChatMessage = function() {
          const input = document.getElementById("chatInput");
          const text = input.value.trim();
          if(!text) return;

          const chatBody = document.getElementById("chatBody");
          chatBody.innerHTML += `<div class="chat-msg user">${text}</div>`;
          input.value = "";
          chatBody.scrollTop = chatBody.scrollHeight;

          setTimeout(() => {
              let reply = "Thanks for your inquiry sweetie! Our solar experts will review your request shortly.";
              if(text.toLowerCase().includes("price") || text.toLowerCase().includes("cost")) {
                  reply = "Solar installation cost depends on your monthly bill. You can use our ROI calculator above for exact estimates!";
              } else if(text.toLowerCase().includes("warranty")) {
                  reply = "All our solar installations come with a 25-year comprehensive performance warranty!";
              }
              chatBody.innerHTML += `<div class="chat-msg bot">${reply}</div>`;
              chatBody.scrollTop = chatBody.scrollHeight;
          }, 1000);
      };

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

      window.switchAdminTab = function(tab) {
          const leadsTabBtn = document.querySelectorAll('.tab-btn')[0];
          const msgsTabBtn = document.querySelectorAll('.tab-btn')[1];
          const leadsDiv = document.getElementById('adminLeadsTab');
          const msgsDiv = document.getElementById('adminMessagesTab');

          if (tab === 'leads') {
              leadsTabBtn.classList.add('active');
              msgsTabBtn.classList.remove('active');
              leadsDiv.style.display = 'block';
              msgsDiv.style.display = 'none';
          } else {
              msgsTabBtn.classList.add('active');
              leadsTabBtn.classList.remove('active');
              msgsDiv.style.display = 'block';
              leadsDiv.style.display = 'none';
              loadAdminMessages();
          }
      }

      function loadAdminData() {
          const container = document.getElementById("leadsContainer");
          container.innerHTML = "<p>Loading records...</p>";

          onValue(ref(db, 'solar_leads'), (snapshot) => {
              const leads = snapshot.val();
              let html = "<h4 style='color:#065f46; margin-bottom:12px;'>Qualified Leads Records:</h4>";
              if (leads) {
                  Object.values(leads).reverse().forEach(lead => {
                      html += `<div class="lead-item"><strong>${lead.firstName} ${lead.lastName}</strong> (${lead.phone})<br>
                      🏠 Address: ${lead.street}, ${lead.city}, ${lead.stateZip}<br>
                      ⚡ Homeowner: ${lead.homeowner} | Bill: $${lead.monthlyBill} | Provider: ${lead.electricProvider}<br>
                      💳 Credit: ${lead.creditScore} | Income: ${lead.householdIncome} [User: ${lead.user}]<br>
                      <small style="color:#64748b;">${new Date(lead.timestamp).toLocaleString()}</small></div>`;
                  });
              } else {
                  html += "<p>No leads found yet.</p>";
              }
              container.innerHTML = html;
          }, { onlyOnce: true });
      }

      function loadAdminMessages() {
          const container = document.getElementById("messagesContainer");
          container.innerHTML = "<p>Loading support messages...</p>";

          onValue(ref(db, 'support_messages'), (snapshot) => {
              const msgs = snapshot.val();
              let html = "<h4 style='color:#0284c7; margin-bottom:12px;'>Customer Support Messages:</h4>";
              if (msgs) {
                  Object.values(msgs).reverse().forEach(m => {
                      html += `<div class="msg-item"><strong>User:</strong> ${m.user}<br><strong>Message:</strong> ${m.message}<br><small style="color:#64748b;">${new Date(m.timestamp).toLocaleString()}</small></div>`;
                  });
              } else {
                  html += "<p>No messages received yet.</p>";
              }
              container.innerHTML = html;
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
