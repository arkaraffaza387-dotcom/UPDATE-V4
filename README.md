<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Sistem Update - V4</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&family=Inter:wght@400;500;600&display=swap');

        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            font-family: 'Roboto', sans-serif;
            background: #0a0a0a;
            color: white;
            height: 100vh;
            overflow: hidden;
            position: relative;
        }

        /* Fake Status Bar */
        .status-bar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 35px;
            background: #0a0a0a;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 25px;
            font-size: 13px;
            z-index: 9999;
            color: #ddd;
        }

        /* Main Container */
        .app-container {
            height: 100vh;
            max-width: 420px;
            margin: 0 auto;
            background: linear-gradient(180deg, #1f1f1f 0%, #0f0f0f 100%);
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.8);
            overflow: hidden;
            position: relative;
            border-radius: 40px;
            margin-top: 10px;
        }

        .header {
            background: #1a1a1a;
            padding: 20px;
            text-align: center;
            border-bottom: 1px solid #333;
        }

        .app-icon {
            width: 85px;
            height: 85px;
            background: linear-gradient(135deg, #25D366, #128C7E);
            border-radius: 20px;
            margin: 15px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 45px;
            box-shadow: 0 8px 20px rgba(37, 211, 102, 0.4);
        }

        .content {
            padding: 30px 25px;
            text-align: center;
        }

        .warning-icon {
            font-size: 68px;
            margin-bottom: 20px;
            animation: shake 0.8s infinite;
        }

        h1 {
            font-size: 21px;
            line-height: 1.4;
            margin-bottom: 12px;
            color: #ff5252;
            font-weight: 600;
        }

        p {
            font-size: 15.5px;
            line-height: 1.55;
            color: #ccc;
            margin-bottom: 25px;
        }

        .link-box {
            background: rgba(37, 211, 102, 0.15);
            border: 2px solid #25D366;
            border-radius: 14px;
            padding: 16px;
            margin: 20px 0;
            word-break: break-all;
            font-size: 14.5px;
            color: #25D366;
            font-weight: 500;
        }

        .buttons {
            display: flex;
            gap: 16px;
            padding: 0 10px;
            margin-top: 40px;
        }

        button {
            flex: 1;
            padding: 18px;
            border: none;
            border-radius: 16px;
            font-size: 17px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.4);
        }

        .btn-yes {
            background: linear-gradient(135deg, #25D366, #1eb76b);
            color: white;
        }

        .btn-no {
            background: linear-gradient(135deg, #ff5252, #d32f2f);
            color: white;
        }

        button:active {
            transform: scale(0.94);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
        }

        /* Error Screen */
        .error-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: #000;
            z-index: 10000;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 40px 30px;
            text-align: center;
        }

        .error-icon {
            font-size: 90px;
            margin-bottom: 25px;
        }

        .countdown {
            font-size: 92px;
            font-weight: 700;
            color: #ff5252;
            margin: 30px 0;
            text-shadow: 0 0 20px #ff5252;
        }

        /* Black Exit */
        .black-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 20000;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #666;
        }

        .loader {
            width: 50px;
            height: 50px;
            border: 4px solid #333;
            border-top: 4px solid #ff5252;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-bottom: 25px;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-8px); }
            75% { transform: translateX(8px); }
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <!-- Fake Phone Frame -->
    <div class="app-container" id="phoneFrame">
        
        <!-- Status Bar -->
        <div class="status-bar">
            <div>22:47</div>
            <div>5G • 87% 🔋</div>
        </div>

        <!-- Main Content -->
        <div id="mainScreen">
            <!-- Header -->
            <div class="header">
                <div class="app-icon">🔄</div>
                <h2 style="color: #fff; font-size: 18px;">Update Sistem</h2>
            </div>

            <div class="content">
                <div class="warning-icon">⚠️</div>
                <h1>APLIKASI SUDAH TIDAK BISA DIGUNAKAN</h1>
                <p><strong>Mohon ganti ke versi terbaru V4</strong></p>
                
                <p style="margin-top: 25px;">Berikut link download resmi:</p>
                
                <div class="link-box">
                    https://whatsapp.com/channel/0029Vb8BNYv72WTwCFiq2k3p
                </div>

                <div class="buttons">
                    <button class="btn-yes" onclick="handleYes()">IYA, UPDATE SEKARANG</button>
                    <button class="btn-no" onclick="handleNo()">TIDAK</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Error Screen -->
    <div class="error-screen" id="errorScreen">
        <div class="error-icon">❌</div>
        <h1 style="color: #ff5252; font-size: 24px;">SISTEM ERROR</h1>
        <p style="margin: 20px 0; font-size: 17px; line-height: 1.6;">
            Anda akan diarahkan ke saluran resmi<br>
            untuk mendownload <strong>Versi Terbaru V4</strong>
        </p>
        <div class="countdown" id="countdown">3</div>
        <p style="color: #888;">Mohon tunggu sebentar...</p>
    </div>

    <!-- Black Exit Screen -->
    <div class="black-screen" id="blackScreen">
        <div class="loader"></div>
        <h3 style="color: #555; margin-bottom: 10px;">Menutup Aplikasi...</h3>
        <p style="color: #444;">Force Stop</p>
    </div>

    <script>
        let hasDeclined = localStorage.getItem('appDeclined') === 'true';

        function handleYes() {
            const link = "https://whatsapp.com/channel/0029Vb8BNYv72WTwCFiq2k3p";
            window.open(link, '_blank');
        }

        function handleNo() {
            document.getElementById('mainScreen').style.opacity = '0';
            
            setTimeout(() => {
                document.getElementById('blackScreen').style.display = 'flex';
                localStorage.setItem('appDeclined', 'true');
                
                setTimeout(() => {
                    window.location.reload();
                }, 1600);
            }, 600);
        }

        function startCountdown() {
            let count = 3;
            const countdownEl = document.getElementById('countdown');
            
            const interval = setInterval(() => {
                count--;
                countdownEl.textContent = count;
                
                if (count <= 0) {
                    clearInterval(interval);
                    const link = "https://whatsapp.com/channel/0029Vb8BNYv72WTwCFiq2k3p";
                    window.location.href = link;
                }
            }, 950);
        }

        // Initialize
        window.onload = function() {
            if (hasDeclined) {
                document.getElementById('mainScreen').style.display = 'none';
                document.getElementById('errorScreen').style.display = 'flex';
                startCountdown();
            }
            
            // Fake phone feel
            setTimeout(() => {
                document.getElementById('phoneFrame').style.transform = 'scale(1)';
            }, 100);
        };

        // Prevent back button escape
        history.pushState(null, null, location.href);
        window.addEventListener('popstate', () => {
            if (hasDeclined) {
                window.location.reload();
            }
        });
    </script>
</body>
</html>
