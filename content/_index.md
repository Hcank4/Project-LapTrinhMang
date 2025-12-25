---
title: "Home"
---

<div class="hero-section">
    <div class="hero-text">
        <h1 class="name-heading">HỒNG CẦN //</h1>
        <p class="slogan">WORK HARD IN SILENCE,<br>LET SUCCESS MAKE NOISE.</p>
        <div class="hero-buttons">
            <a href="/posts" class="btn-primary">XEM ĐỒ ÁN</a>
            <a href="/about" class="btn-secondary">HỒ SƠ CÁ NHÂN</a>
        </div>
    </div>
    <div class="hero-image">
        <img src="images/profile.jpg" alt="Hong Can Profile">
    </div>
</div>

<style>
.hero-section {
    display: flex;
    align-items: center;
    justify-content: space-between;
    min-height: 70vh;
    gap: 20px;
}
.hero-text { flex: 1; }
.name-heading { 
    font-size: 2rem; 
    letter-spacing: 5px; 
    color: var(--secondary);
}
.slogan {
    font-size: 3.5rem;
    font-weight: 800;
    line-height: 1.1;
    margin: 20px 0;
    text-transform: uppercase;
}
.hero-image { flex: 1; text-align: right; }
.hero-image img {
    max-width: 100%;
    height: auto;
    border-radius: 4px; /* Hoặc 0px nếu muốn vuông vức giống mẫu */
    box-shadow: 20px 20px 0px var(--tertiary); /* Hiệu ứng đổ bóng khối chuyên nghiệp */
}
.btn-primary, .btn-secondary {
    display: inline-block;
    padding: 12px 24px;
    margin-right: 10px;
    text-decoration: none;
    font-weight: bold;
    border: 2px solid var(--primary);
}
.btn-primary { background: var(--primary); color: white; }
.btn-secondary { color: var(--primary); }

@media (max-width: 768px) {
    .hero-section { flex-direction: column-reverse; text-align: center; }
    .hero-image { text-align: center; }
    .slogan { font-size: 2rem; }
}
</style>