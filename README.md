# MEMORIAS — Invitación Fiesta de Baile Retro 🎶📼

Invitación web tipo cassette para la fiesta **MEMORIAS**, el **lunes 24 de agosto** desde las **21:00 hs** en **Coraceros 3690, Capurro, Montevideo**.

Sitio estático hecho 100% en **HTML + CSS + JS moderno** (sin frameworks, sin build), mobile-first, con reproducción de audio, SEO básico y vista previa optimizada para compartir por WhatsApp.

---

## 📁 Estructura de archivos

```
memorias-invitacion/
├── index.html            # Página principal (todo el CSS y JS está inline acá)
├── cassete.svg            # Ícono del cassette — favicon principal (SVG)
├── devo.mp3                # Audio que suena al tocar la tarjeta ("himno" de la fiesta)
├── og-image.png            # Imagen 1200x630 para la vista previa de WhatsApp / redes
├── apple-touch-icon.png    # Ícono 180x180 para "Agregar a inicio" en iPhone
├── favicon-32.png          # Favicon PNG de respaldo (navegadores viejos)
├── favicon-16.png          # Favicon PNG de respaldo (navegadores viejos)
└── README.md                # Este archivo
```

Todos los archivos deben quedar **en la misma carpeta**, sin renombrarlos — `index.html` los referencia por nombre exacto y ruta relativa.

---

## ▶️ Cómo probarlo en local

No necesita instalación ni dependencias. Alcanza con levantar un servidor estático simple (abrir el archivo con doble clic también funciona, pero algunos navegadores restringen `audio` con `file://`, así que se recomienda servirlo):

**Opción A — Python (ya viene instalado en Mac/Linux):**
```bash
cd memorias-invitacion
python3 -m http.server 8000
```
Abrir en el navegador: `http://localhost:8000`

**Opción B — Node:**
```bash
cd memorias-invitacion
npx serve .
```

**Opción C — VS Code:**
Instalar la extensión **Live Server** → clic derecho sobre `index.html` → *"Open with Live Server"*.

Probalo especialmente en el **celular** (mismo Wi-Fi, usando la IP de tu compu en vez de `localhost`) para chequear el audio y los tamaños táctiles.

---

## 🚀 Cómo publicarlo (deploy)

Es un sitio 100% estático: sirve **cualquier hosting estático gratuito**. Las más simples:

### Netlify (recomendado, arrastrar y soltar)
1. Entrar a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastrar la carpeta `memorias-invitacion` completa
3. Netlify te da una URL tipo `https://nombre-random.netlify.app`
4. (Opcional) Cambiar el nombre del sitio o conectar un dominio propio en *Site settings → Domain management*

### Vercel
```bash
npm i -g vercel
cd memorias-invitacion
vercel --prod
```

### GitHub Pages
1. Subir la carpeta a un repositorio de GitHub
2. *Settings → Pages → Deploy from branch* → rama `main`, carpeta `/root`
3. La URL queda como `https://tu-usuario.github.io/tu-repo/`

---

## ✅ Metadatos para compartir (Open Graph)

El sitio ya tiene las etiquetas `og:*` configuradas con la URL real **`https://bailemos24.netlify.app/`** (las 7 apariciones de `https://tu-dominio.com/` ya fueron reemplazadas):

- `<link rel="canonical" ...>`
- Todas las etiquetas `og:url` / `og:image` / `og:image:secure_url`
- `twitter:image`
- El bloque `application/ld+json` al final del `<head>` (aparece 2 veces: `image` y `url`)

Si algún día el sitio cambia de dominio, buscá y reemplazá `https://bailemos24.netlify.app/` por la nueva URL en esas mismas 7 apariciones. **Esto es indispensable** para que la vista previa de WhatsApp funcione: WhatsApp necesita poder acceder a esa URL pública para leer las etiquetas `og:*` y descargar `og-image.png` — no lee nada de un archivo local ni de `localhost`.

Después de publicar, podés verificar cómo se ve la tarjeta de WhatsApp con:
- [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) (WhatsApp usa el mismo motor de Open Graph)

---

## 🎛️ Cómo editar los datos de la fiesta

Todo el texto editable está en `index.html`, buscá estas secciones:

| Qué cambiar | Dónde |
|---|---|
| Fecha y hora | `<div class="detail-row">` con el ícono 🗓️ y ⏰ |
| Dirección / link de mapa | `<div class="detail-row">` con el ícono 📍 (el link usa Google Maps con la dirección codificada en la URL) |
| Número de WhatsApp para RSVP | `href="https://wa.me/59899272117?text=..."` |
| Título y subtítulo | `<h1 class="title">` y `<div class="subtitle">` |
| Descripción para buscadores/WhatsApp | `<meta name="description">` y las etiquetas `og:description` |
| Fecha del evento en el schema SEO | `startDate` dentro del bloque `application/ld+json` (formato `AAAA-MM-DDTHH:mm:ss-03:00`) |

---

## 🔊 Cómo funciona el audio

- Tocar el **cassette**, cualquier parte del `<main id="V">`, o el botón **"Tocá para escuchar el himno de la fiesta"** reproduce `devo.mp3` en loop.
- Volver a tocar lo pausa.
- Los carretes del cassette giran únicamente mientras el audio está sonando (sincronizado con los eventos `play` / `pause` / `ended` del audio, no con un simple click).
- Tocar los links de **mapa** o **WhatsApp** no dispara el audio (están excluidos explícitamente en el JS).
- Funciona con teclado (Enter / Espacio) para accesibilidad.

**Nota de tamaño**: `devo.mp3` pesa ~2.5 MB. Si el sitio va a viajar mucho por redes lentas, conviene comprimirlo a ~96 kbps antes de publicar (con Audacity, ffmpeg, o cualquier conversor online) — el tamaño no afecta la carga de la página en sí porque tiene `preload="none"`, pero sí la espera antes de que arranque a sonar la primera vez.

---

## ✅ Checklist antes de mandar el link

- [x] Reemplazar `https://tu-dominio.com/` por la URL real (7 apariciones) — hecho: `https://bailemos24.netlify.app/`
- [ ] Probar el link en el propio WhatsApp (mandártelo a vos mismo) y confirmar que se ve la imagen de vista previa
- [ ] Probar en un celular real que el audio arranca al tocar
- [ ] Confirmar que el número de WhatsApp del RSVP es el correcto
- [ ] Revisar ortografía de dirección, fecha y hora

---

## 🛠️ Próximas mejoras sugeridas

1. Comprimir `devo.mp3` a menor bitrate para una primera reproducción más rápida
2. Agregar un botón visible de silenciar/bajar volumen, además del gesto de tocar la tarjeta
3. Agregar contador regresivo hasta el 24 de agosto
4. Versión con formulario de confirmación propio (en vez de depender solo del link de WhatsApp) si la lista de invitados crece