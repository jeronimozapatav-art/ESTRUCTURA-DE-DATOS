from pathlib import Path

path = Path("/mnt/data/Repositorio_Estructura_de_Datos.html")
html = path.read_text(encoding="utf-8")

# Replace broad multi-unit structure with the exact requested organization.
start = html.index('<section class="section" id="unidades">')
end = html.index('<section class="section two-col" id="recursos">')
replacement = r'''<section class="section" id="personal">
<div class="section-head"><div><h2>Mi información personal</h2><p>Datos del estudiante y presentación del repositorio.</p></div></div>
<div class="card">
  <p><strong>Nombre:</strong> Jerónimo Zapata Vargas</p>
  <p><strong>Programa:</strong> Tecnología en Desarrollo de Software</p>
  <p><strong>Asignatura:</strong> Estructura de Datos</p>
  <p><strong>Propósito:</strong> Organizar los contenidos de las unidades y las actividades desarrolladas durante la materia.</p>
  <p style="color:var(--muted);font-size:.9rem">Puedes editar estos datos directamente en el archivo HTML si necesitas agregar institución, docente, grupo o semestre.</p>
</div>
</section>

<section class="section" id="unidades">
<div class="section-head"><div><h2>Estructura de Datos</h2><p>Solo las tres unidades de la materia, como solicitaste.</p></div></div>
<div class="grid" id="unitsGrid">
<article class="unit"><span class="number">UNIDAD 01</span><h3>Unidad 1</h3><p>Espacio para los temas, apuntes, documentos y ejemplos correspondientes a la primera unidad.</p><div><span class="tag">Teoría</span><span class="tag">Apuntes</span></div><button class="btn" onclick="openUnit(0)">Ver unidad</button></article>
<article class="unit"><span class="number">UNIDAD 02</span><h3>Unidad 2</h3><p>Espacio para el contenido de la segunda unidad, sus ejercicios y códigos de práctica.</p><div><span class="tag">Ejercicios</span><span class="tag">Java</span></div><button class="btn" onclick="openUnit(1)">Ver unidad</button></article>
<article class="unit"><span class="number">UNIDAD 03</span><h3>Unidad 3</h3><p>Espacio para las guías, ejemplos, apuntes y materiales de la tercera unidad.</p><div><span class="tag">Guías</span><span class="tag">Materiales</span></div><button class="btn" onclick="openUnit(2)">Ver unidad</button></article>
</div>
</section>

<section class="section" id="actividades">
<div class="section-head"><div><h2>Actividades</h2><p>Organiza las cuatro actividades de la asignatura.</p></div></div>
<div class="grid">
<article class="unit"><span class="number">ACTIVIDAD 01</span><h3>Actividad 1</h3><p>Espacio para la descripción, archivos, desarrollo y evidencias de la primera actividad.</p><button class="btn" onclick="openActivity(0)">Ver actividad</button></article>
<article class="unit"><span class="number">ACTIVIDAD 02</span><h3>Actividad 2</h3><p>Espacio para las instrucciones y el trabajo realizado en la segunda actividad.</p><button class="btn" onclick="openActivity(1)">Ver actividad</button></article>
<article class="unit"><span class="number">ACTIVIDAD 03</span><h3>Actividad 3</h3><p>Espacio para guardar el desarrollo y los recursos de la tercera actividad.</p><button class="btn" onclick="openActivity(2)">Ver actividad</button></article>
<article class="unit"><span class="number">ACTIVIDAD 04</span><h3>Actividad 4</h3><p>Espacio para reunir los archivos y evidencias de la cuarta actividad.</p><button class="btn" onclick="openActivity(3)">Ver actividad</button></article>
</div>
</section>

'''
html = html[:start] + replacement + html[end:]

