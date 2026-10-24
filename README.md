from pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#050914">
<meta name="description" content="Portafolio académico de Jerónimo Zapata Vargas: Programación Orientada a Objetos, Java, UML, programación funcional y estructuras de datos.">
<title>Jerónimo Zapata Vargas | Portafolio de Desarrollo de Software</title>
<style>
:root{
  color-scheme:dark;--bg:#050914;--panel:#0a1424;--panel2:#0d1b2e;
  --cyan:#39e7ff;--cyan2:#00bfe8;--text:#eaf7ff;--muted:#9bb2c7;
  --line:rgba(57,231,255,.19);--glow:rgba(0,213,255,.12);
  --radius:20px;--max:1180px
}
*{box-sizing:border-box}
html{scroll-behavior:smooth;scroll-padding-top:90px}
body{margin:0;background:var(--bg);color:var(--text);font:16px/1.65 Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",sans-serif;overflow-x:hidden}
body:before{content:"";position:fixed;inset:0;z-index:-3;pointer-events:none;background:radial-gradient(ellipse at 80% 10%,rgba(0,173,255,.13),transparent 35%),radial-gradient(ellipse at 10% 55%,rgba(0,220,255,.055),transparent 35%),linear-gradient(135deg,#050914,#07101e 55%,#030711)}
body:after{content:"";position:fixed;inset:0;z-index:-2;pointer-events:none;background-image:linear-gradient(rgba(57,231,255,.035) 1px,transparent 1px),linear-gradient(90deg,rgba(57,231,255,.035) 1px,transparent 1px);background-size:44px 44px;mask-image:linear-gradient(to bottom,#000,transparent 90%)}
a{color:var(--cyan);text-decoration:none}
a:hover{color:#fff}
button,a{-webkit-tap-highlight-color:transparent}
button{font:inherit}
::selection{background:rgba(57,231,255,.25);color:white}
.skip-link{position:absolute;top:-60px;left:12px;background:var(--cyan);color:#001018;padding:10px 14px;border-radius:8px;z-index:200}
.skip-link:focus{top:12px}
.container{width:min(var(--max),calc(100% - 40px));margin-inline:auto}
.nav-wrap{position:sticky;top:0;z-index:50;background:rgba(4,10,21,.83);backdrop-filter:blur(18px);border-bottom:1px solid var(--line)}
.nav{min-height:74px;display:flex;align-items:center;justify-content:space-between;gap:20px}
.brand{display:flex;align-items:center;gap:11px;color:var(--text);font-weight:850;letter-spacing:.02em}
.brand-mark{display:grid;place-items:center;width:40px;height:40px;border:1px solid var(--cyan);border-radius:12px;color:var(--cyan);box-shadow:0 0 22px var(--glow);font:700 15px ui-monospace,monospace}
.nav-links{display:flex;align-items:center;gap:22px}
.nav-links a{font-size:.83rem;color:#bfd3e5;transition:color .2s}
.nav-links a:hover{color:var(--cyan)}
.menu-toggle{display:none;border:1px solid var(--line);border-radius:10px;padding:8px 11px;color:var(--cyan);background:var(--panel)}
.hero{position:relative;isolation:isolate;padding:94px 0 72px;overflow:hidden;border-bottom:1px solid var(--line)}
.hero-grid{display:grid;grid-template-columns:1.2fr .8fr;align-items:center;gap:42px}
.eyebrow,.kicker{display:inline-flex;align-items:center;gap:9px;color:var(--cyan);font:700 .73rem ui-monospace,monospace;letter-spacing:.13em;text-transform:uppercase}
.live-dot{width:8px;height:8px;border-radius:50%;background:#48f5bc;box-shadow:0 0 13px #48f5bc}
h1{font-size:clamp(2.6rem,6.2vw,5.2rem);line-height:1.02;letter-spacing:-.055em;margin:22px 0}
h1 span{display:block;color:var(--cyan);text-shadow:0 0 32px rgba(57,231,255,.22)}
.hero h2{font-size:clamp(1.1rem,2vw,1.5rem);color:#d6e9f7;font-weight:600;margin:0 0 18px}
.hero p{max-width:680px;color:var(--muted);font-size:1.04rem}
.pills{display:flex;flex-wrap:wrap;gap:9px;margin:24px 0 30px}
.pill{padding:6px 11px;border:1px solid var(--line);border-radius:999px;color:#b9efff;background:rgba(57,231,255,.045);font:700 .72rem ui-monospace,monospace}
.actions{display:flex;flex-wrap:wrap;gap:12px}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:9px;padding:12px 17px;border:1px solid var(--cyan);border-radius:12px;color:#00131a;background:var(--cyan);font-weight:800;transition:transform .2s,box-shadow .2s,background .2s}
.btn:hover{color:#00131a;transform:translateY(-2px);box-shadow:0 9px 30px rgba(57,231,255,.19)}
.btn.secondary{color:var(--text);background:rgba(57,231,255,.055);border-color:var(--line)}
.btn.secondary:hover{background:rgba(57,231,255,.12);color:white}
.hud{position:relative;min-height:330px;border:1px solid rgba(57,231,255,.3);border-radius:28px;background:linear-gradient(145deg,rgba(12,30,51,.94),rgba(3,10,22,.92));box-shadow:0 0 70px rgba(0,166,255,.08),inset 0 0 50px rgba(57,231,255,.025);overflow:hidden;padding:24px}
.hud:before{content:"";position:absolute;inset:18px;border:1px solid rgba(57,231,255,.11);border-radius:19px;pointer-events:none}
.hud-top{display:flex;justify-content:space-between;gap:12px;color:var(--muted);font:700 .68rem ui-monospace,monospace;letter-spacing:.1em}
.orb-wrap{display:grid;place-items:center;min-height:210px;position:relative}
.orb{width:150px;height:150px;border-radius:50%;border:1px solid rgba(57,231,255,.65);background:radial-gradient(circle at 35% 30%,rgba(57,231,255,.35),rgba(0,94,150,.08) 45%,transparent 70%);box-shadow:0 0 28px rgba(57,231,255,.18),inset 0 0 32px rgba(57,231,255,.14);position:relative;animation:float 5s ease-in-out infinite}
.orb:before,.orb:after{content:"";position:absolute;border:1px solid rgba(57,231,255,.45);border-radius:50%;inset:-19px;transform:rotateX(65deg) rotate(-25deg)}
.orb:after{inset:-35px;transform:rotateX(68deg) rotate(32deg);border-color:rgba(57,231,255,.22)}
.orb-core{position:absolute;inset:40px;border-radius:50%;background:radial-gradient(circle,#e4fdff 0,#39e7ff 15%,rgba(0,150,255,.18) 65%,transparent 75%);filter:drop-shadow(0 0 18px var(--cyan))}
.hud-bottom{display:flex;justify-content:space-between;gap:10px;color:#8db4ca;font: .68rem ui-monospace,monospace}
.hud-bottom strong{color:var(--cyan)}
@keyframes float{50%{transform:translateY(-8px)}}
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:13px;margin-top:24px}
.stat{padding:17px;border:1px solid var(--line);border-radius:15px;background:rgba(7,19,34,.68)}
.stat strong{display:block;color:var(--cyan);font:800 1.45rem ui-monospace,monospace}
.stat span{color:var(--muted);font-size:.8rem}
section{padding:76px 0}
.section-head{display:flex;align-items:end;justify-content:space-between;gap:24px;margin-bottom:28px}
.section-head h2{font-size:clamp(1.8rem,3.5vw,2.7rem);letter-spacing:-.035em;margin:8px 0}
.section-head p{max-width:610px;color:var(--muted);margin:0}
.section-number{color:var(--cyan);font:700 .8rem ui-monospace,monospace;letter-spacing:.12em}
.panel{border:1px solid var(--line);border-radius:var(--radius);background:linear-gradient(145deg,rgba(11,25,43,.9),rgba(6,14,27,.85));box-shadow:0 16px 55px rgba(0,0,0,.13)}
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:18px}
.about-copy{padding:28px}
.about-copy p{color:var(--muted)}
.info-list{display:grid;gap:12px;padding:24px}
.info-row{display:flex;align-items:center;justify-content:space-between;gap:15px;padding:13px 0;border-bottom:1px solid rgba(255,255,255,.07)}
.info-row:last-child{border:0}
.info-row span{color:var(--muted);font-size:.9rem}
.info-row strong{font-size:.9rem;text-align:right}
.grid-2{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:18px}
.grid-3{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:18px}
.card{padding:23px;position:relative;overflow:hidden;transition:transform .22s,border-color .22s,box-shadow .22s}
.card:hover{transform:translateY(-4px);border-color:rgba(57,231,255,.46);box-shadow:0 15px 40px rgba(0,0,0,.18),0 0 24px rgba(57,231,255,.06)}
.card h3{margin:8px 0 9px;font-size:1.12rem;line-height:1.35}
.card p{color:var(--muted);font-size:.92rem;margin:0 0 16px}
.card-top{display:flex;justify-content:space-between;align-items:center;gap:12px}
.icon-box{display:grid;place-items:center;width:42px;height:42px;border:1px solid var(--line);border-radius:13px;color:var(--cyan);background:rgba(57,231,255,.06);font:700 1rem ui-monospace,monospace}
.status{display:inline-flex;align-items:center;gap:7px;color:#91f7d0;font:700 .67rem ui-monospace,monospace;text-transform:uppercase;letter-spacing:.08em}
.status:before{content:"";width:6px;height:6px;border-radius:50%;background:#48f5bc}
.card-links{display:flex;flex-wrap:wrap;gap:9px;margin-top:18px}
.text-link{display:inline-flex;align-items:center;gap:7px;font-size:.83rem;font-weight:750}
.text-link:after{content:"↗";font-size:1rem}
.unit-card{padding:25px}
.unit-card .unit-label{color:var(--cyan);font:700 .7rem ui-monospace,monospace;letter-spacing:.1em}
.unit-card h3{margin:9px 0}
.unit-card p{color:var(--muted);font-size:.9rem}
.tag-list{display:flex;flex-wrap:wrap;gap:7px;margin-top:15px}
.tag{border:1px solid rgba(57,231,255,.16);background:rgba(57,231,255,.04);color:#bdefff;border-radius:7px;padding:4px 8px;font: .67rem ui-monospace,monospace}
.activity-card{display:flex;flex-direction:column;min-height:100%}
.activity-card .card-content{flex:1}
.activity-number{color:rgba(57,231,255,.85);font:800 2rem ui-monospace,monospace}
.resource-list{display:grid;gap:11px;margin:16px 0}
.resource{display:flex;align-items:flex-start;gap:12px;padding:13px;border:1px solid rgba(57,231,255,.12);border-radius:12px;background:rgba(57,231,255,.025)}
.resource-icon{color:var(--cyan);font-size:1.1rem}
.resource strong{display:block;font-size:.9rem}
.resource small{display:block;color:var(--muted);font-size:.78rem;margin-top:3px}
.resource a{font-weight:700;font-size:.83rem}
.checklist{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:16px}
.check{padding:10px 12px;border:1px solid var(--line);border-radius:10px;color:#bdefff;font-size:.82rem}
.check:before{content:"✓";color:#48f5bc;margin-right:8px}
.callout{padding:23px;border-left:3px solid var(--cyan);background:rgba(57,231,255,.045);border-radius:0 14px 14px 0;color:#c5d9e8}
footer{border-top:1px solid var(--line);padding:30px 0 40px;background:rgba(2,7,15,.55)}
.footer-inner{display:flex;align-items:center;justify-content:space-between;gap:20px}
footer p{margin:5px 0;color:var(--muted);font-size:.82rem}
.back-top{position:fixed;right:20px;bottom:20px;z-index:40;width:44px;height:44px;display:grid;place-items:center;border:1px solid var(--line);border-radius:14px;background:rgba(6,18,33,.9);color:var(--cyan);opacity:0;pointer-events:none;transform:translateY(8px);transition:.2s}
.back-top.visible{opacity:1;pointer-events:auto;transform:translateY(0)}
.modal{position:fixed;inset:0;z-index:100;display:none;align-items:center;justify-content:center;padding:18px;background:rgba(0,0,0,.78);backdrop-filter:blur(12px)}
.modal.open{display:flex}
.modal-box{width:min(780px,100%);max-height:90vh;overflow:auto;padding:28px;border:1px solid rgba(57,231,255,.45);border-radius:22px;background:linear-gradient(145deg,#0b1a2d,#050a14);box-shadow:0 0 65px rgba(0,190,255,.12)}
.modal-head{display:flex;justify-content:space-between;align-items:start;gap:20px}
.modal-head h2{margin:8px 0}
.modal-close{border:1px solid var(--line);border-radius:10px;background:rgba(57,231,255,.06);color:var(--cyan);padding:7px 12px;cursor:pointer}
.modal-body{color:var(--muted)}
.modal-body .resource{margin-top:10px}
hr{border:0;border-top:1px solid var(--line);margin:25px 0}
.reveal{opacity:0;transform:translateY(16px);transition:opacity .55s ease,transform .55s ease}
.reveal.in-view{opacity:1;transform:none}
@media(max-width:900px){.hero-grid{grid-template-columns:1fr}.hud{min-height:280px}.orb-wrap{min-height:170px}.grid-3{grid-template-columns:repeat(2,minmax(0,1fr))}.nav-links{gap:13px}.nav-links a{font-size:.75rem}}
@media(max-width:680px){
 .container{width:min(100% - 28px,var(--max))}
 .nav{min-height:66px}.menu-toggle{display:block}
 .nav-links{display:none;position:absolute;top:65px;left:14px;right:14px;padding:15px;border:1px solid var(--line);border-radius:15px;background:#07111f;box-shadow:0 20px 50px rgba(0,0,0,.35);align-items:stretch;flex-direction:column;gap:0}
 .nav-links.open{display:flex}.nav-links a{padding:12px;border-bottom:1px solid rgba(255,255,255,.05);font-size:.9rem}.nav-links a:last-child{border:0}
 .hero{padding:64px 0 45px}.hero-grid{gap:25px}h1{font-size:clamp(2.45rem,13vw,4rem)}.hud{min-height:250px;padding:18px}
 .stats{grid-template-columns:repeat(2,1fr)}section{padding:55px 0}.section-head{display:block}.section-head p{margin-top:10px}
 .about-grid,.grid-2,.grid-3{grid-template-columns:1fr}.checklist{grid-template-columns:repeat(2,1fr)}
 .footer-inner{align-items:flex-start;flex-direction:column}.modal-box{padding:20px}
}
@media(prefers-reduced-motion:reduce){*,*:before,*:after{scroll-behavior:auto!important;animation-duration:.01ms!important;animation-iteration-count:1!important;transition-duration:.01ms!important}.reveal{opacity:1;transform:none}}
</style>
</head>
<body>
<a class="skip-link" href="#contenido">Saltar al contenido</a>
<div class="nav-wrap">
  <nav class="nav container" aria-label="Navegación principal">
    <a class="brand" href="#inicio" aria-label="Inicio del portafolio">
      <span class="brand-mark">JZ</span><span>PORTAFOLIO<span style="color:var(--cyan)">_DEV</span></span>
    </a>
    <button class="menu-toggle" id="menuToggle" aria-expanded="false" aria-controls="navLinks">☰ Menú</button>
    <div class="nav-links" id="navLinks">
      <a href="#sobre-mi">Sobre mí</a><a href="#materias">Materias</a><a href="#entregas">Entregas</a><a href="#actividad3">Actividad 3</a><a href="#estructura">Estructura de datos</a>
    </div>
  </nav>
</div>

<header class="hero" id="inicio">
  <div class="container hero-grid">
    <div>
      <div class="eyebrow"><span class="live-dot"></span> SISTEMA ACADÉMICO ONLINE // PORTAFOLIO_DEV_3</div>
      <p style="margin:22px 0 0;color:#a9c4d7">Hola, mi nombre es</p>
      <h1>Jerónimo Zapata <span>Vargas.</span></h1>
      <h2>Estudiante de Tecnología en Desarrollo de Software · 3.er semestre</h2>
      <p>Especializado en el diseño conceptual de sistemas, modelado UML, estructuración de bases de datos relacionales y aplicación del paradigma de Programación Orientada a Objetos.</p>
      <div class="pills"><span class="pill">JAVA</span><span class="pill">UML</span><span class="pill">POO</span><span class="pill">GITHUB</span><span class="pill">PROGRAMACIÓN FUNCIONAL</span></div>
      <div class="actions"><a class="btn" href="#materias">Explorar materias ↓</a><a class="btn secondary" href="#entregas">Ver trabajos ↗</a></div>
    </div>
    <aside class="hud" aria-label="Panel de estado académico">
      <div class="hud-top"><span>J.A.R.V.I.S. // DEV INTERFACE</span><span>SYS. 03</span></div>
      <div class="orb-wrap"><div class="orb"><div class="orb-core"></div></div></div>
      <div class="hud-bottom"><span>CORE STATUS: <strong>ONLINE</strong></span><span>JAVA // UML // POO</span></div>
    </aside>
  </div>
  <div class="container stats">
    <div class="stat"><strong>03</strong><span>Semestre académico</span></div>
    <div class="stat"><strong>JAVA</strong><span>Lenguaje principal</span></div>
    <div class="stat"><strong>POO</strong><span>Paradigma de desarrollo</span></div>
    <div class="stat"><strong>UML</strong><span>Modelado de sistemas</span></div>
  </div>
</header>

<main id="contenido">
<section id="sobre-mi">
  <div class="container">
    <div class="section-head"><div><div class="section-number">01 // PERFIL</div><h2>Sobre mí</h2></div><p>Mi proceso formativo, intereses y enfoque de desarrollo.</p></div>
    <div class="about-grid">
      <article class="panel about-copy reveal">
        <div class="kicker">Perfil del desarrollador</div>
        <p>Soy estudiante de tercer semestre de la Tecnología en Desarrollo de Software en la Institución Universitaria Digital de Antioquia.</p>
        <p>Mi enfoque formativo abarca el ciclo de vida del software, desde el análisis de sistemas y la modelación arquitectónica con UML, hasta la implementación orientada a objetos e integración con bases de datos relacionales.</p>
        <p>Actualmente continúo fortaleciendo mis conocimientos en Programación Orientada a Objetos, Java, diseño de clases, relaciones entre objetos, programación funcional y buenas prácticas de desarrollo de software.</p>
      </article>
      <aside class="panel info-list reveal">
        <div class="info-row"><span>Formación</span><strong>Desarrollo de Software</strong></div>
        <div class="info-row"><span>Institución</span><strong>IU Digital de Antioquia</strong></div>
        <div class="info-row"><span>Semestre</span><strong>Tercero</strong></div>
        <div class="info-row"><span>Enfoque</span><strong>Programación y diseño</strong></div>
        <div class="info-row"><span>Portafolio</span><strong>Evidencias académicas</strong></div>
      </aside>
    </div>
  </div>
</section>

<section id="materias" style="background:rgba(5,15,28,.42);border-block:1px solid rgba(57,231,255,.08)">
  <div class="container">
    <div class="section-head"><div><div class="section-number">02 // FORMACIÓN</div><h2>Contenido de las materias</h2></div><p>Consulta las unidades, conceptos desarrollados y contenidos académicos de cada asignatura.</p></div>
    <div class="grid-2">
      <article class="panel unit-card reveal">
        <div class="unit-label">SEMESTRE 02 // POO I</div><h3>Programación Orientada a Objetos I <span style="color:var(--muted);font-size:.8rem">(Básica)</span></h3>
        <p>Fundamentos de programación orientada a objetos y construcción de modelos mediante clases y relaciones.</p>
        <div class="resource"><span class="resource-icon">01</span><div><strong>Fundamentos de POO</strong><small>Conceptos iniciales, objetos, clases, atributos y métodos.</small></div></div>
        <div class="resource"><span class="resource-icon">02</span><div><strong>Encapsulamiento</strong><small>Estructuración, modificadores de acceso y control de datos.</small></div></div>
        <div class="resource"><span class="resource-icon">03</span><div><strong>Herencia y polimorfismo</strong><small>Relaciones entre clases y comportamiento polimórfico.</small></div></div>
        <div class="tag-list"><span class="tag">CLASES</span><span class="tag">OBJETOS</span><span class="tag">ENCAPSULAMIENTO</span><span class="tag">HERENCIA</span></div>
      </article>
      <article class="panel unit-card reveal">
        <div class="unit-label">SEMESTRE 03 // POO II</div><h3>Programación Orientada a Objetos II <span style="color:var(--muted);font-size:.8rem">(Avanzada)</span></h3>
        <p>Profundización en diseño orientado a objetos, programación funcional, arquitectura y buenas prácticas.</p>
        <div class="resource"><span class="resource-icon">01</span><div><strong>Diseño e implementación orientada a objetos</strong><small>Herencia, polimorfismo, interfaces y clases abstractas.</small></div></div>
        <div class="resource"><span class="resource-icon">02</span><div><strong>Programación avanzada y funcional</strong><small>Funciones lambda, interfaces funcionales, colecciones y Streams.</small></div></div>
        <div class="resource"><span class="resource-icon">03</span><div><strong>Arquitectura, patrones y buenas prácticas</strong><small>Espacio de profundización en arquitectura, patrones y SOLID.</small></div></div>
        <div class="tag-list"><span class="tag">JAVA</span><span class="tag">LAMBDA</span><span class="tag">STREAMS</span><span class="tag">SOLID</span></div>
      </article>
    </div>
  </div>
</section>

<section id="entregas">
  <div class="container">
    <div class="section-head"><div><div class="section-number">03 // EVIDENCIAS</div><h2>Entregables académicos</h2></div><p>Trabajos, proyectos y modelado desarrollados durante el proceso formativo. Abre cada entrega para consultar sus recursos.</p></div>
    <div class="kicker" style="margin-bottom:15px">Programación Orientada a Objetos I · Básica</div>
    <div class="grid-3">
      <article class="panel card activity-card reveal"><div class="card-content"><div class="card-top"><span class="activity-number">01</span><span class="icon-box">UML</span></div><div class="kicker">POO I · Entrega 1</div><h3>Planteando el diagrama de clase UML</h3><p>Diseño y modelado UML del sistema de biblioteca, definiendo las clases y sus relaciones.</p><div class="tag-list"><span class="tag">INDIVIDUAL</span><span class="tag">BIBLIOTECA</span><span class="tag">PDF</span></div></div><div class="card-links"><a class="text-link" target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados">Ver repositorio</a><button class="text-link" data-modal="poo1-1" style="border:0;background:none;cursor:pointer">Ver detalles</button></div></article>
      <article class="panel card activity-card reveal"><div class="card-content"><div class="card-top"><span class="activity-number">02</span><span class="icon-box">JAVA</span></div><div class="kicker">POO I · Entrega 2</div><h3>Implementación del diagrama de clases</h3><p>Implementación en lenguaje de programación de las clases planteadas en el modelo UML.</p><div class="tag-list"><span class="tag">JAVA</span><span class="tag">IMPLEMENTACIÓN</span><span class="tag">DOCX</span></div></div><div class="card-links"><button class="text-link" data-modal="poo1-2" style="border:0;background:none;cursor:pointer">Ver recursos</button></div></article>
      <article class="panel card activity-card reveal"><div class="card-content"><div class="card-top"><span class="activity-number">03</span><span class="icon-box">OOP</span></div><div class="kicker">POO I · Entrega 3</div><h3>Caso de estudio: Herencia y polimorfismo</h3><p>Aplicación de los conceptos de herencia y polimorfismo en programación orientada a objetos.</p><div class="tag-list"><span class="tag">HERENCIA</span><span class="tag">POLIMORFISMO</span><span class="tag">PDF</span></div></div><div class="card-links"><button class="text-link" data-modal="poo1-3" style="border:0;background:none;cursor:pointer">Ver detalles</button></div></article>
    </div>

    <div class="kicker" style="margin:34px 0 15px">Programación Orientada a Objetos II · Avanzada</div>
    <div class="grid-3">
      <article class="panel card activity-card reveal"><div class="card-content"><div class="card-top"><span class="activity-number">01</span><span class="icon-box">UML</span></div><div class="kicker">POO II · Actividad 1</div><h3>Diagrama de clases UML</h3><p>Análisis de requerimientos, abstracción de entidades y modelado estructural de un sistema mediante diagramas de clases UML.</p><div class="tag-list"><span class="tag">COLABORATIVO</span><span class="tag">DIAGRAMA UML</span><span class="tag">DOCUMENTO</span></div></div><div class="card-links"><button class="text-link" data-modal="poo2-1" style="border:0;background:none;cursor:pointer">Ver entregables</button></div></article>
      <article class="panel card activity-card reveal"><div class="card-content"><div class="card-top"><span class="activity-number">02</span><span class="icon-box">JAVA</span></div><div class="kicker">POO II · Actividad 2</div><h3>Implementación de diagrama de clases</h3><p>Implementación en Java del diagrama de clases, llevando el modelo conceptual a una estructura de código.</p><div class="tag-list"><span class="tag">JAVA</span><span class="tag">IMPLEMENTACIÓN</span><span class="tag">CÓDIGO FUENTE</span></div></div><div class="card-links"><button class="text-link" data-modal="poo2-2" style="border:0;background:none;cursor:pointer">Ver información</button></div></article>
      <article class="panel card activity-card reveal"><div class="card-content"><div class="card-top"><span class="activity-number">03</span><span class="icon-box">λ</span></div><div class="kicker">POO II · Actividad 3</div><h3>Programación funcional</h3><p>Procesamiento de datos con funciones puras, inmutabilidad, lambdas, Streams y composición de funciones en Java.</p><div class="tag-list"><span class="tag">LAMBDA</span><span class="tag">STREAMS</span><span class="tag">TECNOMOVIL DATA</span></div></div><div class="card-links"><a class="text-link" href="#actividad3">Explorar actividad</a><button class="text-link" data-modal="poo2-3" style="border:0;background:none;cursor:pointer">Abrir recursos</button></div></article>
    </div>
    <div class="panel" style="padding:22px;margin-top:20px">
      <div class="kicker">Estado académico // POO II</div>
      <div class="grid-3" style="margin-top:14px">
        <div><strong>Unidad 1</strong><p style="margin:5px 0;color:var(--muted);font-size:.88rem">Diseño e implementación orientada a objetos · Vista</p></div>
        <div><strong>Unidad 2</strong><p style="margin:5px 0;color:var(--muted);font-size:.88rem">Programación avanzada y funcional · En curso</p></div>
        <div><strong>Unidad 3</strong><p style="margin:5px 0;color:var(--muted);font-size:.88rem">Arquitectura, patrones y buenas prácticas · Vista</p></div>
      </div>
    </div>
  </div>
</section>

<section id="actividad3" style="background:rgba(5,15,28,.42);border-block:1px solid rgba(57,231,255,.08)">
<div class="container">
  <div class="section-head"><div><div class="section-number">04 // PROYECTO DESTACADO</div><h2>Programación funcional</h2></div><p>F30 · EA3 · TecnoMovil Data — procesamiento declarativo de información de transporte urbano con Java.</p></div>
  <div class="panel" style="padding:clamp(20px,4vw,36px)">
    <div class="grid-2">
      <div>
        <div class="kicker">Caso de estudio // TecnoMovil Data</div>
        <h3 style="font-size:1.55rem;margin:12px 0">Análisis funcional de registros de transporte</h3>
        <p style="color:var(--muted)">Sistema de procesamiento de información para transporte urbano. Los registros pueden provenir de validadores de tarjetas, sensores de estaciones, aplicaciones móviles y dispositivos IoT. La solución procesa los datos de forma declarativa mediante herramientas funcionales de Java.</p>
        <div class="resource-list">
          <div class="resource"><span class="resource-icon">⌁</span><div><strong>Registro</strong><small>Usuario, ruta, estación, acción y fecha/hora.</small></div></div>
          <div class="resource"><span class="resource-icon">↔</span><div><strong>Acciones</strong><small>Entrada y salida.</small></div></div>
          <div class="resource"><span class="resource-icon">☕</span><div><strong>Stack</strong><small>Java, sin frameworks externos.</small></div></div>
        </div>
      </div>
      <div>
        <div class="kicker">Operaciones implementadas</div>
        <div class="resource-list">
          <div class="resource"><span class="resource-icon">01</span><div><strong>Afluencia por estación</strong><small>Cuenta entradas registradas por estación.</small></div></div>
          <div class="resource"><span class="resource-icon">02</span><div><strong>Horas pico</strong><small>Agrupa registros por hora para analizar el flujo.</small></div></div>
          <div class="resource"><span class="resource-icon">03</span><div><strong>Rutas más utilizadas</strong><small>Calcula el volumen de utilización por ruta.</small></div></div>
          <div class="resource"><span class="resource-icon">04</span><div><strong>Patrones de viaje</strong><small>Ordena las estaciones visitadas por usuario según el tiempo.</small></div></div>
          <div class="resource"><span class="resource-icon">05</span><div><strong>Tiempo promedio</strong><small>Estima el tiempo entre registros consecutivos.</small></div></div>
          <div class="resource"><span class="resource-icon">06</span><div><strong>Sobrecarga de rutas</strong><small>Compara el volumen con un umbral simulado.</small></div></div>
        </div>
      </div>
    </div>
    <hr>
    <div class="kicker">Conceptos de programación funcional aplicados</div>
    <div class="checklist"><div class="check">Funciones puras</div><div class="check">Inmutabilidad</div><div class="check">Expresiones lambda</div><div class="check">Streams</div><div class="check">map / filter / reduce</div><div class="check">Funciones de orden superior</div><div class="check">Composición</div><div class="check">Parallel Stream</div><div class="check">Programación declarativa</div></div>
    <hr>
    <div class="grid-2">
      <div><div class="kicker">Código fuente // Java</div><h3>Archivos del proyecto</h3>
        <div class="resource-list">
          <div class="resource"><span class="resource-icon">01</span><div><strong>RegistroTransporte.java</strong><small>Modelo inmutable de cada registro mediante record.</small><a target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/pull/2/changes/c0a3e763de85e02e30f36d631f1c066f3dd6a2d5#diff-dfa13fbed34e863d835cb562eb52a7b16d40f9f1f547cd16bc26f0cf59e1338b">Abrir archivo ↗</a></div></div>
          <div class="resource"><span class="resource-icon">02</span><div><strong>DatosSimulados.java</strong><small>Generación de registros de prueba.</small><a target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/blob/ACTIVIDAD-2/actividad3/DatosSimulados.java">Abrir archivo ↗</a></div></div>
          <div class="resource"><span class="resource-icon">03</span><div><strong>ProcesadorTransporte.java</strong><small>Operaciones funcionales, Streams y composición.</small><a target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/blob/ACTIVIDAD-3/ProcesadorTransporte.java">Abrir archivo ↗</a></div></div>
          <div class="resource"><span class="resource-icon">04</span><div><strong>Main.java</strong><small>Ejecución del procesamiento y presentación de resultados.</small><a target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/blob/ACTIVIDAD-2/actividad3/Main.java">Abrir archivo ↗</a></div></div>
        </div>
      </div>
      <div><div class="kicker">Entregables y recursos</div><h3>Documentación y sustentación</h3>
        <div class="resource-list">
          <div class="resource"><span class="resource-icon">PDF</span><div><strong>Informe de la Actividad 3</strong><small>Portada, introducción, objetivos, implementación, evidencias y conclusiones.</small><a target="_blank" rel="noopener noreferrer" href="https://docs.google.com/document/d/1MLkBMeDfGMyZWMZ-MqeZqNCNHgZV72fJ_wmiV3UkWqA/edit?tab=t.0#heading=h.g52hfkot36m0">Abrir documento ↗</a></div></div>
          <div class="resource"><span class="resource-icon">▶</span><div><strong>Video de sustentación</strong><small>Presentación de la actividad y explicación del código.</small><a target="_blank" rel="noopener noreferrer" href="https://youtu.be/yneOzVhRDIo">Ver video ↗</a></div></div>
          <div class="resource"><span class="resource-icon">ZIP</span><div><strong>Repositorio del proyecto</strong><small>Archivos Java y recursos del proyecto.</small><a target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados">Abrir repositorio ↗</a></div></div>
        </div>
      </div>
    </div>
    <div class="callout" style="margin-top:20px">La Actividad 3 aplica la programación funcional para transformar y analizar registros de TecnoMovil Data mediante operaciones declarativas. La solución separa el modelo de datos, la generación de información y el procesamiento, facilitando la comprensión, reutilización y mantenimiento del código.</div>
  </div>
</div>
</section>

<section id="estructura">
<div class="container">
  <div class="section-head"><div><div class="section-number">05 // MÓDULO ACADÉMICO</div><h2>Estructura de datos</h2></div><p>Fundamentos para organizar, almacenar y procesar información mediante estructuras y algoritmos.</p></div>
  <div class="grid-3">
    <article class="panel card reveal"><div class="icon-box">01</div><h3>Conceptos fundamentales</h3><p>Qué son las estructuras de datos, tipos de datos, abstracción y complejidad algorítmica.</p></article>
    <article class="panel card reveal"><div class="icon-box">02</div><h3>Estructuras lineales</h3><p>Arreglos, listas enlazadas, pilas y colas, con ejemplos de implementación en Java.</p></article>
    <article class="panel card reveal"><div class="icon-box">03</div><h3>Árboles y grafos</h3><p>Estructuras no lineales, nodos, recorridos, relaciones y representación de grafos.</p></article>
    <article class="panel card reveal"><div class="icon-box">04</div><h3>Búsqueda y ordenamiento</h3><p>Búsqueda lineal y binaria, algoritmos de ordenamiento y análisis del rendimiento.</p></article>
    <article class="panel card reveal"><div class="icon-box">05</div><h3>Prácticas en Java</h3><p>Ejercicios prácticos para implementar estructuras de datos y resolver problemas.</p></article>
    <article class="panel card reveal"><div class="icon-box">06</div><h3>Talleres y evidencias</h3><p>Espacio para organizar actividades, talleres, proyectos y entregas académicas.</p></article>
  </div>
  <div class="panel" style="padding:24px;margin-top:20px"><div class="kicker">Objetivo de aprendizaje</div><p style="margin-bottom:0;color:var(--muted)">Comprender e implementar estructuras de datos utilizando Java, seleccionando la estructura adecuada según las necesidades de cada problema.</p></div>
  <div class="section-head" style="margin-top:45px"><div><div class="section-number">06 // ENTREGAS</div><h2>Las 4 entregas académicas</h2></div><p>Sección preparada para incorporar las evidencias de la materia de Estructura de Datos.</p></div>
  <div class="grid-2">
    <article class="panel card reveal"><div class="activity-number">01</div><h3>Actividad 1: Fundamentos de estructuras de datos</h3><p>Espacio para describir el primer trabajo, sus objetivos, procedimiento y conceptos aplicados.</p><div class="callout">Evidencia para publicar: documento, ejercicio, capturas o código de la actividad 1.</div><p style="font-size:.78rem">Pendiente: agrega la descripción y el enlace real de la actividad 1.</p></article>
    <article class="panel card reveal"><div class="activity-number">02</div><h3>Actividad 2: Estructuras lineales</h3><p>Documentación del segundo trabajo de Estructura de Datos y explicación de la solución desarrollada.</p><div class="callout">Evidencia para publicar: código fuente, ejercicio, capturas o documento.</div><p style="font-size:.78rem">Pendiente: agrega la descripción y el enlace real de la actividad 2.</p></article>
    <article class="panel card reveal"><div class="activity-number">03</div><h3>Actividad 3: Estructuras no lineales</h3><p>Presentación del tercer trabajo, los conceptos utilizados y la solución implementada.</p><div class="callout">Evidencia para publicar: ejercicio, código fuente, resultados o informe.</div><p style="font-size:.78rem">Pendiente: agrega la descripción y el enlace real de la actividad 3.</p></article>
    <article class="panel card reveal"><div class="activity-number">04</div><h3>Actividad 4: Proyecto o aplicación</h3><p>Documentación de la cuarta entrega, descripción del problema y aplicación de estructuras de datos.</p><div class="callout">Evidencia para publicar: proyecto, código, capturas y explicación de la solución.</div><p style="font-size:.78rem">Pendiente: agrega la descripción y el enlace real de la actividad 4.</p></article>
  </div>
</div>
</section>
</main>

<footer>
  <div class="container footer-inner">
    <div><a class="brand" href="#inicio"><span class="brand-mark">JZ</span><span>JERÓNIMO ZAPATA VARGAS</span></a><p>Software Developer Portfolio // AI SYSTEM ONLINE</p></div>
    <div><p>Programación · Inteligencia Artificial · Innovación</p><p>Diseñado y desarrollado por Jerónimo Zapata Vargas.</p><a class="text-link" target="_blank" rel="noopener noreferrer" href="https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados">Repositorio en GitHub</a></div>
  </div>
</footer>

<div class="modal" id="detailModal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
  <div class="modal-box">
    <div class="modal-head"><div><div class="kicker" id="modalKicker">DETALLE DE ENTREGA</div><h2 id="modalTitle">Entrega académica</h2></div><button class="modal-close" id="modalClose" aria-label="Cerrar ventana">✕</button></div>
    <div class="modal-body" id="modalBody"></div>
  </div>
</div>
<a class="back-top" id="backTop" href="#inicio" aria-label="Volver al inicio">↑</a>

<script>
const modalData = {
 "poo1-1": {
   kicker:"POO I · ENTREGA N.º 1", title:"Planteando el diagrama de clase UML",
   description:"Primera entrega de Programación Orientada a Objetos I, enfocada en el planteamiento y modelado del diagrama de clases UML para el sistema de biblioteca.",
   links:[["Ver EA1: Diagrama de Clases - Sistema Biblioteca","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados"]]
 },
 "poo1-2": {
   kicker:"POO I · ENTREGA N.º 2", title:"Implementación del diagrama de clases",
   description:"Segunda entrega correspondiente a la guía práctica de Programación 1 y a la implementación del modelo de clases en el lenguaje de programación.",
   links:[["Consultar repositorio del proyecto","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados"]]
 },
 "poo1-3": {
   kicker:"POO I · ENTREGA N.º 3", title:"Caso de estudio: Herencia y Polimorfismo",
   description:"Tercera entrega de Programación Orientada a Objetos I, centrada en el caso de estudio sobre herencia y polimorfismo.",
   links:[["Consultar repositorio del proyecto","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados"]]
 },
 "poo2-1": {
   kicker:"POO II · ACTIVIDAD N.º 1", title:"Diagrama de Clases UML",
   description:"Evidencia de aprendizaje relacionada con el análisis y modelado de un sistema mediante diagramas de clases UML. Integrantes: Franklin Dario Burbano Gaviria, Cristian Julian Monsalve Serna y Jeronimo Zapata Vargas.",
   links:[
     ["Google Drive","https://drive.google.com/"],
     ["Video de YouTube","https://youtu.be/"],
     ["Repositorio y documento Word","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados"],
     ["Diagrama UML","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados"]
   ]
 },
 "poo2-2": {
   kicker:"POO II · ACTIVIDAD N.º 2", title:"Implementación de Diagrama de clases",
   description:"Implementación en Java del diagrama de clases, llevando el modelo conceptual a una estructura funcional de código. Se presenta también la corrección del diagrama UML desarrollado inicialmente en la Actividad 1.",
   links:[
     ["Documento de la actividad","https://docs.google.com/document/d/1MLkBMeDfGMyZWMZ-MqeZqNCNHgZV72fJ_wmiV3UkWqA/edit?tab=t.0#heading=h.g52hfkot36m0"],
     ["Video de la actividad","https://youtu.be/yneOzVhRDIo"],
     ["Repositorio del proyecto y clases Java","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados"]
   ]
 },
 "poo2-3": {
   kicker:"POO II · ACTIVIDAD N.º 3", title:"Programación funcional · TecnoMovil Data",
   description:"Implementación de programación funcional en Java para procesar registros de transporte urbano mediante funciones puras, inmutabilidad, lambdas, interfaces funcionales, Streams y composición.",
   links:[
     ["RegistroTransporte.java","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/pull/2/changes/c0a3e763de85e02e30f36d631f1c066f3dd6a2d5#diff-dfa13fbed34e863d835cb562eb52a7b16d40f9f1f547cd16bc26f0cf59e1338b"],
     ["DatosSimulados.java","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/blob/ACTIVIDAD-2/actividad3/DatosSimulados.java"],
     ["ProcesadorTransporte.java","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/blob/ACTIVIDAD-3/ProcesadorTransporte.java"],
     ["Main.java","https://github.com/jeronimozapatav-art/Programaci-n_2_Objetos_Avanzados/blob/ACTIVIDAD-2/actividad3/Main.java"],
     ["Informe de la Actividad 3","https://docs.google.com/document/d/1MLkBMeDfGMyZWMZ-MqeZqNCNHgZV72fJ_wmiV3UkWqA/edit?tab=t.0#heading=h.g52hfkot36m0"],
     ["Video de sustentación","https://youtu.be/yneOzVhRDIo"]
   ]
 }
};
const modal=document.getElementById("detailModal");
const modalTitle=document.getElementById("modalTitle");
const modalKicker=document.getElementById("modalKicker");
const modalBody=document.getElementById("modalBody");
const closeButton=document.getElementById("modalClose");
let lastFocused=null;
function openModal(key){
  const item=modalData[key]; if(!item)return;
  lastFocused=document.activeElement;
  modalTitle.textContent=item.title;
  modalKicker.textContent=item.kicker;
  modalBody.replaceChildren();
  const p=document.createElement("p");p.textContent=item.description;modalBody.appendChild(p);
  const heading=document.createElement("h3");heading.textContent="Recursos y enlaces";modalBody.appendChild(heading);
  item.links.forEach(([label,url])=>{
    const row=document.createElement("div");row.className="resource";
    const icon=document.createElement("span");icon.className="resource-icon";icon.textContent="↗";
    const box=document.createElement("div");const link=document.createElement("a");
    link.href=url;link.target="_blank";link.rel="noopener noreferrer";link.textContent=label;
    box.appendChild(link);row.append(icon,box);modalBody.appendChild(row);
  });
  modal.classList.add("open");document.body.style.overflow="hidden";closeButton.focus();
}
function closeModal(){modal.classList.remove("open");document.body.style.overflow="";if(lastFocused)lastFocused.focus()}
document.querySelectorAll("[data-modal]").forEach(button=>button.addEventListener("click",()=>openModal(button.dataset.modal)));
closeButton.addEventListener("click",closeModal);
modal.addEventListener("click",event=>{if(event.target===modal)closeModal()});
document.addEventListener("keydown",event=>{if(event.key==="Escape"&&modal.classList.contains("open"))closeModal()});
const menuToggle=document.getElementById("menuToggle");
const navLinks=document.getElementById("navLinks");
menuToggle.addEventListener("click",()=>{
 const open=navLinks.classList.toggle("open");menuToggle.setAttribute("aria-expanded",String(open));
});
navLinks.querySelectorAll("a").forEach(link=>link.addEventListener("click",()=>{
 navLinks.classList.remove("open");menuToggle.setAttribute("aria-expanded","false");
}));
const backTop=document.getElementById("backTop");
window.addEventListener("scroll",()=>backTop.classList.toggle("visible",window.scrollY>450),{passive:true});
if("IntersectionObserver" in window){
 const observer=new IntersectionObserver(entries=>entries.forEach(entry=>{
   if(entry.isIntersecting){entry.target.classList.add("in-view");observer.unobserve(entry.target)}
 }),{threshold:.08});
 document.querySelectorAll(".reveal").forEach(el=>observer.observe(el));
}else{document.querySelectorAll(".reveal").forEach(el=>el.classList.add("in-view"))}
</script>
</body>
</html>
'''
path = Path("/mnt/data/index.html")
path.write_text(html, encoding="utf-8")
print(f"Creado: {path} ({path.stat().st_size:,} bytes)")
