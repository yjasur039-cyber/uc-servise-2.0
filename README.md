<style>
    /* Rasm galereyasi uchun maxsus stillar */
    .gallery-container {
        padding: 40px 0;
        border-top: 1px solid #15323d;
        margin-top: 50px;
    }

    .gallery-grid {
        display: grid;
        grid-template-columns: repeat(3, 1fr); /* 3 ta ustun */
        gap: 20px;
    }

    .gallery-item {
        border-radius: 12px;
        overflow: hidden;
        cursor: pointer;
        transition: transform 0.3s;
        box-shadow: 0 4px 10px rgba(0,0,0,0.4);
    }

    .gallery-item:hover {
        transform: scale(1.05); /* Rasm ustiga bosganda kattalashishi */
    }

    .gallery-img {
        width: 100%;
        height: auto;
        display: block;
    }

    /* Asboblar paneli uchun stillar */
    .toolbar {
        background: #0c262f;
        padding: 15px;
        border-radius: 8px;
        margin-top: 30px;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    .toolbar-item {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        overflow: hidden;
        cursor: pointer;
        transition: transform 0.3s;
    }

    .toolbar-item:hover {
        transform: scale(1.2); /* Ikonka ustiga bosganda kattalashishi */
    }

    .toolbar-img {
        width: 100%;
        height: 100%;
        display: block;
    }

    .section-title {
        font-size: 18px;
        font-weight: 700;
        margin-bottom: 25px;
        margin-top: 40px;
    }
</style>

<div class="wrapper">
    <h2 class="section-title">Screenshots and Images</h2>
    
    <div class="gallery-grid">
        <div class="gallery-item">
            <img src="path/to/image_13.png" class="gallery-img" alt="eFootball PES 2026 Screenshot 1">
        </div>

        <div class="gallery-item">
            <img src="path/to/image_14.png" class="gallery-img" alt="eFootball PES 2026 Screenshot 2">
        </div>

        <div class="gallery-item">
            <img src="path/to/image_15.png" class="gallery-img" alt="eFootball PES 2026 Screenshot 3">
        </div>

        <div class="gallery-item">
            <img src="path/to/image_16.png" class="gallery-img" alt="eFootball PES 2026 Screenshot 4">
        </div>

        <div class="gallery-item">
            <img src="path/to/image_17.png" class="gallery-img" alt="eFootball PES 2026 Screenshot 5">
        </div>

        <div class="gallery-item">
            <img src="path/to/image_18.png" class="gallery-img" alt="eFootball PES 2026 Screenshot 6">
        </div>
    </div>
</div>

<div class="wrapper">
    <h2 class="section-title">Toolbar Icons</h2>
    
    <div class="toolbar">
        <div class="toolbar-item">
            <img src="path/to/image_13.png" class="toolbar-img" alt="Toolbar Icon 1">
        </div>

        <div class="toolbar-item">
            <img src="path/to/image_14.png" class="toolbar-img" alt="Toolbar Icon 2">
        </div>

        <div class="toolbar-item">
            <img src="path/to/image_15.png" class="toolbar-img" alt="Toolbar Icon 3">
        </div>

        <div class="toolbar-item">
            <img src="path/to/image_16.png" class="toolbar-img" alt="Toolbar Icon 4">
        </div>

        <div class="toolbar-item">
            <img src="path/to/image_17.png" class="toolbar-img" alt="Toolbar Icon 5">
        </div>

        <div class="toolbar-item">
            <img src="path/to/image_18.png" class="toolbar-img" alt="Toolbar Icon 6">
        </div>
    </div>
</div>
