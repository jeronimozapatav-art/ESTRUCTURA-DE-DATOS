
from pathlib import Path
from datetime import datetime
import shutil
import sys

from bs4 import BeautifulSoup


# ============================================================
# CONFIGURACIÓN
# ============================================================

HTML_PATH = Path(
    "/mnt/data/Repositorio_Estructura_de_Datos_Profesional.html"
)

GITHUB_BASE = (
    "https://github.com/jeronimozapatav-art/"
    "ESTRUCTURA-DE-DATOS"
)

RAW_BASE = (
    "https://raw.githubusercontent.com/jeronimozapatav-art/"
    "ESTRUCTURA-DE-DATOS/main/"
)

EVIDENCES = [
    ("Diagrama del proyecto", "DIAGRAMA.png"),
    ("Evidencia 1", "EVIDENCIA 1.png"),
    ("Evidencia 2", "EVIDENCIA 2.png"),
    ("Evidencia 3", "EVIDENCIA 3.png"),
    ("Evidencia 4", "EVIDENCIA 4.png"),
    ("Evidencia 5", "EVIDENCIA 5.png"),
    ("Evidencia 6", "EVIDENCIA 6.png"),
]

SOURCE_FILES = [
    "Estudiante.java",
    "Curso.java",
    "Main.java",
]


# ============================================================
# UTILIDADES
# ============================================================

def create_backup(path: Path) -> Path:
    """Crea una copia de seguridad antes de modificar el archivo."""
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    backup = path.with_name(
        f"{path.stem}_backup_{timestamp}{path.suffix}"
    )
    shutil.copy2(path, backup)
    return backup


def github_file_url(filename: str) -> str:
    """Construye el enlace al archivo original de GitHub."""
    from urllib.parse import quote

    return f"{GITHUB_BASE}/blob/main/{quote(filename)}"


def add_styles(soup: BeautifulSoup) -> None:
    """Añade los estilos de la galería sin duplicarlos."""
    if soup.head is None:
        raise ValueError("El documento HTML no contiene <head>.")

    style_id = "professional-evidence-styles"
    style = soup.find("style", id=style_id)

    if style is None:
        style = soup.new_tag("style", id=style_id)
        soup.head.append(style)

    style.string = """
    .evidence-gallery {
        display: grid;
        grid-template-columns: repeat(
            auto-fit, minmax(min(100%, 230px), 1fr)
        );
        gap: 18px;
        margin: 20px 0;
    }

    .evidence-card {
        overflow: hidden;
        border: 1px solid var(--line, #263449);
        border-radius: 16px;
        background: var(--card, #111c2e);
        transition: transform .2s ease,
                    box-shadow .2s ease,
                    border-color .2s ease;
    }

    .evidence-card:hover {
        transform: translateY(-4px);
        border-color: var(--cyan, #48e0e8);
        box-shadow: 0 12px 28px rgba(0, 0, 0, .18);
    }

    .evidence-card a {
        display: block;
        color: inherit;
        text-decoration: none;
    }

    .evidence-card img {
        display: block;
        width: 100%;
        aspect-ratio: 16 / 10;
        object-fit: cover;
        background: #0a1220;
    }

    .evidence-card img[hidden] {
        display: none;
    }

    .evidence-caption {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 12px;
        padding: 14px;
        font-size: 13px;
    }

    .evidence-caption span {
        color: var(--cyan, #48e0e8);
        white-space: nowrap;
    }

    .source-links {
        display: flex;
        flex-wrap: wrap;
        gap: 12px;
        margin: 16px 0;
    }

    .source-links a {
        display: inline-flex;
        align-items: center;
        gap: 8px;
        padding: 11px 15px;
        border: 1px solid var(--line, #263449);
        border-radius: 10px;
        color: var(--cyan, #48e0e8);
        text-decoration: none;
        font-weight: 700;
        transition: background .2s ease;
    }

    .source-links a:hover,
    .source-links a:focus-visible {
        background: rgba(72, 224, 232, .12);
    }

    @media (prefers-reduced-motion: reduce) {
        .evidence-card,
        .source-links a {
            transition: none;
        }
    }
    """


