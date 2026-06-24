<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NexusBotz V2</title>
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
                    animation: {
                        'float': 'float 3s ease-in-out infinite',
                        'glow-pulse': 'glowPulse 2s ease-in-out infinite',
                        'fade-scale': 'fadeScale 0.5s ease-out forwards',
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        * { font-family: 'Inter', sans-serif; }
        
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
        }
        .tombol-utama:hover {
            filter: brightness(1.15);
            box-shadow: 0 0 25px rgba(22,93,255,0.6);
            transform: translateY(-3px);
        }

        .tab-content {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            opacity: 0;
            transform: translateY(20px);
        }
        .tab-content.active {
            opacity: 1;
            transform: translateY(0);
            animation: fadeScale 0.5s ease-out;
        }

        @keyframes fadeScale {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }
        @keyframes glowPulse {
            0%, 100% { box-shadow: 0 0 15px rgba(22,93,255,0.4); }
            50% { box-shadow: 0 0 30px rgba(22,93,255,0.7); }
        }
        .tab-active {
            position: relative;
            color: white;
        }
        .tab-active::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, #165DFF, #00f5ff);
        }

        .notification {
            position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
            background: #111; border: 2px solid #00ff88; padding: 15px 25px;
            z-index: 10000; border-radius: 20px; box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            display: none; text-align: center; width: 85%;
        }
        .hidden { display: none !important; }
    </style>