# Remove prior example sections that imply a different content organization.
start2 = html.index('<section class="section two-col" id="recursos">')
end2 = html.index('</main>', start2)
replacement2 = r'''<section class="section" id="recursos">
<div class="card"><h2>Recursos de la materia</h2><p>En esta sección puedes organizar enlaces y materiales de Estructura de Datos: guías del profesor, documentos PDF, apuntes y códigos Java.</p><p style="color:var(--muted)">Los archivos y las instrucciones reales se pueden incorporar cuando los tengas disponibles.</p></div>
</section>
'''
html = html[:start2] + replacement2 + html[end2:]

# Update navigation.
html = html.replace('<a href="#inicio">Inicio</a><a href="#unidades">Unidades</a><a href="#recursos">Recursos</a><a href="#actividades">Actividades</a>',
                    '<a href="#inicio">Inicio</a><a href="#personal">Mi información</a><a href="#unidades">Unidades</a><a href="#actividades">Actividades</a><a href="#recursos">Recursos</a>')

# Update hero stats and intro.
html = html.replace('Un espacio académico para organizar apuntes, practicar algoritmos, consultar ejemplos en Java y reunir los trabajos de la materia en un solo lugar.',
                    'Mi espacio académico personal para organizar la materia en tres unidades y cuatro actividades, con sus documentos, apuntes y evidencias.')
html = html.replace('<strong>08</strong><span>Unidades sugeridas</span>', '<strong>03</strong><span>Unidades de la materia</span>')
html = html.replace('<strong>Java</strong><span>Lenguaje principal de ejemplos</span>', '<strong>04</strong><span>Actividades</span>')
html = html.replace('<strong>01</strong><span>Repositorio para esta materia</span>', '<strong>100%</strong><span>Dedicado a Estructura de Datos</span>')

# Replace JS unit details and add activity handler.
js_start = html.index('const details=[')
js_end = html.index("const search=document.getElementById('search')", js_start)
js = r'''const details=[
["Unidad 1","Aquí se agregarán los temas, apuntes, documentos y ejercicios de la Unidad 1."],
["Unidad 2","Aquí se agregarán los temas, apuntes, documentos y ejercicios de la Unidad 2."],
["Unidad 3","Aquí se agregarán los temas, apuntes, documentos y ejercicios de la Unidad 3."]
];
function openUnit(i){
 const [name,description]=details[i];
 document.getElementById('unitContent').innerHTML='<p class="kicker">ESTRUCTURA DE DATOS</p><h2>'+name+'</h2><p style="color:#c5d8e8">'+description+'</p><p style="color:#9bb1c6">Cuando compartas los materiales de esta unidad, podemos incorporarlos aquí sin inventar el contenido del curso.</p>';
 document.getElementById('unitDialog').showModal();
}
function openActivity(i){
 const name='Actividad '+(i+1);
 document.getElementById('unitContent').innerHTML='<p class="kicker">ACTIVIDADES</p><h2>'+name+'</h2><p style="color:#c5d8e8">Espacio para la descripción, instrucciones, desarrollo, archivos y evidencias de '+name.toLowerCase()+'.</p><p style="color:#9bb1c6">Los detalles se completarán con las instrucciones reales de la actividad.</p>';
 document.getElementById('unitDialog').showModal();
}
'''
html = html[:js_start] + js + html[js_end:]
# Remove obsolete search/filter listeners, since these controls were removed.
old = """const search=document.getElementById('search'),filter=document.getElementById('filter');
function applyFilters(){let q=search.value.toLowerCase().trim(),cat=filter.value,shown=0;document.querySelectorAll('.unit').forEach(el=>{let ok=(cat==='all'||el.dataset.category===cat)&&((el.dataset.search+' '+el.innerText).toLowerCase().includes(q));el.style.display=ok?'flex':'none';if(ok)shown++});document.getElementById('empty').style.display=shown?'none':'block'}
search.addEventListener('input',applyFilters);filter.addEventListener('change',applyFilters);"""
html = html.replace(old, "")
html = html.replace('Repositorio académico · Estructura de Datos · Tecnología en Desarrollo de Software', 'Repositorio personal · Estructura de Datos · Tecnología en Desarrollo de Software')
path.write_text(html, encoding="utf-8")
print("Repositorio actualizado con información personal, 3 unidades y 4 actividades.")
