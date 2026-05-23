<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WhatsApp Bug Tool</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            margin: 0;
            padding: 0;
            color: #fff;
            min-height: 100vh;
        }
        .container {
            max-width: 1100px;
            margin: 20px auto;
            padding: 30px;
            background: rgba(0, 0, 0, 0.9);
            border-radius: 20px;
            box-shadow: 0 0 40px rgba(0, 255, 136, 0.3);
        }
        h1 { text-align: center; margin-bottom: 10px; }
        .premium-header {
            color: #ffd700;
            font-size: 2.5em;
            text-shadow: 0 0 20px #ffd700;
        }
        button {
            width: 100%;
            padding: 16px;
            margin: 6px 0;
            border: none;
            border-radius: 12px;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        /* Style Khusus untuk List Bug Premium */
        .bug-item {
            background: linear-gradient(145deg, #1e1e2f, #2a2a45);
            border: 1px solid #444;
            color: #ccc;
            text-align: left;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 15px;
            border-radius: 12px;
            cursor: pointer;
        }
        .bug-item:hover {
            border-color: #ffd700;
            background: linear-gradient(145deg, #2a2a45, #3a3a60);
        }
        /* Efek saat bug dipilih */
        .bug-item.selected {
            border: 2px solid #00ff88;
            background: rgba(0, 255, 136, 0.1);
            color: #fff;
            box-shadow: 0 0 10px rgba(0, 255, 136, 0.2);
        }
        .bug-checkbox {
            width: 20px;
            height: 20px;
            accent-color: #00ff88;
            cursor: pointer;
            pointer-events: none; /* Agar klik tembus ke div parent */
        }
        
        input {
            width: 100%;
            padding: 15px;
            margin: 15px 0;
            border-radius: 10px;
            border: 2px solid #ffd700;
            background: rgba(0,0,0,0.7);
            color: white;
            font-size: 16px;
            box-sizing: border-box;
        }
        .error { color: #ff4444; text-align: center; margin: 15px 0; }
        .result { margin: 15px 0; padding: 15px; border-radius: 10px; text-align: center; font-weight: bold; word-wrap: break-word; }
        .channel-btn { background: linear-gradient(#25D366, #128C7E); color: white; }
        
        /* Tombol Kirim Utama di Bawah */
        .send-main-btn {
            background: linear-gradient(90deg, #00ff88, #00cc6a);
            color: #000;
            font-size: 18px;
            margin-top: 20px;
            box-shadow: 0 0 15px rgba(0, 255, 136, 0.4);
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        .send-main-btn:hover {
            transform: scale(1.02);
            box-shadow: 0 0 25px rgba(0, 255, 136, 0.6);
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- LOGIN PAGE -->
        <div id="loginForm">
            <h1>WhatsApp Bug Tool</h1>
            <input type="text" id="username" placeholder="Username">
            <input type="password" id="password" placeholder="Password">
            <button onclick="login()" style="background: #00ff88; color: #000;">Login</button>
            <button onclick="openForm()" class="channel-btn">📢 CREATE AKUN ANDA SEKARANG 100% GRATIS</button>
            <div id="error" class="error"></div>
        </div>

        <!-- FREE PAGE -->
        <div id="freePage" style="display: none;">
            <h1>WhatsApp Bug Tool - Free</h1>
            <button onclick="sendBug()">📤 Send Bug</button>
            <button onclick="forclose()">🔒 Forclose</button>
            <button onclick="ultraLag()">⚡ Ultra Lag</button>
            <button onclick="superLag()">💥 Super Lag</button>
            <button onclick="freeze()">❄️ Freeze Account</button>
            <button onclick="crash()">💣 Crash WhatsApp</button>

            <div style="margin-top: 25px;">
                <label>Target Number (WA):</label>
                <input type="text" id="freeTarget" placeholder="+628xxxxxxxxxx">
            </div>
            <button onclick="logout()" style="background:#ff4444;">Logout</button>
            <div id="freeResult" class="result"></div>
        </div>

        <!-- PREMIUM PAGE (50 BUGS) -->
        <div id="premiumPage" style="display: none;">
            <h1 class="premium-header">🚀 BUG PREMIUM MODE</h1>
            <p style="text-align:center; color:#ffd700;" id="premiumStatus"></p>

            <div style="margin-bottom: 20px;">
                <label>Target Number (WA):</label>
                <input type="text" id="premiumTarget" placeholder="+628xxxxxxxxxx">
            </div>

            <p style="color: #aaa; font-size: 0.9em; margin-bottom: 10px;">✅ Centang bug yang ingin dikirim:</p>
            
            <!-- Grid Checkbox Bug -->
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 12px;" id="premiumGrid"></div>

            <!-- TOMBOL KIRIM DI PALING BAWAH -->
            <button onclick="sendSelectedBugs()" class="send-main-btn">🚀 SEND SELECTED BUGS</button>

            <button onclick="logout()" style="background:#ff4444; margin-top: 25px;">Logout</button>
            <div id="premiumResult" class="result"></div>
        </div>
    </div>

    <script>
        // DATABASE USER (Password PRIVATE2 sudah diubah menjadi PRIVATE2)
        const allowedUsers = [
            { username: "PRIVATE", password: "PRIVATE", premium: false },
            { username: "AZFER.ID", password: "AZFER.ID", premium: true, premiumExpiresAt: null },   // Unlimited
            { username: "PRIVATE2", password: "PRIVATE2", premium: true, premiumExpiresAt: "2026-05-25T03:00:00" }, 
            { username: "PRIVATE3", password: "PRIVATE3", premium: false }
        ];

        let currentUser = null;

        function login() {
            const usernameInput = document.getElementById('username');
            const passwordInput = document.getElementById('password');
            
            // Trim otomatis agar spasi tidak mengganggu login
            const username = usernameInput.value.trim();
            const password = passwordInput.value.trim();
            const errorEl = document.getElementById('error');

            errorEl.textContent = "";

            if (!username || !password) {
                errorEl.textContent = "Isi Username dan Password!";
                return;
            }

            const user = allowedUsers.find(u => u.username === username && u.password === password);

            if (!user) {
                errorEl.textContent = "Username atau Password Salah!";
                return;
            }

            // Cek kadaluarsa Premium
            if (user.premium && user.premiumExpiresAt) {
                if (new Date(user.premiumExpiresAt) < new Date()) {
                    errorEl.textContent = "Premium Kadaluarsa!";
                    return;
                }
            }

            currentUser = user;
            document.getElementById('loginForm').style.display = 'none';

            if (user.premium) {
                document.getElementById('premiumPage').style.display = 'block';
                generatePremiumBugs();
                updatePremiumStatus();
            } else {
                document.getElementById('freePage').style.display = 'block';
            }
        }

        function updatePremiumStatus() {
            const el = document.getElementById('premiumStatus');
            if (currentUser.premiumExpiresAt === null) {
                el.innerHTML = "✅ Premium Unlimited (Tak Terbatas)";
            } else {
                const date = new Date(currentUser.premiumExpiresAt);
                el.innerHTML = `⚠️ Premium aktif sampai: ${date.toLocaleString('id-ID')}`;
            }
        }

        function openForm() {
            window.open("https://forms.gle/8xJRC7XRgEaPFwpu5", "_blank");
        }

        function logout() {
            location.reload();
        }

        function checkTarget(id) {
            const target = document.getElementById(id).value.trim();
            if (!target) {
                alert("MOHON ISI NO WHATSAPP TARGET!");
                return false;
            }
            return true;
        }

        // ==================== FREE FUNCTIONS ====================
        function freeResult(text) {
            document.getElementById('freeResult').innerHTML = `✅ ${text}`;
        }
        function sendBug() { if(checkTarget('freeTarget')) freeResult("Send Bug Terkirim"); }
        function forclose() { if(checkTarget('freeTarget')) freeResult("Forclose Terkirim"); }
        function ultraLag() { if(checkTarget('freeTarget')) freeResult("Ultra Lag Terkirim"); }
        function superLag() { if(checkTarget('freeTarget')) freeResult("Super Lag Terkirim"); }
        function freeze() { if(checkTarget('freeTarget')) freeResult("Freeze Account Terkirim"); }
        function crash() { if(checkTarget('freeTarget')) freeResult("Crash WhatsApp Terkirim"); }

        // ==================== PREMIUM LOGIC ====================
        const premiumBugList = [
            "Super Ultimate Lag","Nuclear Crash","Permanent Ban","Account Destroyer",
            "Freeze Forever","Infinite Loop","Ghost Mode","Device Overheat","Mass Logout",
            "Chat Exploder","Media Bomber","Status Killer","Call Crash","Group Destroyer",
            "Number Blocker","Virus Injector","Premium Forclose","Ultra Freeze","System Killer",
            "Data Eraser","WhatsApp Killer","Blue Screen","Lag Machine","Account Hacker Pro",
            "Mass Report","Ban Wave","Session Hijack","OTP Bomber","Profile Destroyer",
            "Link Crash","Sticker Bomb","Voice Crash","Video Killer","Document Destroyer",
            "Location Bomber","Poll Crasher","Reaction Spam","Mention All Crash","Admin Remover",
            "Group Expander","Anti-Delete","Message Flooder","Hidden Ban","Silent Crash",
            "Deep Freeze","Quantum Lag","Black Hole","Ultimate Destroyer","God Mode Bug",
            "Premium Virus X"
        ];

        function generatePremiumBugs() {
            const grid = document.getElementById('premiumGrid');
            grid.innerHTML = '';
            premiumBugList.forEach((bug, index) => {
                const div = document.createElement('div');
                div.className = 'bug-item';
                
                const span = document.createElement('span');
                span.textContent = bug;
                
                const checkbox = document.createElement('input');
                checkbox.type = 'checkbox';
                checkbox.className = 'bug-checkbox';
                checkbox.value = bug;
                
                // Klik pada div akan mencentang checkbox
                div.addEventListener('click', () => {
                    checkbox.checked = !checkbox.checked;
                    toggleStyle(div, checkbox.checked);
                });

                div.appendChild(span);
                div.appendChild(checkbox);
                grid.appendChild(div);
            });
        }

        function toggleStyle(div, isChecked) {
            if (isChecked) {
                div.classList.add('selected');
            } else {
                div.classList.remove('selected');
            }
        }

        // FUNGSI KIRIM UTAMA (TOMBOL BAWAH)
        function sendSelectedBugs() {
            if (!checkTarget('premiumTarget')) return;

            const target = document.getElementById('premiumTarget').value.trim();
            const checkboxes = document.querySelectorAll('.bug-checkbox:checked');
            const resultEl = document.getElementById('premiumResult');

            if (checkboxes.length === 0) {
                alert("⚠️ PILIH MINIMAL 1 BUG DULU!");
                return;
            }

            let selectedBugs = [];
            checkboxes.forEach((cb) => {
                selectedBugs.push(cb.value);
            });

            // Tampilkan Hasil
            resultEl.innerHTML = `🚀 <b>SUCCESS!</b><br>Mengirim ${selectedBugs.length} Bug ke ${target}<br><br>`;
            
            let listHtml = "<div style='text-align:left; max-height:200px; overflow-y:auto; background:rgba(0,0,0,0.3); padding:10px; border-radius:10px;'>";
            selectedBugs.forEach(bug => {
                listHtml += `<div style='padding:5px; border-bottom:1px solid #333; color:#00ff88;'>✅ ${bug} Sent</div>`;
            });
            listHtml += "</div>";
            
            resultEl.innerHTML += listHtml;
        }
    </script>
</body>
</html>

