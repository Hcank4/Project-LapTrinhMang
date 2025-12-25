---
title: "Home"
---

<div class="hero-section">
    <div class="hero-text">
        <h1 class="name-heading">HỒNG CẦN </h1>
        <p class="slogan">CẦN CÙ BÙ THÔNG MINH </p>
        
        <div class="hero-buttons">
            <a href="posts" class="btn-primary">XEM CÁC BÀI VIẾT</a>
            <a href="https://github.com/hcank4" class="btn-secondary" target="_blank">GITHUB CÁ NHÂN</a>
        </div>

        <div class="social-icons">
            <a href="https://github.com/hcank4" target="_blank" title="GitHub">📁</a>
            <a href="https://www.facebook.com/hongcan.pham.5070" target="_blank" title="Facebook">🔵</a>
            <a href="mailto:canpham522@gmail.com" title="Email">✉️</a>
        </div>
    </div>

    <div class="hero-image">
        <img src="images/profile.jpg" alt="Hong Can Profile">
    </div>
</div>

<style>
/* QUAN TRỌNG: ẨN TOÀN BỘ DANH SÁCH BÀI VIẾT Ở TRANG CHỦ */
.post-entry, .collection-header, .pagination, .main > footer { 
    display: none !important; 
}

.hero-section {
    display: flex;
    align-items: center;
    justify-content: space-between;
    min-height: 65vh;
    gap: 30px;
    padding: 50px 0;
}
.hero-text { flex: 1.2; }
.name-heading { 
    font-size: 1.8rem; 
    letter-spacing: 5px; 
    color: #888;
}
.slogan {
    font-size: 3.2rem;
    font-weight: 900;
    line-height: 1.1;
    margin: 20px 0;
    color: var(--content);
}

/* NÚT BẤM */
.hero-buttons { margin-bottom: 30px; }
.btn-primary, .btn-secondary {
    display: inline-block;
    padding: 12px 28px;
    margin-right: 15px;
    text-decoration: none !important;
    font-weight: bold;
    border: 2px solid var(--primary);
    transition: 0.3s;
}
.btn-primary { background: var(--primary); color: #fff !important; }
.btn-secondary { color: var(--primary) !important; }
.btn-primary:hover { opacity: 0.8; }
.btn-secondary:hover { background: var(--secondary); }

/* ICON MẠNG XÃ HỘI */
.social-icons { display: flex; gap: 20px; font-size: 1.5rem; }
.social-icons a { text-decoration: none !important; transition: 0.3s; }
.social-icons a:hover { transform: translateY(-5px); }

/* ẢNH CÁ NHÂN */
.hero-image { flex: 0.8; text-align: right; }
.hero-image img {
    max-width: 100%;
    height: auto;
    border-radius: 4px;
    box-shadow: 20px 20px 0px var(--primary); /* Đổ bóng khối theo màu theme */
}

/* MOBILE */
@media (max-width: 768px) {
    .hero-section { flex-direction: column-reverse; text-align: center; }
    .hero-image { text-align: center; }
    .slogan { font-size: 2.2rem; }
    .social-icons { justify-content: center; }
}
</style>