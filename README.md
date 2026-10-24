from pathlib import Path
p = Path("/mnt/data/index.html")
html = p.read_text(encoding="utf-8")

# Retitle and reframe hero/profile to focus on Data Structures
html = html.replace(
'<meta name="description" content="Portafolio académico de Jerónimo Zapata Vargas: Programación Orientada a Objetos, Java, UML, programación funcional y estructuras de datos.">',
'<meta name="description" content="Portafolio académico de Jerónimo Zapata Vargas: estructuras de datos, algoritmos, organización de información e implementación en Java.">'
)
html = html.replace(
'<title>Jerónimo Zapata Vargas | Portafolio de Desarrollo de Software</title>',
'<title>Jerónimo Zapata Vargas | Portafolio de Estructura de Datos</title>'
)
html = html.replace('PORTAFOLIO_DEV', 'DATA_STRUCTURES')
html = html.replace('Estudiante de Tecnología en Desarrollo de Software · 3.er semestre', 'Estudiante de Tecnología en Desarrollo de Software · Enfoque en Estructura de Datos')
html = html.replace(
'Especializado en el diseño conceptual de sistemas, modelado UML, estructuración de bases de datos relacionales y aplicación del paradigma de Programación Orientada a Objetos.',
'Enfoque en la organización, representación y procesamiento eficiente de la información mediante estructuras de datos y algoritmos implementados en Java.'
)
html = html.replace(
'<span class="pill">JAVA</span><span class="pill">UML</span><span class="pill">POO</span><span class="pill">GITHUB</span><span class="pill">PROGRAMACIÓN FUNCIONAL</span>',
'<span class="pill">ESTRUCTURAS DE DATOS</span><span class="pill">ALGORITMOS</span><span class="pill">JAVA</span><span class="pill">BÚSQUEDA</span><span class="pill">ORDENAMIENTO</span>'
)
html = html.replace('Explorar materias ↓', 'Explorar estructura ↓').replace('Ver trabajos ↗', 'Ver entregas ↗')
html = html.replace('J.A.R.V.I.S. // DEV INTERFACE', 'DATA STRUCTURES // INTERFACE')
html = html.replace('JAVA // UML // POO', 'JAVA // ALGORITMOS // DATOS')
html = html.replace('<strong>POO</strong><span>Paradigma de desarrollo</span>', '<strong>DSA</strong><span>Estructuras y algoritmos</span>')
html = html.replace('<strong>UML</strong><span>Modelado de sistemas</span>', '<strong>JAVA</strong><span>Implementación práctica</span>')

# Replace profile section content
start = html.index('<section id="sobre-mi">')
end = html.index('</section>', start) + len('</section>')
profile = '''<section id="sobre-mi">
  <div class="container">
    <div class="section-head"><div><div class="section-number">01 // PERFIL</div><h2>Sobre mí</h2></div><p>Mi proceso formativo y enfoque en la organización eficiente de datos.</p></div>
    <div class="about-grid">
      <article class="panel about-copy reveal">
        <div class="kicker">Perfil académico</div>
        <p>Soy estudiante de Tecnología en Desarrollo de Software en la Institución Universitaria Digital de Antioquia, con interés en comprender cómo se organiza y procesa la información para resolver problemas computacionales.</p>
        <p>En este portafolio reúno mis evidencias de aprendizaje de Estructura de Datos, con ejercicios y actividades orientados a arreglos, listas, pilas, colas, árboles, grafos, búsqueda, ordenamiento y análisis de algoritmos.</p>
        <p>Mi objetivo es fortalecer la capacidad de elegir e implementar estructuras adecuadas según las necesidades de cada problema, utilizando Java como herramienta de práctica.</p>
      </article>
      <aside class="panel info-list reveal">
        <div class="info-row"><span>Formación</span><strong>Desarrollo de Software</strong></div>
        <div class="info-row"><span>Institución</span><strong>IU Digital de Antioquia</strong></div>
        <div class="info-row"><span>Área de enfoque</span><strong>Estructura de Datos</strong></div>
        <div class="info-row"><span>Herramienta</span><strong>Java</strong></div>
        <div class="info-row"><span>Portafolio</span><strong>Entregas académicas</strong></div>
      </aside>
    </div>
  </div>
</section>'''
html = html[:start] + profile + html[end:]

