# Meridian Yachts — Hero Section (mobile-first)

Hero de conversión para venta de yates, con estética **v2 high-tech premium**
(azul espacial, tipografía sans fina, glow sutil, badge técnico).
HTML + CSS + JS en archivos separados, sin dependencias externas.

## Estructura del proyecto
```
apex/
├── index.html              # Marcado semántico (solo estructura)
├── css/
│   └── styles.css          # Estilos, organizados por secciones numeradas
├── js/
│   └── main.js             # Comportamiento (mejora progresiva)
├── assets/
│   └── images/             # Tus fotos
│       ├── yacht-hero.jpg      # Imagen principal del hero
│       ├── yacht-view-2.jpg    # Miniatura de galería
│       ├── yacht-view-3.jpg    # Miniatura de galería
│       └── README.md
└── README.md
```

> `index.html` está en la **raíz**, así que referencia a sus hermanos con rutas
> relativas simples (`css/styles.css`, `assets/images/...`). **No usar `../`**:
> en hosting estático (Vercel, Netlify, GitHub Pages…) la carpeta desplegada se
> convierte en la raíz del sitio y una ruta que sube un nivel se sale del
> deployment → el CSS no carga y la página se ve sin estilos.

## Deploy en Vercel
Es un sitio estático puro. **No hace falta configurar nada**: Vercel detecta
`index.html` en la raíz y lo sirve tal cual.

1. Sube el repo y conéctalo en Vercel.
2. Framework Preset: **Other**. Build Command: vacío. Output Directory: vacío (raíz).
3. Listo: `/` sirve `index.html` y `css/`, `js/`, `assets/` quedan disponibles.

> Si alguna vez vuelves a meter `index.html` dentro de una subcarpeta, tendrás
> que indicar esa carpeta como **Root Directory / Output Directory** en Vercel,
> o el CSS no se encontrará.

## Subir al repositorio (Git)
El proyecto ya incluye `.gitignore` y `.gitattributes`. Para publicarlo:

```bash
# 1) Inicializa el repo (solo la primera vez)
git init
git add .
git commit -m "Meridian Yachts hero: responsive mobile-first"

# 2) Crea el repo vacío en GitHub/GitLab y enlázalo
git branch -M main
git remote add origin https://github.com/USUARIO/REPO.git
git push -u origin main
```

Checklist antes de subir:
- [ ] `index.html` en la **raíz** (no dentro de `html/`).
- [ ] Rutas **relativas sin `../`** (`css/…`, `js/…`, `assets/…`).
- [ ] Sin scroll horizontal en móvil (280–1440 px).

## Paleta v2 (high-tech premium)
| Token | Valor | Uso |
|-------|-------|-----|
| `--bg-page` | `#070A14` | Fondo exterior |
| `--bg-surface` | `#0A0F1D` | Azul espacial (superficie) |
| `--bg-elevated` | `#141927` | Tarjetas slate |
| `--ink` | `#E2E8F0` | Texto plata helada |
| `--accent` | `#4FACFE` | Azul eléctrico |
| `--accent-cyan` | `#00F2FE` | Cian (glow / puntos de estado) |

## Responsive (mobile-first)
| Breakpoint | Layout | Contenedor |
|-----------|--------|-----------|
| `≤ 344px` (móvil muy estrecho / texto de sistema ampliado) | 1 columna, nav compacta | fluido |
| `≤ 359px` (móvil pequeño: iPhone SE, Android compactos) | 1 columna, tipografía reducida | fluido |
| `360–599px` (móvil estándar) | 1 columna | 430px |
| `≥ 600px` (tablet) | 1 columna | 680px |
| `≥ 900px` (escritorio) | **2 columnas** (grid-areas: `intro`/`buy` a la izquierda, `visual` a la derecha) | 1160px |
| `≥ 1280px` | 2 columnas | 1240px |

El hero usa tres grupos (`.hero__intro`, `.hero__visual`, `.hero__buy`) que en
móvil se apilan en orden natural y en escritorio se reorganizan con
`grid-template-areas`. Verificado sin scroll horizontal de **280px a 1440px**.

## Cómo verlo
Abre `index.html` en el navegador, o levanta un servidor local desde la raíz:

```bash
npx serve .
# o
python -m http.server 5173
```

## Funciones destacadas
- **Crossfade de galería**: dos capas `<img>` que se funden suavemente (0.5s)
  al cambiar de miniatura, con precarga previa para evitar parpadeos.
- **Barra de estado descartable**: se recuerda durante la sesión.
- **Respaldo vectorial**: si falta una foto, se ve un yate en SVG (no un icono roto).

## Qué puedes editar rápido
- **Colores:** variables en `:root` al inicio de `css/styles.css`.
- **Textos y precios:** en `index.html`, sección `HERO`.

## Verificado
- Lighthouse: **Accesibilidad, Buenas prácticas y SEO en 100**.
- WCAG: CTA principal con contraste AAA (texto oscuro sobre degradado cian→azul).
- Sin scroll horizontal en anchos **280–1440 px** (probado elemento por elemento en cada breakpoint).
- Respeta `prefers-reduced-motion`.
