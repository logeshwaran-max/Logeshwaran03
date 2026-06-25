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

/* ============================================================
   HERO LAYOUT — with profile photo
============================================================ */
.hero-inner{
  display:flex;
  flex-direction:row;
  align-items:center;
  gap:clamp(40px, 6vw, 90px);
  width:100%;
}
.hero-text{ flex:1; min-width:0; }

/* ============================================================
   PROFILE PHOTO
============================================================ */
.profile-photo-wrap{
  flex-shrink:0;
  display:flex;
  align-items:center;
  justify-content:center;
  order:2;
  animation: profileFloat 4.8s ease-in-out infinite;
}

@keyframes profileFloat{
  0%,100%{ transform:translateY(0px); }
  50%{ transform:translateY(-14px); }
}

.profile-photo-ring{
  position:relative;
  width:clamp(200px, 22vw, 300px);
  height:clamp(200px, 22vw, 300px);
  border-radius:50%;
  /* Glassmorphism border */
  background:
    linear-gradient(135deg, rgba(255,22,53,0.35) 0%, rgba(255,255,255,0.06) 40%, rgba(255,22,53,0.2) 100%);
  padding:3px;
  /* Neon red glow — layered for cinematic depth */
  box-shadow:
    0 0 0 1px rgba(255,22,53,0.25),
    0 0 18px 4px rgba(255,22,53,0.55),
    0 0 45px 12px rgba(255,22,53,0.28),
    0 0 90px 24px rgba(255,22,53,0.12),
    inset 0 0 24px rgba(255,22,53,0.08);
  /* Pulse animation on glow */
  animation: profileGlowPulse 3.2s ease-in-out infinite;
}

@keyframes profileGlowPulse{
  0%,100%{
    box-shadow:
      0 0 0 1px rgba(255,22,53,0.25),
      0 0 18px 4px rgba(255,22,53,0.55),
      0 0 45px 12px rgba(255,22,53,0.28),
      0 0 90px 24px rgba(255,22,53,0.12),
      inset 0 0 24px rgba(255,22,53,0.08);
  }
  50%{
    box-shadow:
      0 0 0 1px rgba(255,22,53,0.4),
      0 0 24px 8px rgba(255,22,53,0.7),
      0 0 60px 18px rgba(255,22,53,0.38),
      0 0 110px 32px rgba(255,22,53,0.18),
      inset 0 0 32px rgba(255,22,53,0.12);
  }
}

/* Rotating dashed orbit ring */
.profile-photo-ring::before{
  content:"";
  position:absolute;
  inset:-8px;
  border-radius:50%;
  border:1px dashed rgba(255,22,53,0.3);
  animation: orbitSpin 18s linear infinite;
}

/* Static accent arc */
.profile-photo-ring::after{
  content:"";
  position:absolute;
  inset:-4px;
  border-radius:50%;
  border:1.5px solid transparent;
  border-top-color:rgba(255,22,53,0.7);
  border-right-color:rgba(255,22,53,0.4);
  animation: orbitSpin 6s linear infinite;
}

@keyframes orbitSpin{ to{ transform:rotate(360deg); } }

.profile-photo-inner{
  width:100%;
  height:100%;
  border-radius:50%;
  overflow:hidden;
  /* Glassmorphism inner ring */
  border:1.5px solid rgba(255,255,255,0.1);
  background:var(--panel);
  position:relative;
}

.profile-photo-inner::after{
  content:"";
  position:absolute;
  inset:0;
  border-radius:50%;
  background:
    radial-gradient(ellipse at 30% 20%, rgba(255,22,53,0.08), transparent 55%),
    radial-gradient(ellipse at 70% 80%, rgba(0,0,0,0.3), transparent 50%);
  pointer-events:none;
  z-index:1;
}

.profile-photo-inner img{
  width:100%;
  height:100%;
  object-fit:cover;
  object-position:center top;
  display:block;
  filter:
    contrast(1.05)
    saturate(0.92)
    brightness(0.97);
  transition:filter .6s var(--ease);
}

.profile-photo-wrap:hover .profile-photo-inner img{
  filter:
    contrast(1.08)
    saturate(1.05)
    brightness(1.03);
}

