# Portal IESTP “Catalina Buendía de Pecho” — Ica

Archivos para publicar en Hostinger:

- `portal-private/`: código PHP, vistas y datos. Va **fuera** de `public_html`, al mismo nivel.
- `public_html/`: raíz pública del dominio, con la página, la intranet, el CSS, el JavaScript y las imágenes.

El archivo `portal-private/config.php` (datos de la base de datos y clave de instalación) **no se guarda en GitHub**: el repositorio es público. Se crea a partir de `portal-private/config.example.php`.

## Instalación nueva

1. **Base de datos:** en hPanel › *Bases de datos › Bases de datos MySQL*, crea una base y un usuario con su contraseña. Anota los tres datos.
2. **Descarga el código:** en GitHub, *Code › Download ZIP*.
3. **Sube y extrae:** con el *Administrador de archivos*, sube el ZIP a la carpeta del dominio (la que contiene `public_html`) y extráelo. GitHub mete todo en una carpeta `cbp-main/`; mueve `portal-private/` y `public_html/` desde ahí a la carpeta del dominio y reemplaza el `public_html` vacío.
4. **Configura:** copia `portal-private/config.example.php` como `portal-private/config.php` y completa:
   - `db_name`, `db_user` y `db_password`;
   - `install_key`: una clave privada aleatoria de 32 caracteres o más. Guárdala.
5. **Instala:** abre `https://tu-dominio/install.php`, escribe la `install_key` y crea la cuenta del administrador principal.
6. **Borra** `public_html/install.php`. Después de instalar ya no sirve; si lo vuelves a abrir responde "La aplicación ya está instalada".
7. **Permisos:** `public_html/assets/cache/` debe tener permisos **755**.
8. **Comprueba:**
   - Abre el sitio y entra a la intranet con la cuenta creada.
   - Revisa *Configuración*: datos institucionales y logo.
   - En *Mesa de partes › Áreas receptoras › Editar áreas*, carga las áreas reales con sus correos.
   - En *Usuarios y roles*, crea las cuentas del personal.

**Opcional, respaldos automáticos:** en hPanel › *Avanzado › Trabajos cron*, crea una tarea diaria con `php /home/<usuario>/domains/<dominio>/portal-private/cron.php`. Luego actívala en la intranet, en *Copias de seguridad*.

## Actualizar una instalación existente

Sube `portal-private/` y `public_html/` encima de las carpetas actuales y acepta **sobrescribir**. **No borres las carpetas antes:** así se conservan `config.php`, `backups/` e `install.lock`. Después, borra `public_html/install.php`.

## Dónde se edita

- **CSS y JavaScript del portal:** `public_html/assets/app/` (`portal.css` y `portal-1.js` a `portal-4.js`).
- **Armazón de la página:** `portal-private/views/portal.php`.
- **Contenido inicial** que carga la instalación: `portal-private/data/portal.json`.
- **Imágenes y documentos:** `public_html/assets/cbp/`. Las imágenes grandes tienen una copia `.webp` que el servidor entrega a los navegadores compatibles.

### Actualizar los retratos institucionales

Los retratos retocados usan formato vertical **4:5 (720 × 900)**, con fondo de biblioteca y sin degradado oscuro sobre la fotografía. Se conservan las rutas existentes para que también funcionen con los datos de instalaciones ya creadas; no es necesario reinstalar ni importar de nuevo la base de datos.

Al publicar esta actualización, sube los archivos `docente-*.jpg`, `director-general-*.jpg` y sus versiones `.jpg.webp`, además de `public_html/assets/app/portal.css` y `portal-2.js`. Mantén cada JPG y su WebP sincronizados: Apache puede servir el WebP aunque la URL termine en JPG. El código añade una versión a las URL de estos retratos para renovar la caché del navegador.

Los retratos son retoques digitales de las fotografías existentes, no nuevas tomas. La fotografía de Ricardo Chacaliaza se conserva sin retocar: el rostro original es demasiado pequeño y tiene líneas de escaneo que impiden recuperar sus rasgos con fidelidad. Para mejorarla hace falta una fotografía de origen de mayor calidad. Los originales anteriores siguen disponibles en el historial de Git.

El sistema es una copia del portal de Nasca (`ranyuo/claudenasca`, commit `bf8264c`) adaptada con la información pública de https://www.cbp.edu.pe/, consultada el 30 de octubre de 2026. Las imágenes y los documentos se sirven desde `public_html/assets/cbp/`, no desde la web original. La versión anterior de este repositorio está en la rama `respaldo-main-2026-10-30`.

## Datos que debe confirmar la institución

- RUC y horario de atención de oficinas.
- Estadísticas de ingresantes, matriculados y egresados (la web original no publica las cifras).
- Resultados de admisión 2026 (los enlaces de la web original no funcionan).
- Plan de estudios de Asistencia Administrativa (la web publica el itinerario de Secretariado Ejecutivo).
- Correos de las áreas receptoras de Mesa de partes (se cargó el correo institucional).
