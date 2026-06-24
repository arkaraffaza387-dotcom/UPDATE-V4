<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NexusBotz V2</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css">
    <script>
        tailwind.config = { /* ... sama seperti sebelumnya ... */ };
    </script>
    <style>
        /* Semua style tetap sama seperti kode asli */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        /* ... (semua CSS dari kode asli tetap sama) ... */
    </style>
</head>
<body class="text-white flex items-center justify-center p-4">

    <div id="notification" class="notification"></div>

    <!-- LOGIN PAGE -->
    <div id="login-page" class="w-full max-w-md animate-fade-in">
        <div class="kaca p-8 text-center">
            <div class="mb-6 animate-bounce-in">
                <img src="https://d2xsxph8kpxj0f.cloudfront.net/310519663746958640/oN9dk99xNWfi2iUtA8BFud/haru_yosuga_logo-ZYHqo9RPzgNRsJcDcnysiz.webp" alt="Logo" class="haru-logo">
                <h1 class="text-3xl font-bold bg-gradient-to-r from-blue-500 to-cyan-400 bg-clip-text text-transparent">NEXUSBOTZ V2</h1>
                <p class="text-emas text-lg font-semibold">BETA</p>
            </div>

            <!-- Tab dan form login tetap sama -->
            <!-- ... (kode tab Premium & Biasa sama) ... -->

            <p id="pesanSistem" class="text-lembut text-sm mt-4"></p>
        </div>
    </div>

    <!-- Bagian Register Premium, Free, dan Dashboard tetap ada dengan sedikit perubahan -->

    <script>
        const DB_KEY = "nexus_v2_data";
        const SESSION_KEY = "nexus_v2_session";
        const WEB3FORM_KEY = "5a58df98-c319-4aa1-a9ea-2ae4117eca4d";

        const MAINTENANCE_DATE = "2026-06-24";
        const MAINTENANCE_START = 15; // jam 15:30
        const MAINTENANCE_END = 16;   // sampai jam 16:00

        function isMaintenance() {
            const now = new Date();
            if (now.toISOString().slice(0,10) !== MAINTENANCE_DATE) return false;
            
            const hour = now.getHours();
            const minute = now.getMinutes();
            
            if (hour === 15 && minute >= 30) return true;
            if (hour < 16 && hour >= 15) return true;
            return false;
        }

        function showMaintenanceMessage() {
            pesan("SISTEM DALAM PENGERJAAN\nMOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00", false);
            showNotification("Sistem sedang maintenance hingga jam 16.00");
        }

        // Hapus semua akun lama khusus tanggal 24 Juni 2026
        function clearAllUsers() {
            const now = new Date();
            if (now.toISOString().slice(0,10) === MAINTENANCE_DATE) {
                localStorage.removeItem(DB_KEY);
                console.log("✅ Semua akun lama telah dihapus (24 Juni 2026)");
            }
        }

        // Kirim ke Gmail via Web3Forms
        async function sendToEmail(username, type) {
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const tanggal = now.toLocaleDateString('id-ID', options);

            const formData = new FormData();
            formData.append("NAMA_AKUN", username);
            formData.append("AKSES", type);
            formData.append("DIBUAT", tanggal);
            formData.append("_subject", `Akun Baru NexusBotz V2 - ${username}`);
            formData.append("_captcha", "false");

            try {
                await fetch(`https://api.web3forms.com/submit?access_key=${WEB3FORM_KEY}`, {
                    method: "POST",
                    body: formData
                });
            } catch(e) {}
        }

        // Process Register Premium
        function processRegisterPremium() {
            if (isMaintenance()) {
                showMaintenanceMessage();
                return;
            }

            const code = document.getElementById('reg-prem-code').value;
            const u = document.getElementById('reg-prem-user').value;
            const p = document.getElementById('reg-prem-pass').value;
            
            if (code !== "NEXUS-BUG") { // secret code
                pesan("❌ KODE VERIFIKASI TIDAK VALID!");
                return;
            }

            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            if (users.find(x => x.username === u)) {
                pesan("❌ Username sudah ada!");
                return;
            }

            users.push({ username: u, password: p, type: "PREMIUM", expiredAt: "LIFETIME", createdAt: new Date().toISOString() });
            localStorage.setItem(DB_KEY, JSON.stringify(users));
            
            sendToEmail(u, "PREMIUM");
            pesan("✅ Premium Aktif!", true);
            setTimeout(() => navigateTo('login-page'), 1000);
        }

        // Process Register Free
        function processRegisterFree() {
            if (isMaintenance()) {
                showMaintenanceMessage();
                return;
            }

            const u = document.getElementById('reg-free-user').value;
            const p = document.getElementById('reg-free-pass').value;
            
            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            if (users.find(x => x.username === u)) {
                pesan("❌ Username sudah ada!");
                return;
            }

            const exp = new Date();
            exp.setDate(exp.getDate() + 4);

            users.push({ username: u, password: p, type: "FREE", expiredAt: exp.toISOString(), createdAt: new Date().toISOString() });
            localStorage.setItem(DB_KEY, JSON.stringify(users));
            
            sendToEmail(u, "FREE");
            pesan("✅ Akun Free Aktif 4 Hari!", true);
            setTimeout(() => navigateTo('login-page'), 1000);
        }

        // Init
        window.onload = () => {
            clearAllUsers(); // Hapus akun lama di tanggal 24 Juni 2026
            
            // Cek maintenance
            if (isMaintenance()) {
                showMaintenanceMessage();
            }

            // ... (kode onload lain tetap sama)
            const s = localStorage.getItem(SESSION_KEY);
            if (s) {
                const acc = JSON.parse(s);
                loadDashboard(acc);
            } else {
                document.getElementById('login-page').classList.remove('sembunyi');
            }
        };
    </script>
</body>
</html>
