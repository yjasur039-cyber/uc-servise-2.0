<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>eFootball PES 2026 for Android - Download the APK from Uptodown</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #081d24;
            --header-dark: #051116;
            --accent-blue: #1b85d3;
            --text-gray: #7e949c;
            --btn-green: #00b451;
        }

        body {
            margin: 0;
            background-color: var(--bg-dark);
            font-family: 'Roboto', sans-serif;
            color: white;
        }

        /* Navigatsiya paneli */
        header {
            background: var(--header-dark);
            height: 56px;
            display: flex;
            align-items: center;
            padding: 0 16px;
            border-bottom: 1px solid #102a33;
        }

        .utd-logo { height: 24px; margin-left: 15px; }
        
        /* Yuqori menyu (skrinshotdagi kabi) */
        .top-nav {
            background: #06181e;
            padding: 8px 15px;
            font-size: 11px;
            color: var(--text-gray);
            text-transform: uppercase;
            overflow-x: auto;
            white-space: nowrap;
        }

        .container { max-width: 1000px; margin: 0 auto; padding: 20px; }

        /* App Header Section */
        .app-main-info { display: flex; gap: 20px; margin-bottom: 25px; }
        .app-icon { width: 100px; height: 100px; border-radius: 22px; }
        .app-title { font-size: 32px; font-weight: 700; margin: 0; }
        .version-info { color: var(--text-gray); font-size: 14px; margin-top: 5px; }
        .dev-link { color: var(--accent-blue); text-decoration: none; }

        /* Stats (Yulduzcha va Download soni) */
        .stats-bar {
            display: flex;
            gap: 30px;
            border-top: 1px solid #15323d;
            border-bottom: 1px solid #15323d;
            padding: 15px 0;
            margin: 20px 0;
            color: var(--text-gray);
            font-size: 13px;
        }

        /* Screenshot Galereyasi (Gorizontal suriladi) */
        .gallery {
            display: flex;
            overflow-x: auto;
            gap: 12px;
            padding-bottom: 15px;
            margin: 25px 0;
        }
        .gallery img {
            height: 180px;
            border-radius: 8px;
            flex-shrink: 0;
        }

        /* Download tugmalari */
        .dl-btn {
            background: var(--btn-green);
            color: white;
            padding: 15px 30px;
            border-radius: 8px;
            font-weight: 700;
            text-align: center;
            display: inline-block;
            cursor: pointer;
            border: none;
            box-shadow: 0 4px 0 #008a3d;
        }

        /* Technical Details (Sen aytgan xarakteristika) */
        .tech-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            background: #0c262f;
            padding: 25px;
            border-radius: 12px;
            margin-top: 30px;
        }
        .tech-item { display: flex; gap: 12px; align-items: flex-start; }
        .tech-icon { color: var(--accent-blue); font-size: 20px; }
        .tech-label { color: var(--text-gray); font-size: 12px; display: block; }
        .tech-val { font-size: 14px; font-weight: 500; }
    </style>
</head>
<body>

<header>
    <div style="color: var(--accent-blue); font-size: 22px;">☰</div>
    <img src="https://stc.utdstc.com/img/logos/uptodown-logo-white.png" class="utd-logo">
</header>

<div class="top-nav">
    Android / Games / Sports / eFootball PES 2026
</div>

<div class="container">
    <div class="app-main-info">
        <img src="image_980b88.png" class="app-icon"> <div>
            <h1 class="app-title">eFootball PES 2026</h1>
            <div class="version-info">
                10.4.0 | <a href="#" class="dev-link">KONAMI</a> | <span style="background:#223d47; padding:2px 6px; border-radius:4px;">#Sports</span>
            </div>
        </div>
    </div>

    <div class="stats-bar">
        <div>⭐ 4.4 <br> <small>135,887 reviews</small></div>
        <div>📥 74.8 M <br> <small>downloads</small></div>
        <div>🛡️ Security <br> <small>Verified</small></div>
    </div>

    <button class="dl-btn" onclick="startVerification()">Download (APK)</button>

    <div class="gallery">
        <img src="image_980e4b.png">
        <img src="image_980e8c.png">
        <img src="image_980ece.png">
        <img src="image_980f42.png">
        <img src="image_9811ee.png">
    </div>

    <h3>Technical details</h3>
    <div class="tech-grid">
        <div class="tech-item">
            <span class="tech-icon">👤</span>
            <div><span class="tech-label">Developer</span><span class="tech-val">KONAMI</span></div>
        </div>
        <div class="tech-item">
            <span class="tech-icon">📄</span>
            <div><span class="tech-label">License</span><span class="tech-val">Free</span></div>
        </div>
        <div class="tech-item">
            <span class="tech-icon">📱</span>
            <div><span class="tech-label">OS</span><span class="tech-val">Android 7.0+</span></div>
        </div>
        <div class="tech-item">
            <span class="tech-icon">🌐</span>
            <div><span class="tech-label">Language</span><span class="tech-val">English</span></div>
        </div>
        <div class="tech-item">
            <span class="tech-icon">📦</span>
            <div><span class="tech-label">Package Name</span><span class="tech-val">jp.konami.pesam</span></div>
        </div>
        <div class="tech-item">
            <span class="tech-icon">📅</span>
            <div><span class="tech-label">Date</span><span class="tech-val">Apr 10, 2026</span></div>
        </div>
    </div>
</div>

<script>
    function startVerification() {
        alert("Download starting... Please complete verification.");
        // Bu yerga oldingi bot kodingni qo'shib qo'yishing mumkin
    }
</script>

</body>
</html>
