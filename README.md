# Banco de Tiempo

App familiar (PWA) para asignar tiempo de pantalla a los chicos.
- **Días de colegio = 0.** El finde se gana.
- **Notas (Midterm/Final)** definen el tiempo base del finde.
- **Cada viernes**, papá/mamá evalúan **solo conducta**: mantener o restar.
- Conducta excepcional (sin desaprobar, sin faltas, buen trato/colaboración/extracurriculares/llamadas a familiares) sube el tope **hasta 5 h**.
- Los chicos envían su **autoevaluación por correo** desde la app.
- Zona de padres protegida por **clave** (por defecto `cambiar123`; cámbiala en Ajustes en cada dispositivo — la clave real solo se guarda en ese dispositivo, no en el código).
- **Correos** de papá/mamá: vacíos por defecto; configúralos una vez en Ajustes (se guardan solo en el dispositivo).

100% estático, sin servidor. Todo se guarda en el navegador del dispositivo (localStorage).

## Probar local
El service worker necesita http (no `file://`):
```bash
cd banco-de-tiempo
python3 -m http.server 8080
# abrir http://localhost:8080
```

## Estructura
- `index.html` — la app completa (HTML + CSS + JS en un archivo).
- `manifest.webmanifest` — metadatos de la PWA.
- `sw.js` — service worker (offline).
- `icon-192.png`, `icon-512.png` — iconos.
