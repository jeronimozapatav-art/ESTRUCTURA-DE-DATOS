from pathlib import Path
p = Path("/mnt/data/Repositorio_Estructura_de_Datos_Profesional.html")
html = p.read_text(encoding="utf-8")

# Add styling for evidence gallery and source-code links
style_insert = r'''
.evidence-gallery{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;margin-top:14px}
.evidence-card{overflow:hidden;border:1px solid var(--line);border-radius:13px;background:rgba(255,255,255,.025)}
.evidence-card a{display:block}
.evidence-card img{display:block;width:100%;height:155px;object-fit:cover;background:#0a1220;transition:transform .2s}
.evidence-card a:hover img{transform:scale(1.025)}
.evidence-caption{padding:10px 11px;display:flex;align-items:center;justify-content:space-between;gap:8px;font-size:11px}
.evidence-caption strong{font-weight:700}.evidence-caption span{color:var(--cyan);font-size:10px}
.source-links{display:flex;flex-wrap:wrap;gap:9px;margin-top:12px}
.source-links a{display:inline-flex;align-items:center;gap:8px;border:1px solid rgba(72,224,232,.2);border-radius:10px;padding:9px 12px;color:var(--cyan);background:rgba(72,224,232,.05);font-size:11px;font-weight:750}
.source-links a:hover{background:rgba(72,224,232,.12)}
@media(max-width:520px){.evidence-gallery{grid-template-columns:1fr}.evidence-card img{height:190px}}
'''
html = html.replace('</style>', style_insert + '\n</style>', 1)

# Add evidence section area in modal after the modal-content block
needle = '''    <div class="empty-hint">Este apartado está preparado para completar con el material real de la asignatura. Puedes editar el HTML para agregar tus contenidos.</div>'''
replacement = '''    <div id="evidenceSection" style="display:none">
      <div class="modal-content">
        <h4>📷 Evidencias del trabajo</h4>
        <p class="note">Selecciona una imagen para verla en tamaño completo. Los archivos se cargan desde tu repositorio de GitHub.</p>
        <div class="evidence-gallery" id="evidenceGallery"></div>
      </div>
      <div class="modal-content">
        <h4>⌨ Código fuente del proyecto</h4>
        <p class="note">Consulta los archivos Java utilizados en el ejercicio.</p>
        <div class="source-links" id="sourceLinks"></div>
      </div>
    </div>
    <div class="empty-hint">Este apartado está preparado para completar con el material real de la asignatura. Puedes editar el HTML para agregar tus contenidos.</div>'''
html = html.replace(needle, replacement, 1)

# Add evidence metadata to Activity 1 object
old = """  act1:{kicker:'SEGUIMIENTO · ACTIVIDAD 01',title:'Actividad 1',description:'Documenta aquí las indicaciones y el desarrollo de la actividad 1.',items:['Enunciado e instrucciones','Procedimiento y solución','Evidencias o archivos entregables']},"""
new = """  act1:{kicker:'SEGUIMIENTO · ACTIVIDAD 01',title:'Actividad 1',description:'Consulta las evidencias visuales, el diagrama y el código fuente del proyecto de Estructura de Datos.',items:['Diagrama del proyecto','Seis evidencias visuales del desarrollo','Archivos fuente: Estudiante.java, Curso.java y Main.java'],evidence:true},"""
html = html.replace(old, new, 1)

# Add image/source data and rendering logic before function openModal
needle_js = """function openModal(key){
 const item=content[key]; if(!item)return;"""
replacement_js = r"""const githubRaw='https://raw.githubusercontent.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/main/';
const evidenceFiles=[
 {name:'Diagrama del proyecto',file:'DIAGRAMA.png'},
 {name:'Evidencia 1',file:'EVIDENCIA%201.png'},
 {name:'Evidencia 2',file:'EVIDENCIA%202.png'},
 {name:'Evidencia 3',file:'EVIDENCIA%203.png'},
 {name:'Evidencia 4',file:'EVIDENCIA%204.png'},
 {name:'Evidencia 5',file:'EVIDENCIA%205.png'},
 {name:'Evidencia 6',file:'EVIDENCIA%206.png'}
];
const sourceFiles=[
 {name:'Estudiante.java',file:'Estudiante.java'},
 {name:'Curso.java',file:'Curso.java'},
 {name:'Main.java',file:'Main.java'}
];
function renderEvidence(){
 const gallery=document.getElementById('evidenceGallery');
 gallery.innerHTML='';
 evidenceFiles.forEach(item=>{
   const card=document.createElement('div');card.className='evidence-card';
   const link=document.createElement('a');link.href=githubRaw+item.file;link.target='_blank';link.rel='noopener noreferrer';link.title='Abrir '+item.name+' en tamaño completo';
   const img=document.createElement('img');img.src=githubRaw+item.file;img.alt=item.name;img.loading='lazy';
   img.onerror=()=>{img.alt=item.name+' (vista previa no disponible)';img.style.objectFit='contain';img.style.padding='20px';img.src='data:image/svg+xml;charset=UTF-8,'+encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" width="320" height="160"><rect width="100%" height="100%" fill="#0a1220"/><text x="50%" y="48%" fill="#48e0e8" font-size="14" text-anchor="middle">Vista previa no disponible</text><text x="50%" y="66%" fill="#9aabc2" font-size="11" text-anchor="middle">Abre el archivo en GitHub</text></svg>')};
   link.appendChild(img);card.appendChild(link);
   const caption=document.createElement('div');caption.className='evidence-caption';
   const label=document.createElement('strong');label.textContent=item.name;
   const open=document.createElement('span');open.textContent='Ver ↗';
   caption.append(label,open);card.appendChild(caption);gallery.appendChild(card);
 });
 const sources=document.getElementById('sourceLinks');sources.innerHTML='';
 sourceFiles.forEach(item=>{const a=document.createElement('a');a.href='https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/'+item.file;a.target='_blank';a.rel='noopener noreferrer';a.textContent='⌘ '+item.name+' ↗';sources.appendChild(a)});
}
function openModal(key){
 const item=content[key]; if(!item)return;"""
html = html.replace(needle_js, replacement_js, 1)

# Add show/hide evidence behavior in openModal after list rendering
old = """ item.items.forEach(text=>{const li=document.createElement('li');li.textContent=text;list.appendChild(li)});
 backdrop.classList.add('open');document.body.style.overflow='hidden';document.getElementById('closeModal').focus();"""
new = """ item.items.forEach(text=>{const li=document.createElement('li');li.textContent=text;list.appendChild(li)});
 const evidenceSection=document.getElementById('evidenceSection');
 evidenceSection.style.display=item.evidence?'block':'none';
 if(item.evidence)renderEvidence();
 backdrop.classList.add('open');document.body.style.overflow='hidden';document.getElementById('closeModal').focus();"""
html = html.replace(old, new, 1)

p.write_text(html, encoding="utf-8")
print(f"Actualizado: {p}\nTamaño: {p.stat().st_size:,} bytes\nIncluye galería de 7 imágenes y enlaces a 3 archivos Java.")