</head>
<body class="text-white flex items-center justify-center p-4">

    <div id="notification" class="notification"></div>

    <!-- LOGIN PAGE -->
    <div id="login-page" class="w-full max-w-md">
        <div class="kaca p-8 text-center">
            <div class="mb-6">
                <img src="https://d2xsxph8kpxj0f.cloudfront.net/310519663746958640/oN9dk99xNWfi2iUtA8BFud/haru_yosuga_logo-ZYHqo9RPzgNRsJcDcnysiz.webp" 
                     alt="Logo" class="mx-auto w-28 h-28" style="animation: float 3s ease-in-out infinite;">
                <h1 class="text-4xl font-bold bg-gradient-to-r from-blue-400 to-cyan-300 bg-clip-text text-transparent">NEXUSBOTZ V2</h1>
                <p class="text-emas text-xl font-semibold mt-1">INJECTOR OFFICIAL BUG | PREMIUM | FREE</p>
            </div>

            <!-- Tab Buttons -->
            <div class="flex rounded-2xl overflow-hidden border border-batas mb-8 bg-[#0a0a0f]">
                <button id="tabPremium" onclick="switchTab(0)" 
                        class="flex-1 py-4 text-lg font-semibold tab-active transition-all">💎 PREMIUM</button>
                <button id="tabBiasa" onclick="switchTab(1)" 
                        class="flex-1 py-4 text-lg font-semibold transition-all">👤 FREE</button>
            </div>

            <!-- Premium Content -->
            <div id="contentPremium" class="tab-content active">
                <div class="mb-5">
                    <label class="block text-sm mb-2 text-gray-300">Nama Pengguna</label>
                    <input type="text" id="userPremium" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="Masukkan username">
                </div>
                <div class="mb-6">
                    <label class="block text-sm mb-2 text-gray-300">Kata Sandi</label>
                    <input type="password" id="passPremium" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="••••••••">
                </div>
                <button onclick="masukPremium()" class="w-full py-4 tombol-utama text-lg font-semibold">MASUK PREMIUM</button>
                <button onclick="navigateTo('register-premium-page')" class="w-full py-4 mt-3 bg-[#0F1424] border border-[#232940] hover:border-blue-500 rounded-2xl transition-all">Daftar Premium</button>
            </div>

            <!-- Free Content -->
            <div id="contentBiasa" class="tab-content hidden">
                <div class="mb-5">
                    <label class="block text-sm mb-2 text-gray-300">Nama Pengguna</label>
                    <input type="text" id="userBiasa" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="Masukkan username">
                </div>
                <div class="mb-6">
                    <label class="block text-sm mb-2 text-gray-300">Kata Sandi</label>
                    <input type="password" id="passBiasa" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="••••••••">
                </div>
                <button onclick="masukBiasa()" class="w-full py-4 tombol-utama text-lg font-semibold">MASUK FREE</button>
                <button onclick="navigateTo('reg-step-tiktok')" class="w-full py-4 mt-3 bg-[#0F1424] border border-[#232940] hover:border-blue-500 rounded-2xl transition-all">Daftar Akun Free</button>
            </div>

            <p id="pesanSistem" class="text-sm mt-6 min-h-[1.5rem] text-red-400"></p>
        </div>
    </div>

    <!-- REGISTER PREMIUM -->
    <div id="register-premium-page" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold text-emas mb-6">DAFTAR PREMIUM</h2>
            <input type="password" id="reg-prem-code" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-3" placeholder="Kode Verifikasi">
            <input type="text" id="reg-prem-user" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-3" placeholder="Username Baru">
            <input type="password" id="reg-prem-pass" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-6" placeholder="Password Baru">
            <button onclick="processRegisterPremium()" class="w-full py-3 tombol-utama">Aktivasi Premium</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-[#0F1424] border border-[#232940] rounded-xl">Kembali</button>
        </div>
    </div>

    <!-- REG STEP TIKTOK -->
    <div id="reg-step-tiktok" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold mb-6">Verifikasi TikTok</h2>
            <button onclick="openTikTok()" class="w-full py-3 tombol-utama">Follow TikTok</button>
            <button id="tiktok-next" onclick="navigateTo('reg-step-wa')" class="w-full py-3 mt-2 hidden bg-[#0F1424] border border-[#232940] rounded-xl">Lanjutkan</button>
        </div>
    </div>

    <!-- REG STEP WA -->
    <div id="reg-step-wa" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold mb-6">Verifikasi WA</h2>
            <button onclick="openWAChannel()" class="w-full py-3 tombol-utama">Gabung Saluran</button>
            <button id="wa-next" onclick="navigateTo('register-free-page')" class="w-full py-3 mt-2 hidden bg-[#0F1424] border border-[#232940] rounded-xl">Lanjutkan</button>
        </div>
    </div>

    <!-- REGISTER FREE -->
    <div id="register-free-page" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold mb-6">Daftar Akun Free</h2>
            <input type="text" id="reg-free-user" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-3" placeholder="Username">
            <input type="password" id="reg-free-pass" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-6" placeholder="Password">
            <button onclick="processRegisterFree()" class="w-full py-3 tombol-utama">Buat Akun Free</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-[#0F1424] border border-[#232940] rounded-xl">Kembali</button>
        </div>
    </div>

    <!-- DASHBOARD -->
    <div id="dashboard-page" class="w-full max-w-md hidden bg-[#111111] p-6 rounded-3xl min-h-screen">
        <h2 class="text-center text-2xl font-bold text-green-400 mb-6">NEXUSBOTZ V2</h2>
        <div class="text-center mb-6">
            <span id="user-badge" class="px-6 py-2 rounded-full text-sm font-bold"></span>
        </div>
        <p class="mb-2 text-center">Username: <b id="display-username"></b></p>
        <p class="text-center">Expired: <b id="expiry-date"></b></p>

        <div class="mt-10">
            <input type="tel" id="target-number" class="w-full p-4 bg-[#1a1a1a] border border-gray-700 rounded-2xl text-center" placeholder="628xxxxxxxxxx">
        </div>

        <button onclick="logout()" class="w-full mt-10 py-4 bg-red-600 rounded-2xl font-semibold">LOGOUT</button>
    </div>

    <script>
        const DB_KEY = "nexus_v2_data";
        const SESSION_KEY = "nexus_v2_session";
        const WEB3FORM_KEY = "5a58df98-c319-4aa1-a9ea-2ae4117eca4d";

        function showNotification(msg) {
            const n = document.getElementById('notification');
            n.innerText = msg;
            n.style.display = 'block';
            setTimeout(() => n.style.display = 'none', 4000);
        }

        function pesan(teks) {
            document.getElementById('pesanSistem').innerHTML = teks;
        }

        function navigateTo(id) {
            document.querySelectorAll('div[id$="-page"], div[id^="content"]').forEach(el => el.classList.add('hidden'));
            const target = document.getElementById(id);
            if (target) target.classList.remove('hidden');
        }

        function switchTab(n) {
            const premiumBtn = document.getElementById('tabPremium');
            const biasaBtn = document.getElementById('tabBiasa');
            const contentPremium = document.getElementById('contentPremium');
            const contentBiasa = document.getElementById('contentBiasa');

            if (n === 0) {
                premiumBtn.classList.add('tab-active');
                biasaBtn.classList.remove('tab-active');
                contentPremium.classList.remove('hidden');
                contentBiasa.classList.add('hidden');
                setTimeout(() => contentPremium.classList.add('active'), 10);
            } else {
                biasaBtn.classList.add('tab-active');
                premiumBtn.classList.remove('tab-active');
                contentBiasa.classList.remove('hidden');
                contentPremium.classList.add('hidden');
                setTimeout(() => contentBiasa.classList.add('active'), 10);
            }
        }

        function isMaintenance() {
            const now = new Date();
            if (now.getFullYear() !== 2026 || now.getMonth() !== 5 || now.getDate() !== 24) return false;
            const hour = now.getHours();
            return (hour === 15);
        }

        function clearAllUsers() {
            const now = new Date();
            if (now.getFullYear() === 2026 && now.getMonth() === 5 && now.getDate() === 24) {
                localStorage.removeItem(DB_KEY);
            }
        }

        async function sendToEmail(username, type) {
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const tanggal = now.toLocaleDateString('id-ID', options);

            const formData = new FormData();
            formData.append("NAMA_AKUN", username);
            formData.append("AKSES", type);
            formData.append("DIBUAT", tanggal);
            formData.append("_subject", `NexusBotz V2 - Akun Baru: ${username}`);

            try {
                await fetch(`https://api.web3forms.com/submit?access_key=${WEB3FORM_KEY}`, {
                    method: "POST",
                    body: formData
                });
            } catch(e) {}
        }

        function processRegisterPremium() {
            if (isMaintenance()) {
                pesan("SISTEM DALAM PENGERJAAN<br>MOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00");
                showNotification("Maintenance hingga jam 16.00");
                return;
            }
            const code = document.getElementById('reg-prem-code').value;
            const u = document.getElementById('reg-prem-user').value.trim();
            const p = document.getElementById('reg-prem-pass').value;

            if (code !== "NEXUS-BUG" || u.length < 4) {
                pesan("Kode atau Username tidak valid!");
                return;
            }

            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            if (users.find(x => x.username === u)) {
                pesan("Username sudah digunakan!");
                return;
            }

            users.push({ username: u, password: p, type: "PREMIUM", expiredAt: "LIFETIME" });
            localStorage.setItem(DB_KEY, JSON.stringify(users));
            sendToEmail(u, "PREMIUM");
            pesan("✅ Premium Berhasil Dibuat!");
            setTimeout(() => navigateTo('login-page'), 1200);
        }

        function processRegisterFree() {
            if (isMaintenance()) {
                pesan("SISTEM DALAM PENGERJAAN<br>MOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00");
                showNotification("Maintenance hingga jam 16.00");
                return;
            }
            const u = document.getElementById('reg-free-user').value.trim();
            const p = document.getElementById('reg-free-pass').value;

            if (u.length < 4) {
                pesan("Username minimal 4 karakter!");
                return;
            }

            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            if (users.find(x => x.username === u)) {
                pesan("Username sudah digunakan!");
                return;
            }

            const exp = new Date();
            exp.setDate(exp.getDate() + 4);

            users.push({ username: u, password: p, type: "FREE", expiredAt: exp.toISOString() });
            localStorage.setItem(DB_KEY, JSON.stringify(users));
            sendToEmail(u, "FREE");
            pesan("✅ Akun Free Berhasil Dibuat (4 Hari)!");
            setTimeout(() => navigateTo('login-page'), 1200);
        }

        function masukPremium() {
            const u = document.getElementById('userPremium').value.trim();
            const p = document.getElementById('passPremium').value;
            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            const found = users.find(x => x.username === u && x.password === p && x.type === "PREMIUM");
            if (found) {
                localStorage.setItem(SESSION_KEY, JSON.stringify(found));
                loadDashboard(found);
            } else {
                pesan("Login Premium Gagal!");
            }
        }

        function masukBiasa() {
            const u = document.getElementById('userBiasa').value.trim();
            const p = document.getElementById('passBiasa').value;
            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            const found = users.find(x => x.username === u && x.password === p && x.type === "FREE");
            if (found) {
                localStorage.setItem(SESSION_KEY, JSON.stringify(found));
                loadDashboard(found);
            } else {
                pesan("Login Gagal!");
            }
        }

        function loadDashboard(acc) {
            document.getElementById('login-page').classList.add('hidden');
            document.getElementById('dashboard-page').classList.remove('hidden');
            document.getElementById('display-username').textContent = acc.username;
            const badge = document.getElementById('user-badge');
            badge.textContent = acc.type;
            badge.style.backgroundColor = acc.type === "PREMIUM" ? "#ffd700" : "#22c55e";
            badge.style.color = "#000";
        }

        function logout() {
            localStorage.removeItem(SESSION_KEY);
            location.reload();
        }

        function openTikTok() {
            window.open('https://www.tiktok.com/@kiboyaslinofake', '_blank');
            setTimeout(() => document.getElementById('tiktok-next').classList.remove('hidden'), 800);
        }

        function openWAChannel() {
            window.open('https://whatsapp.com/channel/0029VbDBArY9MF8uLpmviF1S', '_blank');
            setTimeout(() => document.getElementById('wa-next').classList.remove('hidden'), 800);
        }

        window.onload = () => {
            clearAllUsers();
            switchTab(0);

            if (isMaintenance()) {
                pesan("SISTEM DALAM PENGERJAAN<br>MOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00");
                showNotification("Maintenance hingga jam 16.00");
            }

            const session = localStorage.getItem(SESSION_KEY);
            if (session) {
                loadDashboard(JSON.parse(session));
            } else {
                document.getElementById('login-page').classList.remove('hidden');
            }
        };
    </script>
</body>
</html>
