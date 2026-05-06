<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>PermutCI – Plateforme de Permutation des Personnels</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Sora:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
/* ===== DESIGN TOKENS ===== */
:root {
  --emerald:   #00A878;
  --emerald-d: #007D5A;
  --emerald-l: #E6F7F2;
  --gold:      #F4A600;
  --gold-l:    #FEF7E6;
  --ink:       #0D1B2A;
  --ink-60:    #5A6A78;
  --ink-30:    #B8C4CC;
  --surface:   #F7F9FB;
  --white:     #FFFFFF;
  --danger:    #E53E3E;
  --r8:        8px;
  --r16:       16px;
  --r24:       24px;
  --shadow-sm: 0 2px 8px rgba(0,0,0,.08);
  --shadow-md: 0 6px 24px rgba(0,0,0,.12);
  --shadow-lg: 0 12px 40px rgba(0,0,0,.16);
}

/* ===== RESET ===== */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
  font-family:'Plus Jakarta Sans',sans-serif;
  background:var(--surface);
  color:var(--ink);
  min-height:100vh;
  overflow-x:hidden;
}
img{max-width:100%}
button{cursor:pointer;border:none;background:none;font-family:inherit}
input,select,textarea{font-family:inherit}
a{text-decoration:none;color:inherit}

/* ===== UTILITY ===== */
.hidden{display:none!important}
.flex{display:flex}
.items-center{align-items:center}
.justify-between{justify-content:space-between}
.gap-2{gap:8px}
.gap-3{gap:12px}
.gap-4{gap:16px}
.text-sm{font-size:.85rem}
.text-xs{font-size:.75rem}
.fw-600{font-weight:600}
.fw-700{font-weight:700}
.mt-1{margin-top:4px}
.mt-2{margin-top:8px}
.mt-3{margin-top:12px}
.mt-4{margin-top:16px}

/* ===== SPLASH / LOADING ===== */
#splash{
  position:fixed;inset:0;
  background:linear-gradient(145deg,#00A878 0%,#007D5A 60%,#005940 100%);
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  z-index:9999;
  transition:opacity .5s, transform .5s;
}
#splash.fade-out{opacity:0;pointer-events:none}
.splash-logo{
  width:80px;height:80px;
  background:rgba(255,255,255,.15);
  border-radius:20px;
  display:flex;align-items:center;justify-content:center;
  font-size:2rem;
  margin-bottom:20px;
  box-shadow:0 0 0 8px rgba(255,255,255,.08);
}
.splash-title{
  font-family:'Sora',sans-serif;
  font-size:1.8rem;font-weight:700;color:#fff;
  letter-spacing:-0.5px;
}
.splash-sub{color:rgba(255,255,255,.7);font-size:.9rem;margin-top:8px}
.splash-dots{display:flex;gap:8px;margin-top:32px}
.splash-dot{
  width:8px;height:8px;border-radius:50%;
  background:rgba(255,255,255,.4);
  animation:dotPulse 1.2s ease-in-out infinite;
}
.splash-dot:nth-child(2){animation-delay:.2s}
.splash-dot:nth-child(3){animation-delay:.4s}
@keyframes dotPulse{
  0%,100%{transform:scale(1);opacity:.4}
  50%{transform:scale(1.4);opacity:1}
}

/* ===== HEADER ===== */
#app-header{
  position:sticky;top:0;z-index:100;
  background:var(--white);
  border-bottom:1.5px solid rgba(0,0,0,.06);
  box-shadow:var(--shadow-sm);
}
.header-inner{
  max-width:480px;margin:0 auto;
  padding:12px 16px;
  display:flex;align-items:center;justify-content:space-between;
}
.header-brand{
  display:flex;align-items:center;gap:10px;
}
.brand-icon{
  width:38px;height:38px;border-radius:10px;
  background:linear-gradient(135deg,var(--emerald),var(--emerald-d));
  display:flex;align-items:center;justify-content:center;
  font-size:1.1rem;color:#fff;
  flex-shrink:0;
}
.brand-text{font-family:'Sora',sans-serif;font-size:1.1rem;font-weight:700;color:var(--ink)}
.brand-text span{color:var(--emerald)}
.header-btn{
  background:var(--emerald-l);color:var(--emerald-d);
  border-radius:var(--r8);padding:7px 14px;
  font-size:.8rem;font-weight:600;
  transition:background .2s;
}
.header-btn:hover{background:#C8EDE4}

/* ===== BOTTOM NAV ===== */
#bottom-nav{
  position:fixed;bottom:0;left:0;right:0;
  background:var(--white);
  border-top:1.5px solid rgba(0,0,0,.06);
  box-shadow:0 -4px 20px rgba(0,0,0,.08);
  z-index:100;
  padding-bottom:env(safe-area-inset-bottom);
}
.nav-inner{
  max-width:480px;margin:0 auto;
  display:grid;grid-template-columns:repeat(4,1fr);
}
.nav-item{
  display:flex;flex-direction:column;align-items:center;
  padding:10px 4px;gap:4px;
  color:var(--ink-30);
  font-size:.68rem;font-weight:600;
  transition:color .2s;
  cursor:pointer;
}
.nav-item.active{color:var(--emerald)}
.nav-icon{font-size:1.3rem;line-height:1}

/* ===== PAGES ===== */
.page{
  display:none;
  max-width:480px;margin:0 auto;
  padding:16px 16px 90px;
  animation:pageIn .3s ease;
}
.page.active{display:block}
@keyframes pageIn{
  from{opacity:0;transform:translateY(10px)}
  to{opacity:1;transform:translateY(0)}
}

/* ===== HERO ===== */
.hero{
  background:linear-gradient(135deg,var(--emerald) 0%,var(--emerald-d) 100%);
  border-radius:var(--r24);
  padding:28px 24px;
  color:#fff;
  position:relative;overflow:hidden;
  margin-bottom:20px;
}
.hero::before{
  content:'';position:absolute;
  top:-40px;right:-40px;
  width:160px;height:160px;
  background:rgba(255,255,255,.08);
  border-radius:50%;
}
.hero::after{
  content:'';position:absolute;
  bottom:-60px;left:20px;
  width:120px;height:120px;
  background:rgba(255,255,255,.05);
  border-radius:50%;
}
.hero-badge{
  display:inline-flex;align-items:center;gap:6px;
  background:rgba(255,255,255,.18);
  padding:4px 12px;border-radius:20px;
  font-size:.75rem;font-weight:600;
  margin-bottom:14px;
}
.hero h1{font-family:'Sora',sans-serif;font-size:1.5rem;font-weight:700;line-height:1.3;margin-bottom:8px}
.hero p{font-size:.875rem;opacity:.85;line-height:1.6}
.hero-stats{
  display:grid;grid-template-columns:1fr 1fr 1fr;
  gap:12px;margin-top:20px;
}
.hero-stat{
  background:rgba(255,255,255,.15);
  border-radius:var(--r16);padding:12px 8px;text-align:center;
}
.hero-stat-n{font-family:'Sora',sans-serif;font-size:1.3rem;font-weight:700}
.hero-stat-l{font-size:.68rem;opacity:.8;margin-top:2px}

