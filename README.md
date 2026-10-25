<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jerónimo Zapata Vargas | Estructura de Datos</title>

  <script src="https://cdn.tailwindcss.com"></script>

  <style>
    :root{
      --cyan:#00d9ff;
      --blue:#168cff;
      --purple:#8b5cf6;
      --green:#00e5a8;
      --bg:#020711;
      --panel:rgba(3,14,29,.86);
      --line:rgba(0,217,255,.45);
    }

    *{
      scroll-behavior:smooth;
      box-sizing:border-box
    }

    body{
      margin:0;
      color:#e9f7ff;
      background:#020711;
      font-family:Inter,ui-sans-serif,system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;
      overflow-x:hidden;
    }

    /* Fondo futurista */
    body::before{
      content:"";
      position:fixed;
      inset:0;
      z-index:-5;
      background:
        linear-gradient(
          90deg,
          rgba(1,7,17,.96) 0%,
          rgba(1,7,17,.82) 34%,
          rgba(1,7,17,.42) 70%,
          rgba(1,7,17,.72) 100%
        ),
        none;
      filter:saturate(1.15) contrast(1.05);
    }

    body::after{
      content:"";
      position:fixed;
      inset:0;
      z-index:-4;
      pointer-events:none;
      background:
        linear-gradient(rgba(0,217,255,.025) 1px,transparent 1px),
        linear-gradient(90deg,rgba(0,217,255,.025) 1px,transparent 1px);
      background-size:48px 48px;
      mask-image:linear-gradient(to bottom,black,transparent 95%);
    }

    .scanlines{
      position:fixed;
      inset:0;
      z-index:60;
      pointer-events:none;
      opacity:.06;
      background:repeating-linear-gradient(
        to bottom,
        transparent 0px,
        transparent 3px,
        rgba(0,217,255,.35) 4px
      );
    }

    .glass{
      background:linear-gradient(145deg,rgba(3,19,38,.88),rgba(2,8,20,.82));
      border:1px solid rgba(0,217,255,.38);
      box-shadow:
        0 0 35px rgba(0,140,255,.10),
        inset 0 0 30px rgba(0,217,255,.025);
      backdrop-filter:blur(10px);
    }

    .neon{
      text-shadow:
        0 0 8px rgba(0,217,255,.8),
        0 0 25px rgba(0,140,255,.35);
    }

    .neon-border{
      box-shadow:
        0 0 12px rgba(0,217,255,.18),
        inset 0 0 15px rgba(0,217,255,.04);
    }

    .tech-line{
      height:1px;
      background:linear-gradient(
        90deg,
        transparent,
        var(--cyan),
        transparent
      );
      box-shadow:0 0 10px var(--cyan);
    }

    .corner{
      position:relative;
    }

    .corner::before,
    .corner::after{
      content:"";
      position:absolute;
      width:24px;
      height:24px;
      pointer-events:none;
    }

    .corner::before{
      left:-1px;
      top:-1px;
      border-left:2px solid var(--cyan);
      border-top:2px solid var(--cyan);
    }

    .corner::after{
      right:-1px;
      bottom:-1px;
      border-right:2px solid var(--cyan);
      border-bottom:2px solid var(--cyan);
    }

    .nav{
      background:rgba(1,7,17,.82);
      backdrop-filter:blur(16px);
      border-bottom:1px solid rgba(0,217,255,.28);
    }

    .nav-link{
      position:relative;
      color:#a9dfff;
      transition:.25s;
    }

    .nav-link:hover{
      color:white;
      text-shadow:0 0 10px var(--cyan)
    }

    .nav-link::after{
      content:"";
      position:absolute;
      left:0;
      right:0;
      bottom:-9px;
      height:2px;
      background:var(--cyan);
      transform:scaleX(0);
      transition:.25s;
      box-shadow:0 0 10px var(--cyan);
    }

    .nav-link:hover::after{
      transform:scaleX(1)
    }

    /* =========================================================
       HERO
       ========================================================== */

    .hero{
      min-height:430px;
      position:relative;
      display:flex;
      align-items:center;
      overflow:hidden;
      border-bottom:1px solid rgba(0,217,255,.2);
    }

    /*
      CAMBIO REALIZADO:
      Se elimina únicamente la imagen anterior del fondo.
      La imagen ahora se controla desde .hero-robot-layer
      usando hero-robot.png
    */
    .hero::before{
      content:"";
      position:absolute;
      inset:0;
      background:
        linear-gradient(
          90deg,
          #020711 0%,
          rgba(2,7,17,.96) 27%,
          rgba(2,7,17,.55) 55%,
          rgba(2,7,17,.12) 100%
        );
      opacity:.95;
      z-index:0;
    }

    .hero-grid{
      position:absolute;
      inset:0;
      background-image:
        linear-gradient(rgba(0,217,255,.045) 1px,transparent 1px),
        linear-gradient(90deg,rgba(0,217,255,.045) 1px,transparent 1px);
      background-size:45px 45px;
      mask-image:linear-gradient(
        90deg,
        black,
        transparent 85%
      );
      pointer-events:none;
      z-index:1;
    }

    .status-dot{
      width:9px;
      height:9px;
      border-radius:50%;
      background:#00f0a8;
      box-shadow:0 0 10px #00f0a8;
      display:inline-block;
    }

    .tag{
      border:1px solid rgba(0,217,255,.55);
      background:rgba(0,217,255,.06);
      color:#6fe7ff;
      padding:.28rem .65rem;
      border-radius:.45rem;
      font-size:.72rem;
      font-weight:700;
      letter-spacing:.05em;
    }

    .section-title{
      letter-spacing:.02em;
      font-weight:800;
    }

    .unit-card{
      position:relative;
      overflow:hidden;
      transition:.3s ease;
    }

    .unit-card:hover{
      transform:translateY(-5px);
      border-color:var(--cyan);
      box-shadow:0 0 28px rgba(0,217,255,.15);
    }

    .unit-card::after{
      content:"";
      position:absolute;
      left:-40%;
      top:0;
      width:30%;
      height:100%;
      transform:skewX(-18deg);
      background:linear-gradient(
        90deg,
        transparent,
        rgba(255,255,255,.08),
        transparent
      );
      transition:.6s;
    }

    .unit-card:hover::after{
      left:120%
    }

    .code-box{
      background:#01050c;
      border:1px solid rgba(0,217,255,.25);
      color:#8feaff;
      font-family:"Courier New",monospace;
    }

    .activity{
      cursor:pointer;
      transition:.3s;
    }

    .activity:hover{
      transform:translateY(-3px);
      border-color:#00d9ff;
      box-shadow:0 0 22px rgba(0,217,255,.12);
    }

    .modal-bg{
      position:fixed;
      inset:0;
      z-index:100;
      display:none;
      align-items:center;
      justify-content:center;
      padding:1rem;
      background:rgba(0,0,0,.78);
      backdrop-filter:blur(8px);
    }

    .modal-bg.active{
      display:flex
    }

    .modal-box{
      width:min(760px,100%);
      max-height:90vh;
      overflow:auto;
      background:linear-gradient(145deg,#06172c,#020711);
      border:1px solid rgba(0,217,255,.55);
      box-shadow:0 0 50px rgba(0,170,255,.18);
    }

    .btn{
      display:inline-flex;
      align-items:center;
      justify-content:center;
      gap:.5rem;
      border:1px solid var(--cyan);
      color:#c9f7ff;
      background:rgba(0,217,255,.055);
      transition:.25s;
    }

    .btn:hover{
      color:white;
      background:rgba(0,217,255,.14);
      box-shadow:0 0 18px rgba(0,217,255,.22);
      transform:translateY(-1px);
    }

    .pulse{
      animation:pulse 2.8s ease-in-out infinite;
    }

    @keyframes pulse{
      0%,100%{opacity:.65}
      50%{opacity:1}
    }

    .float{
      animation:float 6s ease-in-out infinite;
    }

    @keyframes float{
      0%,100%{transform:translateY(0)}
      50%{transform:translateY(-7px)}
    }

    /* ===== MEJORAS V2: IA / ROBOT / NEÓN ===== */

    .particles-canvas{
      position:fixed;
      inset:0;
      width:100%;
      height:100%;
      z-index:-3;
      pointer-events:none;
      opacity:.7;
    }

    /*
      CAPA DEL ROBOT
      La imagen que se utiliza es:
      hero-robot.png
    */

    .hero-robot-layer{
      position:absolute;
      right:0;
      top:0;
      width:min(68%,900px);
      height:100%;
      pointer-events:none;
      z-index:2;
      overflow:hidden;
    }

    .hero-robot-layer::before{
      content:"";
      position:absolute;
      inset:0;
      background:
        linear-gradient(
          90deg,
          #020711 0%,
          rgba(2,7,17,.72) 20%,
          rgba(2,7,17,.08) 65%,
          rgba(2,7,17,.16) 100%
        );
      z-index:2;
    }

    .hero-robot-layer::after{
      content:"";
      position:absolute;
      inset:0;
      background:
        radial-gradient(
          circle at 72% 50%,
          rgba(0,140,255,.18),
          transparent 48%
        );
      z-index:0;
      pointer-events:none;
    }

    .robot-image{
      position:absolute;
      right:-20px;
      top:50%;
      width:min(850px,100%);
      max-width:none;
      height:100%;
      object-fit:contain;
      object-position:center right;
      transform:translateY(-50%);
      filter:drop-shadow(0 0 22px rgba(0,180,255,.25));
      animation:
        robotEntrance 1.4s cubic-bezier(.2,.8,.2,1) both,
        robotFloat 6s ease-in-out 1.4s infinite;
      z-index:1;
    }

    @keyframes robotEntrance{
      from{
        opacity:0;
        transform:translateY(-50%) translateX(150px) scale(.96)
      }
      to{
        opacity:1;
        transform:translateY(-50%) translateX(0) scale(1)
      }
    }

    @keyframes robotFloat{
      0%,100%{
        transform:translateY(-50%) translateX(0)
      }
      50%{
        transform:translateY(calc(-50% - 8px)) translateX(0)
      }
    }

    .robot-scan{
      position:absolute;
      left:8%;
      right:3%;
      top:10%;
      height:3px;
      background:
        linear-gradient(
          90deg,
          transparent,
          var(--cyan),
          #fff,
          var(--cyan),
          transparent
        );
      box-shadow:
        0 0 10px var(--cyan),
        0 0 28px rgba(0,217,255,.7);
      z-index:4;
      opacity:.75;
      animation:scanRobot 3.8s ease-in-out infinite;
    }

    @keyframes scanRobot{
      0%,100%{
        transform:translateY(0);
        opacity:.15
      }

      12%{
        opacity:.9
      }

      50%{
        transform:translateY(300px);
        opacity:.85
      }

      88%{
        opacity:.9
      }
    }

    .robot-scan-grid{
      position:absolute;
      inset:0;
      z-index:3;
      background:
        linear-gradient(
          rgba(0,217,255,.06) 1px,
          transparent 1px
        ),
        linear-gradient(
          90deg,
          rgba(0,217,255,.06) 1px,
          transparent 1px
        );
      background-size:28px 28px;
      mask-image:linear-gradient(
        90deg,
        transparent 0%,
        black 35%,
        black 100%
      );
    }

    .ai-label{
      position:absolute;
      right:8%;
      bottom:18%;
      z-index:5;
      padding:.55rem .8rem;
      border:1px solid rgba(0,217,255,.65);
      background:rgba(0,8,20,.72);
      color:#9eefff;
      font:700 11px "Courier New",monospace;
      letter-spacing:.12em;
      box-shadow:0 0 18px rgba(0,217,255,.18);
      animation:labelPulse 2.5s ease-in-out infinite;
    }

    @keyframes labelPulse{
      0%,100%{
        opacity:.65
      }

      50%{
        opacity:1;
        box-shadow:0 0 24px rgba(0,217,255,.32)
      }
    }

    .code-float{
      position:absolute;
      z-index:5;
      padding:.6rem .75rem;
      border:1px solid rgba(0,217,255,.28);
      background:rgba(1,8,19,.58);
      color:#66ddff;
      font:11px/1.45 "Courier New",monospace;
      box-shadow:0 0 18px rgba(0,150,255,.10);
      backdrop-filter:blur(5px);
      white-space:pre;
      animation:codeDrift 5s ease-in-out infinite;
    }

    .code-a{
      left:12%;
      top:14%
    }

    .code-b{
      right:4%;
      top:12%;
      animation-delay:1.2s
    }

    .code-c{
      right:17%;
      bottom:8%;
      animation-delay:2.1s
    }

    @keyframes codeDrift{
      0%,100%{
        transform:translateY(0);
        opacity:.55
      }

      50%{
        transform:translateY(-8px);
        opacity:.9
      }
    }

    .dashboard{
      display:grid;
      grid-template-columns:1.15fr .85fr;
      gap:1rem;
    }

    .progress-track{
      height:8px;
      border-radius:99px;
      background:rgba(255,255,255,.07);
      overflow:hidden;
      border:1px solid rgba(0,217,255,.14);
    }

    .progress-fill{
      height:100%;
      border-radius:99px;
      background:
        linear-gradient(
          90deg,
          #0877ff,
          var(--cyan),
          #b6f7ff
        );
      box-shadow:0 0 12px rgba(0,217,255,.65);
      transform-origin:left;
      animation:progressIn 1.5s ease-out both;
    }

    @keyframes progressIn{
      from{
        transform:scaleX(0)
      }

      to{
        transform:scaleX(1)
      }
    }

    .status-grid{
      display:grid;
      grid-template-columns:repeat(5,1fr);
      gap:.55rem;
    }

    .status-chip{
      min-height:70px;
      display:flex;
      flex-direction:column;
      justify-content:center;
      align-items:center;
      text-align:center;
      border:1px solid rgba(0,217,255,.25);
      background:rgba(0,217,255,.035);
      border-radius:.85rem;
      transition:.25s;
    }

    .status-chip:hover{
      border-color:var(--cyan);
      box-shadow:0 0 18px rgba(0,217,255,.16);
      transform:translateY(-3px);
    }

    .neon-btn{
      position:relative;
      overflow:hidden;
    }

    .neon-btn::before{
      content:"";
      position:absolute;
      top:0;
      left:-120%;
      width:80%;
      height:100%;
      background:
        linear-gradient(
          90deg,
          transparent,
          rgba(255,255,255,.28),
          transparent
        );
      transform:skewX(-20deg);
      transition:.55s;
    }

    .neon-btn:hover::before{
      left:140%
    }

    /* =========================================================
       RESPONSIVE
       ========================================================== */

    @media(max-width:900px){

      .hero{
        min-height:650px
      }

      .hero-robot-layer{
        width:100%;
        height:48%;
        top:auto;
        bottom:0;
        opacity:.82;
      }

      .robot-image{
        right:-60px;
        width:620px;
        max-width:none;
        height:100%;
        object-fit:contain;
        object-position:center right;
      }

      .hero::before{
        background:
          linear-gradient(
            180deg,
            rgba(2,7,17,.98) 0%,
            rgba(2,7,17,.90) 48%,
            rgba(2,7,17,.48) 100%
          );
      }

      .robot-scan{
        top:5%;
        animation-duration:3.2s
      }

      .code-a{
        left:3%;
        top:10%;
        font-size:9px
      }

      .code-b{
        right:2%;
        top:8%;
        font-size:9px
      }

      .code-c{
        display:none
      }

      .dashboard{
        grid-template-columns:1fr
      }

      .status-grid{
        grid-template-columns:repeat(2,1fr)
      }
    }

    @media(max-width:520px){

      .hero{
        min-height:700px
      }

      .hero-robot-layer{
        height:42%
      }

      .robot-image{
        right:-105px;
        width:600px;
      }

      .ai-label{
        right:4%;
        bottom:9%;
        font-size:9px
      }

      .status-grid{
        grid-template-columns:repeat(2,1fr)
      }
    }

    @media(prefers-reduced-motion:reduce){

      *,
      *::before,
      *::after{
        animation-duration:.001ms!important;
        animation-iteration-count:1!important;
        scroll-behavior:auto!important;
      }
    }

    /* =========================================================
       STARK / JARVIS UI ENHANCEMENT
       Capa visual añadida sin eliminar la estructura original.
       ========================================================= */

    :root{
      --stark-red:#ff3b30;
      --stark-red-deep:#7a0f16;
      --stark-gold:#ffc857;
      --stark-white:#f4fbff;
      --hud-blue:#39e7ff;
      --hud-cyan:rgba(0,217,255,.18);
      --hud-panel:rgba(1,10,22,.72);
    }

    html{
      background:#01040a;
    }

    body{
      background:
        radial-gradient(circle at 80% 18%, rgba(0,132,255,.13), transparent 30%),
        radial-gradient(circle at 15% 70%, rgba(255,59,48,.045), transparent 26%),
        linear-gradient(135deg,#01040a 0%,#020711 48%,#01040a 100%);
      letter-spacing:.01em;
    }

    body::before{
      background:
        radial-gradient(circle at 72% 32%, rgba(0,217,255,.08), transparent 22%),
        radial-gradient(circle at 88% 78%, rgba(255,200,87,.035), transparent 24%),
        linear-gradient(
          90deg,
          rgba(1,7,17,.98) 0%,
          rgba(1,7,17,.88) 34%,
          rgba(1,7,17,.5) 70%,
          rgba(1,7,17,.78) 100%
        );
      animation:ambientDrift 14s ease-in-out infinite alternate;
    }

    body::after{
      background:
        linear-gradient(rgba(0,217,255,.028) 1px,transparent 1px),
        linear-gradient(90deg,rgba(0,217,255,.028) 1px,transparent 1px);
      background-size:42px 42px;
    }

    ::selection{
      background:rgba(0,217,255,.22);
      color:#fff;
    }

    ::-webkit-scrollbar{
      width:9px;
    }

    ::-webkit-scrollbar-track{
      background:#01050b;
    }

    ::-webkit-scrollbar-thumb{
      background:linear-gradient(var(--stark-red),var(--hud-blue));
      border-radius:999px;
      border:2px solid #01050b;
    }

    @keyframes ambientDrift{
      from{transform:scale(1) translate3d(0,0,0)}
      to{transform:scale(1.035) translate3d(-10px,6px,0)}
    }

    .scanlines{
      opacity:.035;
      mix-blend-mode:screen;
    }

    .nav{
      background:
        linear-gradient(180deg,rgba(2,10,20,.94),rgba(1,7,17,.72));
      border-bottom:1px solid rgba(57,231,255,.28);
      box-shadow:
        0 8px 30px rgba(0,0,0,.25),
        0 0 28px rgba(0,217,255,.045);
    }

    .nav::after{
      content:"";
      position:absolute;
      left:0;
      right:0;
      bottom:-1px;
      height:1px;
      background:linear-gradient(
        90deg,
        transparent 0%,
        rgba(255,59,48,.85) 18%,
        rgba(255,200,87,.75) 50%,
        rgba(57,231,255,.85) 82%,
        transparent 100%
      );
      opacity:.6;
    }

    .nav-link{
      font-family:"Courier New",monospace;
      font-size:.78rem;
      letter-spacing:.08em;
      text-transform:uppercase;
    }

    .nav-link::before{
      content:"";
      position:absolute;
      left:-12px;
      top:50%;
      width:4px;
      height:4px;
      border-radius:50%;
      background:var(--stark-red);
      box-shadow:0 0 8px rgba(255,59,48,.75);
      transform:translateY(-50%) scale(.5);
      opacity:.5;
      transition:.25s ease;
    }

    .nav-link:hover::before{
      transform:translateY(-50%) scale(1);
      opacity:1;
    }

    .hero{
      min-height:520px;
      isolation:isolate;
      border-bottom:1px solid rgba(57,231,255,.24);
    }

    .hero::after{
      content:"";
      position:absolute;
      inset:14px 14px 14px auto;
      width:min(43%,640px);
      border:1px solid rgba(57,231,255,.13);
      border-left-color:transparent;
      clip-path:polygon(
        12% 0,
        100% 0,
        100% 88%,
        90% 100%,
        0 100%,
        0 12%
      );
      z-index:1;
      pointer-events:none;
      box-shadow:inset 0 0 30px rgba(0,217,255,.025);
    }

    .hero-grid{
      opacity:.7;
      background-size:38px 38px;
      mask-image:linear-gradient(90deg,black 0%,black 46%,transparent 88%);
    }

    .hero-robot-layer{
      width:min(70%,980px);
      filter:drop-shadow(0 0 18px rgba(0,217,255,.08));
      transition:transform .18s ease-out;
      will-change:transform;
    }

    .hero-robot-layer::before{
      background:
        linear-gradient(
          90deg,
          #020711 0%,
          rgba(2,7,17,.76) 18%,
          rgba(2,7,17,.16) 55%,
          rgba(2,7,17,.08) 100%
        ),
        linear-gradient(
          180deg,
          rgba(0,217,255,.06),
          transparent 24%,
          transparent 78%,
          rgba(255,59,48,.04)
        );
    }

    .hero-robot-layer::after{
      background:
        radial-gradient(circle at 70% 48%,rgba(57,231,255,.18),transparent 40%),
        radial-gradient(circle at 92% 72%,rgba(255,200,87,.06),transparent 22%);
    }

    .robot-image{
      filter:
        drop-shadow(0 0 12px rgba(0,217,255,.18))
        drop-shadow(10px 0 28px rgba(0,110,255,.13));
    }

    .ai-label{
      border-color:rgba(255,200,87,.46);
      color:#ffe5a3;
      background:rgba(15,8,2,.62);
      box-shadow:
        0 0 18px rgba(255,200,87,.08),
        inset 0 0 18px rgba(255,200,87,.035);
    }

    .code-float{
      border-color:rgba(57,231,255,.22);
      background:rgba(1,8,19,.48);
      box-shadow:
        0 0 18px rgba(0,150,255,.08),
        inset 0 0 16px rgba(0,217,255,.02);
      backdrop-filter:blur(8px);
    }

    .tag{
      position:relative;
      overflow:hidden;
      box-shadow:inset 0 0 12px rgba(0,217,255,.025);
      transition:
        transform .22s ease,
        border-color .22s ease,
        box-shadow .22s ease;
    }

    .tag::after{
      content:"";
      position:absolute;
      inset:0;
      background:linear-gradient(
        105deg,
        transparent 35%,
        rgba(255,255,255,.13) 48%,
        transparent 61%
      );
      transform:translateX(-120%);
      transition:transform .55s ease;
    }

    .tag:hover{
      transform:translateY(-2px);
      border-color:rgba(255,200,87,.65);
      box-shadow:
        0 0 14px rgba(255,200,87,.07),
        inset 0 0 12px rgba(0,217,255,.03);
    }

    .tag:hover::after{
      transform:translateX(120%);
    }

    .btn{
      min-height:44px;
      border-color:rgba(57,231,255,.6);
      position:relative;
      box-shadow:
        0 0 0 1px rgba(0,217,255,.025),
        inset 0 0 16px rgba(0,217,255,.03);
    }

    .btn::after{
      content:"";
      position:absolute;
      inset:3px;
      border:1px solid rgba(255,255,255,.035);
      border-radius:inherit;
      pointer-events:none;
    }

    .btn:hover{
      border-color:rgba(255,200,87,.82);
      box-shadow:
        0 0 22px rgba(0,217,255,.16),
        0 0 14px rgba(255,200,87,.06),
        inset 0 0 18px rgba(0,217,255,.05);
    }

    .glass{
      position:relative;
      overflow:hidden;
      border-color:rgba(57,231,255,.34);
      background:
        linear-gradient(145deg,rgba(4,20,39,.9),rgba(1,7,17,.82));
      box-shadow:
        0 0 35px rgba(0,140,255,.08),
        inset 0 0 28px rgba(0,217,255,.025);
    }

    .glass::before{
      content:"";
      position:absolute;
      top:0;
      left:10%;
      right:10%;
      height:1px;
      background:linear-gradient(
        90deg,
        transparent,
        rgba(255,200,87,.68),
        rgba(57,231,255,.75),
        transparent
      );
      opacity:.55;
      pointer-events:none;
    }

    .corner::before,
    .corner::after{
      width:30px;
      height:30px;
    }

    .corner::before{
      border-left:2px solid var(--hud-blue);
      border-top:2px solid var(--hud-blue);
      box-shadow:-2px -2px 10px rgba(57,231,255,.15);
    }

    .corner::after{
      border-right:2px solid var(--stark-gold);
      border-bottom:2px solid var(--stark-gold);
      box-shadow:2px 2px 10px rgba(255,200,87,.08);
    }

    .dashboard{
      gap:1.25rem;
    }

    .progress-track{
      height:9px;
      background:rgba(255,255,255,.045);
      box-shadow:inset 0 0 12px rgba(0,0,0,.25);
    }

    .progress-fill{
      position:relative;
      overflow:hidden;
      background:
        linear-gradient(
          90deg,
          #006eff,
          var(--hud-blue),
          #e8fbff
        );
    }

    .progress-fill::after{
      content:"";
      position:absolute;
      inset:0;
      background:linear-gradient(
        90deg,
        transparent,
        rgba(255,255,255,.4),
        transparent
      );
      transform:translateX(-100%);
      animation:progressShine 2.7s linear infinite;
    }

    @keyframes progressShine{
      to{transform:translateX(100%)}
    }

    .status-chip{
      position:relative;
      overflow:hidden;
      background:
        linear-gradient(180deg,rgba(0,217,255,.05),rgba(0,0,0,.18));
      box-shadow:inset 0 0 18px rgba(0,217,255,.018);
    }

    .status-chip::after{
      content:"";
      position:absolute;
      left:-10%;
      right:-10%;
      bottom:0;
      height:1px;
      background:linear-gradient(
        90deg,
        transparent,
        rgba(255,200,87,.45),
        transparent
      );
      opacity:.6;
    }

    .activity{
      position:relative;
      overflow:hidden;
    }

    .activity::before{
      content:"";
      position:absolute;
      top:-100%;
      left:-20%;
      width:35%;
      height:300%;
      background:linear-gradient(
        90deg,
        transparent,
        rgba(255,255,255,.08),
        transparent
      );
      transform:rotate(18deg);
      transition:left .7s ease;
    }

    .activity:hover::before{
      left:120%;
    }

    .modal-bg{
      background:
        radial-gradient(circle at center,rgba(0,145,255,.09),transparent 42%),
        rgba(0,0,0,.84);
      backdrop-filter:blur(12px) saturate(1.15);
      overflow-y:auto;
      overscroll-behavior:contain;
    }

    .modal-box{
      position:relative;
      overflow-x:hidden;
      overflow-y:auto;
      max-height:90vh;
      overscroll-behavior:contain;
      -webkit-overflow-scrolling:touch;
      border-color:rgba(57,231,255,.62);
      background:
        linear-gradient(145deg,rgba(5,23,44,.96),rgba(1,7,17,.96));
      box-shadow:
        0 0 70px rgba(0,170,255,.16),
        0 0 18px rgba(255,59,48,.055),
        inset 0 0 40px rgba(0,217,255,.03);
      animation:modalBoot .28s cubic-bezier(.2,.9,.2,1) both;
    }

    .modal-box::before{
      content:"J.A.R.V.I.S. // SECURE CHANNEL";
      position:absolute;
      top:10px;
      right:18px;
      font:700 9px "Courier New",monospace;
      letter-spacing:.16em;
      color:rgba(57,231,255,.45);
      pointer-events:none;
    }

    .modal-box::after{
      content:"";
      position:absolute;
      inset:9px;
      border:1px solid rgba(255,255,255,.025);
      border-radius:inherit;
      pointer-events:none;
    }

    /* ===== SCROLL INTERNO DE LOS MODALES ===== */
    .modal-box::-webkit-scrollbar{
      width:8px;
    }

    .modal-box::-webkit-scrollbar-track{
      background:rgba(0,217,255,.035);
      border-radius:10px;
    }

    .modal-box::-webkit-scrollbar-thumb{
      background:linear-gradient(180deg,rgba(0,217,255,.75),rgba(139,92,246,.7));
      border-radius:10px;
      border:1px solid rgba(255,255,255,.08);
    }

    .modal-box::-webkit-scrollbar-thumb:hover{
      background:linear-gradient(180deg,rgba(0,217,255,.95),rgba(139,92,246,.9));
    }

    .modal-box{
      scrollbar-width:thin;
      scrollbar-color:rgba(0,217,255,.75) rgba(0,217,255,.035);
    }

    @keyframes modalBoot{
      from{
        opacity:0;
        transform:translateY(10px) scale(.985);
        filter:blur(4px);
      }
      to{
        opacity:1;
        transform:translateY(0) scale(1);
        filter:blur(0);
      }
    }

    .code-box{
      box-shadow:inset 0 0 20px rgba(0,217,255,.025);
    }

    footer{
      position:relative;
      overflow:hidden;
      box-shadow:0 -14px 40px rgba(0,0,0,.18);
    }

    footer::before{
      content:"";
      position:absolute;
      top:0;
      left:15%;
      right:15%;
      height:1px;
      background:linear-gradient(
        90deg,
        transparent,
        rgba(255,59,48,.75),
        rgba(255,200,87,.65),
        rgba(57,231,255,.8),
        transparent
      );
    }

    /* Painel HUD añadido dinámicamente */
    .stark-interface{
      position:fixed;
      right:18px;
      bottom:18px;
      z-index:70;
      display:flex;
      align-items:center;
      gap:10px;
      padding:8px 11px;
      border:1px solid rgba(57,231,255,.22);
      background:rgba(1,8,17,.62);
      backdrop-filter:blur(9px);
      box-shadow:
        0 0 24px rgba(0,217,255,.06),
        inset 0 0 18px rgba(0,217,255,.025);
      color:#8edfff;
      font:700 9px/1.2 "Courier New",monospace;
      letter-spacing:.13em;
      text-transform:uppercase;
      pointer-events:none;
    }

    .stark-interface .hud-core{
      width:7px;
      height:7px;
      border-radius:50%;
      background:var(--stark-red);
      box-shadow:
        0 0 6px rgba(255,59,48,.9),
        0 0 14px rgba(255,59,48,.35);
      animation:hudCorePulse 1.8s ease-in-out infinite;
    }

    .stark-interface .hud-time{
      color:#e6fbff;
      min-width:70px;
    }

    @keyframes hudCorePulse{
      0%,100%{opacity:.65;transform:scale(.86)}
      50%{opacity:1;transform:scale(1.15)}
    }

    .stark-reactor{
      position:absolute;
      right:25%;
      top:50%;
      width:180px;
      aspect-ratio:1;
      transform:translate(50%,-50%);
      z-index:1;
      pointer-events:none;
      opacity:.55;
      mix-blend-mode:screen;
    }

    .stark-reactor::before,
    .stark-reactor::after{
      content:"";
      position:absolute;
      inset:0;
      border-radius:50%;
      border:1px solid rgba(57,231,255,.28);
    }

    .stark-reactor::before{
      box-shadow:
        0 0 18px rgba(57,231,255,.1),
        inset 0 0 20px rgba(57,231,255,.05);
      animation:reactorSpin 12s linear infinite;
    }

    .stark-reactor::after{
      inset:19%;
      border-color:rgba(255,200,87,.24);
      border-style:dashed;
      animation:reactorSpinReverse 8s linear infinite;
    }

    .stark-reactor-center{
      position:absolute;
      inset:34%;
      border-radius:50%;
      background:
        radial-gradient(circle,#f4feff 0%,#7deaff 24%,#17bfff 44%,rgba(0,92,255,.08) 73%,transparent 74%);
      box-shadow:
        0 0 16px rgba(57,231,255,.75),
        0 0 42px rgba(0,128,255,.22);
      animation:reactorPulse 2.7s ease-in-out infinite;
    }

    @keyframes reactorSpin{
      to{transform:rotate(360deg)}
    }

    @keyframes reactorSpinReverse{
      to{transform:rotate(-360deg)}
    }

    @keyframes reactorPulse{
      0%,100%{transform:scale(.88);opacity:.62}
      50%{transform:scale(1.08);opacity:1}
    }

    .hud-reveal{
      opacity:0;
      transform:translateY(12px);
      transition:opacity .7s ease,transform .7s ease;
    }

    .hud-reveal.is-visible{
      opacity:1;
      transform:translateY(0);
    }

    .stark-status-line{
      position:absolute;
      top:28px;
      right:28px;
      z-index:5;
      display:flex;
      align-items:center;
      gap:8px;
      padding:5px 9px;
      border:1px solid rgba(57,231,255,.18);
      background:rgba(0,6,15,.4);
      color:rgba(185,241,255,.72);
      font:600 9px "Courier New",monospace;
      letter-spacing:.13em;
      text-transform:uppercase;
      pointer-events:none;
    }

    .stark-status-line::before{
      content:"";
      width:5px;
      height:5px;
      border-radius:50%;
      background:var(--stark-gold);
      box-shadow:0 0 8px rgba(255,200,87,.8);
    }

    .stark-circuit-line{
      position:absolute;
      height:1px;
      background:linear-gradient(90deg,transparent,var(--hud-blue),transparent);
      box-shadow:0 0 8px rgba(57,231,255,.45);
      opacity:.42;
      pointer-events:none;
    }

    .stark-circuit-line.line-a{
      width:170px;
      top:26%;
      right:5%;
      transform:rotate(-12deg);
    }

    .stark-circuit-line.line-b{
      width:120px;
      bottom:21%;
      right:12%;
      transform:rotate(16deg);
    }

    @media(max-width:900px){
      .hero{
        min-height:640px;
      }

      .hero::after{
        inset:auto 12px 14px 12px;
        width:auto;
        height:48%;
        border-left-color:rgba(57,231,255,.13);
      }

      .hero-robot-layer{
        width:100%;
      }

      .stark-reactor{
        right:50%;
        top:66%;
        width:150px;
        opacity:.33;
      }

      .stark-status-line{
        top:16px;
        right:16px;
        font-size:8px;
      }
    }

    @media(max-width:520px){
      .stark-interface{
        right:10px;
        bottom:10px;
        padding:7px 8px;
        font-size:8px;
      }

      .stark-interface .hud-label{
        display:none;
      }

      .stark-reactor{
        width:125px;
        top:73%;
      }
    }

    @media(prefers-reduced-motion:reduce){
      body::before,
      .stark-interface .hud-core,
      .progress-fill::after,
      .stark-reactor::before,
      .stark-reactor::after,
      .stark-reactor-center{
        animation:none!important;
      }

      .hud-reveal{
        opacity:1;
        transform:none;
        transition:none;
      }
    }

  

    /* =========================================================
       J.A.R.V.I.S. WELCOME + STARK ARMOR DISPLAY
       Añadido sobre el diseño existente sin eliminar contenido.
       ========================================================== */

    .jarvis-welcome{
      position:fixed;
      inset:0;
      z-index:9999;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
      background:
        radial-gradient(circle at 50% 45%, rgba(0,217,255,.10), transparent 28%),
        linear-gradient(180deg,rgba(0,4,10,.97),rgba(1,8,18,.985));
      backdrop-filter:blur(16px);
      opacity:1;
      visibility:visible;
      transition:opacity .7s ease, visibility .7s ease;
    }

    .jarvis-welcome.hide{
      opacity:0;
      visibility:hidden;
      pointer-events:none;
    }

    .jarvis-welcome-panel{
      position:relative;
      width:min(720px,100%);
      padding:34px 30px 28px;
      border:1px solid rgba(57,231,255,.5);
      background:
        linear-gradient(145deg,rgba(3,20,38,.92),rgba(1,7,17,.9));
      box-shadow:
        0 0 80px rgba(0,145,255,.13),
        inset 0 0 45px rgba(0,217,255,.035);
      clip-path:polygon(
        14px 0, calc(100% - 14px) 0, 100% 14px,
        100% calc(100% - 14px), calc(100% - 14px) 100%,
        14px 100%, 0 calc(100% - 14px), 0 14px
      );
      overflow:hidden;
      transform:translateY(0) scale(1);
      animation:jarvisPanelIn .8s cubic-bezier(.2,.8,.2,1) both;
    }

    .jarvis-welcome-panel::before,
    .jarvis-welcome-panel::after{
      content:"";
      position:absolute;
      pointer-events:none;
    }

    .jarvis-welcome-panel::before{
      top:0;
      left:18%;
      right:18%;
      height:1px;
      background:linear-gradient(90deg,transparent,var(--hud-blue),transparent);
      box-shadow:0 0 18px var(--hud-blue);
    }

    .jarvis-welcome-panel::after{
      inset:10px;
      border:1px solid rgba(0,217,255,.08);
      clip-path:inherit;
    }

    .jarvis-mark{
      position:relative;
      z-index:2;
      width:88px;
      height:88px;
      margin:0 auto 18px;
      border-radius:50%;
      border:1px solid rgba(57,231,255,.45);
      display:grid;
      place-items:center;
      background:radial-gradient(circle,rgba(119,245,255,.20) 0 8%,rgba(0,130,255,.11) 9% 35%,transparent 36%);
      box-shadow:0 0 28px rgba(0,217,255,.22), inset 0 0 24px rgba(0,217,255,.08);
      animation:jarvisCorePulse 2.4s ease-in-out infinite;
    }

    .jarvis-mark::before,
    .jarvis-mark::after{
      content:"";
      position:absolute;
      border-radius:50%;
      border:1px solid rgba(57,231,255,.22);
    }

    .jarvis-mark::before{ inset:10px; }
    .jarvis-mark::after{ inset:22px; border-color:rgba(255,200,87,.55); }

    .jarvis-mark-core{
      width:13px;
      height:13px;
      border-radius:50%;
      background:#eaffff;
      box-shadow:0 0 8px #fff,0 0 20px var(--hud-blue),0 0 34px var(--hud-blue);
    }

    .jarvis-kicker{
      position:relative;
      z-index:2;
      text-align:center;
      color:#6fe7ff;
      font:700 11px/1.4 "Courier New",monospace;
      letter-spacing:.24em;
      text-transform:uppercase;
    }

    .jarvis-title{
      position:relative;
      z-index:2;
      margin:.5rem 0 0;
      text-align:center;
      font-size:clamp(2rem,5vw,3.8rem);
      line-height:1;
      font-weight:900;
      letter-spacing:.08em;
      color:#ecfbff;
      text-shadow:0 0 12px rgba(57,231,255,.75),0 0 38px rgba(0,145,255,.28);
    }

    .jarvis-message{
      position:relative;
      z-index:2;
      max-width:580px;
      margin:18px auto 0;
      text-align:center;
      color:#c7dbe7;
      line-height:1.7;
      font-size:.98rem;
    }

    .jarvis-message strong{ color:#ffe5a3; }

    .jarvis-system-bar{
      position:relative;
      z-index:2;
      display:grid;
      grid-template-columns:repeat(3,1fr);
      gap:10px;
      margin:24px 0;
    }

    .jarvis-system-chip{
      padding:10px 8px;
      border:1px solid rgba(57,231,255,.18);
      background:rgba(0,217,255,.035);
      text-align:center;
      font:700 10px/1.3 "Courier New",monospace;
      color:#86ddeb;
      letter-spacing:.08em;
    }

    .jarvis-actions{
      position:relative;
      z-index:2;
      display:flex;
      justify-content:center;
      gap:12px;
      flex-wrap:wrap;
    }

    .jarvis-enter,
    .jarvis-owner,
    .jarvis-guest,
    .jarvis-voice{
      min-width:170px;
      border:1px solid rgba(57,231,255,.55);
      background:rgba(0,217,255,.06);
      color:#d8fbff;
      padding:12px 18px;
      border-radius:10px;
      font:800 12px "Courier New",monospace;
      letter-spacing:.08em;
      text-transform:uppercase;
      cursor:pointer;
      transition:.25s ease;
    }

    .jarvis-enter{
      border-color:rgba(255,59,48,.65);
      background:linear-gradient(90deg,rgba(255,59,48,.12),rgba(255,200,87,.08));
    }

    .jarvis-owner{
      border-color:rgba(255,200,87,.58);
      background:rgba(255,200,87,.055);
      color:#ffe7a6;
    }

    .jarvis-owner-active{
      border-color:rgba(0,229,168,.75)!important;
      background:rgba(0,229,168,.08)!important;
      color:#8fffe0!important;
      box-shadow:0 0 18px rgba(0,229,168,.12);
    }

    .jarvis-guest{
      border-color:rgba(180,200,215,.38);
      background:rgba(180,200,215,.035);
      color:#b8c9d4;
    }

    .jarvis-enter:hover,
    .jarvis-owner:hover,
    .jarvis-guest:hover,
    .jarvis-voice:hover{
      transform:translateY(-2px);
      box-shadow:0 0 24px rgba(57,231,255,.16);
      color:white;
    }

    .jarvis-console{
      position:relative;
      z-index:2;
      margin-top:19px;
      padding-top:13px;
      border-top:1px solid rgba(57,231,255,.12);
      text-align:center;
      color:#668a99;
      font:10px/1.5 "Courier New",monospace;
      letter-spacing:.06em;
    }

    @keyframes jarvisPanelIn{
      from{opacity:0;transform:translateY(20px) scale(.96)}
      to{opacity:1;transform:translateY(0) scale(1)}
    }

    @keyframes jarvisCorePulse{
      0%,100%{transform:scale(1);box-shadow:0 0 28px rgba(0,217,255,.22),inset 0 0 24px rgba(0,217,255,.08)}
      50%{transform:scale(1.05);box-shadow:0 0 44px rgba(0,217,255,.34),inset 0 0 28px rgba(0,217,255,.13)}
    }

    .stark-name-armor{
      position:relative;
      margin:20px 0 2px;
      width:min(390px,100%);
      height:178px;
      border:1px solid rgba(57,231,255,.18);
      background:linear-gradient(145deg,rgba(8,20,34,.7),rgba(1,7,17,.18));
      clip-path:polygon(18px 0,calc(100% - 18px) 0,100% 18px,100% calc(100% - 18px),calc(100% - 18px) 100%,18px 100%,0 calc(100% - 18px),0 18px);
      box-shadow:inset 0 0 28px rgba(0,217,255,.025),0 0 30px rgba(0,120,255,.05);
      overflow:hidden;
    }

    .stark-name-armor::before{
      content:"STARK INDUSTRIES // ARMOR INTERFACE";
      position:absolute;
      top:10px;
      left:12px;
      color:#6fe7ff;
      font:700 9px "Courier New",monospace;
      letter-spacing:.13em;
    }

    .armor-helmet{
      position:absolute;
      left:22px;
      top:30px;
      width:84px;
      height:114px;
      background:linear-gradient(155deg,#7b151c 0%,#d03a2d 35%,#7e1117 66%,#351016 100%);
      clip-path:polygon(30% 0,70% 0,90% 18%,86% 81%,65% 100%,35% 100%,14% 81%,10% 18%);
      border:1px solid rgba(255,200,87,.8);
      box-shadow:0 0 25px rgba(255,59,48,.13),inset -10px -12px 25px rgba(0,0,0,.3);
    }

    .armor-helmet::before{
      content:"";
      position:absolute;
      left:14px;
      right:14px;
      top:34px;
      height:18px;
      border:1px solid rgba(255,200,87,.75);
      background:linear-gradient(90deg,rgba(255,200,87,.12),rgba(255,238,172,.6),rgba(255,200,87,.12));
      box-shadow:0 0 10px rgba(255,200,87,.22);
      transform:skewY(-4deg);
    }

    .armor-helmet::after{
      content:"";
      position:absolute;
      left:33px;
      top:63px;
      width:18px;
      height:10px;
      border-left:1px solid rgba(255,200,87,.65);
      border-right:1px solid rgba(255,200,87,.65);
      background:rgba(0,0,0,.24);
    }

    .armor-torso{
      position:absolute;
      left:135px;
      top:42px;
      width:205px;
      height:105px;
      background:linear-gradient(145deg,#451218 0%,#9d2021 24%,#d63b2d 48%,#6a1016 76%,#2a0e12 100%);
      clip-path:polygon(14% 0,86% 0,100% 18%,93% 100%,7% 100%,0 18%);
      border:1px solid rgba(255,200,87,.55);
      box-shadow:0 0 26px rgba(255,59,48,.11),inset 0 0 30px rgba(0,0,0,.23);
    }

    .armor-torso::before{
      content:"";
      position:absolute;
      left:50%;
      top:31%;
      width:38px;
      height:38px;
      transform:translate(-50%,-50%);
      clip-path:polygon(50% 0,100% 50%,50% 100%,0 50%);
      background:#e8ffff;
      box-shadow:0 0 12px #fff,0 0 30px #37e8ff,0 0 45px rgba(57,231,255,.55);
    }

    .armor-torso::after{
      content:"";
      position:absolute;
      left:15%;
      right:15%;
      top:11px;
      height:1px;
      background:linear-gradient(90deg,transparent,rgba(255,200,87,.9),transparent);
      box-shadow:0 37px 0 rgba(255,200,87,.28),0 74px 0 rgba(255,200,87,.12);
    }

    .armor-label{
      position:absolute;
      right:12px;
      bottom:10px;
      color:#ffe5a3;
      font:700 9px "Courier New",monospace;
      letter-spacing:.1em;
    }

    .armor-hud{
      position:absolute;
      right:10px;
      top:31px;
      width:120px;
      color:#7fefff;
      font:9px/1.55 "Courier New",monospace;
      letter-spacing:.06em;
      opacity:.85;
    }

    .armor-hud span{ display:block; }
    .armor-hud i{ color:#ffcf67; font-style:normal; }

    @media(max-width:700px){
      .jarvis-welcome-panel{padding:28px 18px 22px}
      .jarvis-system-bar{grid-template-columns:1fr}
      .stark-name-armor{height:150px}
      .armor-helmet{transform:scale(.85);transform-origin:left top}
      .armor-torso{transform:scale(.83);transform-origin:left top;left:112px}
      .armor-hud{right:7px;width:105px;font-size:8px}
    }

    @media(prefers-reduced-motion:reduce){
      .jarvis-welcome-panel,.jarvis-mark{animation:none!important}
      .jarvis-welcome{transition:none!important}
    }
</style>

<style id="clickable-links-style">
  /* Enlaces añadidos/convertidos automáticamente */
  .auto-clickable-link {
    cursor: pointer;
    text-decoration: underline;
    text-underline-offset: 3px;
  }
</style>

</head>

<body>

  <canvas id="particles" class="particles-canvas"></canvas>\n  <canvas id="snow-canvas" class="snow-canvas" aria-hidden="true"></canvas>
  <div class="scanlines"></div>

  <!-- =========================================================
       NAVBAR
  ========================================================== -->

  <header class="nav fixed top-0 left-0 right-0 z-50">

    <div class="max-w-7xl mx-auto px-5">

      <div class="h-[68px] flex items-center justify-between">

        <a href="#inicio" class="flex items-center gap-3 font-black text-xl">

          <span class="text-3xl text-cyan-400 neon">
            &lt;/&gt;
          </span>

          <span class="hidden sm:block text-cyan-300">
            &lt;JeronimoZapata /&gt;
          </span>

        </a>

        <nav class="hidden md:flex items-center gap-9">
<a class="nav-link" href="#presentacion-personal">
            Presentación personal
          </a>

          <a class="nav-link" href="#contenido-materia">
            Contenido de la materia
          </a>

          <a class="nav-link" href="#entregas-academicas">
            Entregas académicas
          </a>

        </nav>

        <div class="hidden sm:flex items-center gap-3 text-xs text-cyan-200">

          <span class="w-8 h-px bg-cyan-400"></span>

          <span>
            Código hoy, grandes ideas mañana
          </span>

        </div>

      </div>

    </div>

  </header>

  <!-- =========================================================
       HERO
  ========================================================== -->

  <main id="inicio" class="pt-[68px]">

    <section class="hero">

      <div class="hero-grid"></div>

      <!-- =====================================================
           IMAGEN DEL ROBOT
           CAMBIO ÚNICO:
           robot-heroe.png -> hero-robot.png
      ====================================================== -->

      <div class="hero-robot-layer" aria-hidden="true">

        <img
          src="hero-robot.png"
          alt=""
          class="robot-image"
        >

        <div class="robot-scan-grid"></div>

        <div class="robot-scan"></div>

        <div class="code-float code-a">
          &lt;system&gt; status: ONLINE core: DATA
        </div>

        <div class="code-float code-b">
          DATA STRUCTURES =&gt; SMART SOLUTIONS
        </div>

        <div class="code-float code-c">
          class Developer {
            void create() {}
          }
        </div>

        <div class="ai-label">
          SYSTEM ONLINE // DEVELOPER MODE
        </div>

      </div>

      <div class="max-w-7xl mx-auto w-full px-5 py-10 relative z-10">

        <div class="max-w-[610px]">

          <div class="flex items-center gap-3 text-cyan-300 text-xs sm:text-sm font-mono tracking-wider mb-5">

            <span class="status-dot pulse"></span>

            SISTEMA ACADÉMICO ONLINE // PORTAFOLIO_DEV_3

          </div>

          <p class="text-cyan-200 text-lg mb-1">
            Hola, mi nombre es
          </p>

          <h1 class="text-4xl sm:text-6xl font-black leading-tight">

            Jeronimo Zapata Vargas<span class="text-cyan-400">.</span>

          </h1>

          <h2 class="text-xl sm:text-2xl font-bold mt-4 text-slate-200">

            Estudiante de Tecnología en Desarrollo de Software

            <span class="text-cyan-400">
              (3.er Semestre)
            </span>.

          </h2>

          <p class="mt-5 text-slate-300 leading-relaxed max-w-xl">

            Este portafolio reúne mi proceso de aprendizaje en Estructura de Datos:
            organización de información, estructuras lineales y no lineales,
            y algoritmos para buscar y ordenar datos.

          </p>

          <div class="flex flex-wrap gap-3 mt-7">

            <span class="tag">ARREGLOS</span>
            <span class="tag">LISTAS</span>
            <span class="tag">PILAS Y COLAS</span>
            <span class="tag">ÁRBOLES Y GRAFOS</span>

            <span class="tag">
              GITHUB
            </span>

          </div>

          <div class="flex flex-wrap gap-4 mt-9">

            <a
              href="#contenido-materia"
              class="btn neon-btn rounded-lg px-5 py-3 font-bold"
            >
              Explorar estructuras →
            </a>

            <a
              href="#entregas-academicas"
              class="btn neon-btn rounded-lg px-5 py-3 font-bold"
            >
              Ver entregas
            </a>

          </div>

        </div>

      </div>

    </section>

    <!-- =======================================================
         ESTADO ACADÉMICO
    ======================================================== -->

    <section class="max-w-7xl mx-auto px-5 pt-8">
      <div class="dashboard">
        <article class="glass corner rounded-2xl p-6">
          <div class="flex items-center justify-between gap-4 mb-5">
            <div>
              <p class="text-cyan-400 font-mono text-xs">SYSTEM DASHBOARD // ESTRUCTURAS</p>
              <h2 class="text-2xl font-black">Ruta de aprendizaje</h2>
            </div>
            <span class="tag">EN CURSO</span>
          </div>
          <p class="text-slate-300 leading-relaxed mb-5">La asignatura permite estudiar cómo almacenar, organizar y procesar datos para resolver problemas de manera eficiente.</p>
          <div class="space-y-4">
            <div>
              <div class="flex justify-between text-sm mb-2"><span class="text-slate-300">Estructuras lineales</span><span class="text-cyan-300 font-mono">01</span></div>
              <div class="progress-track"><div class="progress-fill" style="width:75%"></div></div>
            </div>
            <div>
              <div class="flex justify-between text-sm mb-2"><span class="text-slate-300">Estructuras no lineales</span><span class="text-cyan-300 font-mono">02</span></div>
              <div class="progress-track"><div class="progress-fill" style="width:55%"></div></div>
            </div>
            <div>
              <div class="flex justify-between text-sm mb-2"><span class="text-slate-300">Búsqueda y ordenamiento</span><span class="text-cyan-300 font-mono">03</span></div>
              <div class="progress-track"><div class="progress-fill" style="width:65%"></div></div>
            </div>
          </div>
        </article>
        <article class="glass corner rounded-2xl p-6">
          <p class="text-cyan-400 font-mono text-xs mb-3">CONTENIDOS CLAVE</p>
          <h2 class="text-2xl font-black mb-5">Conceptos de la materia</h2>
          <div class="status-grid">
            <div class="status-chip"><span class="text-cyan-300 font-black text-xl">[]</span><span class="text-xs text-slate-300 mt-1">Arreglos</span></div>
            <div class="status-chip"><span class="text-cyan-300 font-black text-xl">↔</span><span class="text-xs text-slate-300 mt-1">Listas</span></div>
            <div class="status-chip"><span class="text-cyan-300 font-black text-xl">⇅</span><span class="text-xs text-slate-300 mt-1">Pilas y colas</span></div>
            <div class="status-chip"><span class="text-cyan-300 font-black text-xl">⌘</span><span class="text-xs text-slate-300 mt-1">Árboles y grafos</span></div>
            <div class="status-chip"><span class="text-cyan-300 font-black text-xl">⌕</span><span class="text-xs text-slate-300 mt-1">Algoritmos</span></div>
          </div>
        </article>
      </div>
    </section>

    <!-- =======================================================
         SOBRE MI
    ======================================================== -->

    <!-- Estas subsecciones pertenecen únicamente a Estructura de Datos. -->
    <div class="space-y-4">
    <!-- =======================================================
         PRESENTACIÓN PERSONAL
    ======================================================== -->
    <section id="presentacion-personal" class="max-w-7xl mx-auto px-5 py-14">
      <div class="glass corner rounded-2xl p-7 md:p-9">
        <p class="text-cyan-400 font-mono text-xs mb-3">// PRESENTACIÓN PERSONAL • ESTRUCTURA DE DATOS</p>
        <h2 class="text-3xl md:text-4xl font-black mb-5">Presentación <span class="text-cyan-400 neon">personal</span></h2>
        <div class="grid md:grid-cols-[1.4fr_.8fr] gap-8 items-start">
          <div class="text-slate-300 leading-relaxed space-y-4">
            <p>Mi nombre es <strong class="text-white">Jerónimo Zapata Vargas</strong> y soy estudiante de tercer semestre de Tecnología en Desarrollo de Software.</p>
            <p>Me interesa aprender cómo se diseñan y construyen soluciones tecnológicas, fortalecer mi lógica de programación y convertir los conocimientos de clase en proyectos prácticos.</p>
            <p>Este portafolio reúne mi proceso de aprendizaje, los contenidos de la materia y las evidencias de las actividades académicas realizadas durante el semestre.</p>
          </div>
          <div class="grid grid-cols-2 gap-3">
            <div class="rounded-xl border border-cyan-400/25 bg-cyan-400/[.04] p-4"><p class="text-cyan-300 text-xs font-mono">FORMACIÓN</p><p class="font-bold mt-2">Desarrollo de Software</p></div>
            <div class="rounded-xl border border-cyan-400/25 bg-cyan-400/[.04] p-4"><p class="text-cyan-300 text-xs font-mono">SEMESTRE</p><p class="font-bold mt-2">Tercero</p></div>
            <div class="rounded-xl border border-cyan-400/25 bg-cyan-400/[.04] p-4"><p class="text-cyan-300 text-xs font-mono">ENFOQUE</p><p class="font-bold mt-2">Estructura de Datos</p></div>
            <div class="rounded-xl border border-cyan-400/25 bg-cyan-400/[.04] p-4"><p class="text-cyan-300 text-xs font-mono">PORTAFOLIO</p><p class="font-bold mt-2">Evidencias académicas</p></div>
          </div>
        </div>
      </div>
    </section>

    <!-- =======================================================
         CONTENIDO DE LA MATERIA
    ======================================================== -->
    <section id="contenido-materia" class="max-w-7xl mx-auto px-5 pb-14">
      <div class="glass corner rounded-2xl p-7 md:p-9">
        <p class="text-cyan-400 font-mono text-xs mb-3">// PLAN DE APRENDIZAJE DEL SEMESTRE</p>
        <h2 class="text-3xl md:text-4xl font-black mb-5">Contenido de la materia de <span class="text-cyan-400 neon">Estructura de Datos</span></h2>
        <p class="text-slate-300 leading-relaxed max-w-4xl">Aquí se presentan los principales temas de la asignatura Estructura de Datos. Puedes ajustar los nombres y el orden según el programa oficial del curso.</p>

        <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4 mt-7">
          <article class="rounded-xl border border-cyan-400/25 bg-black/20 p-5"><span class="text-cyan-300 font-mono text-xs">UNIDAD 01</span><h3 class="font-bold mt-2 mb-2">Fundamentos de estructuras de datos</h3><ul class="text-sm text-slate-400 list-disc pl-5 space-y-1"><li>Conceptos y clasificación de estructuras.</li><li>Tipos de datos abstractos.</li><li>Organización y representación de información.</li><li>Nociones de eficiencia algorítmica.</li></ul></article>
          <article class="rounded-xl border border-cyan-400/25 bg-black/20 p-5"><span class="text-cyan-300 font-mono text-xs">UNIDAD 02</span><h3 class="font-bold mt-2 mb-2">Arreglos y matrices</h3><ul class="text-sm text-slate-400 list-disc pl-5 space-y-1"><li>Arreglos unidimensionales y multidimensionales.</li><li>Recorrido, búsqueda y actualización.</li><li>Operaciones básicas sobre colecciones.</li><li>Ejercicios de aplicación.</li></ul></article>
          <article class="rounded-xl border border-cyan-400/25 bg-black/20 p-5"><span class="text-cyan-300 font-mono text-xs">UNIDAD 03</span><h3 class="font-bold mt-2 mb-2">Listas enlazadas</h3><ul class="text-sm text-slate-400 list-disc pl-5 space-y-1"><li>Nodos y referencias.</li><li>Listas simples y dobles.</li><li>Inserción, eliminación y recorrido.</li><li>Comparación con arreglos.</li></ul></article>
          <article class="rounded-xl border border-cyan-400/25 bg-black/20 p-5"><span class="text-cyan-300 font-mono text-xs">UNIDAD 04</span><h3 class="font-bold mt-2 mb-2">Pilas y colas</h3><ul class="text-sm text-slate-400 list-disc pl-5 space-y-1"><li>Principios LIFO y FIFO.</li><li>Operaciones push, pop y peek.</li><li>Encolar y desencolar.</li><li>Casos de uso y ejercicios prácticos.</li></ul></article>
          <article class="rounded-xl border border-cyan-400/25 bg-black/20 p-5"><span class="text-cyan-300 font-mono text-xs">UNIDAD 05</span><h3 class="font-bold mt-2 mb-2">Árboles y grafos</h3><ul class="text-sm text-slate-400 list-disc pl-5 space-y-1"><li>Nodos, raíces, hojas y niveles.</li><li>Árboles binarios y recorridos.</li><li>Conceptos básicos de grafos.</li><li>Representación de relaciones.</li></ul></article>
          <article class="rounded-xl border border-cyan-400/25 bg-black/20 p-5"><span class="text-cyan-300 font-mono text-xs">UNIDAD 06</span><h3 class="font-bold mt-2 mb-2">Búsqueda y ordenamiento</h3><ul class="text-sm text-slate-400 list-disc pl-5 space-y-1"><li>Búsqueda lineal y binaria.</li><li>Algoritmos básicos de ordenamiento.</li><li>Comparación de soluciones.</li><li>Prácticas de implementación.</li></ul></article>
        </div>
        <div class="mt-6 rounded-xl border border-cyan-400/20 bg-cyan-400/[.04] p-4 text-sm text-slate-300"><strong class="text-cyan-300">Resultado esperado:</strong> aplicar estructuras de datos para almacenar, recorrer, buscar y organizar información, justificando la estructura elegida para cada problema.</div>
      </div>
    </section>

    <!-- =======================================================
         CUATRO ENTREGAS ACADÉMICAS DEL SEMESTRE
    ======================================================== -->
    <section id="entregas-academicas" class="max-w-7xl mx-auto px-5 pb-14">
      <div class="glass corner rounded-2xl p-7 md:p-9">
        <p class="text-cyan-400 font-mono text-xs mb-3">// EVIDENCIAS DEL PROCESO</p>
        <h2 class="text-3xl md:text-4xl font-black mb-4">Las 4 entregas <span class="text-cyan-400 neon">académicas</span></h2>
        <p class="text-slate-300 leading-relaxed max-w-4xl">En esta sección se presentan las cuatro actividades principales del semestre. Cada tarjeta explica el propósito de la entrega y permite identificar qué evidencia debe agregarse. Reemplaza los textos o enlaces de ejemplo por los documentos, repositorios, capturas o archivos reales de cada actividad.</p>
        <div class="grid md:grid-cols-2 gap-5 mt-7">
          <article class="rounded-2xl border border-cyan-400/35 bg-black/25 p-6">
            <div class="flex items-start gap-4"><div class="w-12 h-12 shrink-0 rounded-xl border border-cyan-400/50 flex items-center justify-center text-cyan-300 font-black text-lg">01</div><div><p class="text-cyan-300 text-xs font-mono">ENTREGA 01</p><h3 class="text-lg font-bold mt-1">Actividad 1: Fundamentos de estructuras de datos</h3><p class="text-sm text-slate-400 mt-3">Espacio para describir el primer trabajo de la materia, sus objetivos, el procedimiento realizado y los conceptos aplicados.</p></div></div>
            <div class="mt-4 border-t border-slate-700 pt-4">
              <p class="text-xs text-slate-500 uppercase tracking-wider">Documento y archivos de la Actividad 1</p>
              <p class="text-sm text-slate-300 mt-1">Consulta el documento principal y abre los archivos de código, el diagrama y las evidencias desde el repositorio de Estructura de Datos.</p>

              <a class="btn neon-btn rounded-xl px-4 py-3 w-full mt-4 font-bold" href="https://docs.google.com/document/d/1EuNc_nIk1FoNU4hx1dMR1yPNEA9XXJg9mp6M6K3BjLI/edit?tab=t.0" target="_blank" rel="noopener noreferrer">📘 Abrir documento de la Actividad 1 ↗</a>

              <div class="mt-5">
                <p class="text-cyan-300 text-xs font-mono uppercase tracking-wider mb-3">Archivos del repositorio</p>
                <div class="grid sm:grid-cols-2 gap-2">
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Curso.java" target="_blank" rel="noopener noreferrer">💻 Curso.java ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Estudiante.java" target="_blank" rel="noopener noreferrer">💻 Estudiante.java ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Main.java" target="_blank" rel="noopener noreferrer">💻 Main.java ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/DIAGRAMA.png" target="_blank" rel="noopener noreferrer">🖼️ Diagrama ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%201.png" target="_blank" rel="noopener noreferrer">🖼️ Evidencia 1 ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%202.png" target="_blank" rel="noopener noreferrer">🖼️ Evidencia 2 ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%203.png" target="_blank" rel="noopener noreferrer">🖼️ Evidencia 3 ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%204.png" target="_blank" rel="noopener noreferrer">🖼️ Evidencia 4 ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%205.png" target="_blank" rel="noopener noreferrer">🖼️ Evidencia 5 ↗</a>
                  <a class="block rounded-lg border border-cyan-400/20 bg-cyan-400/[.035] p-3 text-sm text-slate-200 hover:border-cyan-400/60 hover:text-cyan-200 transition" href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%206.png" target="_blank" rel="noopener noreferrer">🖼️ Evidencia 6 ↗</a>
                </div>
              </div>
            </div>
          </article>
          <article class="rounded-2xl border border-blue-400/35 bg-black/25 p-6">
            <div class="flex items-start gap-4"><div class="w-12 h-12 shrink-0 rounded-xl border border-blue-400/50 flex items-center justify-center text-blue-300 font-black text-lg">02</div><div><p class="text-blue-300 text-xs font-mono">ENTREGA 02</p><h3 class="text-lg font-bold mt-1">Actividad 2: Estructuras lineales</h3><p class="text-sm text-slate-400 mt-3">Espacio para documentar el segundo trabajo de Estructura de Datos y explicar la solución desarrollada.</p></div></div>
            <div class="mt-4 border-t border-slate-700 pt-4"><p class="text-xs text-slate-500 uppercase tracking-wider">Evidencia para publicar</p><p class="text-sm text-slate-300 mt-1">Código fuente, ejercicio, capturas de ejecución o documento de la actividad 2.</p><p class="text-xs text-amber-300 mt-3">Cuando tengas el documento, pega el enlace de Word en el botón.</p>
              <a class="btn neon-btn rounded-xl px-4 py-3 w-full mt-4 font-bold" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_2" target="_blank" rel="noopener noreferrer">Abrir Word de la Actividad 2 ↗</a></div>
          </article>
          <article class="rounded-2xl border border-purple-400/35 bg-black/25 p-6">
            <div class="flex items-start gap-4"><div class="w-12 h-12 shrink-0 rounded-xl border border-purple-400/50 flex items-center justify-center text-purple-300 font-black text-lg">03</div><div><p class="text-purple-300 text-xs font-mono">ENTREGA 03</p><h3 class="text-lg font-bold mt-1">Actividad 3: Estructuras no lineales</h3><p class="text-sm text-slate-400 mt-3">Espacio para presentar el tercer trabajo, los conceptos de la materia utilizados y la solución implementada.</p></div></div>
            <div class="mt-4 border-t border-slate-700 pt-4"><p class="text-xs text-slate-500 uppercase tracking-wider">Evidencia para publicar</p><p class="text-sm text-slate-300 mt-1">Ejercicio resuelto, código fuente, resultados o informe de la actividad 3.</p><p class="text-xs text-amber-300 mt-3">Cuando tengas el documento, pega el enlace de Word en el botón.</p>
              <a class="btn neon-btn rounded-xl px-4 py-3 w-full mt-4 font-bold" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_3" target="_blank" rel="noopener noreferrer">Abrir Word de la Actividad 3 ↗</a></div>
          </article>
          <article class="rounded-2xl border border-emerald-400/35 bg-black/25 p-6">
            <div class="flex items-start gap-4"><div class="w-12 h-12 shrink-0 rounded-xl border border-emerald-400/50 flex items-center justify-center text-emerald-300 font-black text-lg">04</div><div><p class="text-emerald-300 text-xs font-mono">ENTREGA 04</p><h3 class="text-lg font-bold mt-1">Actividad 4: Proyecto o aplicación de estructuras de datos</h3><p class="text-sm text-slate-400 mt-3">Espacio para documentar la cuarta entrega, describir el problema y explicar cómo se aplicaron los contenidos de Estructura de Datos.</p></div></div>
            <div class="mt-4 border-t border-slate-700 pt-4"><p class="text-xs text-slate-500 uppercase tracking-wider">Evidencia para publicar</p><p class="text-sm text-slate-300 mt-1">Proyecto, código, capturas y explicación de la solución de la actividad 4.</p><p class="text-xs text-amber-300 mt-3">Cuando tengas el documento, pega el enlace de Word en el botón.</p>
              <a class="btn neon-btn rounded-xl px-4 py-3 w-full mt-4 font-bold" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_4" target="_blank" rel="noopener noreferrer">Abrir Word de la Actividad 4 ↗</a></div>
          </article>
        </div>
      </div>
    </section>\n\n  </main>

  <!-- =========================================================
       FOOTER
  ========================================================== -->

  <footer class="border-t border-cyan-400/20 bg-black/50">

    <div class="max-w-7xl mx-auto px-5 py-8 text-center">

      <p class="text-slate-400 text-sm">

        Diseñado y desarrollado por

        <span class="text-cyan-300 font-semibold">
          Jeronimo Zapata Vargas
        </span>

      </p>

      <p class="font-mono text-cyan-400 mt-2 text-sm">

        &lt;/&gt; ESTRUCTURA DE DATOS // ACADEMIC PORTFOLIO

      </p>

      <div class="flex justify-center gap-5 text-xs text-slate-500 mt-4">

        <span>
          Estructura de Datos
        </span>

        <span>
          •
        </span>

        <span>
          Inteligencia Artificial
        </span>

        <span>
          •
        </span>

        <span>
          Innovación
        </span>

      </div>

    </div>

  </footer>

  <script>

    function toggleDesplegable(id){

      const elemento = document.getElementById(id);

      const icono = document.getElementById(
        "icono-" + id
      );

      if(!elemento) return;

      const estaOculto =
        elemento.classList.contains("hidden");

      elemento.classList.toggle("hidden");

      if(icono){

        icono.textContent =
          estaOculto ? "−" : "+";

      }

    }

    function abrirModal(id){

      const modal =
        document.getElementById(id);

      if(modal){

        modal.classList.add("active");

        document.body.style.overflow = "hidden";

      }

    }

    function cerrarModal(id){

      const modal =
        document.getElementById(id);

      if(modal){

        modal.classList.remove("active");

        document.body.style.overflow = "";

      }

    }

    function cerrarSiFondo(event,modal){

      if(event.target === modal){

        modal.classList.remove("active");

        document.body.style.overflow = "";

      }

    }

    document.addEventListener(
      "keydown",
      function(event){

        if(event.key === "Escape"){

          document
            .querySelectorAll(".modal-bg.active")
            .forEach(modal => {

              modal.classList.remove("active");

            });

          document.body.style.overflow = "";

        }

      }
    );

    /* =========================================================
       NIEVE AZUL GLOBAL
       Capa visual independiente: no bloquea botones, modales ni enlaces.
       ========================================================== */

    (function(){
      "use strict";

      if(document.getElementById("blue-snow-canvas")) return;

      const snowCanvas = document.createElement("canvas");
      snowCanvas.id = "blue-snow-canvas";
      snowCanvas.setAttribute("aria-hidden","true");

      Object.assign(snowCanvas.style, {
        position: "fixed",
        inset: "0",
        width: "100%",
        height: "100%",
        pointerEvents: "none",
        zIndex: "40"
      });

      document.body.appendChild(snowCanvas);

      const snowCtx = snowCanvas.getContext("2d");
      if(!snowCtx) return;

      const reduceMotion =
        window.matchMedia &&
        window.matchMedia("(prefers-reduced-motion: reduce)").matches;

      let flakes = [];
      let width = 0;
      let height = 0;
      let dpr = 1;

      function resizeBlueSnow(){
        dpr = Math.min(window.devicePixelRatio || 1, 2);
        width = window.innerWidth;
        height = window.innerHeight;

        snowCanvas.width = Math.floor(width * dpr);
        snowCanvas.height = Math.floor(height * dpr);
        snowCtx.setTransform(dpr, 0, 0, dpr, 0, 0);

        if(reduceMotion){
          flakes = [];
          return;
        }

        const count = Math.min(
          125,
          Math.max(
            45,
            Math.floor(width * height / 11500)
          )
        );

        flakes = Array.from({length: count}, () => ({
          x: Math.random() * width,
          y: Math.random() * height,
          r: Math.random() * 2.2 + 0.7,
          vy: Math.random() * 1.25 + 0.35,
          vx: (Math.random() - 0.5) * 0.45,
          sway: Math.random() * Math.PI * 2,
          swaySpeed: Math.random() * 0.018 + 0.006,
          alpha: Math.random() * 0.55 + 0.3
        }));
      }

      function drawBlueSnow(){
        snowCtx.clearRect(0, 0, width, height);

        for(const flake of flakes){
          flake.sway += flake.swaySpeed;
          flake.x += flake.vx + Math.sin(flake.sway) * 0.25;
          flake.y += flake.vy;

          if(flake.y > height + 8){
            flake.y = -8;
            flake.x = Math.random() * width;
          }

          if(flake.x > width + 8) flake.x = -8;
          if(flake.x < -8) flake.x = width + 8;

          snowCtx.beginPath();
          snowCtx.arc(
            flake.x,
            flake.y,
            flake.r,
            0,
            Math.PI * 2
          );

          snowCtx.fillStyle =
            `rgba(75,185,255,${flake.alpha})`;

          snowCtx.shadowBlur = 9;
          snowCtx.shadowColor = "rgba(0,155,255,.95)";
          snowCtx.fill();
        }

        snowCtx.shadowBlur = 0;

        if(!reduceMotion){
          requestAnimationFrame(drawBlueSnow);
        }
      }

      window.addEventListener("resize", resizeBlueSnow, {passive:true});
      resizeBlueSnow();
      drawBlueSnow();

    })();

    /* Aviso para recursos que todavía no tienen enlace */
    function avisarRecurso(nombre){
      if(!event || !event.currentTarget || event.currentTarget.getAttribute("href") !== "#"){
        return true;
      }

      alert(
        nombre +
        " todavía está pendiente de agregar.\n\n" +
        "Reemplaza el href=\"#\" de este botón por el enlace correspondiente."
      );

      return false;
    }

    /* Partículas azules de fondo */

    const canvas =
      document.getElementById("particles");

    const ctx =
      canvas ? canvas.getContext("2d") : null;

    if(canvas && ctx){

      let particles = [];

      const density = 0.000055;

      function resizeParticles(){

        const dpr =
          Math.min(
            window.devicePixelRatio || 1,
            2
          );

        canvas.width =
          Math.floor(
            window.innerWidth * dpr
          );

        canvas.height =
          Math.floor(
            window.innerHeight * dpr
          );

        canvas.style.width =
          window.innerWidth + "px";

        canvas.style.height =
          window.innerHeight + "px";

        ctx.setTransform(
          dpr,
          0,
          0,
          dpr,
          0,
          0
        );

        const count =
          Math.min(
            95,
            Math.max(
              28,
              Math.floor(
                window.innerWidth *
                window.innerHeight *
                density
              )
            )
          );

        particles =
          Array.from(
            {length:count},
            () => ({

              x:
                Math.random() *
                window.innerWidth,

              y:
                Math.random() *
                window.innerHeight,

              r:
                Math.random() *
                1.5 + .35,

              vx:
                (Math.random()-.5) *
                .22,

              vy:
                (Math.random()-.5) *
                .22,

              a:
                Math.random() *
                .6 + .18

            })
          );

      }

      function drawParticles(){

        ctx.clearRect(
          0,
          0,
          window.innerWidth,
          window.innerHeight
        );

        for(const p of particles){

          p.x += p.vx;
          p.y += p.vy;

          if(p.x < -5)
            p.x =
              window.innerWidth + 5;

          if(p.x >
             window.innerWidth + 5)
            p.x = -5;

          if(p.y < -5)
            p.y =
              window.innerHeight + 5;

          if(p.y >
             window.innerHeight + 5)
            p.y = -5;

          ctx.beginPath();

          ctx.arc(
            p.x,
            p.y,
            p.r,
            0,
            Math.PI * 2
          );

          ctx.fillStyle =
            `rgba(0,217,255,${p.a})`;

          ctx.shadowBlur = 8;

          ctx.shadowColor =
            "rgba(0,170,255,.8)";

          ctx.fill();

        }

        ctx.shadowBlur = 0;

        requestAnimationFrame(
          drawParticles
        );

      }

      window.addEventListener(
        "resize",
        resizeParticles
      );

      resizeParticles();

      drawParticles();

    }


    /* =========================================================
       STARK / JARVIS INTERACTION LAYER
       No modifica las funciones originales; agrega UI y microinteracciones.
       ========================================================== */

    (function(){
      "use strict";

      const prefersReducedMotion =
        window.matchMedia &&
        window.matchMedia("(prefers-reduced-motion: reduce)").matches;

      function createStarkInterface(){
        if(document.querySelector(".stark-interface")) return;

        const hud = document.createElement("div");
        hud.className = "stark-interface";
        hud.setAttribute("aria-hidden","true");
        hud.innerHTML = `
          <span class="hud-core"></span>
          <span class="hud-label">J.A.R.V.I.S. // DEV CORE</span>
          <span class="hud-time" id="stark-clock">00:00:00</span>
        `;

        document.body.appendChild(hud);
      }

      function updateClock(){
        const clock = document.getElementById("stark-clock");
        if(!clock) return;

        const now = new Date();
        const parts = [
          String(now.getHours()).padStart(2,"0"),
          String(now.getMinutes()).padStart(2,"0"),
          String(now.getSeconds()).padStart(2,"0")
        ];

        clock.textContent = `${parts.join(":")} // ${getTimeGreeting()}`;
      }

      // Detecta automáticamente si es de día, tarde o noche según la hora local.
      function getTimeGreeting(){
        const hour = new Date().getHours();

        if(hour >= 5 && hour < 12) return "BUENOS DÍAS";
        if(hour >= 12 && hour < 19) return "BUENAS TARDES";
        return "BUENAS NOCHES";
      }

      function enhanceHero(){
        const hero = document.querySelector(".hero");
        if(!hero) return;

        if(!hero.querySelector(".stark-reactor")){
          const reactor = document.createElement("div");
          reactor.className = "stark-reactor";
          reactor.setAttribute("aria-hidden","true");

          const core = document.createElement("div");
          core.className = "stark-reactor-center";

          reactor.appendChild(core);
          hero.appendChild(reactor);
        }

        if(!hero.querySelector(".stark-status-line")){
          const status = document.createElement("div");
          status.className = "stark-status-line";
          status.textContent = "J.A.R.V.I.S. // CORE STABLE";
          hero.appendChild(status);
        }

        if(!hero.querySelector(".stark-circuit-line.line-a")){
          ["line-a","line-b"].forEach(className => {
            const line = document.createElement("div");
            line.className = `stark-circuit-line ${className}`;
            line.setAttribute("aria-hidden","true");
            hero.appendChild(line);
          });
        }
      }

      function enableParallax(){
        if(prefersReducedMotion) return;

        const hero = document.querySelector(".hero");
        const layer = document.querySelector(".hero-robot-layer");
        if(!hero || !layer) return;

        let raf = 0;

        const move = (event) => {
          if(raf) cancelAnimationFrame(raf);

          raf = requestAnimationFrame(() => {
            const rect = hero.getBoundingClientRect();
            const x = ((event.clientX - rect.left) / rect.width - .5) * 2;
            const y = ((event.clientY - rect.top) / rect.height - .5) * 2;

            const px = Math.max(-12, Math.min(12, x * 7));
            const py = Math.max(-8, Math.min(8, y * 4));

            layer.style.setProperty("--mx", `${px}px`);
            layer.style.setProperty("--my", `${py}px`);
            layer.style.transform = `translate3d(var(--mx),var(--my),0)`;
          });
        };

        const leave = () => {
          layer.style.transform = "translate3d(0,0,0)";
        };

        hero.addEventListener("pointermove", move, {passive:true});
        hero.addEventListener("pointerleave", leave, {passive:true});
      }

      function enableReveal(){
        const candidates = [
          ...document.querySelectorAll(
            "#sobre-mi, #materias, #trabajos, .dashboard, footer"
          )
        ];

        candidates.forEach((element,index) => {
          if(element.classList.contains("hud-reveal")) return;

          element.classList.add("hud-reveal");
          element.style.transitionDelay = `${Math.min(index * 70, 350)}ms`;
        });

        if(prefersReducedMotion || !("IntersectionObserver" in window)){
          candidates.forEach(element => {
            element.classList.add("is-visible");
          });
          return;
        }

        const observer = new IntersectionObserver((entries, obs) => {
          entries.forEach(entry => {
            if(entry.isIntersecting){
              entry.target.classList.add("is-visible");
              obs.unobserve(entry.target);
            }
          });
        },{
          threshold:.12,
          rootMargin:"0px 0px -40px 0px"
        });

        candidates.forEach(element => observer.observe(element));
      }

      function improveModalFocus(){
        document.addEventListener("click", (event) => {
          const openButton = event.target.closest(
            'button[onclick^="abrirModal"]'
          );

          if(!openButton) return;

          const match = openButton.getAttribute("onclick")?.match(
            /abrirModal\(['"]([^'"]+)['"]\)/
          );

          if(!match) return;

          const modal = document.getElementById(match[1]);
          if(!modal) return;

          requestAnimationFrame(() => {
            const closeButton = modal.querySelector("button");
            if(closeButton){
              closeButton.focus({preventScroll:true});
            }
          });
        });
      }



      /* =========================================================
         J.A.R.V.I.S. WELCOME + ARMOR DISPLAY
         ========================================================== */

      function getJarvisVisitorMode(){
        try{
          return localStorage.getItem('jarvis_owner_mode') === 'jeronimo';
        }catch(error){
          return false;
        }
      }

      function setJarvisVisitorMode(isOwner){
        try{
          if(isOwner){
            localStorage.setItem('jarvis_owner_mode','jeronimo');
          }else{
            localStorage.removeItem('jarvis_owner_mode');
          }
        }catch(error){
          // Si el navegador bloquea localStorage, JARVIS sigue funcionando en esta sesión.
        }
      }

      function createJarvisWelcome(){
        if(document.querySelector('.jarvis-welcome')) return;

        const isOwner = getJarvisVisitorMode();
        const overlay = document.createElement('div');
        overlay.className = 'jarvis-welcome';
        overlay.innerHTML = `
          <section class="jarvis-welcome-panel" role="dialog" aria-modal="true" aria-labelledby="jarvis-title">
            <div class="jarvis-mark" aria-hidden="true">
              <span class="jarvis-mark-core"></span>
            </div>
            <div class="jarvis-kicker">STARK SYSTEMS // ARTIFICIAL INTELLIGENCE</div>
            <h2 id="jarvis-title" class="jarvis-title">J.A.R.V.I.S.</h2>
            <p class="jarvis-message" id="jarvis-message"></p>
            <div class="jarvis-system-bar">
              <div class="jarvis-system-chip">CORE<br>ONLINE</div>
              <div class="jarvis-system-chip">ARMOR<br>READY</div>
              <div class="jarvis-system-chip">JAVA // POO<br>ACTIVE</div>
            </div>
            <div class="jarvis-actions">
              <button class="jarvis-enter" type="button">ENTRAR AL SISTEMA</button>
              <button class="jarvis-owner" type="button">SOY JERÓNIMO</button>
              <button class="jarvis-guest" type="button">ENTRAR COMO VISITANTE</button>
              <button class="jarvis-voice" type="button">ACTIVAR VOZ JARVIS</button>
            </div>
            <div class="jarvis-console" id="jarvis-console">&gt; JARVIS BOOT SEQUENCE // SECURE CHANNEL // SYSTEM STABLE</div>
          </section>
        `;

        document.body.appendChild(overlay);
        document.body.style.overflow = 'hidden';

        const message = overlay.querySelector('#jarvis-message');
        const consoleLine = overlay.querySelector('#jarvis-console');
        const ownerButton = overlay.querySelector('.jarvis-owner');
        const guestButton = overlay.querySelector('.jarvis-guest');

        function renderGreeting(owner){
          const greeting = getTimeGreeting();

          if(owner){
            message.innerHTML = `
              ${greeting}, <strong>Jerónimo Zapata Vargas</strong>.<br>
              Soy <strong>J.A.R.V.I.S.</strong>, la inteligencia artificial de tu portafolio.
              El sistema académico está iniciando y la interfaz Stark está lista para mostrar tus proyectos.
            `;
            ownerButton.textContent = 'JERÓNIMO RECONOCIDO';
            ownerButton.classList.add('jarvis-owner-active');
            guestButton.textContent = 'CAMBIAR A VISITANTE';
            consoleLine.innerHTML = '&gt; OWNER PROFILE // JERÓNIMO ZAPATA // ACCESS GRANTED';
          }else{
            message.innerHTML = `
              ${greeting}, bienvenido al <strong>portafolio de Jerónimo Zapata</strong>.<br>
              Soy <strong>J.A.R.V.I.S.</strong>, la inteligencia artificial del sistema.
              Aquí encontrarás el trabajo académico de un estudiante de Tecnología en Desarrollo de Software.
            `;
            ownerButton.textContent = 'SOY JERÓNIMO';
            ownerButton.classList.remove('jarvis-owner-active');
            guestButton.textContent = 'ENTRAR COMO VISITANTE';
            consoleLine.innerHTML = '&gt; VISITOR PROFILE // GUEST ACCESS // WELCOME TO JERÓNIMO\'S PORTFOLIO';
          }
        }

        renderGreeting(isOwner);

        const close = () => {
          overlay.classList.add('hide');
          document.body.style.overflow = '';
          window.setTimeout(() => overlay.remove(), 750);
        };

        overlay.querySelector('.jarvis-enter').addEventListener('click', close);

        ownerButton.addEventListener('click', () => {
          const nowOwner = !getJarvisVisitorMode();
          setJarvisVisitorMode(nowOwner);
          renderGreeting(nowOwner);
          speakJarvis(nowOwner);
        });

        guestButton.addEventListener('click', () => {
          setJarvisVisitorMode(false);
          renderGreeting(false);
          speakJarvis(false);
        });

        overlay.querySelector('.jarvis-voice').addEventListener('click', () => {
          speakJarvis(getJarvisVisitorMode());
        });

        setTimeout(() => {
          if(!overlay.classList.contains('hide')) close();
        }, 9500);

        // Intentar la bienvenida por voz; algunos navegadores exigen interacción.
        setTimeout(() => speakJarvis(isOwner), 500);
      }

      function speakJarvis(isOwner = getJarvisVisitorMode()){
        if(!('speechSynthesis' in window)) return;

        window.speechSynthesis.cancel();

        const greeting = getTimeGreeting()
          .toLowerCase()
          .replace("buenos días", "Buenos días")
          .replace("buenas tardes", "Buenas tardes")
          .replace("buenas noches", "Buenas noches");

        const text = isOwner
          ? `${greeting}, Jerónimo Zapata Vargas. Soy Jarvis. Bienvenido de nuevo a tu portafolio. El sistema está en línea y la interfaz Stark está lista.`
          : `${greeting}, bienvenido al portafolio de Jerónimo Zapata, estudiante de Tecnología en Desarrollo de Software. Soy Jarvis y te acompañaré por el sistema.`;

        const message = new SpeechSynthesisUtterance(text);
        message.lang = 'es-ES';
        message.rate = 0.92;
        message.pitch = 0.82;
        message.volume = 0.95;

        const voices = window.speechSynthesis.getVoices();
        const spanishVoice = voices.find(v => /^es(-|_)/i.test(v.lang));
        if(spanishVoice) message.voice = spanishVoice;

        window.speechSynthesis.speak(message);
      }

      function addArmorToName(){
        const heroName = document.querySelector('.hero h1');
        if(!heroName || document.querySelector('.stark-name-armor')) return;

        const armor = document.createElement('div');
        armor.className = 'stark-name-armor';
        armor.setAttribute('aria-label','Interfaz de armadura Stark');
        armor.innerHTML = `
          <div class="armor-helmet" aria-hidden="true"></div>
          <div class="armor-torso" aria-hidden="true"></div>
          <div class="armor-hud">
            <span>MODEL: <i>MARK-DEV</i></span>
            <span>CORE: <i>ONLINE</i></span>
            <span>ENERGY: <i>98%</i></span>
            <span>JARVIS: <i>READY</i></span>
          </div>
          <div class="armor-label">STARK ARMOR // DEVELOPER MODE</div>
        `;

        heroName.insertAdjacentElement('afterend', armor);
      }

      function preloadVoices(){
        if(!('speechSynthesis' in window)) return;
        window.speechSynthesis.getVoices();
      }

      function init(){
        createStarkInterface();
        enhanceHero();
        addArmorToName();
        preloadVoices();
        createJarvisWelcome();
        updateClock();
        setInterval(updateClock,1000);
        enableParallax();
        enableReveal();
        improveModalFocus();

        document.documentElement.classList.add("stark-ready");
      }

      if(document.readyState === "loading"){
        document.addEventListener("DOMContentLoaded", init, {once:true});
      }else{
        init();
      }
    })();

  </script>


<script id="auto-clickable-links">
(function () {
  'use strict';

  const URL_RE = /https?:\/\/[^\s<>"'`)\]}]+/g;
  const SKIP_TAGS = new Set([
    'A', 'SCRIPT', 'STYLE', 'NOSCRIPT', 'TEXTAREA', 'INPUT',
    'SELECT', 'OPTION', 'CODE', 'PRE', 'SVG'
  ]);

  function makeLinks(root) {
    const walker = document.createTreeWalker(
      root,
      NodeFilter.SHOW_TEXT,
      {
        acceptNode(node) {
          const parent = node.parentElement;
          if (!parent || SKIP_TAGS.has(parent.tagName)) {
            return NodeFilter.FILTER_REJECT;
          }
          return URL_RE.test(node.nodeValue)
            ? NodeFilter.FILTER_ACCEPT
            : NodeFilter.FILTER_REJECT;
        }
      }
    );

    const nodes = [];
    let node;
    while ((node = walker.nextNode())) nodes.push(node);

    nodes.forEach(textNode => {
      const text = textNode.nodeValue;
      URL_RE.lastIndex = 0;

      let match;
      let lastIndex = 0;
      const fragment = document.createDocumentFragment();
      let found = false;

      while ((match = URL_RE.exec(text)) !== null) {
        found = true;

        const start = match.index;
        let url = match[0];
        let trailing = '';

        // Remove common punctuation that should remain outside the link.
        while (/[.,!?;:]+$/.test(url)) {
          trailing = url.slice(-1) + trailing;
          url = url.slice(0, -1);
        }

        if (start > lastIndex) {
          fragment.appendChild(document.createTextNode(text.slice(lastIndex, start)));
        }

        const a = document.createElement('a');
        a.href = url;
        a.target = '_blank';
        a.rel = 'noopener noreferrer';
        a.className = 'auto-clickable-link';
        a.textContent = url;
        fragment.appendChild(a);

        if (trailing) {
          fragment.appendChild(document.createTextNode(trailing));
        }

        lastIndex = match.index + match[0].length;
      }

      if (found) {
        if (lastIndex < text.length) {
          fragment.appendChild(document.createTextNode(text.slice(lastIndex)));
        }
        textNode.parentNode.replaceChild(fragment, textNode);
      }
    });
  }

  function initClickableLinks() {
    makeLinks(document.body);
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', initClickableLinks);
  } else {
    initClickableLinks();
  }
})();
</script>


<script>
(() => {
  const canvas = document.getElementById('snow-canvas');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  if (!ctx) return;

  let width = 0, height = 0, flakes = [];
  const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  function resize() {
    const dpr = Math.min(window.devicePixelRatio || 1, 2);
    width = window.innerWidth;
    height = window.innerHeight;
    canvas.width = Math.floor(width * dpr);
    canvas.height = Math.floor(height * dpr);
    canvas.style.width = width + 'px';
    canvas.style.height = height + 'px';
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
    const amount = Math.min(150, Math.max(55, Math.floor(width / 9)));
    flakes = Array.from({length: amount}, () => ({
      x: Math.random() * width, y: Math.random() * height,
      r: Math.random() * 2.4 + .6, speed: Math.random() * 1.2 + .45,
      drift: (Math.random() - .5) * .7, alpha: Math.random() * .55 + .25
    }));
  }

  function draw() {
    ctx.clearRect(0, 0, width, height);
    for (const f of flakes) {
      ctx.beginPath();
      ctx.fillStyle = `rgba(225,247,255,${f.alpha})`;
      ctx.shadowColor = 'rgba(140,220,255,.45)';
      ctx.shadowBlur = f.r > 1.8 ? 5 : 2;
      ctx.arc(f.x, f.y, f.r, 0, Math.PI * 2);
      ctx.fill();
      f.y += f.speed;
      f.x += f.drift + Math.sin(f.y * .012) * .25;
      if (f.y > height + 5) { f.y = -5; f.x = Math.random() * width; }
      if (f.x < -5) f.x = width + 5;
      if (f.x > width + 5) f.x = -5;
    }
    ctx.shadowBlur = 0;
    if (!reduceMotion) requestAnimationFrame(draw);
  }

  resize();
  draw();
  window.addEventListener('resize', resize, {passive: true});
})();
</script>
\n</body>
</html>
