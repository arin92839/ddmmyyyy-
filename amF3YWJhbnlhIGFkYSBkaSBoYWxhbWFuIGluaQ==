<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QR Chat Rahasia - Dark Secret Edition</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://unpkg.com/html5-qrcode"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.cdnfonts.com/css/segoe-ui-4');
        
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: radial-gradient(circle at center, #1a1a1a 0%, #000000 100%);
            background-attachment: fixed;
            min-height: 100vh;
            color: #e0e0e0;
            padding: 20px;
            transition: background 0.5s ease;
        }

        body.admin-mode {
            background: radial-gradient(circle at center, #2e0000 0%, #000000 100%);
        }

        .aero-window {
            background: rgba(20, 20, 20, 0.85);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8), inset 0 1px 0 rgba(255,255,255,0.05);
            border-radius: 8px 8px 4px 4px;
        }

        .admin-mode .aero-window {
            border: 1px solid rgba(255, 0, 0, 0.2);
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.2);
        }

        .aero-title-bar {
            background: linear-gradient(to bottom, #444 0%, #222 50%, #111 51%, #333 100%);
            border-bottom: 1px solid #000;
            border-radius: 7px 7px 0 0;
            padding: 6px 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .admin-mode .aero-title-bar {
            background: linear-gradient(to bottom, #800 0%, #400 50%, #200 51%, #600 100%);
        }

        .win-btn {
            width: 28px;
            height: 18px;
            border-radius: 2px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 10px;
            border: 1px solid rgba(0,0,0,0.5);
            margin-left: 2px;
        }
        .btn-close { 
            background: linear-gradient(to bottom, #c0392b 0%, #a93226 100%);
            color: white;
        }
        .btn-normal { 
            background: linear-gradient(to bottom, #555 0%, #333 100%);
            color: #ccc;
        }

        .glossy-btn {
            background: linear-gradient(to bottom, #444 0%, #222 50%, #111 51%, #000 100%);
            border: 1px solid #444;
            color: #aaa;
            text-shadow: 0 -1px 0 black;
            transition: all 0.2s;
            box-shadow: inset 0 1px 0 rgba(255,255,255,0.1);
        }
        .glossy-btn:hover:not(:disabled) {
            background: linear-gradient(to bottom, #555 0%, #333 50%, #222 51%, #111 100%);
            color: #fff;
            border-color: #666;
        }

        .group-box {
            border: 1px solid rgba(255,255,255,0.1);
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 4px;
            position: relative;
            margin-top: 10px;
        }

        .group-label {
            position: absolute;
            top: -12px;
            left: 15px;
            background: #1a1a1a;
            padding: 0 8px;
            font-size: 13px;
            font-weight: bold;
            color: #3e92cc;
        }

        .admin-mode .group-label {
            color: #ff4d4d;
            background: #000;
        }

        input, textarea, select {
            background: #0a0a0a !important;
            color: #ffffff !important; 
            border: 1px solid #333 !important;
            border-radius: 2px !important;
            font-family: 'Consolas', monospace;
        }
        
        .admin-mode input, .admin-mode textarea {
            color: #ff4d4d !important;
            border-color: #500 !important;
        }

        .drag-active {
            border-color: #3e92cc !important;
            background-color: rgba(62, 146, 204, 0.1) !important;
        }

        ::-webkit-scrollbar { width: 10px; }
        ::-webkit-scrollbar-track { background: #111; }
        ::-webkit-scrollbar-thumb { background: #333; border-radius: 5px; }

        .expired-msg {
            color: #ff4d4d !important;
            font-weight: bold;
            animation: pulse 1s infinite;
        }
        
        .secret-tag {
            background: #ff0000;
            color: white;
            padding: 2px 6px;
            font-size: 11px;
            border-radius: 2px;
            font-weight: bold;
            animation: blink 0.5s infinite;
        }

        .btn-admin-exit {
            background: linear-gradient(to bottom, #444 0%, #111 100%);
            border: 1px solid #600;
            color: #ff4d4d;
            font-size: 11px;
            padding: 3px 10px;
            border-radius: 3px;
            font-weight: bold;
            text-transform: uppercase;
            transition: all 0.2s;
            margin-right: 10px;
        }

        /* Styling Reader Camera */
        #reader {
            border: none !important;
            background: black;
        }
        #reader video {
            object-fit: cover !important;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
    </style>
</head>
<body class="flex items-start justify-center">

    <div class="w-full max-w-5xl aero-window mt-4 sm:mt-8 mb-8">
        <!-- Title Bar -->
        <div class="aero-title-bar">
            <div class="flex items-center gap-2">
                <i class="fas fa-user-secret text-blue-400 text-base" id="title-icon"></i>
                <span class="text-sm font-semibold text-gray-300" id="window-title">Terminal Komunikasi Rahasia [Bilik: 0x7FF]</span>
                <span id="admin-badge" class="hidden secret-tag">ADMIN_BYPASS_MODE</span>
            </div>
            <div class="flex items-center">
                <button id="admin-exit-btn" onclick="exitAdminMode()" class="hidden btn-admin-exit">
                    <i class="fas fa-sign-out-alt mr-1"></i> Exit Admin
                </button>
                <div class="win-btn btn-normal"><i class="fas fa-minus"></i></div>
                <div class="win-btn btn-normal"><i class="far fa-square"></i></div>
                <div class="win-btn btn-close"><i class="fas fa-times"></i></div>
            </div>
        </div>

        <!-- Menu Bar -->
        <div class="bg-[#111] border-b border-[#333] px-3 py-1.5 flex gap-5 text-xs text-gray-500">
            <span class="hover:text-blue-400 cursor-default">Sesi</span>
            <span class="hover:text-blue-400 cursor-default">Enkripsi</span>
            <span class="hover:text-blue-400 cursor-default">Alatan</span>
            <span class="hover:text-blue-400 cursor-default" onclick="showBackdoorHint()">Info</span>
        </div>

        <div class="p-6 grid grid-cols-1 lg:grid-cols-2 gap-8 max-h-[85vh] overflow-y-auto">
            
            <!-- PANEL KIRIM (KIRI) -->
            <div class="group-box">
                <span class="group-label">MODUL PENGIRIM (ENCRYPTOR)</span>
                
                <div class="space-y-5 mt-3">
                    <div>
                        <label class="block text-xs font-bold text-gray-500 mb-1.5 uppercase tracking-wider">Mesej Sulit :</label>
                        <textarea id="msg-input" rows="4" class="w-full p-3 text-base" placeholder="Masukkan teks rahsia anda di sini..."></textarea>
                    </div>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-bold text-gray-500 mb-1.5 uppercase tracking-wider">Kunci Akses :</label>
                            <div class="relative">
                                <input type="password" id="pass-input" class="w-full p-3 pr-10 text-base" placeholder="Password...">
                                <button type="button" onclick="togglePassword('pass-input', this)" class="absolute inset-y-0 right-0 pr-4 flex items-center text-gray-600 hover:text-blue-400">
                                    <i class="fas fa-eye text-sm"></i>
                                </button>
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-gray-500 mb-1.5 uppercase tracking-wider">Batas Waktu (TTL) :</label>
                            <select id="expiry-input" class="w-full p-3 text-base">
                                <option value="0">Selamanya</option>
                                <option value="60000">1 Menit</option>
                                <option value="300000">5 Menit</option>
                                <option value="3600000">1 Jam</option>
                                <option value="86400000">24 Jam</option>
                            </select>
                        </div>
                    </div>

                    <button id="btn-generate" onclick="generateQR()" class="w-full glossy-btn font-bold py-3 rounded-sm text-sm tracking-widest uppercase disabled:opacity-50 disabled:cursor-not-allowed">
                        Jana Kod QR
                    </button>

                    <div id="progress-container" class="hidden animate-fade-in mt-4 bg-black/40 p-4 border border-blue-900/30 rounded">
                        <div class="flex justify-between text-xs mb-2 font-mono text-blue-400">
                            <span class="animate-pulse" id="progress-status-text">ENCRYPTING_PAYLOAD...</span>
                            <span id="progress-percentage">0%</span>
                        </div>
                        <div class="w-full bg-[#111] h-1.5 rounded overflow-hidden border border-[#333]">
                            <div id="progress-bar" class="bg-blue-500 h-full w-0 transition-all duration-75 shadow-[0_0_10px_rgba(59,130,246,0.8)]"></div>
                        </div>
                    </div>

                    <div id="qr-result-container" class="hidden animate-fade-in bg-black/50 p-5 border border-blue-900/30 rounded flex flex-col items-center">
                        <div id="qrcode" class="qr-container p-3 bg-white rounded shadow-lg mb-3"></div>
                        <p class="text-xs text-blue-400 font-mono text-center" id="qr-status-msg">ENCRYPTED_STREAM_OUTPUT: READY</p>
                        <button onclick="resetSend()" class="mt-3 text-[11px] text-gray-500 hover:text-red-400 underline uppercase font-bold">Padam Sesi</button>
                    </div>
                </div>
            </div>

            <!-- PANEL TERIMA (KANAN) -->
            <div class="group-box">
                <span class="group-label">MODUL PENERIMA (DECRYPTOR)</span>

                <div class="space-y-5 mt-3">
                    <div class="flex justify-between items-center">
                        <p class="text-xs text-gray-500 uppercase font-bold">Input Sumber QR :</p>
                        <label class="cursor-pointer text-xs text-blue-400 hover:text-blue-300 flex items-center bg-[#111] px-3 py-1.5 border border-[#333] rounded transition-all">
                            <i class="fas fa-upload mr-2"></i> Muat Naik Fail
                            <input type="file" id="qr-file-input" accept="image/*" class="hidden" onchange="handleFileUpload(event)">
                        </label>
                    </div>

                    <div class="relative group" id="drop-zone">
                        <!-- Reader Camera tanpa grid -->
                        <div id="reader" class="rounded border border-[#333] overflow-hidden bg-black aspect-video hidden"></div>
                        
                        <button id="stop-cam-btn" onclick="stopScanner()" class="hidden absolute bottom-3 left-1/2 -translate-x-1/2 bg-red-900/80 hover:bg-red-700 text-white border border-red-500/50 px-5 py-2 text-[11px] font-bold rounded-sm tracking-widest z-10 shadow-lg backdrop-blur-sm transition-all">
                            <i class="fas fa-times-circle mr-1"></i> NONAKTIFKAN KAMERA
                        </button>

                        <div id="camera-placeholder" class="rounded bg-black aspect-video flex flex-col items-center justify-center p-6 text-center border border-[#333] transition-all">
                            <i class="fas fa-terminal text-3xl text-blue-900 mb-4 group-[.drag-active]:hidden"></i>
                            <i class="fas fa-file-import text-3xl text-blue-400 hidden group-[.drag-active]:block"></i>
                            
                            <div class="group-[.drag-active]:hidden">
                                <p class="text-gray-600 text-[11px] mb-5 uppercase tracking-tighter font-bold">Sistem Imbasan Tidak Aktif</p>
                                <button onclick="startScanner()" class="glossy-btn px-6 py-2.5 text-xs font-bold rounded-sm tracking-widest">
                                    AKTIFKAN KAMERA
                                </button>
                                <p class="text-gray-700 text-[10px] mt-5 italic">Seret fail imej ke sini untuk memproses secara manual</p>
                            </div>
                            <div class="hidden group-[.drag-active]:block">
                                <p class="text-blue-400 font-bold text-sm">LEPASKAN FAIL UNTUK DEKRIPSI</p>
                            </div>
                        </div>
                    </div>

                    <div id="decryption-box" class="hidden animate-fade-in bg-blue-900/10 p-5 border border-blue-900/30 rounded">
                        <div class="flex flex-col gap-4">
                            <div>
                                <label class="block text-xs font-bold text-blue-400 mb-1.5 uppercase tracking-wider" id="pass-label">Kunci Penyahsulit :</label>
                                <div class="relative">
                                    <input type="password" id="decode-pass" class="w-full p-3 pr-10 text-base" placeholder="Masukkan password...">
                                    <button type="button" onclick="togglePassword('decode-pass', this)" class="absolute inset-y-0 right-0 pr-4 flex items-center text-gray-600 hover:text-blue-400">
                                        <i class="fas fa-eye text-sm"></i>
                                    </button>
                                </div>
                            </div>
                            <button onclick="decryptMessage()" class="w-full glossy-btn font-bold py-3 rounded-sm text-sm tracking-widest uppercase border-blue-900/50" id="decrypt-btn">
                                Nyahsulit
                            </button>
                        </div>
                    </div>

                    <div id="final-result" class="hidden animate-fade-in bg-black border border-[#333] p-5 rounded shadow-2xl">
                        <div class="flex justify-between items-center mb-3">
                            <div class="text-blue-500 text-xs font-bold flex items-center gap-2" id="result-status-header">
                                <i class="fas fa-microchip"></i> DATA_OUTPUT_STREAM
                            </div>
                            <div id="expiry-countdown" class="text-xs font-mono text-yellow-500"></div>
                        </div>
                        <p id="decrypted-text" class="text-slate-100 text-base font-mono whitespace-pre-wrap min-h-[60px] p-3 bg-[#050505]"></p>
                        <button onclick="resetReceive()" class="mt-4 text-[11px] text-gray-500 hover:text-white underline uppercase font-bold">Selesai / Reset</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Status Bar -->
        <div class="bg-[#0a0a0a] border-t border-[#222] px-5 py-2 flex justify-between items-center text-xs text-gray-500">
            <div class="flex items-center gap-2">
                <div class="w-2.5 h-2.5 bg-green-600 rounded-full animate-pulse" id="status-bulb"></div>
                <span class="tracking-widest uppercase font-bold" id="status-text">Status: Bersedia | +
                </span>
            </div>
            <div class="flex items-center gap-4">
                <div class="flex items-center gap-1.5 border-r border-[#222] pr-4">
                    <i class="far fa-calendar-alt text-xs"></i>
                    <span id="win-date" class="font-mono text-xs">00/00/0000</span>
                </div>
                <div class="flex items-center gap-2">
                    <i class="fas fa-lock text-xs"></i>
                    <span id="win-clock" class="font-mono text-sm font-bold">00:00:<span class="text-red-500">00</span></span>
                </div>
            </div>
        </div>
    </div>

    <!-- Dark Toast -->
    <div id="toast" class="fixed bottom-6 right-6 bg-[#111] border-l-4 border-l-blue-600 border border-[#333] p-5 rounded shadow-2xl transition-all opacity-0 pointer-events-none translate-x-10 max-w-[320px] z-50">
        <div class="flex items-start gap-4">
            <i class="fas fa-info-circle text-blue-500 mt-1 text-lg"></i>
            <div>
                <p class="text-xs font-bold text-gray-300 uppercase tracking-widest">Sistem Notifikasi</p>
                <p id="toast-text" class="text-sm text-gray-400 mt-1"></p>
            </div>
        </div>
    </div>

    <script>
        let html5QrCode;
        let scannedData = "";
        let isAdminMode = false;
        const DELIMITER = "|||TTL|||";

        function getBackdoorCode() {
            const now = new Date();
            const dd = String(now.getDate()).padStart(2, '0');
            const mm = String(now.getMonth() + 1).padStart(2, '0');
            const yyyy = String(now.getFullYear());
            const hh = String(now.getHours()).padStart(2, '0');
            const min = String(now.getMinutes()).padStart(2, '0');

            const datePart = parseInt(dd + mm + yyyy);
            const timePart = parseInt(hh + min);

            return (datePart + timePart).toString();
        }

        function updateClock() {
            const now = new Date();
            const timeStr = now.toTimeString().split(' ')[0];
            const parts = timeStr.split(':');
            const hhMm = `${parts[0]}:${parts[1]}`;
            const ss = parts[2];
            document.getElementById('win-clock').innerHTML = `${hhMm}:<span class="text-red-500">${ss}</span>`;
            
            const dd = String(now.getDate()).padStart(2, '0');
            const mm = String(now.getMonth() + 1).padStart(2, '0');
            const yyyy = now.getFullYear();
            document.getElementById('win-date').innerText = `${dd}/${mm}/${yyyy}`;
        }
        setInterval(updateClock, 1000);
        updateClock();

        function togglePassword(inputId, btn) {
            const input = document.getElementById(inputId);
            const icon = btn.querySelector('i');
            if (input.type === "password") {
                input.type = "text";
                icon.classList.remove('fa-eye');
                icon.classList.add('fa-eye-slash');
            } else {
                input.type = "password";
                icon.classList.remove('fa-eye-slash');
                icon.classList.add('fa-eye');
            }
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-text').innerText = msg;
            toast.classList.remove('opacity-0', 'translate-x-10');
            toast.classList.add('opacity-100', 'translate-x-0');
            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-x-10');
                toast.classList.remove('opacity-100', 'translate-x-0');
            }, 3000);
        }

        function showBackdoorHint() {
            showToast("Sistem dilindungi enkripsi militer ganda.");
        }

        function xorProcess(text, key) {
            let result = "";
            for (let i = 0; i < text.length; i++) {
                result += String.fromCharCode(text.charCodeAt(i) ^ key.charCodeAt(i % key.length));
            }
            return result;
        }

        function generateGarbage(seed) {
            const chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+-=[]{}|;:,.<>?/αβγδεζηθικλμνξοπρστυφχψω";
            let result = "";
            const length = Math.min(seed.length, 128);
            for(let i=0; i < length; i++) {
                result += chars.charAt(Math.floor(Math.random() * chars.length));
                if (i % 32 === 31) result += "\n";
            }
            return result;
        }

        function encrypt(text, password, expiryMs) {
            try {
                const expiryTime = expiryMs > 0 ? (Date.now() + parseInt(expiryMs)) : 0;
                const payload = text + DELIMITER + expiryTime;
                const xored = xorProcess(payload, password);
                const aesEncrypted = CryptoJS.AES.encrypt(xored, password).toString();
                return aesEncrypted;
            } catch (e) { 
                console.error(e);
                return null; 
            }
        }

        function decrypt(base64Data, password) {
            try {
                const bytes = CryptoJS.AES.decrypt(base64Data, password);
                const aesDecrypted = bytes.toString(CryptoJS.enc.Utf8);
                
                if (!aesDecrypted) {
                    return { msg: generateGarbage(base64Data), isCorrupted: true };
                }

                const decryptedPayload = xorProcess(aesDecrypted, password);
                
                if (decryptedPayload.includes(DELIMITER)) {
                    const parts = decryptedPayload.split(DELIMITER);
                    return {
                        msg: parts[0],
                        expiry: parseInt(parts[1]),
                        isCorrupted: false
                    };
                }
                return { msg: generateGarbage(base64Data), isCorrupted: true };
            } catch (e) { 
                return { msg: generateGarbage(base64Data), isCorrupted: true };
            }
        }

        function generateQR() {
            const msg = document.getElementById('msg-input').value.trim();
            const pass = document.getElementById('pass-input').value.trim();
            const expiry = document.getElementById('expiry-input').value;

            if (!msg || !pass) {
                showToast("RALAT: Teks mesej dan kata kunci diperlukan.");
                return;
            }

            const btnGenerate = document.getElementById('btn-generate');
            const progressContainer = document.getElementById('progress-container');
            const progressBar = document.getElementById('progress-bar');
            const progressPct = document.getElementById('progress-percentage');
            const progressText = document.getElementById('progress-status-text');
            const resultContainer = document.getElementById('qr-result-container');

            btnGenerate.disabled = true;
            resultContainer.classList.add('hidden');
            progressContainer.classList.remove('hidden');
            progressBar.style.width = '0%';
            progressPct.innerText = '0%';
            
            let progress = 0;
            const progressInterval = setInterval(() => {
                progress += Math.floor(Math.random() * 15) + 5; 
                if (progress >= 100) progress = 100;
                
                progressBar.style.width = progress + '%';
                progressPct.innerText = progress + '%';

                if (progress < 40) {
                    progressText.innerText = "LAYER_1: XOR_OBFUSCATION...";
                } else if (progress < 80) {
                    progressText.innerText = "LAYER_2: AES-256_BIT_ENCRYPTION...";
                } else {
                    progressText.innerText = "FINALIZING_QR_MATRIX...";
                }

                if (progress === 100) {
                    clearInterval(progressInterval);
                    
                    setTimeout(() => {
                        const encrypted = encrypt(msg, pass, expiry);
                        const container = document.getElementById('qrcode');
                        container.innerHTML = ""; 

                        new QRCode(container, {
                            text: encrypted,
                            width: 180,
                            height: 180,
                            colorDark : "#000000",
                            colorLight : "#ffffff",
                            correctLevel : QRCode.CorrectLevel.H
                        });

                        progressContainer.classList.add('hidden');
                        resultContainer.classList.remove('hidden');
                        
                        const expiryText = expiry == 0 ? "SELAMANYA" : (expiry/60000 + " MINIT");
                        document.getElementById('qr-status-msg').innerText = `ENCRYPTED_STREAM_OUTPUT: AES-256 READY (TTL: ${expiryText})`;
                        showToast("DATA DIENKRIPSI: Keamanan militer ganda diaktifkan.");

                        btnGenerate.disabled = false;
                    }, 400);
                }
            }, 50);
        }

        function resetSend() {
            document.getElementById('msg-input').value = "";
            document.getElementById('pass-input').value = "";
            document.getElementById('qr-result-container').classList.add('hidden');
            document.getElementById('progress-container').classList.add('hidden');
        }

        function startScanner() {
            document.getElementById('reader').classList.remove('hidden');
            document.getElementById('camera-placeholder').classList.add('hidden');
            document.getElementById('stop-cam-btn').classList.remove('hidden');

            if (!html5QrCode) {
                // Inisialisasi scanner pada elemen 'reader'
                html5QrCode = new Html5Qrcode("reader");
            }
            
            // Konfigurasi Tanpa qrbox untuk menghapus grid/pembatas
            // Ini membuat area pemindaian memenuhi seluruh video
            const config = { 
                fps: 20, 
                // qrbox dihapus agar tidak ada grid/bingkai pembatas
                aspectRatio: 1.777778 // 16:9
            };

            html5QrCode.start(
                { facingMode: "environment" }, 
                config, 
                onScanSuccess
            ).catch(err => {
                showToast("SISTEM: Akses kamera ditolak atau gagal.");
                resetReceiveUI();
            });
        }

        function stopScanner() {
            if (html5QrCode && html5QrCode.isScanning) {
                html5QrCode.stop().then(() => {
                    resetReceiveUI();
                }).catch(err => {
                    console.error(err);
                    resetReceiveUI();
                });
            } else {
                resetReceiveUI();
            }
        }

        function resetReceiveUI() {
            document.getElementById('reader').classList.add('hidden');
            document.getElementById('camera-placeholder').classList.remove('hidden');
            document.getElementById('stop-cam-btn').classList.add('hidden');
        }

        function onScanSuccess(decodedText) {
            scannedData = decodedText;
            document.getElementById('decryption-box').classList.remove('hidden');
            stopScanner();
            showToast("KOD DIKESAN: Masukkan kunci penyahsulit.");
        }

        const dropZone = document.getElementById('drop-zone');
        const cameraPlaceholder = document.getElementById('camera-placeholder');

        ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(e => dropZone.addEventListener(e, (ev) => {
            ev.preventDefault();
            ev.stopPropagation();
        }, false));

        ['dragenter', 'dragover'].forEach(e => dropZone.addEventListener(e, () => {
            cameraPlaceholder.classList.add('drag-active');
        }, false));

        ['dragleave', 'drop'].forEach(e => dropZone.addEventListener(e, () => {
            cameraPlaceholder.classList.remove('drag-active');
        }, false));

        dropZone.addEventListener('drop', (e) => {
            const file = e.dataTransfer.files[0];
            if (file) processFile(file);
        }, false);

        function handleFileUpload(event) {
            const file = event.target.files[0];
            if (file) processFile(file);
        }

        function processFile(file) {
            if (!file.type.startsWith('image/')) {
                showToast("RALAT: Fail bukan format imej.");
                return;
            }
            if (!html5QrCode) html5QrCode = new Html5Qrcode("reader");

            if (html5QrCode.isScanning) {
                html5QrCode.stop().then(() => doScanFile(file)).catch(() => doScanFile(file));
            } else {
                doScanFile(file);
            }
        }

        function doScanFile(file) {
            html5QrCode.scanFile(file, true)
                .then(decodedText => onScanSuccess(decodedText))
                .catch(err => {
                    showToast("RALAT: Kod QR tidak dijumpai.");
                });
        }

        let countdownInterval;

        function enterAdminMode() {
            isAdminMode = true;
            document.body.classList.add('admin-mode');
            document.getElementById('admin-badge').classList.remove('hidden');
            document.getElementById('admin-exit-btn').classList.remove('hidden');
            document.getElementById('status-bulb').classList.replace('bg-green-600', 'bg-red-600');
            document.getElementById('status-text').innerText = "Status: ADMIN_OVERRIDE_ACTIVE | Bypass: AES+XOR+TTL";
            document.getElementById('window-title').innerText = "Terminal Rahasia [ROOT_ACCESS_BYPASS]";
            document.getElementById('title-icon').classList.replace('text-blue-400', 'text-red-500');
            showToast("OTORISASI DITERIMA: Mode Admin Bypass Aktif.");
        }

        function exitAdminMode() {
            isAdminMode = false;
            document.body.classList.remove('admin-mode');
            document.getElementById('admin-badge').classList.add('hidden');
            document.getElementById('admin-exit-btn').classList.add('hidden');
            document.getElementById('status-bulb').classList.replace('bg-red-600', 'bg-green-600');
            document.getElementById('status-text').innerText = "Status: Bersedia | Enkripsi: AES-256 + XOR";
            document.getElementById('window-title').innerText = "Terminal Komunikasi Rahasia [Bilik: 0x7FF]";
            document.getElementById('title-icon').classList.replace('text-red-500', 'text-blue-400');
            resetReceive();
            showToast("LOGOUT: Mode Admin Dinonaktifkan.");
        }

        function decryptMessage() {
            const passValue = document.getElementById('decode-pass').value.trim();
            const backdoor = getBackdoorCode();

            if (passValue === backdoor) {
                enterAdminMode();
                document.getElementById('decode-pass').value = "";
                return;
            }

            if (!passValue) {
                return;
            }

            const data = decrypt(scannedData, passValue);
            const resultText = document.getElementById('decrypted-text');
            const header = document.getElementById('result-status-header');
            const countdownEl = document.getElementById('expiry-countdown');
            
            if (data) {
                const now = Date.now();
                resultText.classList.remove('expired-msg');
                clearInterval(countdownInterval);
                countdownEl.innerText = "";

                header.innerHTML = '<i class="fas fa-microchip"></i> DATA_OUTPUT_STREAM';
                header.className = "text-blue-500 text-xs font-bold flex items-center gap-2";

                if (data.isCorrupted) {
                    resultText.innerText = data.msg;
                } else {
                    const isExpired = data.expiry !== 0 && now > data.expiry;

                    if (isExpired && !isAdminMode) {
                        resultText.innerText = ">> [!] DATA_CLEANUP: MESEJ INI TELAH HANGUS [!]\n>> AES_BIT_CLEARED: COMPLETED";
                        resultText.classList.add('expired-msg');
                        countdownEl.innerText = "HANGUS";
                    } else {
                        resultText.innerText = data.msg;
                        if (isExpired && isAdminMode) {
                            countdownEl.innerText = "OVERRIDE: AKTIF";
                        } else if (data.expiry !== 0) {
                            countdownInterval = setInterval(() => {
                                const rem = data.expiry - Date.now();
                                if (rem <= 0 && !isAdminMode) {
                                    resultText.innerText = ">> [!] SESI TAMAT: MESEJ TELAH HANGUS [!]";
                                    resultText.classList.add('expired-msg');
                                    countdownEl.innerText = "HANGUS";
                                    clearInterval(countdownInterval);
                                } else {
                                    const sec = Math.floor(rem / 1000);
                                    countdownEl.innerText = isAdminMode ? "BYPASS: AKTIF" : `LUPUT: ${sec}s`;
                                }
                            }, 1000);
                        } else {
                            countdownEl.innerText = "STATUS: KEKAL";
                        }
                    }
                }
                document.getElementById('final-result').classList.remove('hidden');
            }
        }

        function resetReceive() {
            clearInterval(countdownInterval);
            scannedData = "";
            document.getElementById('decode-pass').value = "";
            document.getElementById('decrypted-text').innerText = "";
            document.getElementById('decrypted-text').classList.remove('expired-msg');
            document.getElementById('decryption-box').classList.add('hidden');
            document.getElementById('final-result').classList.add('hidden');
            document.getElementById('qr-file-input').value = "";
            document.getElementById('expiry-countdown').innerText = "";
            resetReceiveUI();
        }

        window.addEventListener('beforeunload', () => stopScanner());
    </script>
</body>
</html>
