# bin-base64-converter

Conversor de binario ↔ Base64 100% del lado del cliente. Sin servidores, sin uploads, sin dependencias externas (excepto JSZip para exportar ZIPs).

## Qué ofrece

**Binario → Base64** — Seleccioná o arrastrá uno o más archivos binarios. La app los convierte a Base64 en chunks de 8 KB (evita el stack limit del browser) y los empaqueta en un ZIP listo para descargar.

**Base64 → Binario** — Pegá una cadena Base64 en el textarea o arrastrá archivos `.txt` / `.b64`. La app la decodifica a binario y la descarga como `.bin`. Si son múltiples archivos, los agrupa en un ZIP.

**JSON → Base64** — Cargá un archivo JSON, seleccioná una propiedad cuyo valor sea Base64, y descargalo como texto (`.txt`) o como binario decodificado (`.bin`).

**Conversiones 100% locales** — Todo el procesamiento ocurre en el navegador con la FileReader API, Blob, y Clipboard API. Ningún dato se envía a ningún servidor.

## Cómo usar

```bash
# Abrir directo (JSZip no cargará por CORS con archivos locales)
open index.html

# Opción recomendada — servir con HTTP
python3 -m http.server
# después abrir http://localhost:8000
```

JSZip se carga desde CDN de Cloudflare, por eso necesita un servidor HTTP local si no hay conexión a Internet.

## Stack

- HTML5 + CSS3 + Vanilla JS (ES6+)
- [JSZip 3.10](https://stuk.github.io/jszip/) — creación de ZIPs en el browser
- [Inter](https://rsms.me/inter/) — tipografía
- Zero build steps, zero frameworks, zero backend
