from pathlib import Path

source = Path("/mnt/data/index_estructura_de_datos.html")
html = source.read_text(encoding="utf-8")

start = html.index('<section id="entregas">')
end = html.index('<section id="estructura">')

new_section = '''<section id="entregas">
  <div class="container">
    <div class="section-head">
      <div>
        <div class="section-number">03 // PORTAFOLIO</div>
        <h2>Entregas académicas</h2>
      </div>
      <p>Consulta las cuatro actividades del semestre. Cada botón está preparado para enlazar directamente con su documento Word.</p>
    </div>

    <div class="grid-2">
      <article class="panel card reveal">
        <div class="activity-number">01</div>
        <div class="kicker">ACTIVIDAD 1</div>
        <h3>Primera entrega</h3>
        <p>Documento Word correspondiente a la primera actividad de la asignatura Estructura de Datos.</p>
        <div class="tag-list"><span class="tag">WORD</span><span class="tag">ENTREGA 01</span></div>
        <!-- Reemplaza la URL de abajo por el enlace compartido del Word de la Actividad 1. -->
        <a class="btn" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_1" target="_blank" rel="noopener noreferrer">Abrir Word ↗</a>
      </article>

      <article class="panel card reveal">
        <div class="activity-number">02</div>
        <div class="kicker">ACTIVIDAD 2</div>
        <h3>Segunda entrega</h3>
        <p>Espacio para el documento Word de la segunda actividad del semestre.</p>
        <div class="tag-list"><span class="tag">WORD</span><span class="tag">ENTREGA 02</span></div>
        <!-- Reemplaza la URL de abajo por el enlace compartido del Word de la Actividad 2. -->
        <a class="btn" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_2" target="_blank" rel="noopener noreferrer">Abrir Word ↗</a>
      </article>

      <article class="panel card reveal">
        <div class="activity-number">03</div>
        <div class="kicker">ACTIVIDAD 3</div>
        <h3>Tercera entrega</h3>
        <p>Espacio para el documento Word de la tercera actividad del semestre.</p>
        <div class="tag-list"><span class="tag">WORD</span><span class="tag">ENTREGA 03</span></div>
        <!-- Reemplaza la URL de abajo por el enlace compartido del Word de la Actividad 3. -->
        <a class="btn" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_3" target="_blank" rel="noopener noreferrer">Abrir Word ↗</a>
      </article>

      <article class="panel card reveal">
        <div class="activity-number">04</div>
        <div class="kicker">ACTIVIDAD 4</div>
        <h3>Cuarta entrega</h3>
        <p>Espacio para el documento Word de la cuarta actividad del semestre.</p>
        <div class="tag-list"><span class="tag">WORD</span><span class="tag">ENTREGA 04</span></div>
        <!-- Reemplaza la URL de abajo por el enlace compartido del Word de la Actividad 4. -->
        <a class="btn" href="PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD_4" target="_blank" rel="noopener noreferrer">Abrir Word ↗</a>
      </article>
    </div>

    <div class="panel" style="padding:24px;margin-top:20px">
      <div class="kicker">Cómo agregar los documentos</div>
      <p style="color:var(--muted);margin-bottom:0">Sube cada Word a Google Drive, configura el acceso para que las personas con el enlace puedan verlo y copia el enlace en el botón de su actividad. Reemplaza únicamente el texto PEGA_AQUI_EL_ENLACE_WORD_ACTIVIDAD correspondiente, conservando las comillas.</p>
    </div>
  </div>
</section>


'''

html = html[:start] + new_section + html[end:]

# Keep a conventional filename for direct upload to the new GitHub Pages repository.
output = Path("/mnt/data/index.html")
output.write_text(html, encoding="utf-8")
print(f"Archivo listo: {output} ({output.stat().st_size:,} bytes)")