# Remove POO / subject section, replace with focused learning topics section.
start = html.index('<section id="materias"')
end = html.index('</section>', start) + len('</section>')
topics = '''<section id="materias" style="background:rgba(5,15,28,.42);border-block:1px solid rgba(57,231,255,.08)">
  <div class="container">
    <div class="section-head"><div><div class="section-number">02 // CONTENIDO</div><h2>Fundamentos de Estructura de Datos</h2></div><p>Conceptos y herramientas para representar, organizar, buscar y procesar información de forma eficiente.</p></div>
    <div class="grid-3">
      <article class="panel card reveal"><div class="icon-box">01</div><h3>Tipos y abstracción de datos</h3><p>Conceptos básicos, tipos de datos abstractos y selección de estructuras según el problema.</p><div class="tag-list"><span class="tag">TAD</span><span class="tag">ABSTRACCIÓN</span></div></article>
      <article class="panel card reveal"><div class="icon-box">02</div><h3>Estructuras lineales</h3><p>Arreglos, listas enlazadas, pilas y colas, junto con sus operaciones principales.</p><div class="tag-list"><span class="tag">ARREGLOS</span><span class="tag">LISTAS</span><span class="tag">PILAS</span><span class="tag">COLAS</span></div></article>
      <article class="panel card reveal"><div class="icon-box">03</div><h3>Estructuras no lineales</h3><p>Árboles y grafos para representar jerarquías, conexiones y recorridos entre elementos.</p><div class="tag-list"><span class="tag">ÁRBOLES</span><span class="tag">GRAFOS</span></div></article>
      <article class="panel card reveal"><div class="icon-box">04</div><h3>Búsqueda de información</h3><p>Búsqueda lineal y binaria, condiciones de aplicación y comparación de su eficiencia.</p><div class="tag-list"><span class="tag">LINEAL</span><span class="tag">BINARIA</span></div></article>
      <article class="panel card reveal"><div class="icon-box">05</div><h3>Algoritmos de ordenamiento</h3><p>Organización de datos y análisis de los pasos y el rendimiento de diferentes algoritmos.</p><div class="tag-list"><span class="tag">ORDENAMIENTO</span><span class="tag">COMPLEJIDAD</span></div></article>
      <article class="panel card reveal"><div class="icon-box">06</div><h3>Implementación con Java</h3><p>Desarrollo de operaciones, pruebas y ejercicios prácticos para aplicar los conceptos estudiados.</p><div class="tag-list"><span class="tag">JAVA</span><span class="tag">PRÁCTICA</span></div></article>
    </div>
  </div>
</section>'''
html = html[:start] + topics + html[end:]

# Remove original mixed academic deliveries section and replace with one unified section
start = html.index('<section id="entregas">')
end = html.index('</section>', start) + len('</section>')
deliveries = '''<section id="entregas">
  <div class="container">
    <div class="section-head"><div><div class="section-number">03 // PORTAFOLIO</div><h2>Entregas académicas</h2></div><p>Espacio único para consultar las cuatro entregas de Estructura de Datos, sus descripciones y recursos.</p></div>
    <div class="grid-2">
      <article class="panel card reveal"><div class="activity-number">01</div><div class="kicker">ENTREGA 01</div><h3>Fundamentos de estructuras de datos</h3><p>Presentación de conceptos iniciales, clasificación de estructuras de datos y análisis de su utilidad para resolver problemas computacionales.</p><div class="tag-list"><span class="tag">CONCEPTOS</span><span class="tag">ANÁLISIS</span></div><div class="callout" style="margin-top:17px">Añade aquí el documento, las capturas, el código o el enlace correspondiente a la primera entrega.</div><p style="font-size:.78rem">Enlace pendiente de completar con el recurso real.</p></article>
      <article class="panel card reveal"><div class="activity-number">02</div><div class="kicker">ENTREGA 02</div><h3>Estructuras de datos lineales</h3><p>Ejercicios de implementación y uso de arreglos, listas enlazadas, pilas o colas, según los requisitos de la actividad.</p><div class="tag-list"><span class="tag">LISTAS</span><span class="tag">PILAS</span><span class="tag">COLAS</span></div><div class="callout" style="margin-top:17px">Añade aquí el documento, las capturas, el código o el enlace correspondiente a la segunda entrega.</div><p style="font-size:.78rem">Enlace pendiente de completar con el recurso real.</p></article>
      <article class="panel card reveal"><div class="activity-number">03</div><div class="kicker">ENTREGA 03</div><h3>Estructuras no lineales y algoritmos</h3><p>Aplicación de árboles, grafos, algoritmos de búsqueda u ordenamiento para organizar y procesar información.</p><div class="tag-list"><span class="tag">ÁRBOLES</span><span class="tag">GRAFOS</span><span class="tag">ALGORITMOS</span></div><div class="callout" style="margin-top:17px">Añade aquí el documento, las capturas, el código o el enlace correspondiente a la tercera entrega.</div><p style="font-size:.78rem">Enlace pendiente de completar con el recurso real.</p></article>
      <article class="panel card reveal"><div class="activity-number">04</div><div class="kicker">ENTREGA 04</div><h3>Proyecto integrador de Estructura de Datos</h3><p>Aplicación práctica de las estructuras estudiadas para resolver un problema, con explicación del diseño, implementación y resultados.</p><div class="tag-list"><span class="tag">PROYECTO</span><span class="tag">JAVA</span><span class="tag">RESULTADOS</span></div><div class="callout" style="margin-top:17px">Añade aquí el documento, las capturas, el código o el enlace correspondiente a la cuarta entrega.</div><p style="font-size:.78rem">Enlace pendiente de completar con el recurso real.</p></article>
    </div>
    <div class="panel" style="padding:24px;margin-top:20px"><div class="kicker">Cómo completar las evidencias</div><p style="color:var(--muted);margin-bottom:0">En cada tarjeta, reemplaza el texto de recurso pendiente por los enlaces reales de tu documento, repositorio, video o capturas. Así mantendrás todas las entregas organizadas en un único apartado.</p></div>
  </div>
</section>'''
html = html[:start] + deliveries + html[end:]

# Remove Activity 3 / functional programming section and replace structure section with a concise final summary
start = html.index('<section id="actividad3"')
end = html.index('</section>', start) + len('</section>')
html = html[:start] + html[end:]

# replace structure section including old 4-delivery subsection
