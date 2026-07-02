# rentafamiliar.com — Landing del SaaS Renta Familiar

Sitio estático de una página (index.html autocontenido: CSS y logo incrustados).

## Contenido del repositorio

| Archivo | Función |
|---|---|
| `index.html` | Landing completa (HTML + CSS + logo en base64) |
| `og.png` | Imagen de vista previa al compartir el enlace (WhatsApp, Facebook, LinkedIn) |
| `favicon.png` | Ícono de pestaña del navegador |
| `apple-touch-icon.png` | Ícono al guardar en pantalla de inicio (iPhone/iPad) |

## Publicación (opción recomendada: GitHub + Vercel)

1. Crear repositorio en GitHub (ej. `rentafamiliar-landing`) y subir los 4 archivos a la raíz.
2. En Vercel: **Add New → Project → importar el repositorio**. Framework preset: **Other** (sitio estático, sin build). Deploy.
3. En Vercel → Settings → **Domains**: agregar `rentafamiliar.com` y `www.rentafamiliar.com`. Vercel mostrará los registros DNS requeridos.
4. En **Cloudflare** (DNS del dominio): crear/editar los registros que indique Vercel, típicamente:
   - `A` @ → `76.76.21.21`
   - `CNAME` www → `cname.vercel-dns.com`
   - Modo del registro: **DNS only** (nube gris) para evitar doble proxy con Vercel.

### Alternativa: GitHub Pages
1. Repositorio → Settings → Pages → Deploy from branch (`main`, `/root`).
2. Custom domain: `rentafamiliar.com` (crea el archivo CNAME).
3. En Cloudflare: registros `A` del apex hacia las 4 IPs de GitHub Pages y `CNAME` www → `<usuario>.github.io`.

## ⚠️ Registros de Cloudflare que NO se deben tocar

- `checkin` → ruta del **Cloudflare Worker** `checkin-proxy` (check-in de huéspedes y acceso de anfitriones).
- `send` y registros **MX/SPF/DKIM/DMARC** → correo transaccional **Resend**.
- Solo se modifican los registros del **apex (@)** y **www**.

## Publicar cambios

Editar `index.html` → commit → push. Vercel (o Pages) redespliega solo.

## Nota

Al apuntar el apex a este sitio, el sitio actual de Hostinger Builder (Host Family)
dejará de servirse en rentafamiliar.com. Las URLs antiguas (/blog, /inversion, etc.)
devolverán 404 salvo que se configuren redirecciones.