/* ===== CARDS ===== */
.card{
  background:var(--white);
  border-radius:var(--r16);
  box-shadow:var(--shadow-sm);
  border:1.5px solid rgba(0,0,0,.05);
  overflow:hidden;
  margin-bottom:12px;
}
.card-header{
  padding:14px 16px 0;
  display:flex;align-items:center;gap:12px;
}
.card-avatar{
  width:46px;height:46px;border-radius:12px;
  background:linear-gradient(135deg,var(--emerald-l),#C0E8DC);
  display:flex;align-items:center;justify-content:center;
  font-size:1.2rem;flex-shrink:0;
}
.card-name{font-size:.95rem;font-weight:700;color:var(--ink)}
.card-function{font-size:.78rem;color:var(--emerald-d);font-weight:600;margin-top:2px}
.card-body{padding:12px 16px}
.route{
  display:flex;align-items:center;gap:8px;
  background:var(--surface);
  border-radius:var(--r8);padding:10px 12px;
  margin-bottom:10px;
}
.route-city{font-size:.82rem;font-weight:600;color:var(--ink)}
.route-arrow{color:var(--emerald);font-size:1rem;flex-shrink:0}
.card-tags{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:10px}
.tag{
  font-size:.7rem;font-weight:600;
  padding:3px 10px;border-radius:20px;
}
.tag-motive{background:var(--gold-l);color:#B57A00}
.tag-date{background:var(--surface);color:var(--ink-60)}
.card-footer{
  padding:10px 16px;
  border-top:1px solid rgba(0,0,0,.05);
  display:flex;gap:8px;
}

/* ===== SCORE BADGE ===== */
.score-badge{
  display:inline-flex;align-items:center;gap:6px;
  border-radius:var(--r8);padding:6px 12px;
  font-size:.8rem;font-weight:700;
}
.score-high{background:#E6F7F2;color:#007D5A}
.score-medium{background:#FEF7E6;color:#B57A00}
.score-low{background:#FEE;color:#C00}

/* ===== BUTTONS ===== */
.btn{
  display:inline-flex;align-items:center;justify-content:center;gap:8px;
  border-radius:var(--r8);padding:10px 16px;
  font-size:.85rem;font-weight:600;
  transition:all .2s;
}
.btn-primary{
  background:linear-gradient(135deg,var(--emerald),var(--emerald-d));
  color:#fff;flex:1;
  box-shadow:0 4px 14px rgba(0,168,120,.3);
}
.btn-primary:hover{transform:translateY(-1px);box-shadow:0 6px 20px rgba(0,168,120,.4)}
.btn-primary:active{transform:translateY(0)}
.btn-whatsapp{
  background:linear-gradient(135deg,#25D366,#128C7E);
  color:#fff;flex:1;
  box-shadow:0 4px 14px rgba(37,211,102,.3);
}
.btn-outline{
  background:var(--surface);color:var(--ink-60);
  border:1.5px solid rgba(0,0,0,.08);
}
.btn-outline:hover{background:#eee}
.btn-sm{padding:7px 12px;font-size:.78rem}
.btn-block{width:100%;border-radius:var(--r16);padding:15px;}
.btn-full{
  background:linear-gradient(135deg,var(--emerald),var(--emerald-d));
  color:#fff;width:100%;border-radius:var(--r16);
  padding:15px;font-size:1rem;font-weight:700;
  box-shadow:0 4px 20px rgba(0,168,120,.35);
  margin-top:16px;
  letter-spacing:.3px;
}

/* ===== SECTION HEADER ===== */
.section-header{
  display:flex;align-items:center;justify-content:space-between;
  margin-bottom:14px;
}
.section-title{font-family:'Sora',sans-serif;font-size:1rem;font-weight:700;color:var(--ink)}
.section-link{font-size:.8rem;color:var(--emerald);font-weight:600}

/* ===== SEARCH BAR ===== */
.search-bar{
  display:flex;align-items:center;gap:10px;
  background:var(--white);
  border:1.5px solid rgba(0,0,0,.08);
  border-radius:var(--r16);
  padding:10px 14px;
  margin-bottom:16px;
  box-shadow:var(--shadow-sm);
}
.search-bar input{
  flex:1;border:none;outline:none;
  font-size:.9rem;color:var(--ink);background:transparent;
}
.search-bar input::placeholder{color:var(--ink-30)}
.search-icon{color:var(--ink-30);font-size:1.1rem}

/* ===== FILTER PILLS ===== */
.filter-pills{
  display:flex;gap:8px;overflow-x:auto;
  padding-bottom:4px;margin-bottom:16px;
  scrollbar-width:none;
}
.filter-pills::-webkit-scrollbar{display:none}
.pill{
  flex-shrink:0;
  padding:6px 14px;border-radius:20px;
  font-size:.78rem;font-weight:600;
  background:var(--white);color:var(--ink-60);
  border:1.5px solid rgba(0,0,0,.08);
  cursor:pointer;transition:all .15s;
}
.pill.active{
  background:var(--emerald);color:#fff;border-color:var(--emerald);
  box-shadow:0 4px 12px rgba(0,168,120,.3);
}

/* ===== FORM ===== */
.form-section{
  background:var(--white);
  border-radius:var(--r16);
  border:1.5px solid rgba(0,0,0,.06);
  padding:16px;
  margin-bottom:14px;
}
.form-section-title{
  font-size:.8rem;font-weight:700;
  color:var(--emerald-d);text-transform:uppercase;
  letter-spacing:.8px;margin-bottom:14px;
  display:flex;align-items:center;gap:8px;
}
.form-group{margin-bottom:14px}
.form-group:last-child{margin-bottom:0}
.form-label{
  display:block;
  font-size:.8rem;font-weight:600;color:var(--ink-60);
  margin-bottom:6px;
}
.form-label .req{color:var(--danger)}
.form-control{
  width:100%;
  background:var(--surface);
  border:1.5px solid rgba(0,0,0,.08);
  border-radius:var(--r8);
  padding:11px 14px;
  font-size:.9rem;color:var(--ink);
  outline:none;
  transition:border-color .2s,box-shadow .2s;
  appearance:none;
}
.form-control:focus{
  border-color:var(--emerald);
  box-shadow:0 0 0 4px rgba(0,168,120,.12);
  background:var(--white);
}
select.form-control{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%235A6A78' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 12px center;background-size:16px;padding-right:36px}
textarea.form-control{resize:none;min-height:80px}
.char-count{font-size:.72rem;color:var(--ink-30);text-align:right;margin-top:4px}
.form-hint{font-size:.75rem;color:var(--ink-60);margin-top:4px}

/* ===== WA PREVIEW ===== */
.wa-preview{
  background:linear-gradient(135deg,#E8F8EF,#D4F0E2);
  border:1.5px solid #A8DFC0;
  border-radius:var(--r16);
  padding:16px;
  margin-top:16px;
}
.wa-preview-header{
  display:flex;align-items:center;gap:10px;
  margin-bottom:12px;
}
.wa-bubble{
  background:#fff;
  border-radius:0 var(--r16) var(--r16) var(--r16);
  padding:12px 14px;
  font-size:.82rem;line-height:1.7;
  color:var(--ink);
  white-space:pre-wrap;
  box-shadow:var(--shadow-sm);
  word-break:break-word;
}

/* ===== PROFILE PAGE ===== */
.profile-header{
  background:linear-gradient(135deg,var(--emerald),var(--emerald-d));
  border-radius:var(--r24);padding:24px;
  text-align:center;color:#fff;
  margin-bottom:16px;position:relative;overflow:hidden;
}
.profile-avatar{
  width:72px;height:72px;border-radius:20px;
  background:rgba(255,255,255,.2);
  display:flex;align-items:center;justify-content:center;
  font-size:2rem;margin:0 auto 12px;
  border:3px solid rgba(255,255,255,.3);
}
.profile-name{font-family:'Sora',sans-serif;font-size:1.2rem;font-weight:700}
.profile-role{font-size:.82rem;opacity:.8;margin-top:4px}
.profile-stat-row{
  display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px;
}
.p-stat{
  background:var(--white);border-radius:var(--r16);
  padding:14px;text-align:center;
  box-shadow:var(--shadow-sm);
}
.p-stat-n{font-family:'Sora',sans-serif;font-size:1.4rem;font-weight:700;color:var(--emerald)}
.p-stat-l{font-size:.75rem;color:var(--ink-60);margin-top:4px}
.info-row{
  display:flex;align-items:flex-start;gap:12px;
  padding:12px 0;
  border-bottom:1px solid rgba(0,0,0,.05);
}
.info-row:last-child{border-bottom:none}
.info-icon{font-size:1rem;flex-shrink:0;margin-top:2px}
.info-key{font-size:.75rem;color:var(--ink-60);margin-bottom:3px}
.info-val{font-size:.88rem;font-weight:600;color:var(--ink)}

/* ===== MODAL ===== */
.modal-overlay{
  position:fixed;inset:0;z-index:500;
  background:rgba(0,0,0,.55);backdrop-filter:blur(6px);
  display:flex;align-items:flex-end;justify-content:center;
  animation:fadeIn .2s ease;
}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.modal{
  background:var(--white);
  border-radius:var(--r24) var(--r24) 0 0;
  padding:24px 20px calc(24px + env(safe-area-inset-bottom));
  width:100%;max-width:480px;
  animation:slideUp .3s ease;
  max-height:80vh;overflow-y:auto;
}
@keyframes slideUp{from{transform:translateY(100%)}to{transform:translateY(0)}}
.modal-handle{
  width:40px;height:4px;border-radius:2px;
  background:var(--ink-30);margin:0 auto 20px;
}
.modal-title{font-family:'Sora',sans-serif;font-size:1.1rem;font-weight:700;margin-bottom:16px}

/* ===== SUCCESS SCREEN ===== */
#success-overlay{
  position:fixed;inset:0;z-index:600;
  background:linear-gradient(145deg,var(--emerald-d),var(--emerald));
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  text-align:center;padding:32px;
  animation:fadeIn .4s ease;
}
.success-icon{
  width:90px;height:90px;border-radius:24px;
  background:rgba(255,255,255,.2);
  display:flex;align-items:center;justify-content:center;
  font-size:2.5rem;margin-bottom:24px;
  box-shadow:0 0 0 12px rgba(255,255,255,.1);
}
.success-title{font-family:'Sora',sans-serif;font-size:1.6rem;font-weight:700;color:#fff;margin-bottom:12px}
.success-msg{color:rgba(255,255,255,.8);font-size:.9rem;line-height:1.7;margin-bottom:32px}
.success-actions{display:flex;flex-direction:column;gap:12px;width:100%}
.btn-wa-big{
  background:#fff;color:var(--emerald-d);
  border-radius:var(--r16);padding:16px;
  font-size:1rem;font-weight:700;
  display:flex;align-items:center;justify-content:center;gap:10px;
}
.btn-continue{
  background:rgba(255,255,255,.15);color:#fff;
  border-radius:var(--r16);padding:14px;
  font-size:.9rem;font-weight:600;
  border:1.5px solid rgba(255,255,255,.3);
}

/* ===== TOAST ===== */
.toast{
  position:fixed;top:80px;left:50%;transform:translateX(-50%) translateY(-20px);
  background:var(--ink);color:#fff;
  padding:10px 20px;border-radius:20px;
  font-size:.85rem;font-weight:500;
  z-index:800;
  opacity:0;pointer-events:none;
  transition:all .3s;
  white-space:nowrap;
}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}

/* ===== EMPTY STATE ===== */
.empty{
  text-align:center;padding:40px 20px;
  color:var(--ink-60);
}
.empty-icon{font-size:3rem;margin-bottom:12px;opacity:.4}
.empty-title{font-weight:700;margin-bottom:6px}
.empty-sub{font-size:.85rem}

/* ===== MATCH BADGE ===== */
.match-label{
  display:flex;align-items:center;gap:6px;
  background:linear-gradient(135deg,var(--gold-l),#FEF3C7);
  border:1px solid #F4D060;
  border-radius:var(--r8);padding:6px 10px;
  font-size:.75rem;font-weight:700;color:#92600A;
  margin-bottom:8px;
}

/* ===== STEP INDICATOR ===== */
.steps{display:flex;align-items:center;gap:0;margin-bottom:20px}
.step{
  display:flex;flex-direction:column;align-items:center;
  flex:1;
}
.step-dot{
  width:28px;height:28px;border-radius:50%;
  background:var(--surface);border:2px solid var(--ink-30);
  display:flex;align-items:center;justify-content:center;
  font-size:.75rem;font-weight:700;color:var(--ink-30);
  z-index:1;transition:all .3s;
}
.step.done .step-dot{background:var(--emerald);border-color:var(--emerald);color:#fff}
.step.active .step-dot{background:var(--white);border-color:var(--emerald);color:var(--emerald);box-shadow:0 0 0 4px rgba(0,168,120,.15)}
.step-label{font-size:.65rem;color:var(--ink-30);margin-top:5px;font-weight:600;text-align:center}
.step.active .step-label,.step.done .step-label{color:var(--emerald)}
.step-line{flex:1;height:2px;background:var(--ink-30);margin:0 -1px;margin-bottom:18px;transition:background .3s}
.step.done+.step-line{background:var(--emerald)}

/* ===== RESPONSIVE ===== */
@media(min-width:481px){
  .page,.header-inner,.nav-inner{max-width:480px}
  #app-header{border-radius:0}
}
</style>
</head>
<body>

<!-- SPLASH -->
<div id="splash">
  <div class="splash-logo">🔄</div>
  <div class="splash-title">PermutCI</div>
  <div class="splash-sub">Plateforme de Permutation des Personnels</div>
  <div class="splash-dots">
    <div class="splash-dot"></div>
    <div class="splash-dot"></div>
    <div class="splash-dot"></div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- HEADER -->
<div id="app-header">
  <div class="header-inner">
    <div class="header-brand">
      <div class="brand-icon">🔄</div>
      <div class="brand-text">Permut<span>CI</span></div>
    </div>
    <button class="header-btn" onclick="showPage('soumettre')">+ Demande</button>
  </div>
</div>

<!-- PAGES -->

<!-- PAGE: ACCUEIL -->
<div class="page active" id="page-accueil">

  <div class="hero">
    <div class="hero-badge">🇨🇮 Éduc Nat– Permutation</div>
    <h1>Trouver votre partenaire de permutation</h1>
    <p>Connectez-vous avec des collègues qui souhaitent permuter avec vous. Matching intelligent et contact direct via WhatsApp.</p>
    <div class="hero-stats">
      <div class="hero-stat">
        <div class="hero-stat-n" id="stat-total">0</div>
        <div class="hero-stat-l">Demandes</div>
      </div>
      <div class="hero-stat">
        <div class="hero-stat-n" id="stat-match">0</div>
        <div class="hero-stat-l">Matchs</div>
      </div>
      <div class="hero-stat">
        <div class="hero-stat-n" id="stat-regions">11</div>
        <div class="hero-stat-l">Régions</div>
      </div>
    </div>
  </div>

  <!-- MATCHES INTELLIGENTS -->
  <div class="section-header">
    <div class="section-title">🎯 Matchs intelligents</div>
    <div class="section-link" onclick="showPage('recherche')">Voir tout</div>
  </div>
  <div id="matches-container">
    <div class="empty">
      <div class="empty-icon">🔍</div>
      <div class="empty-title">Aucun match pour l'instant</div>
      <div class="empty-sub">Soumettez une demande pour voir vos correspondances</div>
    </div>
  </div>

  <!-- DERNIERES DEMANDES -->
  <div class="section-header mt-4">
    <div class="section-title">📋 Dernières demandes</div>
    <div class="section-link" onclick="showPage('recherche')">Voir tout</div>
  </div>
  <div id="recent-container">
    <div class="empty">
      <div class="empty-icon">📄</div>
      <div class="empty-title">Aucune demande enregistrée</div>
      <div class="empty-sub">Soyez le premier à soumettre une demande</div>
    </div>
  </div>

</div>

<!-- PAGE: RECHERCHE -->
<div class="page" id="page-recherche">

  <div style="margin-bottom:16px">
    <div style="font-family:'Sora',sans-serif;font-size:1.1rem;font-weight:700;margin-bottom:4px">Annuaire des demandes</div>
    <div style="font-size:.82rem;color:var(--ink-60)">Recherchez un profil compatible</div>
  </div>

  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="Nom, ville, région…" id="search-input" oninput="filterDemandes()">
  </div>

  <div class="filter-pills" id="filter-pills">
    <div class="pill active" data-filter="tous" onclick="setFilter(this,'tous')">Tous</div>
    <div class="pill" data-filter="Abidjan" onclick="setFilter(this,'Abidjan')">Abidjan</div>
    <div class="pill" data-filter="Yamoussoukro" onclick="setFilter(this,'Yamoussoukro')">Yamoussoukro</div>
    <div class="pill" data-filter="Bouaké" onclick="setFilter(this,'Bouaké')">Bouaké</div>
    <div class="pill" data-filter="San-Pédro" onclick="setFilter(this,'San-Pédro')">San-Pédro</div>
    <div class="pill" data-filter="Daloa" onclick="setFilter(this,'Daloa')">Daloa</div>
    <div class="pill" data-filter="Korhogo" onclick="setFilter(this,'Korhogo')">Korhogo</div>
    <div class="pill" data-filter="Man" onclick="setFilter(this,'Man')">Man</div>
    <div class="pill" data-filter="Bondougou" onclick="setFilter(this,'Bondougou')">Bondougou</div>

  <div id="search-results"></div>
</div>

<!-- PAGE: SOUMETTRE -->
<div class="page" id="page-soumettre">

  <div style="margin-bottom:16px">
    <div style="font-family:'Sora',sans-serif;font-size:1.1rem;font-weight:700;margin-bottom:4px">Soumettre une demande</div>
    <div style="font-size:.82rem;color:var(--ink-60)">Formulaire rapide — moins de 2 minutes</div>
  </div>

  <!-- STEPS -->
  <div class="steps">
    <div class="step active" id="step1-dot">
      <div class="step-dot">1</div>
      <div class="step-label">Profil</div>
    </div>
    <div class="step-line"></div>
    <div class="step" id="step2-dot">
      <div class="step-dot">2</div>
      <div class="step-label">Poste</div>
    </div>
    <div class="step-line"></div>
    <div class="step" id="step3-dot">
      <div class="step-dot">3</div>
      <div class="step-label">Souhait</div>
    </div>
    <div class="step-line"></div>
    <div class="step" id="step4-dot">
      <div class="step-dot">4</div>
      <div class="step-label">Contact</div>
    </div>
  </div>

  <!-- STEP 1 -->
  <div id="form-step1">
    <div class="form-section">
      <div class="form-section-title">👤 Identité</div>
      <div class="form-group">
        <label class="form-label">Nom <span class="req">*</span></label>
        <input class="form-control" type="text" id="f-nom" placeholder="Ex: KOUAKOU">
      </div>
      <div class="form-group">
        <label class="form-label">Prénom(s) <span class="req">*</span></label>
        <input class="form-control" type="text" id="f-prenom" placeholder="Ex: Jean-Baptiste">
      </div>
      <div class="form-group">
        <label class="form-label">Fonction <span class="req">*</span></label>
        <select class="form-control" id="f-fonction">
          <option value="">— Sélectionner —</option>
          <option>Inspecteur d'Education</option>
          <option>Inspecteur d'Orientation</option>
          <option>Professeur de lycée</option>
          <option>Professeur de collège</option>
          <option>Conseiller Pédagogique</option>
          <option>Directeur d'école</option>
          <option>Instituteur / Institutrice</option>
          <option>Autre</option>
        </select>
      </div>
    </div>
    <button class="btn-full" onclick="goStep(2)">Continuer →</button>
  </div>

  <!-- STEP 2 -->
  <div id="form-step2" class="hidden">
    <div class="form-section">
      <div class="form-section-title">🏫 Poste actuel</div>
      <div class="form-group">
        <label class="form-label">Établissement actuel <span class="req">*</span></label>
        <input class="form-control" type="text" id="f-etab" placeholder="Nom de l'école / inspection">
      </div>
      <div class="form-group">
        <label class="form-label">Ville actuelle <span class="req">*</span></label>
        <select class="form-control" id="f-ville-actuelle">
          <option value="">— Sélectionner la ville —</option>
          <option>Abidjan</option><option>Adjamé</option><option>Abobo</option>
          <option>Bouaké</option><option>Daloa</option><option>San-Pédro</option>
          <option>Korhogo</option><option>Yamoussoukro</option><option>Man</option>
          <option>Gagnoa</option><option>Divo</option><option>Grand-Bassam</option>
          <option>Abengourou</option><option>Bondoukou</option><option>Odienné</option>
          <option>Touba</option><option>Séguéla</option><option>Mankono</option>
          <option>Soubré</option><option>Tabou</option><option>Sassandra</option>
          <option>Autre</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Région / District</label>
        <select class="form-control" id="f-region">
          <option value="">— Sélectionner —</option>
          <option>Lagunes</option><option>Lacs</option><option>Savanes</option>
          <option>Vallée du Bandama</option><option>Moyen-Comoé</option>
          <option>N'zi-Comoé</option><option>Marahoué</option><option>Haut-Sassandra</option>
          <option>Sassandra-Marahoué</option><option>Bas-Sassandra</option>
          <option>Sud-Comoé</option><option>Montagnes</option><option>Woroba</option>
          <option>Zanzan</option><option>Gôh-Djiboua</option><option>Hambol</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Ancienneté au poste actuel</label>
        <select class="form-control" id="f-anciennete">
          <option value="">— Sélectionner —</option>
          <option>Moins d'1 an</option><option>1-2 ans</option>
          <option>3-5 ans</option><option>6-10 ans</option>
          <option>Plus de 10 ans</option>
        </select>
      </div>
    </div>
    <div style="display:flex;gap:10px">
      <button class="btn btn-outline" onclick="goStep(1)">← Retour</button>
      <button class="btn btn-primary" style="flex:2" onclick="goStep(3)">Continuer →</button>
    </div>
  </div>

  <!-- STEP 3 -->
  <div id="form-step3" class="hidden">
    <div class="form-section">
      <div class="form-section-title">🎯 Souhait de permutation</div>
      <div class="form-group">
        <label class="form-label">Ville souhaitée <span class="req">*</span></label>
        <select class="form-control" id="f-ville-souhaitee">
          <option value="">— Sélectionner la ville —</option>
          <option>Abidjan</option><option>Adjamé</option><option>Abobo</option>
          <option>Bouaké</option><option>Daloa</option><option>San-Pédro</option>
          <option>Korhogo</option><option>Yamoussoukro</option><option>Man</option>
          <option>Gagnoa</option><option>Divo</option><option>Grand-Bassam</option>
          <option>Abengourou</option><option>Bondoukou</option><option>Odienné</option>
          <option>Touba</option><option>Séguéla</option><option>Mankono</option>
          <option>Soubré</option><option>Tabou</option><option>Sassandra</option>
          <option>Flexible / Toute ville</option><option>Autre</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Établissement ou zone souhaité(e)</label>
        <input class="form-control" type="text" id="f-etab-souhaite" placeholder="Précisez si besoin (optionnel)">
      </div>
      <div class="form-group">
        <label class="form-label">Motif de la permutation <span class="req">*</span></label>
        <select class="form-control" id="f-motif">
          <option value="">— Sélectionner le motif —</option>
          <option>Rapprochement familial (conjoint)</option>
          <option>Rapprochement familial (enfants/parents)</option>
          <option>Raisons médicales</option>
          <option>Avancement de carrière</option>
          <option>Conditions de vie difficiles</option>
          <option>Retour au pays d'origine</option>
          <option>Éloignement du lieu de service</option>
          <option>Autre motif personnel</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">Précisions sur le motif</label>
        <textarea class="form-control" id="f-motif-detail" placeholder="Décrivez brièvement votre situation..." maxlength="250" oninput="updateCharCount(this,'motif-count')"></textarea>
        <div class="char-count"><span id="motif-count">0</span>/250</div>
      </div>
      <div class="form-group">
        <label class="form-label">Urgence</label>
        <select class="form-control" id="f-urgence">
          <option value="normale">Normale</option>
          <option value="prioritaire">Prioritaire</option>
          <option value="urgente">Urgente</option>
        </select>
      </div>
    </div>
    <div style="display:flex;gap:10px">
      <button class="btn btn-outline" onclick="goStep(2)">← Retour</button>
      <button class="btn btn-primary" style="flex:2" onclick="goStep(4)">Continuer →</button>
    </div>
  </div>

  <!-- STEP 4 -->
  <div id="form-step4" class="hidden">
    <div class="form-section">
      <div class="form-section-title">📱 Contact</div>
      <div class="form-group">
        <label class="form-label">Numéro WhatsApp <span class="req">*</span></label>
        <input class="form-control" type="tel" id="f-whatsapp" placeholder="Ex: 0708901234" maxlength="15">
        <div class="form-hint">Format: 07XXXXXXXX ou +225XXXXXXXXXX</div>
      </div>
      <div class="form-group">
        <label class="form-label">Téléphone (optionnel)</label>
        <input class="form-control" type="tel" id="f-telephone" placeholder="Ex: 0102030405">
      </div>
      <div class="form-group">
        <label class="form-label">Email (optionnel)</label>
        <input class="form-control" type="email" id="f-email" placeholder="votre@email.com">
      </div>
    </div>

    <!-- WA PREVIEW -->
    <div class="wa-preview">
      <div class="wa-preview-header">
        <span style="font-size:1.3rem">💬</span>
        <span style="font-size:.82rem;font-weight:700;color:#128C7E">Aperçu du message WhatsApp</span>
      </div>
      <div class="wa-bubble" id="wa-preview-text">Remplissez le formulaire pour voir le message…</div>
    </div>

    <div style="display:flex;gap:10px;margin-top:16px">
      <button class="btn btn-outline" onclick="goStep(3)">← Retour</button>
      <button class="btn btn-primary" style="flex:2" onclick="submitDemande()">✅ Soumettre</button>
    </div>
  </div>

</div>

<!-- PAGE: MON PROFIL -->
<div class="page" id="page-profil">

  <div id="profil-content">
    <div class="empty" style="padding-top:60px">
      <div class="empty-icon">👤</div>
      <div class="empty-title">Aucune demande soumise</div>
      <div class="empty-sub">Soumettez une demande pour voir votre profil ici</div>
      <button class="btn btn-primary mt-4" onclick="showPage('soumettre')" style="margin:16px auto 0;display:flex">+ Soumettre une demande</button>
    </div>
  </div>

</div>

<!-- SUCCESS OVERLAY -->
<div id="success-overlay" class="hidden">
  <div class="success-icon">🎉</div>
  <div class="success-title">Demande soumise !</div>
  <div class="success-msg">Votre demande de permutation a été enregistrée avec succès. Partagez-la sur WhatsApp pour maximiser vos chances de trouver un partenaire.</div>
  <div class="success-actions">
    <button class="btn-wa-big" id="btn-wa-redirect" onclick="redirectWhatsApp()">
      <span style="font-size:1.3rem">💬</span>
      Partager sur WhatsApp
    </button>
    <button class="btn-continue" onclick="closeSuccess()">Continuer sans partager</button>
  </div>
</div>

<!-- DETAIL MODAL -->
<div class="modal-overlay hidden" id="detail-modal" onclick="closeModal(event)">
  <div class="modal" id="modal-content">
    <div class="modal-handle"></div>
    <div id="modal-body"></div>
  </div>
</div>

<!-- BOTTOM NAV -->
<div id="bottom-nav">
  <div class="nav-inner">
    <div class="nav-item active" onclick="showPage('accueil')" id="nav-accueil">
      <div class="nav-icon">🏠</div>
      <div>Accueil</div>
    </div>
    <div class="nav-item" onclick="showPage('recherche')" id="nav-recherche">
      <div class="nav-icon">🔍</div>
      <div>Recherche</div>
    </div>
    <div class="nav-item" onclick="showPage('soumettre')" id="nav-soumettre">
      <div class="nav-icon">➕</div>
      <div>Soumettre</div>
    </div>
    <div class="nav-item" onclick="showPage('profil')" id="nav-profil">
      <div class="nav-icon">👤</div>
      <div>Mon profil</div>
    </div>
  </div>
</div>

<script>
/* =========================================
   ÉTAT GLOBAL
   ========================================= */
let demandes = JSON.parse(localStorage.getItem('permutci_demandes') || '[]');
let maDemande = JSON.parse(localStorage.getItem('permutci_ma_demande') || 'null');
let currentStep = 1;
let currentFilter = 'tous';

/* =========================================
   DONNÉES DE DÉMO
   ========================================= */
const DEMO_DATA = [
  {id:'d1',nom:'KONÉ',prenom:'Mariam',fonction:'Inspecteur de l\'Enseignement Préscolaire et Primaire',etab:'Inspection EP Korhogo 1',villeActuelle:'Korhogo',region:'Savanes',villesSouhaitee:'Abidjan',motif:'Rapprochement familial (conjoint)',whatsapp:'2250707010101',date:'2025-01-10',urgence:'prioritaire'},
  {id:'d2',nom:'BAMBA',prenom:'Seydou',fonction:'Inspecteur de l\'Enseignement Préscolaire et Primaire',etab:'Inspection EP Abobo 3',villeActuelle:'Abidjan',region:'Lagunes',villesSouhaitee:'Korhogo',motif:'Retour au pays d\'origine',whatsapp:'2250505020202',date:'2025-01-08',urgence:'normale'},
  {id:'d3',nom:'YAO',prenom:'Adjoua Christelle',fonction:'Conseiller Pédagogique',etab:'Circonscription Bouaké Sud',villeActuelle:'Bouaké',region:'Vallée du Bandama',villesSouhaitee:'Abidjan',motif:'Raisons médicales',whatsapp:'2250101030303',date:'2025-01-06',urgence:'urgente'},
  {id:'d4',nom:'COULIBALY',prenom:'Ibrahim',fonction:'Inspecteur de l\'Enseignement Préscolaire et Primaire',etab:'Inspection EP San-Pédro 1',villeActuelle:'San-Pédro',region:'Bas-Sassandra',villesSouhaitee:'Yamoussoukro',motif:'Rapprochement familial (conjoint)',whatsapp:'2250909040404',date:'2025-01-04',urgence:'normale'},
  {id:'d5',nom:'DIALLO',prenom:'Fatoumata',fonction:'Instituteur / Institutrice',etab:'École Primaire Daloa Centre',villeActuelle:'Daloa',region:'Haut-Sassandra',villesSouhaitee:'Abidjan',motif:'Avancement de carrière',whatsapp:'2250505050505',date:'2024-12-28',urgence:'normale'},
];

/* Fusionner les démos avec les vraies données */
function getAllDemandes() {
  const ids = demandes.map(d=>d.id);
  return [...demandes, ...DEMO_DATA.filter(d=>!ids.includes(d.id))];
}

/* =========================================
   SPLASH
   ========================================= */
window.addEventListener('load', ()=>{
  setTimeout(()=>{
    document.getElementById('splash').classList.add('fade-out');
    setTimeout(()=>document.getElementById('splash').style.display='none', 500);
    renderAll();
  }, 1800);
});

/* =========================================
   NAVIGATION
   ========================================= */
function showPage(name){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('page-'+name).classList.add('active');
  document.getElementById('nav-'+name).classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
  if(name==='recherche') renderSearch();
  if(name==='profil') renderProfil();
  if(name==='accueil') renderAll();
}

/* =========================================
   STEPS FORMULAIRE
   ========================================= */
function goStep(n){
  if(n>currentStep && !validateStep(currentStep)) return;
  // Update UI
  for(let i=1;i<=4;i++){
    const el = document.getElementById('form-step'+i);
    if(el) el.classList.toggle('hidden', i!==n);
    const dot = document.getElementById('step'+i+'-dot');
    if(dot){
      dot.classList.remove('active','done');
      if(i<n) dot.classList.add('done');
      if(i===n) dot.classList.add('active');
    }
  }
  currentStep = n;
  window.scrollTo({top:0,behavior:'smooth'});
  if(n===4) updateWaPreview();
}

function validateStep(n){
  const rules = {
    1: [{id:'f-nom',msg:'Veuillez saisir votre nom'},{id:'f-prenom',msg:'Veuillez saisir votre prénom'},{id:'f-fonction',msg:'Veuillez sélectionner votre fonction'}],
    2: [{id:'f-etab',msg:'Veuillez saisir votre établissement'},{id:'f-ville-actuelle',msg:'Veuillez sélectionner votre ville actuelle'}],
    3: [{id:'f-ville-souhaitee',msg:'Veuillez sélectionner la ville souhaitée'},{id:'f-motif',msg:'Veuillez sélectionner le motif'}],
    4: [{id:'f-whatsapp',msg:'Veuillez saisir votre numéro WhatsApp'}],
  };
  for(const r of (rules[n]||[])){
    const el = document.getElementById(r.id);
    if(!el||!el.value.trim()){showToast('⚠️ '+r.msg);el&&el.focus();return false;}
  }
  return true;
}

/* =========================================
   CHAR COUNT
   ========================================= */
function updateCharCount(el,countId){
  document.getElementById(countId).textContent = el.value.length;
}

/* =========================================
   WA PREVIEW
   ========================================= */
function updateWaPreview(){
  const nom = val('f-nom'), prenom = val('f-prenom');
  const fn = val('f-fonction'), ville = val('f-ville-actuelle');
  const dest = val('f-ville-souhaitee'), motif = val('f-motif');
  const etab = val('f-etab');
  const msg = `🔄 *DEMANDE DE PERMUTATION*\n\n👤 *${nom} ${prenom}*\n🏷️ ${fn}\n🏫 ${etab}\n📍 Actuellement à : *${ville}*\n🎯 Souhaite aller à : *${dest}*\n💬 Motif : ${motif}\n\n📌 Je suis disponible pour une permutation croisée. Merci de me contacter si vous êtes intéressé(e) !\n\n_Via PermutCI – Plateforme officielle_`;
  document.getElementById('wa-preview-text').textContent = msg;
}

function val(id){ return (document.getElementById(id)||{}).value||''; }

/* =========================================
   SOUMETTRE
   ========================================= */
function submitDemande(){
  if(!validateStep(4)) return;
  const d = {
    id: 'u_'+Date.now(),
    nom: val('f-nom').toUpperCase(),
    prenom: val('f-prenom'),
    fonction: val('f-fonction'),
    etab: val('f-etab'),
    villeActuelle: val('f-ville-actuelle'),
    region: val('f-region'),
    villesSouhaitee: val('f-ville-souhaitee'),
    etabSouhaite: val('f-etab-souhaite'),
    motif: val('f-motif'),
    motifDetail: val('f-motif-detail'),
    urgence: val('f-urgence'),
    whatsapp: formatWA(val('f-whatsapp')),
    telephone: val('f-telephone'),
    email: val('f-email'),
    anciennete: val('f-anciennete'),
    date: new Date().toISOString().slice(0,10),
    isOwn: true,
  };

  demandes.unshift(d);
  maDemande = d;
  localStorage.setItem('permutci_demandes', JSON.stringify(demandes));
  localStorage.setItem('permutci_ma_demande', JSON.stringify(maDemande));

  document.getElementById('success-overlay').classList.remove('hidden');
  resetForm();
}

function formatWA(num){
  num = num.replace(/\D/g,'');
  if(num.startsWith('225')) return num;
  if(num.startsWith('0') && num.length===10) return '225'+num.slice(1);
  if(num.length===8) return '225'+num;
  return '225'+num;
}

function redirectWhatsApp(){
  if(!maDemande) return;
  const nom = maDemande.nom, prenom = maDemande.prenom;
  const fn = maDemande.fonction, ville = maDemande.villeActuelle;
  const dest = maDemande.villesSouhaitee, motif = maDemande.motif;
  const etab = maDemande.etab;
  const msg = encodeURIComponent(
    `🔄 *DEMANDE DE PERMUTATION*\n\n👤 *${nom} ${prenom}*\n🏷️ ${fn}\n🏫 ${etab}\n📍 Actuellement à : *${ville}*\n🎯 Souhaite aller à : *${dest}*\n💬 Motif : ${motif}\n\n📌 Je suis disponible pour une permutation croisée. Merci de me contacter si vous êtes intéressé(e) !\n\n_Via PermutCI – Plateforme officielle_`
  );
  // Numéro du groupe PermutCI ou numéro générique
  const groupNum = '2250700000000'; // À configurer avec le vrai numéro
  window.open(`https://wa.me/${maDemande.whatsapp}?text=${msg}`, '_blank');
  closeSuccess();
}

function closeSuccess(){
  document.getElementById('success-overlay').classList.add('hidden');
  showPage('profil');
  renderAll();
}

function resetForm(){
  ['f-nom','f-prenom','f-fonction','f-etab','f-ville-actuelle','f-region','f-anciennete',
   'f-ville-souhaitee','f-etab-souhaite','f-motif','f-motif-detail','f-urgence',
   'f-whatsapp','f-telephone','f-email'].forEach(id=>{
    const el = document.getElementById(id);
    if(el) el.value = id==='f-urgence'?'normale':'';
  });
  document.getElementById('motif-count').textContent='0';
  goStep(1);
}

/* =========================================
   SCORE DE COMPATIBILITÉ
   ========================================= */
function computeScore(a, b){
  let score = 0;
  // Permutation croisée parfaite
  const crossMatch = a.villeActuelle===b.villesSouhaitee && b.villeActuelle===a.villesSouhaitee;
  if(crossMatch) score += 60;
  // Même fonction
  if(a.fonction===b.fonction) score += 20;
  // Même région
  if(a.region && b.region && a.region===b.region) score += 10;
  // Flexibilité
  if(b.villesSouhaitee==='Flexible / Toute ville') score += 15;
  // Motif similaire
  if(a.motif && b.motif && a.motif===b.motif) score += 5;
  return Math.min(score, 100);
}

function scoreLabel(s){
  if(s>=70) return {cls:'score-high', label:'🟢 '+s+'% – Fort match'};
  if(s>=40) return {cls:'score-medium', label:'🟡 '+s+'% – Match partiel'};
  return {cls:'score-low', label:'🔴 '+s+'% – Faible match'};
}

function findMatches(ref, pool){
  return pool
    .filter(d=>d.id!==ref.id)
    .map(d=>({...d, score: computeScore(ref,d)}))
    .filter(d=>d.score>=30)
    .sort((a,b)=>b.score-a.score)
    .slice(0,5);
}

/* =========================================
   RENDER CARD
   ========================================= */
function renderCard(d, showScore, score){
  const urgTag = d.urgence==='urgente'?'🔴 Urgent':d.urgence==='prioritaire'?'🟠 Prioritaire':'🟢 Normale';
  const sc = score!=null ? scoreLabel(score) : null;
  const isCross = maDemande && d.villeActuelle===maDemande.villesSouhaitee && maDemande.villeActuelle===d.villesSouhaitee;
  return `
  <div class="card" onclick="openDetail('${d.id}')">
    <div class="card-header">
      <div class="card-avatar">${d.prenom[0]}${d.nom[0]}</div>
      <div style="flex:1">
        <div class="card-name">${d.nom} ${d.prenom}</div>
        <div class="card-function">${d.fonction}</div>
      </div>
      ${sc?`<div class="score-badge ${sc.cls}" style="font-size:.72rem">${sc.label}</div>`:''}
    </div>
    <div class="card-body">
      ${isCross?`<div class="match-label">⚡ Permutation croisée possible !</div>`:''}
      <div class="route">
        <span style="font-size:.8rem">📍</span>
        <span class="route-city">${d.villeActuelle}</span>
        <span class="route-arrow">→</span>
        <span class="route-city">${d.villesSouhaitee}</span>
      </div>
      <div class="card-tags">
        <span class="tag tag-motive">💬 ${d.motif.split('(')[0].trim()}</span>
        <span class="tag tag-date">📅 ${formatDate(d.date)}</span>
        <span class="tag tag-date">${urgTag}</span>
      </div>
    </div>
    <div class="card-footer">
      <button class="btn btn-whatsapp btn-sm" onclick="event.stopPropagation();contactWA('${d.id}')">💬 WhatsApp</button>
      <button class="btn btn-outline btn-sm" onclick="event.stopPropagation();openDetail('${d.id}')">Voir détail</button>
    </div>
  </div>`;
}

function formatDate(d){
  if(!d) return '';
  const dt = new Date(d);
  return dt.toLocaleDateString('fr-FR',{day:'2-digit',month:'short',year:'numeric'});
}

/* =========================================
   RENDER ALL
   ========================================= */
function renderAll(){
  const all = getAllDemandes();
  // Stats
  document.getElementById('stat-total').textContent = all.length;
  const matchCount = all.filter(d=>{
    return all.some(o=>o.id!==d.id && d.villeActuelle===o.villesSouhaitee && o.villeActuelle===d.villesSouhaitee);
  }).length;
  document.getElementById('stat-match').textContent = Math.floor(matchCount/2);

  // Matches
  const mc = document.getElementById('matches-container');
  if(maDemande){
    const matches = findMatches(maDemande, all);
    if(matches.length){
      mc.innerHTML = matches.map(m=>renderCard(m,true,m.score)).join('');
    } else {
      mc.innerHTML = `<div class="empty"><div class="empty-icon">🔍</div><div class="empty-title">Aucun match trouvé</div><div class="empty-sub">Votre demande est enregistrée. Revenez bientôt !</div></div>`;
    }
  } else {
    mc.innerHTML = `<div class="empty"><div class="empty-icon">🔍</div><div class="empty-title">Soumettez d'abord une demande</div><div class="empty-sub">Le système trouvera vos correspondances automatiquement</div></div>`;
  }

  // Recent
  const rc = document.getElementById('recent-container');
  if(all.length){
    rc.innerHTML = all.slice(0,3).map(d=>renderCard(d,false,null)).join('');
  } else {
    rc.innerHTML = `<div class="empty"><div class="empty-icon">📄</div><div class="empty-title">Aucune demande</div><div class="empty-sub">Soyez le premier !</div></div>`;
  }
}

/* =========================================
   RENDER SEARCH
   ========================================= */
function renderSearch(query='', filter='tous'){
  let data = getAllDemandes();
  if(filter!=='tous') data = data.filter(d=>d.villeActuelle===filter||d.villesSouhaitee===filter);
  if(query) {
    const q = query.toLowerCase();
    data = data.filter(d=>
      (d.nom+' '+d.prenom+' '+d.villeActuelle+' '+d.villesSouhaitee+' '+d.region).toLowerCase().includes(q)
    );
  }
  const sr = document.getElementById('search-results');
  if(data.length){
    sr.innerHTML = `<div style="font-size:.8rem;color:var(--ink-60);margin-bottom:12px">${data.length} résultat(s) trouvé(s)</div>`+data.map(d=>{
      const score = maDemande ? computeScore(maDemande, d) : null;
      return renderCard(d, !!maDemande, score);
    }).join('');
  } else {
    sr.innerHTML = `<div class="empty"><div class="empty-icon">🔍</div><div class="empty-title">Aucun résultat</div><div class="empty-sub">Essayez un autre terme ou filtre</div></div>`;
  }
}

function filterDemandes(){
  const q = document.getElementById('search-input').value;
  renderSearch(q, currentFilter);
}

function setFilter(el, filter){
  document.querySelectorAll('.pill').forEach(p=>p.classList.remove('active'));
  el.classList.add('active');
  currentFilter = filter;
  filterDemandes();
}

/* =========================================
   RENDER PROFIL
   ========================================= */
function renderProfil(){
  const pc = document.getElementById('profil-content');
  const d = maDemande;
  if(!d){
    pc.innerHTML = `<div class="empty" style="padding-top:60px"><div class="empty-icon">👤</div><div class="empty-title">Aucune demande soumise</div><div class="empty-sub">Soumettez une demande pour voir votre profil ici</div><button class="btn btn-primary mt-4" onclick="showPage('soumettre')" style="margin:16px auto 0;display:flex">+ Soumettre une demande</button></div>`;
    return;
  }
  const all = getAllDemandes();
  const matches = findMatches(d, all);
  const urgTag = d.urgence==='urgente'?'🔴 Urgent':d.urgence==='prioritaire'?'🟠 Prioritaire':'🟢 Normale';
  pc.innerHTML = `
    <div class="profile-header">
      <div class="profile-avatar">${d.prenom[0]}${d.nom[0]}</div>
      <div class="profile-name">${d.nom} ${d.prenom}</div>
      <div class="profile-role">${d.fonction}</div>
      <div style="margin-top:12px;font-size:.75rem;opacity:.7">${urgTag} • Soumis le ${formatDate(d.date)}</div>
    </div>

    <div class="profile-stat-row">
      <div class="p-stat">
        <div class="p-stat-n">${matches.length}</div>
        <div class="p-stat-l">Matchs trouvés</div>
      </div>
      <div class="p-stat">
        <div class="p-stat-n">${matches.filter(m=>m.score>=70).length}</div>
        <div class="p-stat-l">Forts matchs</div>
      </div>
    </div>

    <div class="card">
      <div class="card-body">
        <div style="font-size:.8rem;font-weight:700;color:var(--emerald-d);margin-bottom:12px;text-transform:uppercase;letter-spacing:.8px">📋 Informations</div>
        <div class="info-row"><div class="info-icon">🏫</div><div><div class="info-key">Établissement actuel</div><div class="info-val">${d.etab}</div></div></div>
        <div class="info-row"><div class="info-icon">📍</div><div><div class="info-key">Ville actuelle</div><div class="info-val">${d.villeActuelle}${d.region?' – '+d.region:''}</div></div></div>
        <div class="info-row"><div class="info-icon">🎯</div><div><div class="info-key">Souhait</div><div class="info-val">${d.villesSouhaitee}${d.etabSouhaite?' ('+d.etabSouhaite+')':''}</div></div></div>
        <div class="info-row"><div class="info-icon">💬</div><div><div class="info-key">Motif</div><div class="info-val">${d.motif}</div></div></div>
        ${d.motifDetail?`<div class="info-row"><div class="info-icon">📝</div><div><div class="info-key">Précisions</div><div class="info-val">${d.motifDetail}</div></div></div>`:''}
        <div class="info-row"><div class="info-icon">📱</div><div><div class="info-key">WhatsApp</div><div class="info-val">+${d.whatsapp}</div></div></div>
      </div>
      <div class="card-footer">
        <button class="btn btn-whatsapp" onclick="shareMyDemande()">💬 Partager ma demande</button>
        <button class="btn btn-outline" onclick="deleteDemande()" style="color:var(--danger)">🗑️ Supprimer</button>
      </div>
    </div>

    ${matches.length?`<div class="section-header mt-4"><div class="section-title">🎯 Mes correspondances (${matches.length})</div></div>${matches.map(m=>`<div class="card" onclick="openDetail('${m.id}')"><div class="card-header"><div class="card-avatar">${m.prenom[0]}${m.nom[0]}</div><div style="flex:1"><div class="card-name">${m.nom} ${m.prenom}</div><div class="card-function">${m.fonction}</div></div><div class="score-badge ${scoreLabel(m.score).cls}">${scoreLabel(m.score).label}</div></div><div class="card-body"><div class="route"><span style="font-size:.8rem">📍</span><span class="route-city">${m.villeActuelle}</span><span class="route-arrow">→</span><span class="route-city">${m.villesSouhaitee}</span></div></div><div class="card-footer"><button class="btn btn-whatsapp btn-sm" onclick="event.stopPropagation();contactWA('${m.id}')">💬 Contacter</button></div></div>`).join('')}`:''}
  `;
}

function shareMyDemande(){
  if(!maDemande) return;
  const d = maDemande;
  const msg = encodeURIComponent(`🔄 *DEMANDE DE PERMUTATION*\n\n👤 *${d.nom} ${d.prenom}*\n🏷️ ${d.fonction}\n🏫 ${d.etab}\n📍 Actuellement à : *${d.villeActuelle}*\n🎯 Souhaite aller à : *${d.villesSouhaitee}*\n💬 Motif : ${d.motif}\n\n📌 Je suis disponible pour une permutation croisée !\n_Via PermutCI_`);
  window.open(`https://wa.me/${d.whatsapp}?text=${msg}`, '_blank');
}

function deleteDemande(){
  if(!confirm('Supprimer votre demande ?')) return;
  const idx = demandes.findIndex(d=>d.id===maDemande?.id);
  if(idx>=0) demandes.splice(idx,1);
  maDemande = null;
  localStorage.setItem('permutci_demandes', JSON.stringify(demandes));
  localStorage.removeItem('permutci_ma_demande');
  renderProfil();
  showToast('✅ Demande supprimée');
}

/* =========================================
   CONTACT WA
   ========================================= */
function contactWA(id){
  const all = getAllDemandes();
  const d = all.find(x=>x.id===id);
  if(!d) return;
  const me = maDemande;
  const intro = me ? `*${me.nom} ${me.prenom}* (${me.villeActuelle} → ${me.villesSouhaitee})` : 'Un collègue';
  const msg = encodeURIComponent(`🔄 Bonjour ${d.prenom},\n\nJe suis ${intro}.\n\nJ'ai vu votre demande de permutation de *${d.villeActuelle}* vers *${d.villesSouhaitee}* sur PermutCI.\n\n✅ Nos profils semblent compatibles pour une permutation croisée !\n\nPouvons-nous en discuter ?\n\n_Via PermutCI_`);
  window.open(`https://wa.me/${d.whatsapp}?text=${msg}`, '_blank');
}

/* =========================================
   MODAL DETAIL
   ========================================= */
function openDetail(id){
  const all = getAllDemandes();
  const d = all.find(x=>x.id===id);
  if(!d) return;
  const score = maDemande ? computeScore(maDemande,d) : null;
  const sc = score!=null ? scoreLabel(score) : null;
  const isCross = maDemande && d.villeActuelle===maDemande.villesSouhaitee && maDemande.villeActuelle===d.villesSouhaitee;
  document.getElementById('modal-body').innerHTML = `
    <div style="text-align:center;margin-bottom:20px">
      <div style="width:64px;height:64px;border-radius:18px;background:linear-gradient(135deg,var(--emerald-l),#C0E8DC);display:flex;align-items:center;justify-content:center;font-size:1.6rem;margin:0 auto 12px">${d.prenom[0]}${d.nom[0]}</div>
      <div style="font-family:'Sora',sans-serif;font-size:1.1rem;font-weight:700">${d.nom} ${d.prenom}</div>
      <div style="font-size:.8rem;color:var(--emerald-d);font-weight:600;margin-top:4px">${d.fonction}</div>
      ${sc?`<div class="score-badge ${sc.cls}" style="margin:10px auto;display:inline-flex">${sc.label}</div>`:''}
      ${isCross?`<div class="match-label" style="justify-content:center;margin-top:8px">⚡ Permutation croisée possible !</div>`:''}
    </div>

    <div class="route" style="margin-bottom:16px">
      <span>📍</span><strong>${d.villeActuelle}</strong>
      <span class="route-arrow" style="flex:1;text-align:center">→</span>
      <strong>${d.villesSouhaitee}</strong>
    </div>

    <div class="info-row"><div class="info-icon">🏫</div><div><div class="info-key">Établissement</div><div class="info-val">${d.etab}</div></div></div>
    ${d.region?`<div class="info-row"><div class="info-icon">🗺️</div><div><div class="info-key">Région</div><div class="info-val">${d.region}</div></div></div>`:''}
    ${d.anciennete?`<div class="info-row"><div class="info-icon">⏱️</div><div><div class="info-key">Ancienneté</div><div class="info-val">${d.anciennete}</div></div></div>`:''}
    <div class="info-row"><div class="info-icon">💬</div><div><div class="info-key">Motif</div><div class="info-val">${d.motif}</div></div></div>
    ${d.motifDetail?`<div class="info-row"><div class="info-icon">📝</div><div><div class="info-key">Précisions</div><div class="info-val">${d.motifDetail}</div></div></div>`:''}
    <div class="info-row"><div class="info-icon">📅</div><div><div class="info-key">Date de soumission</div><div class="info-val">${formatDate(d.date)}</div></div></div>

    <div style="display:flex;gap:10px;margin-top:20px">
      <button class="btn btn-whatsapp" style="flex:1" onclick="contactWA('${d.id}')">💬 Contacter sur WhatsApp</button>
      ${d.telephone?`<button class="btn btn-outline" onclick="window.open('tel:${d.telephone}')">📞</button>`:''}
    </div>
  `;
  document.getElementById('detail-modal').classList.remove('hidden');
}

function closeModal(e){
  if(e.target.id==='detail-modal')
    document.getElementById('detail-modal').classList.add('hidden');
}

/* =========================================
   TOAST
   ========================================= */
function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 2800);
}

/* =========================================
   INIT SEARCH PAGE
   ========================================= */
document.addEventListener('DOMContentLoaded', ()=>{
  renderSearch();
});
</script>
</body>
</html>
