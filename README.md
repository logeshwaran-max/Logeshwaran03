<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Logeshwaran A — Aspiring Film Director</title>
<meta name="description" content="Logeshwaran &amp; Creative Storyteller. Cinematic stories. Real emotions. Powerful impact.">

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Space+Mono:wght@400;700&family=Outfit:wght@300;400;500;600;700&family=Noto+Sans+JP:wght@300;500;700&display=swap" rel="stylesheet">

<style>
body::before{
  content:"";
  position:fixed;
  inset:0;
  background:
    radial-gradient(circle at 20% 20%, rgba(255,0,0,0.25), transparent 40%),
    radial-gradient(circle at 80% 80%, rgba(255,0,0,0.15), transparent 40%),
    repeating-linear-gradient(0deg, rgba(255,0,0,0.08) 0px, transparent 2px),
    repeating-linear-gradient(90deg, rgba(255,0,0,0.08) 0px, transparent 2px);
  z-index:-1;
}

/* ============================================================
   RESET
============================================================ */
*,*::before,*::after{box-sizing:border-box;}
html,body{margin:0;padding:0;}
html{-webkit-text-size-adjust:100%;}

ul{margin:0;padding:0;list-style:none;}
a{color:inherit;text-decoration:none;}
button{font-family:inherit;background:none;border:none;color:inherit;cursor:pointer;}
img,svg{display:block;max-width:100%;}

/* ========body{
  background:black;
  overflow:hidden;
}

body::before{
  content:"";
  position:fixed;
  inset:0;
  background:
    radial-gradient(circle at 20% 20%, rgba(255,0,0,0.25), transparent 40%),
    radial-gradient(circle at 80% 80%, rgba(255,0,0,0.15), transparent 40%),
    repeating-linear-gradient(0deg, rgba(255,0,0,0.08) 0px, transparent 2px),
    repeating-linear-gradient(90deg, rgba(255,0,0,0.08) 0px, transparent 2px);
  z-index:-1;
}====================================================
   TOKENS
============================================================ */
:root{
  --black:#020203;
  --panel:#0c0c0e;
  --red:#ff1635;
  --red-2:#ff4d5e;
  --red-soft:rgba(255,22,53,.45);
  --white:#f3f1ec;
  --muted:#97968f;
  --line:rgba(255,255,255,.09);
  --glass:rgba(255,255,255,.04);
  --glass-bd:rgba(255,255,255,.12);
  --mono:'Space Mono',monospace;
  --display:'Anton',sans-serif;
  --body:'Outfit',sans-serif;
  --jp:'Noto Sans JP',sans-serif;
  --frame-inset:12px;
  --frame-radius:30px;
  --ease:cubic-bezier(.22,1,.36,1);
}
@media (max-width:720px){
  :root{ --frame-inset:6px; --frame-radius:20px; }
}

