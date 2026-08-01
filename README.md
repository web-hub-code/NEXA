<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Solar Energy Solutions - Pro Live Platform & User History CRM</title>
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
            -webkit-tap-highlight-color: transparent;
        }
        header {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            color: white;
            padding: 40px 15px;
            text-align: center;
            cursor: pointer;
            user-select: none;
            position: relative;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
        }
        header h1 {
            font-size: 2.1rem;
            margin-bottom: 8px;
            font-weight: 700;
            letter-spacing: -0.5px;
        }
        header p {
            font-size: 1rem;
            opacity: 0.85;
            font-weight: 300;
        }
        /* Top Auth Bar */
        #authBar {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 6px 12px;
            border-radius: 30px;
            font-size: 0.8rem;
            display: flex;
            align-items: center;
            gap: 8px;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }
        #authBar button {
            background: #10b981;
            color: white;
            border: none;
            padding: 4px 10px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: 600;
        }
        .container {
            width: 100%;
            max-width: 900px;
            margin: -20px auto 30px auto;
            background: white;
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.05);
            position: relative;
            z-index: 10;
        }
        @media(min-width: 768px) {
            .container {
                padding: 40px;
                margin-top: -30px;
            }
            header h1 { font-size: 2.75rem; }
        }
        .section-title {
            color: #0f172a;
            font-size: 1.5rem;
            margin-bottom: 15px;
            font-weight: 600;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 8px;
        }
        @media(min-width: 768px) {
            .section-title { font-size: 1.8rem; }
        }
        p {
            margin-bottom: 15px;
            font-size: 0.95rem;
            color: #475569;
        }
        @media(min-width: 768px) {
            p { font-size: 1.05rem; }
        }
        /* Trust Badges */
        .trust-bar {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
            margin: 20px 0;
            text-align: center;
        }
        @media(min-width: 640px) {
            .trust-bar { grid-template-columns: repeat(3, 1fr); }
        }
        .trust-badge {
            background: #f1f5f9;
            border: 1px solid #e2e8f0;
            padding: 12px;
            border-radius: 8px;
            color: #0f172a;
            font-weight: 600;
            font-size: 0.85rem;
        }
        .features {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
            margin: 25px 0;
        }
        @media(min-width: 640px) {
            .features { grid-template-columns: repeat(3, 1fr); }
        }
        .feature-card {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }
        .feature-card h3 {
            color: #0f172a;
            margin-bottom: 8px;
            font-size: 1.05rem;
        }
        /* Widgets */
        .widget-box {
            background: #f8fafc;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid #e2e8f0;
            margin-top: 25px;
        }
        @media(min-width: 768px) {
            .widget-box { padding: 30px; }
        }
        .widget-box h3 {
            color: #0f172a;
            margin-bottom: 12px;
            font-size: 1.2rem;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            font-size: 0.9rem;
            color: #334155;
        }
        .form-group input, .form-group select {
            width: 100%;
            padding: 12px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 1rem;
            background: white;
        }
        .submit-btn {
            background: #10b981;
            color: white;
            border: none;
            padding: 14px;
            font-size: 1rem;
            border-radius: 8px;
            cursor: pointer;
            width: 100%;
            font-weight: 600;
        }
        .submit-btn:hover { background: #059669; }

        /* Extra Modern Live Phone Dialer Modal */
        #dialerModal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(15, 23, 42, 0.85);
            backdrop-filter: blur(8px);
            z-index: 99999;
            justify-content: center;
            align-items: center;
        }
        .dialer-screen {
            background: linear-gradient(180deg, #1e293b 0%, #0f172a 100%);
            color: white;
            width: 100%;
            max-width: 380px;
            height: 100%;
            max-height: 720px;
            border-radius: 0;
            padding: 30px 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
            position: relative;
        }
        @media(min-width: 480px) {
            .dialer-screen {
                border-radius: 36px;
                height: 680px;
                border: 4px solid #334155;
            }
        }
        .dialer-header {
            text-align: center;
            margin-top: 20px;
        }
        .caller-avatar {
            width: 90px;
            height: 90px;
            background: linear-gradient(135deg, #10b981, #059669);
            border-radius: 50%;
            margin: 0 auto 15px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.2rem;
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.4);
            animation: pulseAvatar 2s infinite;
        }
        @keyframes pulseAvatar {
            0% { transform: scale(1); box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.6); }
            70% { transform: scale(1.05); box-shadow: 0 0 0 15px rgba(16, 185, 129, 0); }
            100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); }
        }
        .dialer-controls {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin-bottom: 25px;
            padding: 0 20px;
        }
        .dialer-btn {
            background: rgba(255, 255, 255, 0.1);
            border: none;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto;
            transition: background 0.2s;
        }
        .dialer-btn:hover { background: rgba(255, 255, 255, 0.2); }
        .end-call-btn {
            background: #ef4444;
            width: 75px;
            height: 75px;
            border-radius: 50%;
            border: none;
            color: white;
            font-size: 1.8rem;
            cursor: pointer;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 10px 20px rgba(239, 68, 68, 0.4);
            transition: transform 0.2s;
        }
        .end-call-btn:hover { transform: scale(1.05); }

        /* Floating Call Launcher Banner */
        .live-call-banner {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            color: white;
            padding: 25px;
            border-radius: 12px;
            margin-top: 25px;
            text-align: center;
        }
        
        /* Floating Chat Widget */
        #floatingChatBtn {
            position: fixed;
            bottom: 25px;
            right: 25px;
            background: #10b981;
            color: white;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.6rem;
            cursor: pointer;
            box-shadow: 0 10px 25px rgba(16, 185, 129, 0.4);
            z-index: 9999;
            transition: transform 0.2s;
        }
        #floatingChatBtn:hover { transform: scale(1.1); }
        #chatWidgetModal {
            display: none;
            position: fixed;
            bottom: 95px;
            right: 20px;
            width: 340px;
            height: 440px;
            background: white;
            border-radius: 16px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            z-index: 99999;
            flex-direction: column;
            overflow: hidden;
            border: 1px solid #e2e8f0;
        }
        .chat-header {
            background: #0f172a;
            color: white;
            padding: 15px;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .chat-body {
            flex: 1;
            padding: 15px;
            overflow-y: auto;
            background: #f8fafc;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .chat-msg {
            background: white;
            padding: 10px 14px;
            border-radius: 10px;
            font-size: 0.85rem;
            max-width: 80%;
            border: 1px solid #e2e8f0;
        }
        .chat-msg.user { background: #d1fae5; align-self: flex-end; border-color: #a7f3d0; }
        .chat-msg.bot { background: #ffffff; align-self: flex-start; border-color: #cbd5e1; }
        .chat-footer {
            padding: 10px;
            background: white;
            border-top: 1px solid #e2e8f0;
            display: flex;
            gap: 8px;
        }
        .chat-footer input {
            flex: 1;
            padding: 8px 12px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 0.85rem;
        }
        .chat-footer button {
            background: #10b981;
            color: white;
            border: none;
            padding: 8px 14px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
        }

        /* FAQ & Modals */
        .faq-item {
            background: #fff;
            border: 1px solid #e2e8f0;
            margin-bottom: 8px;
            border-radius: 8px;
            overflow: hidden;
        }
        .faq-question {
            padding: 15px;
            font-weight: 600;
            cursor: pointer;
            color: #0f172a;
            display: flex;
            justify-content: space-between;
        }
        .faq-answer {
            padding: 15px;
            display: none;
            background: #f8fafc;
            border-top: 1px solid #e2e8f0;
        }
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
            padding: 25px;
            border-radius: 16px;
            width: 92%;
            max-width: 480px;
            position: relative;
        }
        .admin-content { max-width: 800px; max-height: 85vh; overflow-y: auto; }
        .close-btn { position: absolute; top: 15px; right: 20px; font-size: 1.5rem; cursor: pointer; color: #94a3b8; }
        .google-btn { background: #ef4444; color: white; border: none; padding: 12px; width: 100%; border-radius: 8px; font-weight: 600; cursor: pointer; margin-top: 10px; }
        #toastNotification {
            position: fixed;
            bottom: 20px;
            left: 20px;
            right: 20px;
            max-width: 380px;
            background: #0f172a;
            color: white;
            padding: 14px 18px;
            border-radius: 12px;
            font-size: 0.9rem;
            z-index: 999;
            display: none;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            border-left: 4px solid #10b981;
            animation: slideIn 0.3s ease;
        }
        @keyframes slideIn {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        .lead-item {
            background: #f8fafc;
            padding: 14px;
            margin-bottom: 12px;
            border-radius: 8px;
            border-left: 4px solid #10b981;
            font-size: 0.9rem;
            border: 1px solid #e2e8f0;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            gap: 15px;
        }
        .lead-actions {
            display: flex;
            flex-direction: column;
            gap: 6px;
        }
        .lead-actions button {
            padding: 6px 12px;
            border: none;
            border-radius: 6px;
            font-weight: 600;
            font-size: 0.75rem;
            cursor: pointer;
            color: white;
        }
        .btn-approve { background: #10b981; }
        .btn-approve:hover { background: #059669; }
        .btn-reject { background: #f59e0b; }
        .btn-reject:hover { background: #d97706; }
        .btn-delete { background: #ef4444; }
        .btn-delete:hover { background: #dc2626; }
        footer { text-align: center; padding: 25px; color: #64748b; font-size: 0.85rem; border-top: 1px solid #e2e8f0; margin-top: 30px; }
    </style>
</head>
<body>

    <!-- Header (Tap 4 times for Secret Admin Panel) -->
    <header id="secretTrigger">
        <div id="authBar">
            <span id="userDisplay">Guest</span>
            <button id="authBtn">Login</button>
        </div>
        <h1>Solar Energy Solutions</h1>
        <p>US Nationwide Clean Renewable Power Consultation & Live Voice Hub</p>
    </header>

    <div class="container">
        <div style="display:inline-flex; align-items:center; gap:8px; background:#ecfdf5; color:#065f46; padding:6px 14px; border-radius:30px; font-size:0.85rem; font-weight:600; margin-bottom:20px; border:1px solid #a7f3d0;">
            <span style="width:7px; height:7px; background:#10b981; border-radius:50%; display:inline-block;"></span>
            Suzanne Foster Online & Ready (US Federal Tax Credit 30% Active)
        </div>
        
        <h2 class="section-title">Consultation & Live Voice Hub</h2>
        <p>Connect instantly with our US solar specialist <strong>Suzanne Foster</strong> using the interactive voice call platform below, or chat live with her automated AI assistant.</p>
        
        <!-- Trust Bar -->
        <div class="trust-bar">
            <div class="trust-badge">🛡️ 25-Yr US Federal Warranty</div>
            <div class="trust-badge">⚡ 0-Down Financing</div>
            <div class="trust-badge">👷 NABCEP Certified Experts</div>
        </div>

        <div class="features">
            <div class="feature-card">
                <h3>Live Web Call</h3>
                <p>Interactive speech synthesis & simulated live voice streaming with Suzanne.</p>
            </div>
            <div class="feature-card">
                <h3>Real-Time AI Chat</h3>
                <p>Suzanne Foster AI replies instantly to your queries in the chat box.</p>
            </div>
            <div class="feature-card">
                <h3>Admin & User History</h3>
                <p>View real-time user activity history with 1-click clear options.</p>
            </div>
        </div>

        <!-- Extra Modern Live Call Launcher Box -->
        <div class="live-call-banner">
            <h3>📞 Talk Live with Suzanne Foster (Voice Session)</h3>
            <p style="color:#cbd5e1; margin-bottom:15px; font-size:0.9rem;">Launch the live interactive phone dialer interface to start your voice consultation session.</p>
            <button type="button" class="submit-btn" id="launchDialerBtn" style="background:#10b981; max-width:260px; margin:0 auto; display:block;">Open Live Phone Dialer</button>
        </div>

        <!-- Real-Time User History Section -->
        <div class="widget-box" style="background:#ffffff; border: 2px dashed #cbd5e1;">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
                <h3 style="margin-bottom:0;">📜 Your Real-Time Activity & Submission History</h3>
                <button type="button" id="clearUserHistoryBtn" style="background:#ef4444; color:white; border:none; padding:6px 12px; border-radius:6px; font-size:0.8rem; font-weight:600; cursor:pointer;">Clear My History</button>
            </div>
            <p style="font-size:0.85rem; color:#64748b; margin-bottom:15px;">Here is your live history of consultations, calls, and qualification form submissions:</p>
            <div id="userHistoryList" style="max-height: 220px; overflow-y: auto; display: flex; flex-direction: column; gap: 8px;">
                <p style="font-size:0.9rem; color:#94a3b8;">No activity history recorded yet.</p>
            </div>
        </div>

        <!-- Solar Calculator -->
        <div class="widget-box">
            <h3>⚡ US Solar Savings & ROI Calculator</h3>
            <div class="form-group">
                <label for="monthlyBill">Average Monthly Electric Bill ($):</label>
                <input type="number" id="monthlyBill" placeholder="e.g. 250" oninput="calculateSavings()">
            </div>
            <div id="savingsResult" style="background:#e2e8f0; padding:15px; border-radius:8px; font-weight:bold; color:#0f172a; display:none;">
                Estimated Annual Savings: <span id="savedAmount" style="color:#059669;">$0</span><br>
                Estimated 25-Year Savings: <span id="longTermSavings" style="color:#059669;">$0</span><br>
                Payback Period: <span id="paybackPeriod">3.2 Years</span>
            </div>
        </div>

        <!-- A-to-Z Qualification Wizard -->
        <div class="widget-box" style="margin-top:25px;">
            <h3>📋 A-to-Z US Solar Qualification Wizard</h3>
            <form id="wizardForm">
                <div class="form-group">
                    <label>1. Property Ownership:</label>
                    <select id="ownership" required>
                        <option value="">Select option</option>
                        <option value="Homeowner">Homeowner</option>
                        <option value="Renter">Renter</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>2. Roof Type & Sunlight:</label>
                    <select id="roofType" required>
                        <option value="">Select roof type</option>
                        <option value="Shingle - Full Sun">Asphalt Shingle (Full Sun)</option>
                        <option value="Tile - Partial Shade">Tile Roof (Partial Shade)</option>
                        <option value="Metal Roof">Metal Roof</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>3. Monthly Power Bill Range:</label>
                    <select id="billRange" required>
                        <option value="">Select range</option>
                        <option value="$100 - $250">$100 - $250</option>
                        <option value="$250 - $450">$250 - $450</option>
                        <option value="$450+">$450+</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>4. Primary Energy Goal:</label>
                    <select id="energyGoal" required>
                        <option value="">Select goal</option>
                        <option value="Bill Reduction">Bill Reduction</option>
                        <option value="Battery Backup">Battery Backup</option>
                        <option value="Off-Grid">Off-Grid Independence</option>
                    </select>
                </div>
                <div class="form-group">
                    <input type="text" id="wizName" placeholder="Full Name (e.g. Michael Smith)" required>
                </div>
                <div class="form-group">
                    <input type="tel" id="wizPhone" placeholder="US Phone Number (+1 ...)" required>
                </div>
                <div class="form-group">
                    <input type="text" id="wizAddress" placeholder="City, State (e.g. Austin, TX)" required>
                </div>
                <button type="submit" class="submit-btn">Submit Qualification & Get Custom PDF Proposal</button>
            </form>
            <p id="wizardResponseMsg" style="margin-top:10px; font-weight:600; color:#10b981; display:none;"></p>
        </div>

        <!-- FAQ Section -->
        <div class="widget-box" style="margin-top:25px;">
            <h3>❓ Frequently Asked Questions</h3>
            <div class="faq-item">
                <div class="faq-question">How long does installation take? <span>+</span></div>
                <div class="faq-answer">Usually 1 to 3 days depending on system scale and utility interconnection approval.</div>
            </div>
            <div class="faq-item">
                <div class="faq-question">Will it work during power outages? <span>+</span></div>
                <div class="faq-answer">Yes, when paired with an energy storage battery backup like Tesla Powerwall or Enphase.</div>
            </div>
        </div>
    </div>

    <!-- Floating AI Chat Widget -->
    <div id="floatingChatBtn">💬</div>
    <div id="chatWidgetModal">
        <div class="chat-header">
            <span>💬 Suzanne Foster (AI Assistant)</span>
            <span id="closeChat" style="cursor:pointer; font-size:1.2rem;">&times;</span>
        </div>
        <div class="chat-body" id="chatBody">
            <div class="chat-msg bot">Hello! I'm Suzanne Foster. How can I assist you with your US solar consultation today?</div>
        </div>
        <div class="chat-footer">
            <input type="text" id="chatInput" placeholder="Type your message...">
            <button id="sendChatBtn">Send</button>
        </div>
    </div>

    <!-- Extra Modern Local Phone Dialer Simulator Modal -->
    <div id="dialerModal">
        <div class="dialer-screen">
            <div class="dialer-header">
                <div class="caller-avatar">👩‍💼</div>
                <h3 style="font-size: 1.4rem; font-weight: 600; margin-bottom: 5px;">Suzanne Foster</h3>
                <p style="color: #34d399; font-size: 0.9rem; margin-bottom: 5px;" id="callStatusText">Connected & Speaking...</p>
                <div id="callTimer" style="font-size: 1.1rem; font-weight: 300; letter-spacing: 1px; color: #cbd5e1;">00:00</div>
            </div>

            <!-- Sound Wave Visualizer & Recording Badge -->
            <div style="background: rgba(239, 68, 68, 0.15); border: 1px solid rgba(239, 68, 68, 0.4); padding: 6px 12px; border-radius: 20px; font-size: 0.75rem; text-align: center; color: #fca5a5; margin: 10px auto; width: fit-content; display: flex; align-items: center; gap: 6px;">
                <span style="width: 8px; height: 8px; background: #ef4444; border-radius: 50%; display:inline-block; animation: pulseRed 1s infinite;"></span>
                HD Call Recording Active
            </div>
            <style>
                @keyframes pulseRed { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
            </style>

            <div style="display: flex; justify-content: center; align-items: center; gap: 4px; height: 35px; margin: 10px 0;">
                <span style="width: 4px; height: 15px; background: #34d399; border-radius: 2px; animation: wave 1s infinite alternate;"></span>
                <span style="width: 4px; height: 28px; background: #34d399; border-radius: 2px; animation: wave 0.6s infinite alternate;"></span>
                <span style="width: 4px; height: 20px; background: #34d399; border-radius: 2px; animation: wave 0.8s infinite alternate;"></span>
                <span style="width: 4px; height: 32px; background: #34d399; border-radius: 2px; animation: wave 0.5s infinite alternate;"></span>
                <span style="width: 4px; height: 12px; background: #34d399; border-radius: 2px; animation: wave 0.9s infinite alternate;"></span>
            </div>
            <style>
                @keyframes wave { 0% { height: 8px; } 100% { height: 32px; } }
            </style>

            <!-- Dialer Action Buttons -->
            <div>
                <div class="dialer-controls">
                    <button class="dialer-btn" onclick="alert('Microphone Muted')">🔇</button>
                    <button class="dialer-btn" onclick="alert('Speaker Enabled')">🔊</button>
                    <button class="dialer-btn" onclick="alert('Keypad Active')">⌨️</button>
                </div>
                <div style="text-align: center;">
                    <button class="end-call-btn" id="endCallBtn">📞</button>
                    <p style="font-size: 0.75rem; color: #94a3b8; margin-top: 8px;">End Call & Sync Log</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Toast Notification (US Context) -->
    <div id="toastNotification">🔔 New US visitor initialized consultation session!</div>

    <!-- Login Modal -->
    <div id="authModal">
        <div class="auth-content">
            <span class="close-btn" id="closeAuth">&times;</span>
            <h3 style="margin-bottom: 15px; color:#0f172a;">Account Login</h3>
            <form id="emailAuthForm">
                <div class="form-group"><input type="email" id="authEmail" placeholder="Email" required></div>
                <div class="form-group"><input type="password" id="authPassword" placeholder="Password" required></div>
                <button type="submit" class="submit-btn">Login / Sign Up</button>
            </form>
            <button class="google-btn" id="googleLoginBtn">Sign in with Google</button>
        </div>
    </div>

    <!-- Secret Admin CRM Modal with Approval System -->
    <div id="adminModal">
        <div class="admin-content">
            <span class="close-btn" id="closeAdmin">&times;</span>
            <h3 style="color:#0f172a; margin-bottom: 5px;">🔒 Real-Time US Leads CRM & Approval System</h3>
            <p style="font-size:0.85rem; color:#64748b; margin-bottom:15px;">Manage, review, approve, reject, or clear consultation leads:</p>
            <div id="leadsContainer"><p>Loading records...</p></div>
        </div>
    </div>

    <footer>&copy; 2026 Solar Energy Solutions USA. Powered by AI Voice & Firebase.</footer>

    <!-- Firebase & Core Script with Real-Time User History & Clear Options -->
    <script type="module">
      import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
      import { getDatabase, ref, push, onValue, update, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
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
          if (user) {
              currentUserEmail = user.email || user.displayName || "User";
              document.getElementById("userDisplay").innerText = currentUserEmail.split('@')[0];
              document.getElementById("authBtn").innerText = "Logout";
          } else {
              currentUserEmail = "Guest";
              document.getElementById("userDisplay").innerText = "Guest";
              document.getElementById("authBtn").innerText = "Logout";
          }
          loadUserHistory();
      });

      const authModal = document.getElementById("authModal");
      document.getElementById("authBtn").addEventListener("click", (e) => {
          e.stopPropagation();
          if (auth.currentUser) { signOut(auth); } else { authModal.style.display = "flex"; }
      });
      document.getElementById("closeAuth").addEventListener("click", () => { authModal.style.display = "none"; });
      document.getElementById("googleLoginBtn").addEventListener("click", () => {
          signInWithPopup(auth, googleProvider).then(() => { authModal.style.display = "none"; });
      });
      document.getElementById("emailAuthForm").addEventListener("submit", (e) => {
          e.preventDefault();
          const email = document.getElementById("authEmail").value;
          const password = document.getElementById("authPassword").value;
          signInWithEmailAndPassword(auth, email, password).then(() => { authModal.style.display = "none"; }).catch(() => {
              createUserWithEmailAndPassword(auth, email, password).then(() => { authModal.style.display = "none"; });
          });
      });

      window.calculateSavings = function() {
          const bill = parseFloat(document.getElementById("monthlyBill").value) || 0;
          const annualSavings = Math.round(bill * 12 * 0.75);
          const longTerm = annualSavings * 25;
          const resBox = document.getElementById("savingsResult");
          if (bill > 0) {
              resBox.style.display = "block";
              document.getElementById("savedAmount").innerText = "$" + annualSavings.toLocaleString();
              document.getElementById("longTermSavings").innerText = "$" + longTerm.toLocaleString();
              document.getElementById("paybackPeriod").innerText = ((bill * 12 * 3.5) / annualSavings).toFixed(1) + " Years";
          } else { resBox.style.display = "none"; }
      };

      document.querySelectorAll(".faq-question").forEach(item => {
          item.addEventListener("click", () => {
              const ans = item.nextElementSibling;
              ans.style.display = ans.style.display === "block" ? "none" : "block";
          });
      });

      // Real-Time User History Loader & Clear Feature
      function loadUserHistory() {
          const historyList = document.getElementById("userHistoryList");
          onValue(ref(db, 'leads'), (snap) => {
              const data = snap.val();
              historyList.innerHTML = "";
              if (!data) {
                  historyList.innerHTML = '<p style="font-size:0.9rem; color:#94a3b8;">No activity history recorded yet.</p>';
                  return;
              }
              let hasItems = false;
              Object.keys(data).reverse().forEach(key => {
                  const item = data[key];
                  // Show history if it belongs to current user or if guest
                  if (item.user === currentUserEmail || currentUserEmail === "Guest") {
                      hasItems = true;
                      const statusColor = item.status === 'Approved' ? '#10b981' : (item.status === 'Rejected' ? '#f59e0b' : '#64748b');
                      const div = document.createElement("div");
                      div.style.cssText = "background:white; padding:10px 12px; border-radius:8px; border:1px solid #e2e8f0; font-size:0.85rem; display:flex; justify-content:between; align-items:center;";
                      div.innerHTML = `
                          <div>
                              <strong>[${item.type}]</strong> <span style="background:${statusColor}; color:white; padding:1px 6px; border-radius:8px; font-size:0.65rem;">${item.status || 'Pending'}</span><br>
                              <span style="color:#334155;">${item.name || item.user} - ${item.energyGoal || item.billRange || ''}</span><br>
                              <small style="color:#94a3b8;">${item.timestamp}</small>
                          </div>
                          <button onclick="deleteUserHistoryItem('${key}')" style="background:none; border:none; color:#ef4444; font-weight:bold; cursor:pointer; font-size:1rem;" title="Delete item">&times;</button>
                      `;
                      historyList.appendChild(div);
                  }
              });
              if (!hasItems) {
                  historyList.innerHTML = '<p style="font-size:0.9rem; color:#94a3b8;">No activity history recorded yet.</p>';
              }
          });
      }

      window.deleteUserHistoryItem = function(key) {
          remove(ref(db, 'leads/' + key)).then(() => {
              alert("History record cleared.");
          });
      };

      document.getElementById("clearUserHistoryBtn").addEventListener("click", () => {
          if (confirm("Are you sure you want to clear all your consultation history records?")) {
              // Clear records matching current user
              onValue(ref(db, 'leads'), (snap) => {
                  const data = snap.val();
                  if (data) {
                      Object.keys(data).forEach(key => {
                          if (data[key].user === currentUserEmail || currentUserEmail === "Guest") {
                              remove(ref(db, 'leads/' + key));
                          }
                      });
                      alert("Your history has been cleared successfully.");
                  }
              }, { onlyOnce: true });
          }
      });

      // Real AI Chat Widget Logic (Suzanne Foster Responding)
      const chatBtn = document.getElementById("floatingChatBtn");
      const chatModal = document.getElementById("chatWidgetModal");
      const closeChat = document.getElementById("closeChat");
      const sendChatBtn = document.getElementById("sendChatBtn");
      const chatInput = document.getElementById("chatInput");
      const chatBody = document.getElementById("chatBody");

      chatBtn.addEventListener("click", () => { chatModal.style.display = "flex"; });
      closeChat.addEventListener("click", () => { chatModal.style.display = "none"; });

      function getSuzanneAIResponse(userInput) {
          const text = userInput.toLowerCase();
          if (text.includes("cost") || text.includes("price") || text.includes("bill")) {
              return "Solar installation costs vary based on your energy consumption, but with the 30% US Federal Tax Credit and our 0-down financing, most homeowners save immediately from month one!";
          } else if (text.includes("battery") || text.includes("backup")) {
              return "Yes! We pair our solar setups with top-tier battery storage systems like Tesla Powerwall so your home stays powered during grid outages.";
          } else if (text.includes("time") || text.includes("long") || text.includes("install")) {
              return "The complete installation process usually takes between 1 to 3 days once utility interconnection and permits are approved.";
          } else {
              return "That's a great question! As your US solar specialist, I recommend scheduling our free consultation or filling out our quick qualification wizard to lock in your 30% tax savings.";
          }
      }

      sendChatBtn.addEventListener("click", () => {
          const text = chatInput.value.trim();
          if(!text) return;
          
          const userMsg = document.createElement("div");
          userMsg.className = "chat-msg user";
          userMsg.innerText = text;
          chatBody.appendChild(userMsg);
          chatInput.value = "";
          chatBody.scrollTop = chatBody.scrollHeight;

          setTimeout(() => {
              const reply = getSuzanneAIResponse(text);
              const botMsg = document.createElement("div");
              botMsg.className = "chat-msg bot";
              botMsg.innerText = reply;
              chatBody.appendChild(botMsg);
              chatBody.scrollTop = chatBody.scrollHeight;

              if ('speechSynthesis' in window) {
                  const utterance = new SpeechSynthesisUtterance(reply);
                  utterance.rate = 1.0;
                  window.speechSynthesis.speak(utterance);
              }
          }, 800);
      });

      // Wizard Submission & PDF Proposal Simulator
      const wizardForm = document.getElementById("wizardForm");
      wizardForm.addEventListener("submit", (e) => {
          e.preventDefault();
          const timestamp = new Date().toLocaleString();
          const name = document.getElementById("wizName").value;
          push(ref(db, 'leads'), {
              type: "US A-to-Z Qualification + PDF",
              status: "Pending Approval",
              user: currentUserEmail,
              name: name,
              phone: document.getElementById("wizPhone").value,
              ownership: document.getElementById("ownership").value,
              roofType: document.getElementById("roofType").value,
              billRange: document.getElementById("billRange").value,
              energyGoal: document.getElementById("energyGoal").value,
              address: document.getElementById("wizAddress").value,
              timestamp: timestamp
          }).then(() => {
              const msg = document.getElementById("wizardResponseMsg");
              msg.style.display = "block";
              msg.innerHTML = `Success! Profile saved.<br><a href="#" onclick="alert('Downloading Custom Solar Proposal PDF for ${name}...'); return false;" style="color:#047857; text-decoration:underline;">📥 Download Custom Solar Savings PDF Proposal</a>`;
              wizardForm.reset();
          });
      });

      // Phone Dialer Modal Logic & Interactive Voice Speech
      const dialerModal = document.getElementById("dialerModal");
      const launchDialerBtn = document.getElementById("launchDialerBtn");
      const endCallBtn = document.getElementById("endCallBtn");
      let callTimerInterval = null;
      let secondsElapsed = 0;

      launchDialerBtn.addEventListener("click", () => {
          dialerModal.style.display = "flex";
          secondsElapsed = 0;
          document.getElementById("callStatusText").innerText = "Connected with Suzanne";
          document.getElementById("callTimer").innerText = "00:00";
          
          if ('speechSynthesis' in window) {
              const greeting = new SpeechSynthesisUtterance("Hello! This is Suzanne Foster from US Solar Energy Solutions. Thank you for connecting with our live voice consultation. How can I assist you with your clean energy goals today?");
              window.speechSynthesis.speak(greeting);
          }

          callTimerInterval = setInterval(() => {
              secondsElapsed++;
              let mins = Math.floor(secondsElapsed / 60).toString().padStart(2, '0');
              let secs = (secondsElapsed % 60).toString().padStart(2, '0');
              document.getElementById("callTimer").innerText = `${mins}:${secs}`;
          }, 1000);
      });

      endCallBtn.addEventListener("click", () => {
          clearInterval(callTimerInterval);
          dialerModal.style.display = "none";
          if ('speechSynthesis' in window) { window.speechSynthesis.cancel(); }
          
          const timestamp = new Date().toLocaleString();
          push(ref(db, 'leads'), {
              type: "Suzanne US Live Voice Call Log",
              status: "Pending Approval",
              user: currentUserEmail,
              name: currentUserEmail,
              phone: "US Phone Dialer Consultation",
              ownership: "US Voice Session",
              roofType: "Consulted Suzanne",
              billRange: `Duration: ${Math.floor(secondsElapsed/60)}m ${secondsElapsed%60}s`,
              energyGoal: "US Live Phone Call Completed & Recorded",
              address: "US Dialer Simulator",
              timestamp: timestamp
          }).then(() => {
              alert("US Call ended, HD audio recording saved, and consultation log synced!");
          });
      });

      // Admin Action Functions for Approval, Rejection, and Deletion
      window.updateLeadStatus = function(key, newStatus) {
          update(ref(db, 'leads/' + key), { status: newStatus }).then(() => {
              alert("Lead status successfully updated to: " + newStatus);
          });
      };

      window.deleteLeadItem = function(key) {
          if (confirm("Are you sure you want to delete this lead record?")) {
              remove(ref(db, 'leads/' + key)).then(() => {
                  alert("Lead deleted successfully.");
              });
          }
      };

      // Randomized US Fake Live Notifications Popup Generator
      const usNames = ["Michael Smith (Austin, TX)", "Sarah Johnson (Miami, FL)", "David Miller (Phoenix, AZ)", "Jessica Davis (Denver, CO)", "Robert Wilson (San Diego, CA)", "Emily Brown (Atlanta, GA)"];
      const usActions = ["just completed US solar qualification wizard!", "started a live voice call with Suzanne Foster!", "downloaded a custom solar proposal PDF!"];

      function showFakeUSNotification() {
          const randomName = usNames[Math.floor(Math.random() * usNames.length)];
          const randomAction = usActions[Math.floor(Math.random() * usActions.length)];
          const toast = document.getElementById("toastNotification");
          toast.innerHTML = `🇺🇸 <strong>${randomName}</strong><br><span style="color:#cbd5e1; font-size:0.85rem;">${randomAction}</span>`;
          toast.style.display = "block";
          setTimeout(() => {
              toast.style.display = "none";
          }, 5000);
      }

      setTimeout(() => {
          showFakeUSNotification();
          setInterval(showFakeUSNotification, 15000);
      }, 6000);

      // Secret Admin Panel 4-Tap with PIN 5426
      let tapCount = 0, tapTimer = null;
      document.getElementById("secretTrigger").addEventListener("click", () => {
          tapCount++;
          clearTimeout(tapTimer);
          if (tapCount === 4) {
              tapCount = 0;
              let pin = prompt("Enter Secret Admin PIN:");
              if (pin === "5426") {
                  document.getElementById("adminModal").style.display = "flex";
                  const container = document.getElementById("leadsContainer");
                  onValue(ref(db, 'leads'), (snap) => {
                      const data = snap.val();
                      container.innerHTML = "";
                      if (!data) { container.innerHTML = "<p>No records found.</p>"; return; }
                      Object.keys(data).reverse().forEach(key => {
                          const item = data[key];
                          const statusColor = item.status === 'Approved' ? '#10b981' : (item.status === 'Rejected' ? '#f59e0b' : '#64748b');
                          const div = document.createElement("div");
                          div.className = "lead-item";
                          div.innerHTML = `
                              <div>
                                  <strong>[${item.type}]</strong> <span style="background:${statusColor}; color:white; padding:2px 8px; border-radius:10px; font-size:0.7rem;">${item.status || 'Pending'}</span><br>
                                  <strong>User:</strong> ${item.user}<br>
                                  <strong>Name:</strong> ${item.name} | <strong>Phone:</strong> ${item.phone}<br>
                                  <strong>Details:</strong> ${item.ownership}, ${item.roofType}, ${item.billRange}<br>
                                  <strong>Goal/Note:</strong> ${item.energyGoal} (${item.address})<br>
                                  <small style="color:#64748b;">Time: ${item.timestamp}</small>
                              </div>
                              <div class="lead-actions">
                                  <button class="btn-approve" onclick="updateLeadStatus('${key}', 'Approved')">Approve</button>
                                  <button class="btn-reject" onclick="updateLeadStatus('${key}', 'Rejected')">Reject</button>
                                  <button class="btn-delete" onclick="deleteLeadItem('${key}')">Delete</button>
                              </div>
                          `;
                          container.appendChild(div);
                      });
                  });
              } else if (pin !== null) { alert("Incorrect PIN!"); }
          } else { tapTimer = setTimeout(() => { tapCount = 0; }, 600); }
      });

      document.getElementById("closeAdmin").addEventListener("click", () => { document.getElementById("adminModal").style.display = "none"; });
    </script>
</body>
</html>
