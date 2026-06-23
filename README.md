<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS - Bug WA Simulation v1 (Beta)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        dasar: '#050714',
                        kartu: '#0F1424',
                        utama: '#165DFF',
                        emas: '#D4AF37',
                        lembut: '#A8B2D1',
                        batas: '#232940'
                    },
                    fontFamily: { inter: ['Inter', 'sans-serif'] },
                    animation: {
                        'float': 'float 3s ease-in-out infinite',
                        'glow': 'glow 2s ease-in-out infinite',
                        'pulse-glow': 'pulse-glow 2s ease-in-out infinite',
                        'slide-up': 'slide-up 0.6s ease-out',
                        'fade-in': 'fade-in 0.8s ease-out',
                        'bounce-in': 'bounce-in 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55)',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-20px)' }
                        },
                        glow: {
                            '0%, 100%': { boxShadow: '0 0 20px rgba(22,93,255,0.3)' },
                            '50%': { boxShadow: '0 0 40px rgba(22,93,255,0.6)' }
                        },
                        'pulse-glow': {
                            '0%, 100%': { opacity: '1' },
                            '50%': { opacity: '0.5' }
                        },
                        'slide-up': {
                            'from': { opacity: '0', transform: 'translateY(30px)' },
                            'to': { opacity: '1', transform: 'translateY(0)' }
                        },
                        'fade-in': {
                            'from': { opacity: '0' },
                            'to': { opacity: '1' }
                        },
                        'bounce-in': {
                            'from': { opacity: '0', transform: 'scale(0.3)' },
                            'to': { opacity: '1', transform: 'scale(1)' }
                        }
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        * {
            font-family: 'Inter', sans-serif;
        }
        body {
            background-color: #050714;
            background-image: radial-gradient(circle at top, rgba(22,93,255,0.08), transparent 55%);
            min-height: 100vh;
            margin: 0;
            overflow-x: hidden;
        }
        .kaca {
            background: rgba(15, 20, 36, 0.85);
            border: 1px solid rgba(255,255,255,0.08);
            backdrop-filter: blur(12px);
            box-shadow: 0 8px 24px rgba(0,0,0,0.35);
            border-radius: 1.5rem;
        }
        .tombol-utama {
            background: linear-gradient(135deg,#165DFF,#367BFF);
            color: #fff;
            border-radius: 0.75rem;
            transition: all .3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            position: relative;
            overflow: hidden;
        }
        .tombol-utama::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }
        .tombol-utama:hover::before {
            left: 100%;
        }
        .tombol-utama:hover {
            filter: brightness(1.15);
            box-shadow: 0 0 20px rgba(22,93,255,0.5), 0 8px 16px rgba(22,93,255,0.3);
            transform: translateY(-2px);
        }
        .tombol-aktif {
            background-color: #165DFF;
            border-color: #165DFF;
            box-shadow: 0 0 15px rgba(22,93,255,0.4);
        }
        .tombol-pasif {
            background-color: #0F1424;
            border-color: #232940;
            transition: all 0.3s ease;
        }
        .tombol-pasif:hover {
            border-color: #165DFF;
            background-color: rgba(22,93,255,0.1);
        }
        .sembunyi { display: none !important; }
        input {
            background-color: #050714;
            border: 1px solid #232940;
            color: #fff;
            padding: 0.75rem;
            border-radius: 0.75rem;
            width: 100%;
            outline: none;
            transition: all 0.3s ease;
        }
        input:focus { 
            border-color: #165DFF;
            box-shadow: 0 0 10px rgba(22,93,255,0.3);
            background-color: rgba(22,93,255,0.05);
        }
        label { 
            font-size: 0.875rem; 
            color: #A8B2D1; 
            margin-bottom: 0.25rem; 
            display: block;
            font-weight: 500;
        }
        select {
            background-color: #050714;
            border: 1px solid #232940;
            color: #fff;
            padding: 0.75rem;
            border-radius: 0.75rem;
            width: 100%;
            outline: none;
            transition: all 0.3s ease;
        }
        select:focus {
            border-color: #165DFF;
            box-shadow: 0 0 10px rgba(22,93,255,0.3);
        }

        /* DASHBOARD STYLES */
        :root {
            --primary: #00ff88;
            --primary-dark: #00cc66;
            --bg: #0a0a0a;
            --panel: #111111;
            --text: #e0e0e0;
            --text-muted: #aaaaaa;
            --danger: #ff4444;
            --accent: #00ff88;
            --premium: #ffd700;
        }
        
        .dashboard-container {
            width: 100%;
            max-width: 480px;
            background: var(--panel);
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            position: relative;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.1);
            animation: fade-in 0.8s ease-out;
        }

        .dashboard-h1, .dashboard-h2 {
            text-align: center;
            color: var(--primary);
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 0 0 10px rgba(0, 255, 136, 0.4);
            animation: slide-up 0.6s ease-out;
        }

        .dashboard-input-group { 
            margin-bottom: 12px;
            animation: slide-up 0.6s ease-out;
        }
        .dashboard-label { 
            display: block; 
            margin-bottom: 4px; 
            font-size: 0.7em; 
            color: var(--text-muted); 
            text-transform: uppercase;
            font-weight: 600;
        }
        
        .dashboard-input {
            width: 100%;
            padding: 10px;
            background: #1a1a1a;
            border: 1px solid #333;
            color: var(--primary);
            outline: none;
            border-radius: 6px;
            font-size: 0.9em;
            transition: all 0.3s ease;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }
        .dashboard-input:focus { 
            border-color: var(--primary);
            box-shadow: 0 0 10px rgba(0, 255, 136, 0.3);
            background: rgba(0, 255, 136, 0.05);
        }

        .dashboard-button {
            width: 100%;
            padding: 12px;
            background: transparent;
            color: var(--primary);
            border: 1px solid var(--primary);
            cursor: pointer;
            margin-top: 8px;
            text-transform: uppercase;
            font-weight: bold;
            border-radius: 6px;
            transition: all 0.3s ease;
            font-size: 0.85em;
            position: relative;
            overflow: hidden;
        }
        .dashboard-button::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(0, 255, 136, 0.2);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }
        .dashboard-button:active::before {
            width: 300px;
            height: 300px;
        }
        .dashboard-button:active { 
            background: var(--primary); 
            color: #000; 
            transform: scale(0.98);
        }
        .dashboard-button.premium-btn {
            border-color: var(--premium);
            color: var(--premium);
        }
        .dashboard-button.premium-btn:active {
            background: var(--premium);
            color: #000;
        }
        .dashboard-button.secondary { 
            border-color: #555; 
            color: #aaa; 
        }
        .dashboard-button.danger { 
            border-color: var(--danger); 
            color: var(--danger); 
        }

        .notification {
            position: fixed; 
            top: 20px; 
            left: 50%; 
            transform: translateX(-50%);
            background: #111; 
            border: 2px solid var(--primary); 
            padding: 15px 25px;
            z-index: 10000; 
            display: none; 
            font-size: 0.9em;
            border-radius: 20px;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5), 0 0 20px rgba(0, 255, 136, 0.3);
            width: 85%;
            text-align: center;
            animation: bounce-in 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        .bug-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            margin-bottom: 20px;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 5px;
            animation: slide-up 0.8s ease-out;
        }
        .bug-btn {
            background: #151515;
            border: 1px solid #333;
            color: var(--primary);
            padding: 12px 5px;
            border-radius: 8px;
            text-align: center;
            font-size: 0.7em;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 3px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        .bug-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 136, 0.2), transparent);
            transition: left 0.5s;
        }
        .bug-btn:hover::before {
            left: 100%;
        }
        .bug-btn:hover {
            border-color: var(--primary);
            box-shadow: 0 0 10px rgba(0, 255, 136, 0.3);
            transform: translateY(-2px);
        }
        .bug-btn:active {
            background: var(--primary);
            color: #000;
            transform: scale(0.95);
        }
        .bug-btn.prem-only { 
            border-color: var(--premium); 
            color: var(--premium);
        }
        .bug-btn.prem-only:hover {
            box-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
        }

        .console-log {
            background: #050505;
            border: 1px solid #222;
            height: 100px;
            overflow-y: auto;
            padding: 8px;
            font-size: 0.65em;
            color: #00ff44;
            font-family: monospace;
            border-radius: 6px;
            margin-top: 10px;
            animation: slide-up 0.8s ease-out;
            box-shadow: inset 0 0 10px rgba(0, 255, 136, 0.1);
        }

        .status-bar {
            display: flex;
            justify-content: space-between;
            font-size: 0.65em;
            color: #888;
            margin-bottom: 10px;
            background: #000;
            padding: 6px;
            border-radius: 4px;
            border: 1px solid rgba(0, 255, 136, 0.2);
            animation: slide-up 0.6s ease-out;
        }

        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #000; }
        ::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 10px; }

        .haru-logo {
            width: 120px;
            height: 120px;
            margin: 0 auto 15px;
            animation: float 3s ease-in-out infinite;
            filter: drop-shadow(0 0 20px rgba(22,93,255,0.4));
        }

        .logo-glow {
            animation: glow 2s ease-in-out infinite;
        }
    </style>