/* Scanline overlay for cinematic effect */
.profile-photo-scanlines{
  position:absolute;
  inset:0;
  border-radius:50%;
  background:repeating-linear-gradient(
    0deg,
    transparent,
    transparent 3px,
    rgba(0,0,0,0.04) 3px,
    rgba(0,0,0,0.04) 4px
  );
  pointer-events:none;
  z-index:2;
}

/* Small corner accent badge */
.profile-photo-badge{
  position:absolute;
  bottom:8%;
  right:4%;
  width:36px;
  height:36px;
  border-radius:50%;
  background:var(--red);
  box-shadow:0 0 16px rgba(255,22,53,0.7);
  display:flex;
  align-items:center;
  justify-content:center;
  font-family:var(--mono);
  font-size:.48rem;
  letter-spacing:.1em;
  color:#fff;
  text-transform:uppercase;
  z-index:3;
  animation: badgePulse 2s ease-in-out infinite;
}
@keyframes badgePulse{
  0%,100%{ transform:scale(1); box-shadow:0 0 16px rgba(255,22,53,0.7); }
  50%{ transform:scale(1.1); box-shadow:0 0 24px rgba(255,22,53,0.9); }
}

/* ============================================================
   RESPONSIVE — stack on mobile
============================================================ */
@media (max-width:900px){
  .hero-inner{
    flex-direction:column;
    align-items:center;
    text-align:center;
  }
  .profile-photo-wrap{ order:0; }
  .profile-photo-ring{
    width:clamp(160px, 42vw, 230px);
    height:clamp(160px, 42vw, 230px);
  }
  .hero-bottom{
    flex-direction:column;
    align-items:center;
  }
  .hero-cta{ justify-content:center; }
  .eyebrow{ justify-content:center; }
}
@media (max-width:540px){
  .profile-photo-ring{
    width:160px;
    height:160px;
  }
  .hero-inner{ gap:28px; }
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
        <div class="hero-inner">

          <!-- TEXT SIDE -->
          <div class="hero-text">
            <div class="home-frame-no reveal">FRAME <span>001</span> — TAMIL NADU, INDIA</div>
            <h1 class="hero-title reveal reveal-delay-1">I'M<br><span class="accent">LOGESHWARAN</span></h1>

            <div class="hero-bottom">
              <div class="reveal reveal-delay-2">
                <p class="hero-sub">Aspiring Film Director</p>
                <p class="hero-desc">Cyber Security Student | Technology & Coding Enthusiast | Learning Programming & Cybersecurity</p>
              </div>
              <div class="hero-cta reveal reveal-delay-3">
                <a href="#projects" class="btn btn-solid" data-hover>View Work</a>
                <a href="#contact" class="btn btn-ghost" data-hover>Contact us</a>
              </div>
            </div>
          </div>

          <!-- PROFILE PHOTO -->
          <div class="profile-photo-wrap reveal reveal-delay-2">
            <div class="profile-photo-ring">
              <div class="profile-photo-inner">
                <img src="data:image/jpeg;base64,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" alt="Logeshwaran A — Aspiring Film Director">
                <div class="profile-photo-scanlines"></div>
              </div>
              <div class="profile-photo-badge">DIR</div>
            </div>
          </div>

        

      <div class="scroll-cue"><span class="line"></span>CLG:RD NATIONAL COLLEGE OF A/S <BR>ADDRESS:SURAMPATTI VALASU,ERODE</div>
      </section>

    <!-- ABOUT -->
    <section class="section" id="about">
      <span class="kanji" style="top:10%; right:4%;" data-speed="0.08">感情</span>
      <div class="section-inner">
        <p class="eyebrow reveal">About / 17 Years Old</p>
        <h2 class="sec-title reveal">Behind<br>The Lens</h2>

        <div class="about-grid">
          <div class="about-text reveal reveal-delay-1">
            <p>I am <strong>Logeshwaran</strong>, an aspiring film director turning emotions into stories, with the endless support of my mom <strong>Malar A</strong> and my bro <strong>Mouneshwaran A</strong>-From Erode to the big screen - that's the dream I'm chasing
 .</p>
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