def create_gallery(soup: BeautifulSoup) -> None:
    """Crea la galería de evidencias y sus enlaces originales."""
    gallery = soup.find(id="evidenceGallery")

    if gallery is None:
        print(
            "Aviso: no existe #evidenceGallery. "
            "La galería debe insertarse en el modal existente."
        )
        return

    gallery.clear()
    gallery["class"] = list(
        set(gallery.get("class", []) + ["evidence-gallery"])
    )

    for title, filename in EVIDENCES:
        card = soup.new_tag("article", **{"class": "evidence-card"})
        link = soup.new_tag(
            "a",
            href=github_file_url(filename),
            target="_blank",
            rel="noopener noreferrer",
            title=f"Abrir {title} en GitHub",
        )

        image_url = RAW_BASE + filename.replace(" ", "%20")
        image = soup.new_tag(
            "img",
            src=image_url,
            alt=title,
            loading="lazy",
        )

        link.append(image)
        card.append(link)

        caption = soup.new_tag(
            "div", **{"class": "evidence-caption"}
        )

        label = soup.new_tag("strong")
        label.string = title

        action = soup.new_tag("span")
        action.string = "Ver en GitHub ↗"

        caption.extend([label, action])
        card.append(caption)
        gallery.append(card)


def create_source_links(soup: BeautifulSoup) -> None:
    """Actualiza los enlaces al código fuente."""
    container = soup.find(id="activityEvidenceLinks")

    if container is None:
        print(
            "Aviso: no existe #activityEvidenceLinks. "
            "No se modificaron los enlaces fuente."
        )
        return

    # Elimina solamente el contenedor de enlaces administrado
    # por este script, no el resto del contenido del modal.
    links = container.find(id="professionalSourceLinks")

    if links is None:
        links = soup.new_tag(
            "div", id="professionalSourceLinks",
            **{"class": "source-links"}
        )
        container.append(links)
    else:
        links.clear()

    for filename in SOURCE_FILES:
        link = soup.new_tag(
            "a",
            href=github_file_url(filename),
            target="_blank",
            rel="noopener noreferrer",
        )
        link.string = f"{filename} ↗"
        links.append(link)


def validate_html(soup: BeautifulSoup) -> None:
    """Comprueba los elementos necesarios para la página."""
    required_ids = [
        "activityEvidenceLinks",
        "activityEvidenceGallery",
    ]

    missing = [
        element_id
        for element_id in required_ids
        if soup.find(id=element_id) is None
    ]

    if missing:
        raise ValueError(
            "Faltan elementos HTML necesarios: "
            + ", ".join(missing)
        )


# ============================================================
# EJECUCIÓN PRINCIPAL
# ============================================================

def main() -> int:
    if not HTML_PATH.is_file():
        print(f"Error: no se encontró el archivo: {HTML_PATH}")
        return 1

    try:
        original = HTML_PATH.read_text(encoding="utf-8")
        soup = BeautifulSoup(original, "html.parser")

        # Validar antes de tocar el archivo original.
        validate_html(soup)

        backup = create_backup(HTML_PATH)

        add_styles(soup)
        create_gallery(soup)
        create_source_links(soup)

        # Escritura temporal y reemplazo para reducir el riesgo
        # de dejar el documento incompleto.
        temporary = HTML_PATH.with_suffix(".tmp")
        temporary.write_text(
            str(soup),
            encoding="utf-8",
        )
        temporary.replace(HTML_PATH)

        print("Página HTML actualizada correctamente.")
        print(f"Archivo: {HTML_PATH}")
        print(f"Copia de seguridad: {backup}")
        print(f"Tamaño final: {HTML_PATH.stat().st_size:,} bytes")

        return 0

    except (OSError, ValueError) as error:
        print(f"Error durante la actualización: {error}")
        return 1


if __name__ == "__main__":
    sys.exit(main())

