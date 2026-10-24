from pathlib import Path

path = Path("/mnt/data/Repositorio_Estructura_de_Datos_Profesional.html")
html = path.read_text(encoding="utf-8")

# Keep the existing professional page and its layout. Remove the gallery additions,
# then add only plain evidence/source links inside the Activity 1 modal.
gallery_css = r'''
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
html = html.replace(gallery_css, "")

# Remove the gallery block added to the modal
gallery_block = '''    <div id="evidenceSection" style="display:none">
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
'''
html = html.replace(gallery_block, "")

# Restore activity 1 description/items to generic activity wording; add links separately in modal via data.
html = html.replace(
"act1:{kicker:'SEGUIMIENTO · ACTIVIDAD 01',title:'Actividad 1',description:'Consulta las evidencias visuales, el diagrama y el código fuente del proyecto de Estructura de Datos.',items:['Diagrama del proyecto','Seis evidencias visuales del desarrollo','Archivos fuente: Estudiante.java, Curso.java y Main.java'],evidence:true},",
"act1:{kicker:'SEGUIMIENTO · ACTIVIDAD 01',title:'Actividad 1',description:'Documenta aquí las indicaciones y el desarrollo de la actividad 1.',items:['Enunciado e instrucciones','Procedimiento y solución','Evidencias o archivos entregables']},"
)

# Remove image gallery/source JavaScript, leaving the rest of the existing JavaScript untouched.
start = html.find("const githubRaw='https://raw.githubusercontent.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/main/';")
end = html.find("function openModal(key){", start)
if start != -1 and end != -1:
    html = html[:start] + html[end:]

html = html.replace(
""" item.items.forEach(text=>{const li=document.createElement('li');li.textContent=text;list.appendChild(li)});
 const evidenceSection=document.getElementById('evidenceSection');
 evidenceSection.style.display=item.evidence?'block':'none';
 if(item.evidence)renderEvidence();
 backdrop.classList.add('open');document.body.style.overflow='hidden';document.getElementById('closeModal').focus();""",
""" item.items.forEach(text=>{const li=document.createElement('li');li.textContent=text;list.appendChild(li)});
 const evidenceLinks=document.getElementById('activityEvidenceLinks');
 if(evidenceLinks)evidenceLinks.style.display=key==='act1'?'block':'none';
 backdrop.classList.add('open');document.body.style.overflow='hidden';document.getElementById('closeModal').focus();"""
)

# Add a compact plain-link section in the modal. No images, no new gallery behavior.
needle = '''    <div class="empty-hint">Este apartado está preparado para completar con el material real de la asignatura. Puedes editar el HTML para agregar tus contenidos.</div>'''
links_block = '''    <div class="modal-content" id="activityEvidenceLinks" style="display:none">
      <h4>Enlaces de evidencias y código</h4>
      <ul>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/DIAGRAMA.png" target="_blank" rel="noopener noreferrer">DIAGRAMA.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%201.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 1.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%202.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 2.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%203.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 3.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%204.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 4.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%205.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 5.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/EVIDENCIA%206.png" target="_blank" rel="noopener noreferrer">EVIDENCIA 6.png</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Estudiante.java" target="_blank" rel="noopener noreferrer">Estudiante.java</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Main.java" target="_blank" rel="noopener noreferrer">Main.java</a></li>
        <li><a href="https://github.com/jeronimozapatav-art/ESTRUCTURA-DE-DATOS/blob/main/Curso.java" target="_blank" rel="noopener noreferrer">Curso.java</a></li>
      </ul>
    </div>
'''
html = html.replace(needle, links_block + needle, 1)

path.write_text(html, encoding="utf-8")
print("Actualización mínima realizada.")
print(f"Archivo: {path}")
print(f"Tamaño final: {path.stat().st_size:,} bytes")
print("Se mantuvo el diseño profesional y se agregaron únicamente enlaces de texto a la Actividad 1.")
