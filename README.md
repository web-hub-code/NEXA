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

    <header>
        <h1>Prime Solutions Solar Energy</h1>
        <p>Empowering Your Property with Clean, Renewable Power</p>
    </header>

    <div class="container">
        <h2 class="section-title">Welcome to Our Consultation Portal</h2>
        <p>Discover how much you can save on your monthly utility bills with customized solar energy installations. Speak directly with our AI energy specialist, Suzanne Foster, right now to check your property eligibility and schedule an expert callback.</p>
        
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
    </div>

    <footer>
        &copy; 2026 Prime Solutions. All rights reserved. Powered by Vapi AI.
    </footer>

    <!-- Vapi Web Widget SDK Script -->
    <script
      src="https://cdn.jsdelivr.net/gh/VapiAI/html-script-tag@latest/dist/assets/index.js"
      defer
    ></script>
    <script>
      window.addEventListener("DOMContentLoaded", () => {
        window.vapiSDK.run({
          apiKey: "YOUR_VAPI_PUBLIC_API_KEY",
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
      });
    </script>
</body>
</html>