/* ============================================================
   FIXED BACKDROP (grid / grain / vignette) — sits behind the
   scrolling frame content, matched exactly to the frame bounds
============================================================ */
.backdrop{
  position:fixed;
  inset:var(--frame-inset);
  border-radius:var(--frame-radius);
  overflow:hidden;
  z-index:0;
  background:var(--black);
  pointer-events:none;
}
.backdrop::before{ /* vertical grid lines */
  content:"";
  position:absolute;
  inset:0;
  background-image:repeating-linear-gradient(
    90deg,
    transparent 0,
    transparent 87px,
    var(--line) 87px,
    var(--line) 88px
  );
  opacity:.55;
}
.backdrop::after{ /* radial vignette */
  content:"";
  position:absolute;
  inset:-10%;
  background:
    radial-gradient(60% 50% at 18% 8%, rgba(255,22,53,.16), transparent 60%),
    radial-gradient(50% 40% at 100% 100%, rgba(255,22,53,.10), transparent 65%),
    radial-gradient(120% 90% at 50% 50%, transparent 40%, #000 100%);
}
.grain{
  position:absolute;inset:0;
  opacity:.05;
  mix-blend-mode:overlay;
  background-image:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='160' height='160'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
  animation:grain 1s steps(2) infinite;
}
@keyframes grain{ 0%{transform:translate(0,0);} 50%{transform:translate(-1%,1%);} 100%{transform:translate(1%,-1%);} }

/* kanji decorations, parallax-driven (set via JS transform) */
.kanji{
  position:absolute;
  font-family:var(--jp);
  font-weight:300;
  writing-mode:vertical-rl;
  letter-spacing:.3em;
  color:rgba(255,255,255,.05);
  white-space:nowrap;
  pointer-events:none;
  user-select:none;
  z-index:1;
  font-size:clamp(2.4rem,7vw,5.6rem);
}
.kanji.is-red{ color:rgba(255,22,53,.10); }

/* ============================================================
   FRAME — the rounded white outer border + scroll container
============================================================ */
.frame{
  position:fixed;
  inset:var(--frame-inset);
  border-radius:var(--frame-radius);
  border:1px solid rgba(245,243,238,.55);
  box-shadow:0 0 0 1px rgba(255,255,255,.03), 0 40px 120px rgba(0,0,0,.8);
  overflow-y:auto;
  overflow-x:hidden;
  -webkit-overflow-scrolling:touch;
  z-index:2;
  background:transparent;
  scroll-behavior:smooth;
}
.frame::-webkit-scrollbar{ width:5px; }
.frame::-webkit-scrollbar-track{ background:transparent; }
.frame::-webkit-scrollbar-thumb{ background:var(--red); border-radius:6px; }

.content{ position:relative; min-height:100%; }

/* ============================================================
   LOADER
============================================================ */
.loader{
  position:fixed; inset:0; z-index:9999;
  background:#000;
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  gap:28px;
  transition:transform 1s var(--ease), opacity .8s ease;
}
.loader.is-done{ transform:translateY(-100%); opacity:.4; pointer-events:none; }
.loader-mark{
  font-family:var(--display);
  font-size:clamp(2.4rem,9vw,4.2rem);
  letter-spacing:.02em;
  color:var(--white);
  display:flex; gap:.25em;
  overflow:hidden;
}
.loader-mark span{
  display:inline-block;
  transform:translateY(110%);
  animation:rise .7s var(--ease) forwards;
}
.loader-mark span:nth-child(2){ color:var(--red); animation-delay:.08s; }
@keyframes rise{ to{ transform:translateY(0); } }
.loader-bar-wrap{
  width:min(280px,60vw);
  height:1px;
  background:var(--line);
  position:relative;
}
.loader-bar{
  position:absolute; left:0; top:0; bottom:0;
  width:0%;
  background:var(--red);
  box-shadow:0 0 12px var(--red-soft);
  transition:width .15s linear;
}
.loader-meta{
  display:flex; justify-content:space-between; width:min(280px,60vw);
  font-family:var(--mono); font-size:.68rem; letter-spacing:.15em; color:var(--muted);
  text-transform:uppercase;
}
.loader-pct{ color:var(--red); }

/* ============================================================
   CUSTOM CURSOR
============================================================ */
.cursor-dot,.cursor-ring{
  position:fixed; top:0; left:0;
  pointer-events:none; z-index:9998;
  border-radius:50%;
  transform:translate(-50%,-50%);
  will-change:transform;
}
.cursor-dot{ width:5px; height:5px; background:var(--red); }
.cursor-ring{
  width:34px; height:34px;
  border:1px solid rgba(255,22,53,.55);
  transition:width .25s var(--ease),height .25s var(--ease),border-color .25s var(--ease),background .25s var(--ease);
}
.cursor-ring.is-active{
  width:64px; height:64px;
  background:rgba(255,22,53,.08);
  border-color:var(--red);
}
@media (pointer:coarse){
  .cursor-dot,.cursor-ring{ display:none; }
}

/* ============================================================
   TIMECODE HUD (signature cinematic element)
============================================================ */
.hud{
  position:fixed;
  top:calc(var(--frame-inset) + 22px);
  right:calc(var(--frame-inset) + 26px);
  z-index:50;
  display:flex; align-items:center; gap:10px;
  font-family:var(--mono);
  font-size:.72rem;
  letter-spacing:.12em;
  color:var(--muted);
  pointer-events:none;
  mix-blend-mode:difference;
}
.hud .rec{
  width:6px;height:6px;border-radius:50%;background:var(--red);
  animation:blink 1.4s ease-in-out infinite;
  box-shadow:0 0 8px var(--red);
}
@keyframes blink{ 0%,100%{opacity:1;} 50%{opacity:.15;} }
.hud .tc{ color:var(--white); }
@media (max-width:600px){ .hud{ display:none; } }

/* ============================================================
   LEFT FLOATING NAV (becomes bottom bar on mobile)
============================================================ */
.nav{
  position:fixed;
  left:calc(var(--frame-inset) + 28px);
  top:50%;
  transform:translateY(-50%);
  z-index:60;
  display:flex; flex-direction:column; align-items:center;
  gap:22px;
  padding:18px 12px;
  border-radius:999px;
  background:var(--glass);
  border:1px solid var(--glass-bd);
  backdrop-filter:blur(14px) saturate(140%);
  -webkit-backdrop-filter:blur(14px) saturate(140%);
}
.nav-logo{
  font-family:var(--mono);
  font-size:.62rem;
  letter-spacing:.2em;
  color:var(--muted);
  writing-mode:vertical-rl;
  margin-bottom:6px;
}
.nav-link{
  position:relative;
  width:9px;height:9px;
  border-radius:50%;
  background:rgba(255,255,255,.25);
  transition:background .3s var(--ease), transform .3s var(--ease);
}
.nav-link::after{
  content:attr(data-label);
  position:absolute;
  left:22px; top:50%;
  transform:translateY(-50%) translateX(-6px);
  font-family:var(--mono);
  font-size:.64rem;
  letter-spacing:.18em;
  color:var(--white);
  white-space:nowrap;
  text-transform:uppercase;
  opacity:0;
  transition:opacity .25s var(--ease), transform .25s var(--ease);
  background:rgba(10,10,10,.7);
  padding:4px 10px;
  border-radius:4px;
  border:1px solid var(--glass-bd);
}
.nav-link:hover::after{ opacity:1; transform:translateY(-50%) translateX(0); }
.nav-link:hover{ background:rgba(255,255,255,.6); }
.nav-link.is-active{ background:var(--red); box-shadow:0 0 10px var(--red-soft); transform:scale(1.25); }
.nav-line{ width:1px; height:26px; background:var(--line); }

@media (max-width:720px){
  .nav{
    left:50%; top:auto; bottom:calc(var(--frame-inset) + 14px);
    transform:translateX(-50%);
    flex-direction:row;
    padding:12px 18px;
    gap:18px;
  }
  .nav-logo{ display:none; }
  .nav-line{ width:18px; height:1px; }
  .nav-link::after{ display:none; }
}

/* ============================================================
   SHARED LAYOUT
============================================================ */
.section{
  position:relative;
  min-height:100vh;
  padding:120px 9vw 100px;
  display:flex;
  flex-direction:column;
  justify-content:center;
  border-bottom:1px solid var(--line);
}
.section-inner{ position:relative; z-index:3; width:100%; max-width:1180px; margin:0 auto; }
.eyebrow{
  display:flex; align-items:center; gap:14px;
  font-family:var(--mono);
  font-size:.74rem;
  letter-spacing:.28em;
  text-transform:uppercase;
  color:var(--red);
  margin-bottom:26px;
}
.eyebrow::before{ content:""; width:26px; height:1px; background:var(--red); }
.sec-title{
  font-family:var(--display);
  font-weight:400;
  text-transform:uppercase;
  line-height:.94;
  letter-spacing:.01em;
  color:var(--white);
  font-size:clamp(2.6rem,7vw,5.2rem);
  margin:0 0 28px;
}

.reveal{ opacity:0; transform:translateY(34px); transition:opacity .9s var(--ease), transform .9s var(--ease); }
.reveal.is-visible{ opacity:1; transform:translateY(0); }
.reveal-delay-1{ transition-delay:.08s; }
.reveal-delay-2{ transition-delay:.16s; }
.reveal-delay-3{ transition-delay:.24s; }

/* ============================================================
   HOME
============================================================ */
.home{ padding-top:140px; }
.home-frame-no{
  font-family:var(--mono); font-size:.74rem; letter-spacing:.2em; color:var(--muted);
  display:flex; gap:18px; align-items:center; margin-bottom:34px; text-transform:uppercase;
}
.home-frame-no span{ color:var(--red); }
.hero-title{
  font-family:var(--display);
  text-transform:uppercase;
  font-size:clamp(3.4rem,15vw,10.5rem);
  line-height:.86;
  letter-spacing:.01em;
  margin:0;
  color:var(--white);
}
.hero-title .accent{
  color:var(--red);
  text-shadow:0 0 24px var(--red-soft), 0 0 60px rgba(255,22,53,.25);
}
.hero-bottom{
  display:flex; flex-wrap:wrap; align-items:flex-end; justify-content:space-between;
  gap:40px; margin-top:46px;
}
.hero-sub{
  font-family:var(--mono);
  font-size:clamp(.9rem,1.6vw,1.05rem);
  letter-spacing:.12em;
  text-transform:uppercase;
  color:var(--white);
  margin:0 0 14px;
}
.hero-sub::before{ content:"// "; color:var(--red); }
.hero-desc{
  max-width:420px;
  font-size:1.02rem;
  line-height:1.7;
  color:var(--muted);
  margin:0;
}
.hero-cta{ display:flex; gap:16px; flex-wrap:wrap; }
.btn{
  font-family:var(--mono);
  font-size:.78rem;
  letter-spacing:.16em;
  text-transform:uppercase;
  padding:16px 30px;
  border-radius:999px;
  display:inline-flex; align-items:center; gap:10px;
  transition:transform .35s var(--ease), background .35s var(--ease), color .35s var(--ease), border-color .35s var(--ease);
}
.btn-solid{ background:var(--red); color:#100002; }
.btn-solid:hover{ transform:translateY(-3px); box-shadow:0 14px 30px rgba(255,22,53,.32); }
.btn-ghost{ border:1px solid var(--glass-bd); color:var(--white); background:var(--glass); backdrop-filter:blur(10px); }
.btn-ghost:hover{ border-color:var(--red); color:var(--red); transform:translateY(-3px); }

.scroll-cue{
  position:absolute; bottom:46px; left:9vw;
  display:flex; align-items:center; gap:12px;
  font-family:var(--mono); font-size:.66rem; letter-spacing:.22em; color:var(--muted); text-transform:uppercase;
}
.scroll-cue .line{ width:1px; height:40px; background:linear-gradient(var(--red),transparent); position:relative; overflow:hidden; }
.scroll-cue .line::after{
  content:""; position:absolute; top:-40px; left:0; width:100%; height:40px; background:var(--white);
  animation:cue 2.2s ease-in-out infinite;
}
@keyframes cue{ 0%{ top:-40px; } 60%{ top:40px; } 100%{ top:40px; } }

/* ============================================================
   ABOUT
============================================================ */
.about-grid{
  display:grid; grid-template-columns:1.2fr .8fr; gap:70px; align-items:start;
}
.about-text p{
  font-size:1.06rem; line-height:1.85; color:#cfcdc6; max-width:620px; margin:0 0 22px;
}
.about-text strong{ color:var(--white); font-weight:600; }
.about-quote{
  margin:34px 0 0;
  padding-left:22px;
  border-left:2px solid var(--red);
  font-family:var(--display);
  font-size:clamp(1.2rem,2.4vw,1.7rem);
  line-height:1.3;
  text-transform:uppercase;
  color:var(--white);
}
.about-quote span{ display:block; font-family:var(--mono); font-size:.68rem; letter-spacing:.18em; color:var(--muted); margin-top:14px; text-transform:uppercase; }

.skills-label{ font-family:var(--mono); font-size:.7rem; letter-spacing:.2em; color:var(--muted); text-transform:uppercase; margin-bottom:18px; }
.skills{ display:flex; flex-direction:column; gap:0; border-top:1px solid var(--line); }
.skill-row{
  display:flex; align-items:center; gap:18px;
  padding:16px 6px;
  border-bottom:1px solid var(--line);
  transition:padding-left .35s var(--ease), color .35s var(--ease);
}
.skill-row:hover{ padding-left:14px; color:var(--red); }
.skill-row .no{ font-family:var(--mono); font-size:.72rem; color:var(--red); width:28px; flex-shrink:0; }
.skill-row .name{ font-size:.98rem; letter-spacing:.02em; }

/* ============================================================
   PROJECTS
============================================================ */
.projects-list{ display:flex; flex-direction:column; gap:1px; margin-top:10px; }
.project-card{
  position:relative;
  display:grid;
  grid-template-columns:90px 1fr auto;
  align-items:center;
  gap:34px;
  padding:38px 26px;
  border:1px solid var(--line);
  border-radius:18px;
  margin-bottom:18px;
  background:var(--glass);
  backdrop-filter:blur(12px) saturate(140%);
  -webkit-backdrop-filter:blur(12px) saturate(140%);
  overflow:hidden;
  transition:border-color .4s var(--ease), transform .4s var(--ease), background .4s var(--ease);
}
.project-card::before{
  content:""; position:absolute; inset:0;
  background:radial-gradient(420px 200px at var(--mx,50%) var(--my,50%), rgba(255,22,53,.14), transparent 65%);
  opacity:0; transition:opacity .4s var(--ease); pointer-events:none;
}
.project-card:hover{ border-color:rgba(255,22,53,.45); transform:translateY(-4px); }
.project-card:hover::before{ opacity:1; }
.project-no{
  font-family:var(--mono); font-size:.78rem; color:var(--muted); letter-spacing:.1em;
}
.project-icon{
  width:42px; height:42px; color:var(--red); opacity:.9;
}
.project-main h3{
  font-family:var(--display); text-transform:uppercase; font-size:clamp(1.3rem,2.6vw,2rem);
  margin:0 0 10px; color:var(--white); letter-spacing:.01em;
}
.project-main p{ margin:0; color:var(--muted); font-size:.96rem; line-height:1.6; max-width:520px; }
.project-status{
  font-family:var(--mono); font-size:.66rem; letter-spacing:.14em; text-transform:uppercase;
  color:var(--red); border:1px solid rgba(255,22,53,.4); padding:7px 14px; border-radius:999px;
  white-space:nowrap; justify-self:end;
}
.project-status.is-quiet{ color:var(--muted); border-color:var(--glass-bd); }

@media (max-width:760px){
  .project-card{ grid-template-columns:1fr; text-align:left; gap:14px; padding:28px 22px; }
  .project-status{ justify-self:start; }
}

/* ============================================================
   CONTACT
============================================================ */
.contact-grid{ display:flex; flex-direction:column; gap:50px; }
.contact-lead{ max-width:560px; color:var(--muted); font-size:1.05rem; line-height:1.8; }
.contact-links{ display:flex; flex-direction:column; }
.contact-link{
  display:flex; justify-content:space-between; align-items:center;
  padding:26px 6px;
  border-top:1px solid var(--line);
  font-family:var(--display);
  text-transform:uppercase;
  font-size:clamp(1.5rem,4vw,2.6rem);
  color:var(--white);
  transition:color .35s var(--ease), padding-left .35s var(--ease);
}
.contact-link:last-child{ border-bottom:1px solid var(--line); }
.contact-link:hover{ color:var(--red); padding-left:14px; }
.contact-link .tag{
  font-family:var(--mono); font-size:.7rem; letter-spacing:.16em; color:var(--muted); text-transform:uppercase;
}
.contact-link .arrow{ font-family:var(--mono); font-size:1.4rem; transform:translateX(0); transition:transform .35s var(--ease); }
.contact-link:hover .arrow{ transform:translateX(8px); color:var(--red); }

/* ============================================================
   FOOTER
============================================================ */
.footer{
  padding:46px 9vw 60px;
  display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:16px;
  font-family:var(--mono); font-size:.68rem; letter-spacing:.12em; color:var(--muted); text-transform:uppercase;
}
.footer a{ color:var(--white); transition:color .3s var(--ease); }
.footer a:hover{ color:var(--red); }

@media (prefers-reduced-motion: reduce){
  *{ animation-duration:.001ms !important; animation-iteration-count:1 !important; transition-duration:.001ms !important; scroll-behavior:auto !important; }
}

@media (max-width:720px){
  .section{ padding:100px 7vw 80px; }
  .about-grid{ grid-template-columns:1fr; gap:50px; }
}
</style>
</head>
<body>

  <!-- 🕷️ BACKGROUND -->
  body::before (CSS)

  <!-- 🕷️ HOME -->
  <section id="home">
     <img src="logesh.jpg.jpeg" alt="Profile Photo">
  </section>

  <!-- ABOUT -->
  <section id="about">...</section>

  <!-- PROJECTS -->
  <section id="projects">...</section>

<!-- LOADER -->
 <div class="loader" id="loader">
  <div class="loader-mark">
    <span>LOGE</span><span>SH</span>
  </div>
  <div class="loader-bar-wrap"><div class="loader-bar" id="loaderBar"></div></div>
  <div class="loader-meta">
    <span>LOADING REEL</span>
    <span class="loader-pct" id="loaderPct">0%</span>
  </div>
</div>
<!-- FIXED BACKDROP -->
<div class="backdrop"><div class="grain"></div></div>

<!-- CUSTOM CURSOR -->
<div class="cursor-dot" id="cursorDot"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- TIMECODE HUD -->
<div class="hud"><span class="rec"></span><span>REC</span><span class="tc" id="hudTime">00:00:00:00</span></div>

<!-- LEFT NAV -->
<nav class="nav" id="siteNav">
  <span class="nav-logo">LOGESH / 01</span>
  <a href="#home" class="nav-link is-active" data-target="home" data-label="Home"></a>
  <span class="nav-line"></span>
  <a href="#about" class="nav-link" data-target="about" data-label="About"></a>
  <span class="nav-line"></span>
  <a href="#projects" class="nav-link" data-target="projects" data-label="Projects"></a>
  <span class="nav-line"></span>
  <a href="#contact" class="nav-link" data-target="contact" data-label="Contact"></a>
</nav>

<!-- FRAME -->
<div class="frame" id="frame">
  <div class="content">

    <!-- HOME -->
    <section class="section home" id="home">
      <span class="kanji is-red" style="top:8%; left:4%;" data-speed="0.06">夢</span>
      <span class="kanji" style="top:30%; right:6%;" data-speed="0.1">映画</span>
      <span class="kanji is-red" style="bottom:6%; left:46%;" data-speed="0.04">物語</span>

      <div class="section-inner">
        <div class="home-frame-no reveal">FRAME <span>001</span> — TAMIL NADU, INDIA</div>
        <h1 class="hero-title reveal reveal-delay-1">I'M<br><span class="accent">LOGESH</span></h1>

        <div class="hero-bottom">
          <div class="reveal reveal-delay-2">
            <p class="hero-sub">Aspiring Film Director</p>
            <p class="hero-desc">Cyber Security Student | Technology & Coding Enthusiast | Learning Programming & Cybersecurity</p>
          </div>
          <div class="hero-cta reveal reveal-delay-3">
            <a href="#projects" class="btn btn-solid" data-hover>View Work</a>
            <a href="#contact" class="btn btn-ghost" data-hover> Contact us</a>
          </div>
        </div>
      </div>

      <div class="scroll-cue"><span class="line"></span>CLG:RD NATIONAL COLLEGE OF A/S <BR>ADDRESS:SURAMPATTI VALASU,ERODE</div>
    </section>SCIENCE

    <!-- ABOUT -->
    <section class="section" id="about">
      <span class="kanji" style="top:10%; right:4%;" data-speed="0.08">感情</span>
      <div class="section-inner">
        <p class="eyebrow reveal">About / 17 Years Old</p>
        <h2 class="sec-title reveal">Behind<br>The Lens</h2>

        <div class="about-grid">
          <div class="about-text reveal reveal-delay-1">
            <p>I am <strong>Logeshwaran</strong>, a 17-year-old aspiring film director from studying in Rd National College of Arts & Science in Erode. I'm passionate about storytelling, screenplay writing, filmmaking, and creating emotional experiences through cinema.</p>
            <p>Inspired by director <strong>Lokesh Kanagaraj</strong>, I dream of directing films that connect deeply with audiences — stories that linger long after the credits roll.</p>
            <p>Alongside filmmaking, I'm learning technology and building creative digital projects — because every great story today needs a great way to be told.</p>
            <p>🏅 Honored to receive the "Most Promising Developer" Award from RD National College of Arts & Science. I sincerely thank our Chairman, Mr. Rahul sir and the entire institution for their support, encouragement, and belief in young innovators. This recognition inspires me to continue learning, building, and growing as a developer while striving for greater achievements in the future. 🚀✨</p>
            <div class="about-quote">
              "Cinema isn't made of frames. It's made of feeling."
              <span>— a belief I'm building my work around</span>
            </div>
          </div>

          <div class="reveal reveal-delay-2">
            <p class="skills-label">Interested Skills / 08</p>
            <div class="skills">
              <div class="skill-row"><span class="no">01</span><span class="name">Story Writing</span></div>
              <div class="skill-row"><span class="no">02</span><span class="name">Screenplay Writing</span></div>
              <div class="skill-row"><span class="no">03</span><span class="name">Film Direction</span></div>
              <div class="skill-row"><span class="no">04</span><span class="name">Short Film Creater</span></div>
              <div class="skill-row"><span class="no">05</span><span class="name">Creative Thinking</span></div>
              <div class="skill-row"><span class="no">06</span><span class="name">Video Editing</span></div>
              <div class="skill-row"><span class="no">07</span><span class="name">Learning of macOS</span></div>
              <div class="skill-row"><span class="no">08</span><span class="name">Basic Web Development</span></div>
            </div>
          </div>
        </div>
      </div>
    </section>
      
   <!-- PROJECTS -->
    <section class="section" id="projects">
      <span class="kanji is-red" style="bottom:8%; right:5%;" data-speed="0.07">創造</span>
      <div class="section-inner">
        <p class="eyebrow reveal">Selected Work / 03</p>
        <h2 class="sec-title reveal">Projects</h2>
        

       <div class="projects-list">

          <div class="project-card reveal" data-hover>
            <span class="project-no">01</span>
            <div class="project-main">
              <h3>Thanimaiyil Thelivu</h3>
              <p>A short film about friendship, loneliness, misunderstanding, realization, and emotional connection.</p>
            </div>
            <span class="project-status">In Development</span>
            <svg class="project-icon" style="display:none;" viewBox="0 0 48 48"></svg>
          </div>

          <div class="project-card reveal reveal-delay-1" data-hover>
            <span class="project-no">02</span>
            <div class="project-main">
              <h3>Director Journey</h3>
              <p>A personal creative project documenting my path toward becoming a film director.</p>
            </div>
            <span class="project-status is-quiet">Ongoing</span>
          </div>

          <div class="project-card reveal reveal-delay-2" data-hover>
            <span class="project-no">03</span>
            <div class="project-main">
              <h3>Portfolio Website</h3>
              <p>A futuristic personal portfolio showcasing my journey, projects, and creative vision.</p>
            </div>
            <span class="project-status is-quiet">Live</span>
          </div>

        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section class="section" id="contact">
      <span class="kanji" style="top:12%; left:5%;" data-speed="0.05">未来</span>
      <div class="section-inner">
        <p class="eyebrow reveal">Contact Us</p>
        <h2 class="sec-title reveal">Let's Create<br>Something Real</h2>
        <p class="contact-lead reveal reveal-delay-1">Have a story to tell, a project in mind, or just want to talk cinema? I'd love to hear from you.</p>

        <div class="contact-links reveal reveal-delay-2">
          <a href="https://www.instagram.com/logexh_.x3?igsh=N2ppcm01YmxscmZl" class="contact-link" target="_blank" rel="noopener" data-hover>
           Instagram <span class="tag">@logesh._x3</span><span class="arrow">→</span>
          </a>
          <a href="https://www.linkedin.com/in/logeshwaran-a-2330a2414?utm_source=share_via&utm_content=profile&utm_medium=member_android" class="contact-link" target="_blank" rel="noopener" data-hover>
            Linkedin<span class="tag">Logeshwaran A</span><span class="arrow">→</span>
          </a>
          <a href="mailto:skynetlogeshwaran@gmail.com" class="contact-link" data-hover>
            Email <span class="tag">skynetlogeshwaran@gmail.com</span><span class="arrow">→</span>
          </a>
          <a href="https://wa.me/918248926823" class="contact-link" target="_blank" rel="noopener" data-hover>
            WhatsApp <span class="tag">8248926823</span><span class="arrow">→</span>
          </a>
        </div>
      </div>
    </section>

    <footer class="footer">
      <span>© 2026 Logeshwaran A — All Stories Reserved</span>
      <a href="#home">Back to Top ↑</a>
    </footer>

  </div>
</div>

<script>
(function(){
  "use strict";
  var reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  var isFinePointer = window.matchMedia('(pointer: fine)').matches;
  var frame = document.getElementById('frame');

  /* ---------- LOADER ---------- */
  var loader = document.getElementById('loader');
  var bar = document.getElementById('loaderBar');
  var pct = document.getElementById('loaderPct');
  var progress = 0;

  function tickLoader(){
    progress += Math.random() * 14 + 6;
    if(progress >= 100){
      progress = 100;
      bar.style.width = '100%';
      pct.textContent = '100%';
      setTimeout(function(){
        loader.classList.add('is-done');
        document.body.style.overflow = '';
      }, 280);
      return;
    }
    bar.style.width = progress + '%';
    pct.textContent = Math.floor(progress) + '%';
    setTimeout(tickLoader, reduceMotion ? 10 : (Math.random()*150 + 80));
  }
  tickLoader();

  /* ---------- CUSTOM CURSOR ---------- */
  if(isFinePointer && !reduceMotion){
    var dot = document.getElementById('cursorDot');
    var ring = document.getElementById('cursorRing');
    var mx=0,my=0,rx=0,ry=0;
    window.addEventListener('mousemove', function(e){
      mx = e.clientX; my = e.clientY;
      dot.style.transform = 'translate('+mx+'px,'+my+'px) translate(-50%,-50%)';
    });
    function loop(){
      rx += (mx-rx)*0.16; ry += (my-ry)*0.16;
      ring.style.transform = 'translate('+rx+'px,'+ry+'px) translate(-50%,-50%)';
      requestAnimationFrame(loop);
    }
    loop();
    document.querySelectorAll('[data-hover]').forEach(function(el){
      el.addEventListener('mouseenter', function(){ ring.classList.add('is-active'); });
      el.addEventListener('mouseleave', function(){ ring.classList.remove('is-active'); });
    });
  } else {
    document.getElementById('cursorDot').style.display='none';
    document.getElementById('cursorRing').style.display='none';
  }

  /* ---------- TIMECODE HUD ---------- */
  var hudTime = document.getElementById('hudTime');
  function pad(n){ return (n<10?'0':'')+n; }
  function updateHud(){
    var d = new Date();
    var ff = Math.floor((d.getMilliseconds()/1000)*24);
    hudTime.textContent = pad(d.getHours())+':'+pad(d.getMinutes())+':'+pad(d.getSeconds())+':'+pad(ff);
    requestAnimationFrame(updateHud);
  }
  if(!reduceMotion){ updateHud(); } else {
    hudTime.textContent = '--:--:--:--';
  }

  /* ---------- SCROLL REVEAL ---------- */
  var revealEls = document.querySelectorAll('.reveal');
  if('IntersectionObserver' in window){
    var io = new IntersectionObserver(function(entries){
      entries.forEach(function(entry){
        if(entry.isIntersecting){
          entry.target.classList.add('is-visible');
          io.unobserve(entry.target);
        }
      });
    }, { threshold:0.15 });
    revealEls.forEach(function(el){ io.observe(el); });
  } else {
    revealEls.forEach(function(el){ el.classList.add('is-visible'); });
  }

  /* ---------- ACTIVE NAV TRACKING ---------- */
  var sections = document.querySelectorAll('.section[id]');
  var navLinks = document.querySelectorAll('.nav-link');
  if('IntersectionObserver' in window){
    var navIo = new IntersectionObserver(function(entries){
      entries.forEach(function(entry){
        if(entry.isIntersecting){
          navLinks.forEach(function(l){ l.classList.remove('is-active'); });
          var active = document.querySelector('.nav-link[data-target="'+entry.target.id+'"]');
          if(active) active.classList.add('is-active');
        }
      });
    }, { threshold:0.5 });
    sections.forEach(function(s){ navIo.observe(s); });
  }

  /* ---------- SMOOTH NAV CLICK ---------- */
  navLinks.forEach(function(link){
    link.addEventListener('click', function(e){
      e.preventDefault();
      var target = document.getElementById(link.getAttribute('data-target'));
      if(target) target.scrollIntoView({ behavior: reduceMotion ? 'auto' : 'smooth' });
    });
  });

  /* ---------- KANJI PARALLAX ---------- */
  if(!reduceMotion){
    var kanjis = document.querySelectorAll('.kanji');
    var ticking = false;
    frame.addEventListener('scroll', function(){
      if(!ticking){
        requestAnimationFrame(function(){
          var y = frame.scrollTop;
          kanjis.forEach(function(k){
            var speed = parseFloat(k.getAttribute('data-speed')) || 0.05;
            k.style.transform = 'translateY(' + (y*speed) + 'px)';
          });
          ticking = false;
        });
        ticking = true;
      }
    });
  }

  /* ---------- PROJECT CARD GLOW FOLLOW ---------- */
  document.querySelectorAll('.project-card').forEach(function(card){
    card.addEventListener('mousemove', function(e){
      var r = card.getBoundingClientRect();
      card.style.setProperty('--mx', (e.clientX - r.left) + 'px');
      card.style.setProperty('--my', (e.clientY - r.top) + 'px');
    });
  });

})();
</script>
</body>
</html>
