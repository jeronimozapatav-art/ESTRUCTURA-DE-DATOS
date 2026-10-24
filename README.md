from pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#080d18">
<title>Jerónimo Zapata Vargas | Estructura de Datos</title>
<style>
:root{
  --bg:#080d18;--panel:#101827;--panel2:#131f31;--line:rgba(148,163,184,.16);
  --text:#eef5ff;--muted:#9aabc2;--cyan:#48e0e8;--blue:#6488ff;--purple:#a78bfa;
  --green:#53e0a0;--radius:20px;--shadow:0 18px 50px rgba(0,0,0,.28)
}
*{box-sizing:border-box}
html{scroll-behavior:smooth;scroll-padding-top:90px}
body{margin:0;background:radial-gradient(ellipse at 80% 0%,rgba(72,224,232,.10),transparent 34%),radial-gradient(ellipse at 5% 35%,rgba(100,136,255,.09),transparent 30%),var(--bg);color:var(--text);font:15px/1.6 Inter,Segoe UI,Roboto,Arial,sans-serif}
a{color:inherit;text-decoration:none}
button,input{font:inherit}
button{cursor:pointer}
.layout{display:grid;grid-template-columns:260px minmax(0,1fr);min-height:100vh}
.sidebar{height:100vh;position:sticky;top:0;border-right:1px solid var(--line);padding:26px 18px;background:rgba(8,13,24,.88);backdrop-filter:blur(18px);display:flex;flex-direction:column;gap:28px}
.brand{display:flex;align-items:center;gap:12px;padding:0 8px}
.brand-mark{width:43px;height:43px;border-radius:14px;display:grid;place-items:center;background:linear-gradient(135deg,var(--cyan),var(--blue));color:#06101b;font-weight:900;font-size:18px;box-shadow:0 0 28px rgba(72,224,232,.22)}
.brand strong{display:block;font-size:14px;letter-spacing:.02em}.brand small{color:var(--muted);font-size:11px}
.nav-label{padding:0 12px;color:#71829b;font-size:10px;font-weight:800;letter-spacing:.16em;text-transform:uppercase}
.nav{display:grid;gap:7px}.nav a{display:flex;align-items:center;gap:12px;padding:11px 13px;border:1px solid transparent;border-radius:12px;color:var(--muted);transition:.2s}
.nav a:hover,.nav a.active{color:var(--text);background:linear-gradient(100deg,rgba(72,224,232,.12),rgba(100,136,255,.08));border-color:rgba(72,224,232,.15)}
.nav-icon{width:22px;text-align:center;font-size:17px}
.side-bottom{margin-top:auto}.profile-mini{border:1px solid var(--line);border-radius:16px;background:rgba(255,255,255,.025);padding:14px;display:flex;gap:11px;align-items:center}
.avatar{height:38px;width:38px;border-radius:12px;display:grid;place-items:center;background:linear-gradient(135deg,#1d5264,#28356a);border:1px solid rgba(72,224,232,.25);font-weight:800;color:var(--cyan)}
.profile-mini strong{display:block;font-size:12px}.profile-mini small{color:var(--muted);font-size:11px}
main{min-width:0;padding:28px clamp(18px,4vw,54px) 44px;max-width:1600px;width:100%;margin:0 auto}
.topbar{display:flex;justify-content:space-between;align-items:center;gap:16px;margin-bottom:28px}
.breadcrumb{font-size:12px;color:var(--muted)}.breadcrumb span{color:var(--cyan)}
.status{display:inline-flex;align-items:center;gap:8px;border:1px solid var(--line);padding:8px 12px;border-radius:999px;color:#c6d5e8;font-size:11px;background:rgba(255,255,255,.025)}
.status i{width:7px;height:7px;border-radius:50%;background:var(--green);box-shadow:0 0 12px var(--green)}
.hero{position:relative;overflow:hidden;border:1px solid rgba(72,224,232,.19);border-radius:26px;padding:clamp(25px,4vw,48px);background:linear-gradient(120deg,rgba(17,31,48,.96),rgba(12,20,38,.91));box-shadow:var(--shadow)}
.hero:after{content:"";position:absolute;width:320px;height:320px;right:-80px;top:-130px;border-radius:50%;border:1px solid rgba(72,224,232,.17);box-shadow:0 0 0 35px rgba(72,224,232,.025),0 0 0 75px rgba(100,136,255,.025);pointer-events:none}
.eyebrow{color:var(--cyan);font-size:11px;font-weight:800;letter-spacing:.17em;text-transform:uppercase;display:flex;align-items:center;gap:10px}
.eyebrow:before{content:"";width:24px;height:2px;background:var(--cyan)}
h1{font-size:clamp(30px,4.5vw,52px);line-height:1.08;letter-spacing:-.04em;margin:17px 0 15px;max-width:700px}
.gradient-text{background:linear-gradient(90deg,#f4fbff 0%,var(--cyan) 52%,#93a8ff 100%);-webkit-background-clip:text;background-clip:text;color:transparent}
.hero p{max-width:650px;color:#aabbd0;margin:0;font-size:15px}
.hero-actions{display:flex;flex-wrap:wrap;gap:10px;margin-top:25px}
.btn{border:1px solid var(--line);border-radius:12px;padding:11px 16px;color:var(--text);background:rgba(255,255,255,.04);font-weight:700;font-size:12px;transition:.2s}
.btn:hover{transform:translateY(-2px);border-color:rgba(72,224,232,.5)}
.btn.primary{background:linear-gradient(100deg,var(--cyan),#83f0ed);color:#07121c;border:0}
.section{margin-top:38px}.section-head{display:flex;justify-content:space-between;align-items:end;gap:16px;margin-bottom:17px}
.section-head h2{margin:0;font-size:21px;letter-spacing:-.025em}.section-head p{margin:5px 0 0;color:var(--muted);font-size:12px}
.kicker{font-size:10px;letter-spacing:.14em;color:var(--cyan);font-weight:800;text-transform:uppercase}
.stats{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:14px;margin-top:18px}
.stat{padding:18px 20px;border:1px solid var(--line);border-radius:17px;background:rgba(16,24,39,.72);display:flex;gap:14px;align-items:center}
.stat-icon{width:42px;height:42px;border-radius:13px;display:grid;place-items:center;font-size:18px;background:rgba(72,224,232,.09);color:var(--cyan)}
.stat strong{display:block;font-size:23px;line-height:1.2}.stat span{color:var(--muted);font-size:11px}
.grid{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:15px}
.card{min-width:0;border:1px solid var(--line);border-radius:18px;background:linear-gradient(145deg,rgba(19,31,49,.88),rgba(13,21,35,.88));padding:20px;transition:transform .22s,border-color .22s,box-shadow .22s}
.card:hover{transform:translateY(-4px);border-color:rgba(72,224,232,.32);box-shadow:0 15px 35px rgba(0,0,0,.2)}
.card-top{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-bottom:17px}
.card-icon{height:43px;width:43px;display:grid;place-items:center;border-radius:13px;background:rgba(100,136,255,.12);color:#a9bbff;font-size:19px}
.pill{font-size:10px;padding:5px 9px;border:1px solid rgba(72,224,232,.2);color:var(--cyan);background:rgba(72,224,232,.06);border-radius:999px;white-space:nowrap}
.card h3{font-size:16px;margin:0 0 8px}.card p{color:var(--muted);font-size:12px;margin:0;min-height:42px}
.card-foot{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-top:20px;padding-top:14px;border-top:1px solid var(--line)}
.card-foot small{font-size:10px;color:#8192aa}.text-btn{background:none;border:0;color:var(--cyan);font-weight:800;font-size:11px;padding:5px 0}
.info-grid{display:grid;grid-template-columns:1.15fr .85fr;gap:15px}
.info-panel{border:1px solid var(--line);border-radius:18px;padding:22px;background:rgba(16,24,39,.72)}
.info-panel h3{margin:0 0 14px;font-size:15px}
.details{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:15px}
.detail label{display:block;color:#788ba5;font-size:10px;text-transform:uppercase;letter-spacing:.1em;margin-bottom:4px}
.detail strong{font-size:12px;font-weight:650}
.note{color:var(--muted);font-size:12px;margin:0}
.resource-line{display:flex;gap:12px;align-items:flex-start;padding:12px 0;border-bottom:1px solid var(--line)}.resource-line:last-child{border-bottom:0;padding-bottom:0}
.resource-line .r-icon{width:32px;height:32px;flex:0 0 32px;border-radius:10px;display:grid;place-items:center;background:rgba(167,139,250,.12);color:var(--purple)}
.resource-line strong{display:block;font-size:12px}.resource-line small{color:var(--muted);font-size:11px}
.progress-wrap{height:6px;border-radius:20px;background:#202c3e;overflow:hidden;margin-top:10px}.progress-bar{height:100%;width:0;background:linear-gradient(90deg,var(--cyan),var(--blue));border-radius:20px;transition:width .3s}
footer{border-top:1px solid var(--line);margin-top:44px;padding-top:20px;display:flex;justify-content:space-between;gap:12px;flex-wrap:wrap;color:#73849c;font-size:10px}
.modal-backdrop{position:fixed;inset:0;background:rgba(2,6,14,.78);backdrop-filter:blur(8px);display:none;align-items:center;justify-content:center;padding:20px;z-index:20}
.modal-backdrop.open{display:flex}.modal{width:min(560px,100%);max-height:85vh;overflow:auto;border:1px solid rgba(72,224,232,.25);border-radius:22px;background:#0f1929;box-shadow:0 25px 100px rgba(0,0,0,.5);padding:25px;animation:pop .18s ease-out}
@keyframes pop{from{opacity:0;transform:translateY(10px) scale(.98)}to{opacity:1;transform:translateY(0) scale(1)}}
.modal-head{display:flex;justify-content:space-between;gap:16px;align-items:flex-start}.modal h2{font-size:22px;margin:5px 0 8px}.modal p{color:var(--muted);font-size:13px}.close{height:34px;width:34px;border:1px solid var(--line);border-radius:10px;background:#172337;color:#dce8f8;font-size:19px}
.modal-content{border:1px solid var(--line);border-radius:14px;padding:16px;margin-top:18px;background:rgba(255,255,255,.02)}
.modal-content h4{margin:0 0 8px;font-size:12px}.modal-content ul{margin:0;padding-left:19px;color:var(--muted);font-size:12px}
.empty-hint{margin-top:14px;padding:12px;border-radius:12px;border:1px dashed rgba(72,224,232,.25);font-size:11px;color:#9eb1c9}
.mobile-menu{display:none}
@media(max-width:1100px){.grid{grid-template-columns:repeat(2,minmax(0,1fr))}.layout{grid-template-columns:225px minmax(0,1fr)}.sidebar{padding:22px 13px}}
@media(max-width:760px){.layout{display:block}.sidebar{height:auto;position:relative;padding:14px 18px;border-right:0;border-bottom:1px solid var(--line);gap:14px}.brand{padding:0}.nav-label,.side-bottom{display:none}.nav{display:flex;overflow-x:auto;padding-bottom:3px}.nav a{white-space:nowrap;padding:8px 10px;font-size:12px}.nav-icon{font-size:14px;width:auto}.layout main{padding-top:18px}.topbar{margin-bottom:18px}.stats{grid-template-columns:1fr}.grid{grid-template-columns:1fr}.info-grid{grid-template-columns:1fr}.hero:after{right:-220px}.details{grid-template-columns:1fr 1fr}}
@media(prefers-reduced-motion:reduce){*{scroll-behavior:auto!important;transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div class="layout">
  <aside class="sidebar">
    <a class="brand" href="#inicio" aria-label="Ir al inicio">
      <span class="brand-mark">JZ</span>
      <span><strong>JERÓNIMO ZAPATA</strong><small>PORTAFOLIO ACADÉMICO</small></span>
    </a>
    <div class="nav-label">Espacio de trabajo</div>
    <nav class="nav" aria-label="Navegación principal">
      <a class="active" href="#inicio"><span class="nav-icon">⌂</span>Inicio</a>
      <a href="#perfil"><span class="nav-icon">◎</span>Mi información</a>
      <a href="#unidades"><span class="nav-icon">▤</span>Unidades</a>
      <a href="#actividades"><span class="nav-icon">✓</span>Actividades</a>
      <a href="#recursos"><span class="nav-icon">↗</span>Recursos</a>
    </nav>
    <div class="side-bottom">
      <div class="profile-mini"><div class="avatar">JZ</div><div><strong>Jerónimo Zapata Vargas</strong><small>Tecnología en Desarrollo de Software</small></div></div>
    </div>
  </aside>

  <main>
    <div class="topbar">
      <div class="breadcrumb">PORTAFOLIO / <span>ESTRUCTURA DE DATOS</span></div>
      <div class="status"><i></i> Repositorio personal</div>
    </div>

    <section class="hero" id="inicio">
      <div class="eyebrow">Mi espacio académico</div>
      <h1>Repositorio de<br><span class="gradient-text">Estructura de Datos</span></h1>
      <p>Un espacio organizado para recopilar mis apuntes, aprendizajes, actividades y recursos de la asignatura. Aquí puedo consultar y actualizar el contenido de cada unidad durante el semestre.</p>
      <div class="hero-actions">
        <a class="btn primary" href="#unidades">Explorar unidades&nbsp; ↗</a>
        <a class="btn" href="#actividades">Ver actividades</a>
      </div>
    </section>

    <section class="stats" aria-label="Resumen del repositorio">
      <div class="stat"><div class="stat-icon">▤</div><div><strong>03</strong><span>Unidades académicas</span></div></div>
      <div class="stat"><div class="stat-icon">✓</div><div><strong>04</strong><span>Actividades del curso</span></div></div>
      <div class="stat"><div class="stat-icon">⌘</div><div><strong>01</strong><span>Repositorio personal</span></div></div>
    </section>

    <section class="section" id="perfil">
      <div class="section-head"><div><div class="kicker">Perfil del estudiante</div><h2>Mi información</h2><p>Datos generales de este espacio académico.</p></div></div>
      <div class="info-grid">
        <div class="info-panel">
          <h3>Información académica</h3>
          <div class="details">
            <div class="detail"><label>Nombre completo</label><strong>Jerónimo Zapata Vargas</strong></div>
            <div class="detail"><label>Programa</label><strong>Tecnología en Desarrollo de Software</strong></div>
            <div class="detail"><label>Asignatura</label><strong>Estructura de Datos</strong></div>
            <div class="detail"><label>Tipo de espacio</label><strong>Repositorio de aprendizaje</strong></div>
          </div>
        </div>
        <div class="info-panel">
          <h3>Propósito del repositorio</h3>
          <p class="note">Organizar el material del curso, registrar los avances de cada unidad y reunir las evidencias de las actividades en un solo lugar.</p>
          <div class="progress-wrap" aria-label="Progreso del repositorio"><div class="progress-bar" id="progressBar"></div></div>
          <p class="note" id="progressText" style="margin-top:8px">Contenido pendiente de completar según el avance de la asignatura.</p>
        </div>
      </div>
    </section>

    <section class="section" id="unidades">
      <div class="section-head"><div><div class="kicker">Contenido del curso</div><h2>Unidades de aprendizaje</h2><p>Selecciona una unidad para consultar su espacio de trabajo.</p></div></div>
      <div class="grid">
        <article class="card">
          <div class="card-top"><div class="card-icon">01</div><span class="pill">Unidad 01</span></div>
          <h3>Unidad 1</h3><p>Espacio para conceptos, apuntes, ejemplos y material de estudio de la primera unidad.</p>
          <div class="card-foot"><small>Apuntes · Material · Repaso</small><button class="text-btn" data-open="unit1">Abrir unidad ↗</button></div>
        </article>
        <article class="card">
          <div class="card-top"><div class="card-icon">02</div><span class="pill">Unidad 02</span></div>
          <h3>Unidad 2</h3><p>Organiza aquí los temas trabajados, ejercicios prácticos y notas importantes de la segunda unidad.</p>
          <div class="card-foot"><small>Apuntes · Material · Repaso</small><button class="text-btn" data-open="unit2">Abrir unidad ↗</button></div>
        </article>
        <article class="card">
          <div class="card-top"><div class="card-icon">03</div><span class="pill">Unidad 03</span></div>
          <h3>Unidad 3</h3><p>Reúne el contenido de la tercera unidad, ejemplos de código y conclusiones de aprendizaje.</p>
          <div class="card-foot"><small>Apuntes · Material · Repaso</small><button class="text-btn" data-open="unit3">Abrir unidad ↗</button></div>
        </article>
      </div>
    </section>

    <section class="section" id="actividades">
      <div class="section-head"><div><div class="kicker">Seguimiento académico</div><h2>Actividades</h2><p>Cuatro espacios para documentar el desarrollo y las evidencias.</p></div></div>
      <div class="grid">
        <article class="card"><div class="card-top"><div class="card-icon">✎</div><span class="pill">Actividad 01</span></div><h3>Actividad 1</h3><p>Descripción, instrucciones, solución y evidencias de la primera actividad.</p><div class="card-foot"><small>Estado: por completar</small><button class="text-btn" data-open="act1">Ver actividad ↗</button></div></article>
        <article class="card"><div class="card-top"><div class="card-icon">⌘</div><span class="pill">Actividad 02</span></div><h3>Actividad 2</h3><p>Documenta el procedimiento, los aprendizajes y los archivos correspondientes.</p><div class="card-foot"><small>Estado: por completar</small><button class="text-btn" data-open="act2">Ver actividad ↗</button></div></article>
        <article class="card"><div class="card-top"><div class="card-icon">⌨</div><span class="pill">Actividad 03</span></div><h3>Actividad 3</h3><p>Registra el desarrollo, las pruebas realizadas y las conclusiones de la actividad.</p><div class="card-foot"><small>Estado: por completar</small><button class="text-btn" data-open="act3">Ver actividad ↗</button></div></article>
        <article class="card"><div class="card-top"><div class="card-icon">◈</div><span class="pill">Actividad 04</span></div><h3>Actividad 4</h3><p>Espacio para incluir el trabajo final, soportes y reflexión sobre lo aprendido.</p><div class="card-foot"><small>Estado: por completar</small><button class="text-btn" data-open="act4">Ver actividad ↗</button></div></article>
      </div>
    </section>

    <section class="section" id="recursos">
      <div class="section-head"><div><div class="kicker">Material de apoyo</div><h2>Recursos</h2><p>Zona preparada para enlaces, documentos y herramientas del curso.</p></div></div>
      <div class="info-grid">
        <div class="info-panel">
          <div class="resource-line"><div class="r-icon">▧</div><div><strong>Documentos de clase</strong><small>Agrega aquí guías, lecturas y presentaciones compartidas por el docente.</small></div></div>
          <div class="resource-line"><div class="r-icon">⌘</div><div><strong>Ejemplos de código</strong><small>Organiza ejercicios y programas utilizados para practicar los conceptos.</small></div></div>
          <div class="resource-line"><div class="r-icon">↗</div><div><strong>Enlaces de consulta</strong><small>Incluye enlaces confiables relacionados con los contenidos de la asignatura.</small></div></div>
        </div>
        <div class="info-panel"><h3>Personaliza tu repositorio</h3><p class="note">Este archivo funciona localmente en tu navegador. Puedes editar el código para reemplazar los textos de ejemplo por los temas reales de cada unidad, adjuntar enlaces y actualizar el estado de las actividades.</p><div class="empty-hint">Nota: los temas específicos de las unidades no se inventaron; se pueden completar con la guía oficial de la asignatura.</div></div>
      </div>
    </section>

    <footer><span>© 2026 · Jerónimo Zapata Vargas</span><span>Repositorio personal · Estructura de Datos</span></footer>
  </main>
</div>

<div class="modal-backdrop" id="modalBackdrop" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
  <div class="modal">
    <div class="modal-head"><div><div class="kicker" id="modalKicker">ESPACIO ACADÉMICO</div><h2 id="modalTitle">Contenido</h2><p id="modalDescription">Aquí se organizará el contenido de este apartado.</p></div><button class="close" id="closeModal" aria-label="Cerrar ventana">×</button></div>
    <div class="modal-content"><h4>Contenido de este espacio</h4><ul id="modalList"><li>Apuntes y conceptos principales.</li><li>Ejemplos, ejercicios o instrucciones.</li><li>Archivos, enlaces y evidencias.</li></ul></div>
    <div class="empty-hint">Este apartado está preparado para completar con el material real de la asignatura. Puedes editar el HTML para agregar tus contenidos.</div>
    <div style="display:flex;justify-content:flex-end;margin-top:18px"><button class="btn primary" id="doneModal">Entendido</button></div>
  </div>
</div>

<script>
const content = {
  unit1:{kicker:'UNIDAD DE APRENDIZAJE · 01',title:'Unidad 1',description:'Espacio de trabajo para la primera unidad de Estructura de Datos.',items:['Conceptos y apuntes principales','Ejemplos y ejercicios desarrollados','Material de clase y repaso']},
  unit2:{kicker:'UNIDAD DE APRENDIZAJE · 02',title:'Unidad 2',description:'Espacio de trabajo para la segunda unidad de Estructura de Datos.',items:['Conceptos y apuntes principales','Ejemplos y ejercicios desarrollados','Material de clase y repaso']},
  unit3:{kicker:'UNIDAD DE APRENDIZAJE · 03',title:'Unidad 3',description:'Espacio de trabajo para la tercera unidad de Estructura de Datos.',items:['Conceptos y apuntes principales','Ejemplos y ejercicios desarrollados','Material de clase y repaso']},
  act1:{kicker:'SEGUIMIENTO · ACTIVIDAD 01',title:'Actividad 1',description:'Documenta aquí las indicaciones y el desarrollo de la actividad 1.',items:['Enunciado e instrucciones','Procedimiento y solución','Evidencias o archivos entregables']},
  act2:{kicker:'SEGUIMIENTO · ACTIVIDAD 02',title:'Actividad 2',description:'Documenta aquí las indicaciones y el desarrollo de la actividad 2.',items:['Enunciado e instrucciones','Procedimiento y solución','Evidencias o archivos entregables']},
  act3:{kicker:'SEGUIMIENTO · ACTIVIDAD 03',title:'Actividad 3',description:'Documenta aquí las indicaciones y el desarrollo de la actividad 3.',items:['Enunciado e instrucciones','Procedimiento y solución','Evidencias o archivos entregables']},
  act4:{kicker:'SEGUIMIENTO · ACTIVIDAD 04',title:'Actividad 4',description:'Documenta aquí las indicaciones y el desarrollo de la actividad 4.',items:['Enunciado e instrucciones','Procedimiento y solución','Evidencias o archivos entregables']}
};
const backdrop=document.getElementById('modalBackdrop');
function openModal(key){
 const item=content[key]; if(!item)return;
 document.getElementById('modalKicker').textContent=item.kicker;
 document.getElementById('modalTitle').textContent=item.title;
 document.getElementById('modalDescription').textContent=item.description;
 const list=document.getElementById('modalList');list.innerHTML='';
 item.items.forEach(text=>{const li=document.createElement('li');li.textContent=text;list.appendChild(li)});
 backdrop.classList.add('open');document.body.style.overflow='hidden';document.getElementById('closeModal').focus();
}
function closeModal(){backdrop.classList.remove('open');document.body.style.overflow=''}
document.querySelectorAll('[data-open]').forEach(button=>button.addEventListener('click',()=>openModal(button.dataset.open)));
document.getElementById('closeModal').addEventListener('click',closeModal);
document.getElementById('doneModal').addEventListener('click',closeModal);
backdrop.addEventListener('click',event=>{if(event.target===backdrop)closeModal()});
document.addEventListener('keydown',event=>{if(event.key==='Escape')closeModal()});
const navLinks=[...document.querySelectorAll('.nav a')];
const sections=navLinks.map(link=>document.querySelector(link.getAttribute('href'))).filter(Boolean);
if('IntersectionObserver' in window){
 const observer=new IntersectionObserver(entries=>entries.forEach(entry=>{if(entry.isIntersecting){navLinks.forEach(link=>link.classList.toggle('active',link.getAttribute('href')==='#'+entry.target.id))}}),{rootMargin:'-25% 0px -65% 0px'});
 sections.forEach(section=>observer.observe(section));
}
document.getElementById('progressBar').style.width='8%';
</script>
</body>
</html>'''

path = Path("/mnt/data/Repositorio_Estructura_de_Datos_Profesional.html")
path.write_text(html, encoding="utf-8")
print(f"Archivo creado: {path} | Tamaño: {path.stat().st_size:,} bytes")

