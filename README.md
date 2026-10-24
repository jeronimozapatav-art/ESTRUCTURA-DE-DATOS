from pathlib import Path

path = Path("/mnt/data/Repositorio_Estructura_de_Datos_Profesional.html")
html = path.read_text(encoding="utf-8")

# Enhance the existing professional design without replacing its page structure.
# Add a polished evidence gallery to Activity 1, while preserving all provided links.
style_add = r'''
/* Galería de evidencias de la Actividad 1 */
.evidence-gallery{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;margin-top:14px}
.evidence-card{overflow:hidden;border:1px solid var(--line);border-radius:13px;background:rgba(255,255,255,.025);transition:border-color .2s,transform .2s}
.evidence-card:hover{border-color:rgba(72,224,232,.4);transform:translateY(-2px)}
.evidence-card a{display:block}
.evidence-card img{display:block;width:100%;height:150px;object-fit:cover;background:#0a1220}
.evidence-caption{padding:10px 11px;display:flex;align-items:center;justify-content:space-between;gap:8px;font-size:11px}
.evidence-caption strong{font-weight:700}.evidence-caption span{color:var(--cyan);font-size:10px}
.source-links{display:flex;flex-wrap:wrap;gap:9px;margin-top:12px}
.source-links a{display:inline-flex;align-items:center;gap:8px;border:1px solid rgba(72,224,232,.2);border-radius:10px;padding:9px 12px;color:var(--cyan);background:rgba(72,224,232,.05);font-size:11px;font-weight:750}
.source-links a:hover{background:rgba(72,224,232,.12)}
@media(max-width:520px){.evidence-gallery{grid-template-columns:1fr}.evidence-card img{height:185px}}
'''
if '/* Galería de evidencias de la Actividad 1 */' not in html:
    html = html.replace('</style>', style_add + '\n</style>', 1)

# Add the evidence UI inside the existing modal, without altering other sections.
modal_anchor = '''    <div class="modal-content" id="activityEvidenceLinks" style="display:none">'''
gallery_ui = '''    <div class="modal-content" id="activityEvidenceGallery" style="display:none">
      <h4>Vista previa de evidencias</h4>
      <p class="note">Selecciona una imagen para abrir el archivo original en GitHub.</p>
      <div class="evidence-gallery" id="evidenceGallery"></div>
    </div>
'''
if 'id="activityEvidenceGallery"' not in html:
    html = html.replace(modal_anchor, gallery_ui + modal_anchor, 1)

# Replace the plain text list with a neat, professional set of links, preserving all URLs.
start = html.find('    <div class="modal-content" id="activityEvidenceLinks" style="display:none">')
if start != -1:
    end = html.find('    </div>', start)
    # The first closing div would be the outer modal block because list is plain HTML.
    end = end + len('    </div>')
    replacement = '''    <div class="modal-content" id="activityEvidenceLinks" style="display:none">
      <h4>Código fuente del proyecto</h4>
      <p class="note">Abre los archivos Java del proyecto en GitHub.</p>
      <div class="source-links">
        <a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Estudiante.java" target="_blank" rel="noopener noreferrer">⌘ Estudiante.java ↗</a>
        <a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Curso.java" target="_blank" rel="noopener noreferrer">⌘ Curso.java ↗</a>
        <a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Main.java" target="_blank" rel="noopener noreferrer">⌘ Main.java ↗</a>
      </div>
      <div style="margin-top:15px">
        <h4>Todos los archivos de evidencias</h4>
        <ul>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/DIAGRAMA.png" target="_blank" rel="noopener noreferrer">DIAGRAMA.png</a></li>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%201.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 1.png</a></li>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%202.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 2.png</a></li>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%203.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 3.png</a></li>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%204.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 4.png</a></li>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%205.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 5.png</a></li>
          <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%206.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 6.png</a></li>
        </ul>
      </div>
    </div>'''
    html = html[:start] + replacement + html[end:]

# Add rendering of image previews and toggle gallery only for Activity 1.
js_anchor = """function openModal(key){
 const item=content[key]; if(!item)return;"""
gallery_js = r"""const evidenceImages=[
 {name:'Diagrama del proyecto',file:'DIAGRAMA.png'},
 {name:'Evidencia 1',file:'EVIDENCIA%201.png'},
 {name:'Evidencia 2',file:'EVIDENCIA%202.png'},
 {name:'Evidencia 3',file:'EVIDENCIA%203.png'},
 {name:'Evidencia 4',file:'EVIDENCIA%204.png'},
 {name:'Evidencia 5',file:'EVIDENCIA%205.png'},
 {name:'Evidencia 6',file:'EVIDENCIA%206.png'}
];
function renderEvidenceGallery(){
 const gallery=document.getElementById('evidenceGallery');
 if(!gallery || gallery.dataset.loaded==='yes')return;
 const base='https://raw.githubusercontent.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/main/';
 evidenceImages.forEach(item=>{
   const card=document.createElement('div');card.className='evidence-card';
   const link=document.createElement('a');
   link.href='https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/'+item.file;
   link.target='_blank';link.rel='noopener noreferrer';link.title='Abrir '+item.name+' en GitHub';
   const img=document.createElement('img');img.src=base+item.file;img.alt=item.name;img.loading='lazy';
   img.onerror=()=>{img.style.display='none'};
   link.appendChild(img);card.appendChild(link);
   const caption=document.createElement('div');caption.className='evidence-caption';
   const label=document.createElement('strong');label.textContent=item.name;
   const open=document.createElement('span');open.textContent='Ver ↗';
   caption.append(label,open);card.appendChild(caption);gallery.appendChild(card);
 });
 gallery.dataset.loaded='yes';
}
function openModal(key){
 const item=content[key]; if(!item)return;"""
if 'function renderEvidenceGallery()' not in html:
    html = html.replace(js_anchor, gallery_js, 1)

# Add show/hide gallery and links in openModal without disturbing existing modal logic.
needle = """ const evidenceLinks=document.getElementById('activityEvidenceLinks');
 if(evidenceLinks)evidenceLinks.style.display=key==='act1'?'block':'none';
 backdrop.classList.add('open');"""
replacement = """ const evidenceLinks=document.getElementById('activityEvidenceLinks');
 const evidenceGallery=document.getElementById('activityEvidenceGallery');
 if(evidenceLinks)evidenceLinks.style.display=key==='act1'?'block':'none';
 if(evidenceGallery)evidenceGallery.style.display=key==='act1'?'block':'none';
 if(key==='act1')renderEvidenceGallery();
 backdrop.classList.add('open');"""
if needle in html:
    html = html.replace(needle, replacement, 1)

path.write_text(html, encoding="utf-8")
print(f"Página mejorada sin reconstruirla: {path}")
print(f"Tamaño: {path.stat().st_size:,} bytes")
print("Se conservó la estructura existente y se añadió una galería visual más profesional para las evidencias de Actividad 1.")
