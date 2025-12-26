---
title: "Home"
---

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">

<div class="hero-section">
<div class="hero-text">
<h1 class="name-heading">PHẠM HỒNG CẨN </h1>
<p class="slogan">CẦN CÙ BÙ <br> THÔNG MINH</p>

<div class="hero-buttons">
<a href="posts" class="btn-primary">XEM CÁC BÀI VIẾT</a>
<a href="https://github.com/hcank4" class="btn-secondary" target="_blank">GITHUB CÁ NHÂN</a>
</div>

<div class="social-icons">
<a href="https://github.com/hcank4" target="_blank" title="GitHub"><i class="fab fa-github"></i></a>
<a href="https://www.facebook.com/hongcan.pham.5070" target="_blank" title="Facebook"><i class="fab fa-facebook"></i></a>
<a href="mailto:canpham522@gmail.com" title="Email"><i class="fas fa-envelope"></i></a>
</div>
</div>

<div class="hero-image">
<img src="images/profile.jpg" alt="Pham Hong Can Profile">
</div>
</div>

<style>
/* LỆNH ẨN TOÀN BỘ BÀI VIẾT Ở TRANG CHỦ */
.post-entry, .collection-header, .pagination, .main > footer { 
display: none !important; 
}

.hero-section {
display: flex;
align-items: center;
justify-content: space-between;
min-height: 60vh;
gap: 40px;
padding: 40px 0;
}
.hero-text { flex: 1.2; }
.name-heading { 
font-size: 1.8rem; 
letter-spacing: 5px; 
color: #888;
font-weight: 700;
}
.slogan {
font-size: 3rem;
font-weight: 900;
line-height: 1.1;
margin: 20px 0;
color: var(--content);
text-transform: uppercase;
}
.hero-buttons { margin-bottom: 25px; }
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

.social-icons { display: flex; gap: 25px; font-size: 1.8rem; margin-top: 20px; }
.social-icons a { color: var(--primary) !important; text-decoration: none !important; }

.hero-image { flex: 0.8; text-align: right; }
.hero-image img {
max-width: 100%;
height: auto;
border-radius: 4px;
box-shadow: 20px 20px 0px var(--primary);
}

@media (max-width: 768px) {
.hero-section { flex-direction: column-reverse; text-align: center; }
.hero-image { text-align: center; }
.slogan { font-size: 2.2rem; }
.social-icons { justify-content: center; }
}
</style>