</head>
<body class="text-white flex items-center justify-center p-4">

    <div id="notification" class="notification"></div>

    <!-- LOGIN PAGE (TAILWIND DESIGN) -->
    <div id="login-page" class="w-full max-w-md animate-fade-in">
        <div class="kaca p-8 text-center">
            <div class="mb-6 animate-bounce-in">
                <img src="https://d2xsxph8kpxj0f.cloudfront.net/310519663746958640/oN9dk99xNWfi2iUtA8BFud/haru_yosuga_logo-ZYHqo9RPzgNRsJcDcnysiz.webp" alt="Haru Logo" class="haru-logo">
                <h1 class="text-3xl font-bold bg-gradient-to-r from-utama to-blue-400 bg-clip-text text-transparent">NEXUS BUG</h1>
                <p class="text-emas text-lg font-semibold">V1 (BETA)</p>
                <p class="text-lembut text-sm mt-2">Ultimate Bug Injector</p>
            </div>

            <div class="flex rounded-xl overflow-hidden border border-batas mb-6 animate-slide-up" style="animation-delay: 0.2s">
                <button id="tabPremium" class="flex-1 py-3 border-0 tombol-aktif transition-all duration-300">💎 Premium</button>
                <button id="tabBiasa" class="flex-1 py-3 border-0 tombol-pasif transition-all duration-300">👤 Biasa</button>
            </div>

            <!-- BAGIAN LOGIN PREMIUM -->
            <div id="bagianPremium" class="animate-slide-up" style="animation-delay: 0.3s">
                <div class="mb-4">
                    <label>Nama Pengguna</label>
                    <input type="text" id="userPremium" placeholder="Masukkan username">
                </div>
                <div class="mb-4">
                    <label>Kata Sandi</label>
                    <input type="password" id="passPremium" placeholder="••••••••">
                </div>
                <button onclick="masukPremium()" class="w-full py-3 tombol-utama">Masuk Premium</button>
                <button onclick="navigateTo('register-premium-page')" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg hover:border-utama hover:bg-opacity-50 transition-all duration-300">Daftar Premium</button>
            </div>

            <!-- BAGIAN LOGIN BIASA -->
            <div id="bagianBiasa" class="sembunyi animate-slide-up" style="animation-delay: 0.3s">
                <div class="mb-4">
                    <label>Nama Pengguna</label>
                    <input type="text" id="userBiasa" placeholder="Masukkan username">
                </div>
                <div class="mb-4">
                    <label>Kata Sandi</label>
                    <input type="password" id="passBiasa" placeholder="••••••••">
                </div>
                <button onclick="masukBiasa()" class="w-full py-3 tombol-utama">Masuk</button>
                <button onclick="navigateTo('reg-step-tiktok')" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg hover:border-utama hover:bg-opacity-50 transition-all duration-300">Daftar Akun Free</button>
            </div>

            <p id="pesanSistem" class="text-lembut text-sm mt-4 animate-fade-in" style="animation-delay: 0.5s"></p>
        </div>
    </div>

    <!-- REGISTER PREMIUM -->
    <div id="register-premium-page" class="w-full max-w-md sembunyi animate-fade-in">
        <div class="kaca p-8 text-center">
            <div class="mb-6 animate-bounce-in">
                <i class="fa fa-lock text-emas text-4xl"></i>
                <h2 class="text-2xl font-bold text-emas mt-3">DAFTAR PREMIUM</h2>
            </div>
            <div class="mb-4 animate-slide-up">
                <label>Kode Verifikasi</label>
                <input type="password" id="reg-prem-code" placeholder="••••••">
            </div>
            <div class="mb-4 animate-slide-up" style="animation-delay: 0.1s">
                <label>Username Baru</label>
                <input type="text" id="reg-prem-user" placeholder="Min 4 karakter">
            </div>
            <div class="mb-4 animate-slide-up" style="animation-delay: 0.2s">
                <label>Password Baru</label>
                <input type="password" id="reg-prem-pass" placeholder="Min 4 karakter">
            </div>
            <button onclick="processRegisterPremium()" class="w-full py-3 tombol-utama animate-slide-up" style="animation-delay: 0.3s">Aktivasi Premium</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg hover:border-utama hover:bg-opacity-50 transition-all duration-300">Kembali</button>
        </div>
    </div>

    <!-- REGISTRATION FLOW FREE - STEP 1 (TIKTOK) -->
    <div id="reg-step-tiktok" class="w-full max-w-md sembunyi animate-fade-in">
        <div class="kaca p-8 text-center">
            <div class="mb-6 animate-bounce-in">
                <i class="fa fa-music text-pink-500 text-4xl"></i>
                <h2 class="text-2xl font-bold mt-3">Verifikasi TikTok</h2>
            </div>
            <p class="text-lembut text-sm mb-6 animate-slide-up">Follow <b>kiboyaslinofake</b> untuk akses 4 hari.</p>
            <button onclick="openTikTok()" class="w-full py-3 tombol-utama bg-gradient-to-r from-pink-500 to-rose-500 hover:from-pink-600 hover:to-rose-600 animate-slide-up">Follow TikTok</button>
            <button id="tiktok-next" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg sembunyi hover:border-utama hover:bg-opacity-50 transition-all duration-300 animate-bounce-in" onclick="navigateTo('reg-step-wa')">Lanjutkan</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg hover:border-utama hover:bg-opacity-50 transition-all duration-300">Batal</button>
        </div>
    </div>

    <!-- REGISTRATION FLOW FREE - STEP 2 (WHATSAPP) -->
    <div id="reg-step-wa" class="w-full max-w-md sembunyi animate-fade-in">
        <div class="kaca p-8 text-center">
            <div class="mb-6 animate-bounce-in">
                <i class="fa fa-whatsapp text-green-500 text-4xl"></i>
                <h2 class="text-2xl font-bold mt-3">Verifikasi Komunitas</h2>
            </div>
            <p class="text-lembut text-sm mb-6 animate-slide-up">Gabung Saluran WA kami.</p>
            <button onclick="openWAChannel()" class="w-full py-3 tombol-utama bg-gradient-to-r from-green-500 to-emerald-500 hover:from-green-600 hover:to-emerald-600 animate-slide-up">Gabung Saluran</button>
            <button id="wa-next" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg sembunyi hover:border-utama hover:bg-opacity-50 transition-all duration-300 animate-bounce-in" onclick="navigateTo('register-free-page')">Lanjutkan ke Pendaftaran</button>
            <button onclick="navigateTo('reg-step-tiktok')" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg hover:border-utama hover:bg-opacity-50 transition-all duration-300">Kembali</button>
        </div>
    </div>

    <!-- REGISTER FREE FORM -->
    <div id="register-free-page" class="w-full max-w-md sembunyi animate-fade-in">
        <div class="kaca p-8 text-center">
            <div class="mb-6 animate-bounce-in">
                <i class="fa fa-user-plus text-utama text-4xl"></i>
                <h2 class="text-2xl font-bold mt-3">Daftar Akun Free</h2>
            </div>
            <p class="text-red-400 text-sm mb-6 font-semibold animate-pulse">⏰ Masa Aktif: 4 Hari</p>
            <div class="mb-4 animate-slide-up">
                <label>Username Baru</label>
                <input type="text" id="reg-free-user" placeholder="Min 4 karakter">
            </div>
            <div class="mb-4 animate-slide-up" style="animation-delay: 0.1s">
                <label>Password Baru</label>
                <input type="password" id="reg-free-pass" placeholder="Min 4 karakter">
            </div>
            <button onclick="processRegisterFree()" class="w-full py-3 tombol-utama animate-slide-up" style="animation-delay: 0.2s">Buat Akun Free</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-kartu border border-batas rounded-lg hover:border-utama hover:bg-opacity-50 transition-all duration-300">Kembali</button>
        </div>
    </div>

    <!-- DASHBOARD -->
    <div id="dashboard-page" class="dashboard-container sembunyi">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px; animation: slide-up 0.6s ease-out">
            <h2 class="dashboard-h2" style="margin:0; font-size:1.1em;">DASHBOARD CORE</h2>
            <span id="user-badge" style="font-size:0.55em; border:1px solid #555; padding:2px 6px; border-radius:8px; animation: bounce-in 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);">STD</span>
        </div>

        <div class="status-bar">
            <span>USER: <b id="display-username">-</b></span>
            <span>EXP: <b id="expiry-date">-</b></span>
        </div>

        <!-- DEVICE LOCK SECTION (PREMIUM ONLY) -->
        <div id="lock-section" class="sembunyi" style="border:1px solid var(--premium); padding:12px; border-radius:8px; margin-bottom:15px; background:rgba(255,215,0,0.05); animation: slide-up 0.6s ease-out; animation-delay: 0.1s">
            <h3 style="color:var(--premium); font-size:0.8em; margin-bottom:10px; text-align:center; font-weight: 600;">🔒 LOCK PERANGKAT TARGET</h3>
            <div class="dashboard-input-group">
                <label class="dashboard-label">NOMOR ANDA (PENGIRIM)</label>
                <input type="tel" id="lock-sender" placeholder="628xxx" class="dashboard-input">
            </div>
            <div class="dashboard-input-group">
                <label class="dashboard-label">NOMOR TARGET (UNTUK DI-LOCK)</label>
                <input type="tel" id="lock-target" placeholder="628xxx" class="dashboard-input">
            </div>
            <div class="dashboard-input-group">
                <label class="dashboard-label">SET KODE PEMBUKA (UNLOCK CODE)</label>
                <input type="text" id="lock-code" placeholder="Contoh: 123456" class="dashboard-input">
            </div>
            <button class="dashboard-button premium-btn" onclick="executeDeviceLock()" style="font-size:0.75em;">INJEKSI DEVICE LOCK</button>
        </div>

        <div class="dashboard-input-group">
            <label class="dashboard-label">NOMOR TARGET BUG (FORMAT 62)</label>
            <input type="tel" id="target-number" placeholder="628xxxxxxxxxx" class="dashboard-input">
        </div>

        <h2 class="dashboard-h2" style="font-size:0.8em; text-align:left; margin:10px 0; color:var(--text-muted);">BUG LIST (<span id="bug-count">0</span>):</h2>
        <div class="bug-grid" id="bug-list">
            <!-- Bugs generated by JS -->
        </div>

        <div class="console-log" id="console-output">
            <div>> System Ready...</div>
        </div>

        <button class="dashboard-button danger" style="margin-top:10px;" onclick="logout()">LOGOUT</button>
    </div>

    <script>
        // --- CONFIG & ENCRYPTION ---
        const DB_KEY = "nexus_v1_data";
        const SESSION_KEY = "nexus_v1_session";
        
        // Kode "NEXUS-BUG" di-encode ke Base64
        const _0x5a2e = "TkVYVVMtQlVH"; 
        const getSecret = () => atob(_0x5a2e);

        // --- DATA BUGS (100 Unik) ---
        const BUG_TYPES = [
            "GHOST_CALL", "MEDIA_BURST", "RAM_EATER", "TEXT_BOMB", "SENSOR_BUG", "DB_CORRUPT", "NOTIF_SPAM", "FLICKER", "DARK_LOCK", "REPLY_LOOP",
            "BATTERY_DRAIN", "CPU_OVERHEAT", "GPS_GLITCH", "MIC_MUTE", "CAM_FREEZE", "STORAGE_FULL", "WIFI_DROP", "BLUETOOTH_LAG", "UI_SHAKE", "FONT_MESS",
            "KEYBOARD_STUCK", "STATUS_ERROR", "BIO_GLITCH", "PP_REMOVER", "CALL_BLOCK", "LINK_CORRUPT", "STICKER_BOMB", "VOICE_DISTORT", "THEME_CRASH", "PROXY_INJECT",
            "PACKET_LOSS", "RESTART_LOOP", "BOOT_DELAY", "TOUCH_FREEZE", "VOLUME_MAX", "BRIGHTNESS_LOW", "SCREEN_INVERT", "APP_FORCLOSE", "LOG_OVERFLOW", "CACHE_BOMB",
            "CONTACT_HIDE", "GROUP_EXIT", "READ_RECEIPT_BUG", "TYPING_GHOST", "ONLINE_STUCK", "OFFLINE_FORCE", "VERIFY_FAIL", "OTP_BLOCK", "E2EE_ERROR", "SERVER_TIMEOUT",
            "DNS_POISON", "SSL_INVALID", "API_ERROR", "TOKEN_EXPIRE", "AUTH_FAIL", "SQL_INJECT_SIM", "JS_ERROR_SIM", "CSS_MESS", "HTML_STRIP", "DOM_CRASH",
            "XSS_SIMULATE", "FRAME_DROP", "PING_SPIKE", "LATENCY_HIGH", "PORT_BLOCK", "FIREWALL_BYPASS", "SHELL_EXEC", "CMD_ERROR", "BASH_CRASH", "ROOT_FAIL",
            "SYSTEM_LAG", "KERNEL_PANIC", "DRV_ERROR", "BIOS_GLITCH", "GPU_ARTIFACT", "RAM_LEAK", "SWAP_FULL", "ZOMBIE_PROC", "THREAD_LOCK", "MUTEX_WAIT",
            "DEADLOCK_SIM", "IO_WAIT", "FS_CORRUPT", "MBR_WIPE_SIM", "PARTITION_ERROR", "BOOTLOADER_BUG", "RECOVERY_FAIL", "ADB_DISABLE", "FASTBOOT_ERROR", "ODIN_FAIL",
            "WIPE_SIMULATE", "FACTORY_RESET_BUG", "OTA_BLOCK", "PATCH_FAIL", "SECURITY_BREACH", "ENCRYPT_ERROR", "DECRYPT_FAIL", "RSA_MESS", "AES_CORRUPT", "MD5_COLLISION"
        ];

        // --- CORE FUNCTIONS ---
        function showNotification(msg) {
            const n = document.getElementById('notification');
            n.innerText = msg;
            n.style.display = 'block';
            setTimeout(() => n.style.display = 'none', 3000);
        }

        function pesan(teks, ok=false){
            const el=document.getElementById('pesanSistem');
            el.textContent=teks;
            el.className=`text-sm mt-4 ${ok?'text-green-300':'text-red-300'} animate-bounce-in`;
        }

        function navigateTo(id) {
            document.querySelectorAll('[id$="-page"], [id^="bagian"]').forEach(c => c.classList.add('sembunyi'));
            document.getElementById(id).classList.remove('sembunyi');
        }

        // --- TAB SWITCHING ---
        document.getElementById('tabPremium').onclick = () => {
            document.getElementById('tabPremium').className = 'flex-1 py-3 border-0 tombol-aktif transition-all duration-300';
            document.getElementById('tabBiasa').className = 'flex-1 py-3 border-0 tombol-pasif transition-all duration-300';
            document.getElementById('bagianPremium').classList.remove('sembunyi');
            document.getElementById('bagianBiasa').classList.add('sembunyi');
        };
        document.getElementById('tabBiasa').onclick = () => {
            document.getElementById('tabBiasa').className = 'flex-1 py-3 border-0 tombol-aktif transition-all duration-300';
            document.getElementById('tabPremium').className = 'flex-1 py-3 border-0 tombol-pasif transition-all duration-300';
            document.getElementById('bagianBiasa').classList.remove('sembunyi');
            document.getElementById('bagianPremium').classList.add('sembunyi');
        };

        // --- REGISTRATION FUNCTIONS ---
        function openTikTok() { 
            window.open('https://www.tiktok.com/@kiboyaslinofake', '_blank'); 
            setTimeout(() => {
                document.getElementById('tiktok-next').classList.remove('sembunyi');
                pesan('✅ Tombol Lanjutkan sudah aktif!', true);
            }, 500);
        }

        function openWAChannel() { 
            window.open('https://whatsapp.com/channel/0029VbDBArY9MF8uLpmviF1S', '_blank'); 
            setTimeout(() => {
                document.getElementById('wa-next').classList.remove('sembunyi');
                pesan('✅ Tombol Lanjutkan sudah aktif!', true);
            }, 500);
        }

        function getUsers() { 
            return JSON.parse(localStorage.getItem(DB_KEY) || "[]"); 
        }

        function saveUsers(u) { 
            localStorage.setItem(DB_KEY, JSON.stringify(u)); 
        }

        function processRegisterPremium() {
            const code = document.getElementById('reg-prem-code').value;
            const u = document.getElementById('reg-prem-user').value;
            const p = document.getElementById('reg-prem-pass').value;
            
            if (code !== getSecret()) {
                pesan("❌ KODE VERIFIKASI TIDAK VALID!");
                return;
            }
            if (u.length < 4) {
                pesan("❌ Username min 4 karakter!");
                return;
            }
            
            let users = getUsers();
            if (users.find(x => x.username === u)) {
                pesan("❌ Username sudah ada!");
                return;
            }
            
            users.push({ username: u, password: p, type: "PREMIUM", expiredAt: "LIFETIME" });
            saveUsers(users);
            pesan("✅ Premium Aktif!", true);
            setTimeout(() => navigateTo('login-page'), 1000);
            document.getElementById('reg-prem-code').value = '';
            document.getElementById('reg-prem-user').value = '';
            document.getElementById('reg-prem-pass').value = '';
        }

        function processRegisterFree() {
            const u = document.getElementById('reg-free-user').value;
            const p = document.getElementById('reg-free-pass').value;
            
            if (u.length < 4) {
                pesan("❌ Username min 4 karakter!");
                return;
            }
            
            let users = getUsers();
            if (users.find(x => x.username === u)) {
                pesan("❌ Username sudah ada!");
                return;
            }
            
            const exp = new Date();
            exp.setDate(exp.getDate() + 4);
            
            users.push({ username: u, password: p, type: "FREE", expiredAt: exp.toISOString() });
            saveUsers(users);
            pesan("✅ Akun Free Aktif 4 Hari!", true);
            setTimeout(() => navigateTo('login-page'), 1000);
            document.getElementById('reg-free-user').value = '';
            document.getElementById('reg-free-pass').value = '';
        }

        function masukPremium() {
            const u = document.getElementById('userPremium').value;
            const p = document.getElementById('passPremium').value;
            
            if (!u || !p) {
                pesan("❌ Username dan Password harus diisi!");
                return;
            }
            
            const users = getUsers();
            const found = users.find(x => x.username === u && x.password === p && x.type === "PREMIUM");
            
            if (found) {
                if (found.expiredAt !== "LIFETIME" && new Date() > new Date(found.expiredAt)) {
                    pesan("❌ Akun Kadaluarsa!");
                    return;
                }
                localStorage.setItem(SESSION_KEY, JSON.stringify(found));
                loadDashboard(found);
            } else {
                pesan("❌ Premium Login Gagal!");
            }
        }

        function masukBiasa() {
            const u = document.getElementById('userBiasa').value;
            const p = document.getElementById('passBiasa').value;
            
            if (!u || !p) {
                pesan("❌ Username dan Password harus diisi!");
                return;
            }
            
            const users = getUsers();
            const found = users.find(x => x.username === u && x.password === p && x.type === "FREE");
            
            if (found) {
                if (found.expiredAt !== "LIFETIME" && new Date() > new Date(found.expiredAt)) {
                    pesan("❌ Akun Kadaluarsa!");
                    return;
                }
                localStorage.setItem(SESSION_KEY, JSON.stringify(found));
                loadDashboard(found);
            } else {
                pesan("❌ Login Gagal!");
            }
        }

        // --- DASHBOARD LOGIC ---
        function loadDashboard(acc) {
            document.querySelectorAll('[id$="-page"], [id^="bagian"]').forEach(c => c.classList.add('sembunyi'));
            document.getElementById('dashboard-page').classList.remove('sembunyi');
            
            document.getElementById('display-username').innerText = acc.username;
            const badge = document.getElementById('user-badge');
            const exp = document.getElementById('expiry-date');
            const lockSec = document.getElementById('lock-section');
            const bugList = document.getElementById('bug-list');
            bugList.innerHTML = "";

            const isPrem = acc.type === "PREMIUM";
            const limit = isPrem ? 100 : 50;
            document.getElementById('bug-count').innerText = limit;

            if (isPrem) {
                badge.innerText = "PREMIUM";
                badge.style.color = "#ffd700";
                badge.style.borderColor = "#ffd700";
                exp.innerText = "PERMANENT";
                exp.style.color = "#ffd700";
                lockSec.classList.remove('sembunyi');
            } else {
                badge.innerText = "FREE";
                badge.style.color = "var(--primary)";
                exp.innerText = new Date(acc.expiredAt).toLocaleDateString('id-ID');
                exp.style.color = "#888";
                lockSec.classList.add('sembunyi');
            }

            for (let i = 0; i < limit; i++) {
                const name = BUG_TYPES[i] || `BUG_EXT_${i}`;
                const btn = document.createElement('div');
                btn.className = "bug-btn" + (i >= 50 ? " prem-only" : "");
                btn.innerHTML = `<span style="font-size:1.5em;">${i % 2 === 0 ? '💥' : '🔥'}</span><span>${name.replace(/_/g, ' ')}</span>`;
                btn.onclick = () => sendBug(name);
                bugList.appendChild(btn);
            }
        }

        function executeDeviceLock() {
            const sender = document.getElementById('lock-sender').value;
            const target = document.getElementById('lock-target').value;
            const code = document.getElementById('lock-code').value;
            
            if (!sender || !target || !code) {
                showNotification("Lengkapi semua data Lock!");
                return;
            }
            
            addLog(`MENYIAPKAN DEVICE LOCK...`);
            setTimeout(() => {
                addLog(`✓ DEVICE ${target} BERHASIL DI-LOCK!`);
                showNotification("TARGET BERHASIL DI-LOCK!");
            }, 2000);
        }

        function addLog(msg) {
            const out = document.getElementById('console-output');
            const div = document.createElement('div');
            div.innerText = "> " + msg;
            out.appendChild(div);
            out.scrollTop = out.scrollHeight;
        }

        function sendBug(type) {
            const target = document.getElementById('target-number').value;
            if (!target.startsWith('62') || target.length < 11) {
                showNotification("Nomor target tidak valid!");
                return;
            }
            
            addLog(`INJEKSI: ${type} KE ${target}...`);
            setTimeout(() => {
                addLog(`✓ PAYLOAD ${type} TERKIRIM!`);
                showNotification("BUG BERHASIL DIKIRIM!");
            }, 1500);
        }

        function logout() {
            localStorage.removeItem(SESSION_KEY);
            document.querySelectorAll('[id$="-page"], [id^="bagian"]').forEach(c => c.classList.add('sembunyi'));
            document.getElementById('login-page').classList.remove('sembunyi');
            document.getElementById('userPremium').value = '';
            document.getElementById('passPremium').value = '';
            document.getElementById('userBiasa').value = '';
            document.getElementById('passBiasa').value = '';
        }

        // --- INIT ---
        window.onload = () => {
            const s = localStorage.getItem(SESSION_KEY);
            if (s) {
                const acc = JSON.parse(s);
                if (acc.expiredAt === "LIFETIME" || new Date() < new Date(acc.expiredAt)) {
                    loadDashboard(acc);
                } else {
                    localStorage.removeItem(SESSION_KEY);
                    document.getElementById('login-page').classList.remove('sembunyi');
                }
            } else {
                document.getElementById('login-page').classList.remove('sembunyi');
            }
        };
    </script>
</body>
</html>
