<style>
    /* Texnik bo'lim uchun maxsus stillar */
    .specs-container {
        display: grid;
        grid-template-columns: repeat(3, 1fr); /* 3 ta ustun */
        gap: 40px 20px;
        padding: 40px 0;
        border-top: 1px solid #15323d;
        margin-top: 50px;
    }

    .spec-item {
        display: flex;
        align-items: flex-start;
        gap: 15px;
    }

    /* Dumaloq ko'k ikonkalar */
    .spec-icon {
        width: 32px;
        height: 32px;
        border: 1px solid #1b85d3;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #1b85d3;
        font-size: 14px;
        flex-shrink: 0;
    }

    .spec-info b {
        display: block;
        color: #ffffff;
        font-size: 15px;
        margin-bottom: 4px;
        font-weight: 500;
    }

    .spec-info span, .spec-info a {
        color: #7e949c;
        font-size: 14px;
        text-decoration: none;
    }

    .spec-info a:hover { text-decoration: underline; }

    .section-title {
        font-size: 18px;
        font-weight: 700;
        margin-bottom: 25px;
        margin-top: 40px;
    }
</style>

<div class="wrapper">
    <h2 class="section-title">Technical information</h2>
    
    <div class="specs-container">
        <div class="spec-item">
            <div class="spec-icon">👤</div>
            <div class="spec-info">
                <b>Developer</b>
                <a href="#">KONAMI</a>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">📄</div>
            <div class="spec-info">
                <b>License</b>
                <span>Free</span>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">⚽</div>
            <div class="spec-info">
                <b>Category</b>
                <a href="#">Sports</a>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-item">
                <div class="spec-icon">📱</div>
                <div class="spec-info">
                    <b>Operating System</b>
                    <span>Android</span>
                </div>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">⚙️</div>
            <div class="spec-info">
                <b>Architecture</b>
                <span>arm64-v8a</span>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">🌐</div>
            <div class="spec-info">
                <b>Language</b>
                <span>English <small>(44 more)</small></span>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">📥</div>
            <div class="spec-info">
                <b>Downloads</b>
                <span>74,839,915</span>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">📅</div>
            <div class="spec-info">
                <b>Date</b>
                <span>Apr 10, 2026</span>
            </div>
        </div>

        <div class="spec-item">
            <div class="spec-icon">📦</div>
            <div class="spec-info">
                <b>Package Name</b>
                <span>jp.konami.pesam</span>
            </div>
        </div>
    </div>
</div>
