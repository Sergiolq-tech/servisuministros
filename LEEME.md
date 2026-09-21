# Catálogo de una sola página

Página estática (HTML + CSS + JS, sin instalar nada) lista para Vercel y para compartir por WhatsApp.

```
catalogo/
├─ index.html      ← toda la página (aquí editas textos y productos)
├─ og-image.jpg    ← imagen de vista previa de WhatsApp (1200×630)
├─ vercel.json     ← configuración de caché
└─ img/            ← fotos de los productos
```

## 1. Editar el contenido (todo en `index.html`)

Es una sola página: no hay menú ni otras secciones. Todo lo editable está en dos bloques marcados con ✏️ dentro de `<script>`:

**CONFIG** (datos generales de la página)
- Marca, eslogan y **tu logo**: copia el archivo (PNG, WebP o SVG) a la carpeta `img/` y escribe `logo: "img/logo.png"`. Con `altoLogo` cambias el tamaño y con `mostrarTextoLogo` decides si se escribe el nombre al lado. Si `logo` está vacío se muestra solo el nombre en texto.
- El logo también se usa como icono de la pestaña del navegador.
- Textos del botón de arriba, título, subtítulo e **imagen de la portada** (`imagenHero`).
- **WhatsApp** (`573013614102` → tu número con código de país, sin `+`). Lo usan todos los botones.
  - Botón verde flotante de WhatsApp (escritorio y celular): `botonFlotante: true/false` lo muestra u oculta y `textoBotonFlotante` cambia el texto que aparece al pasar el mouse.
- Tarjeta morada "¿Necesitas asesoría?" y los 4 sellos de confianza de la columna izquierda.
- **Contacto e información** (bloque al final de la página): teléfono, correo, dirección, horario y redes. Si dejas un campo vacío (`""`), no se muestra.
- Rangos de edad del filtro y cuántos productos se ven antes de "Ver más".

**PRODUCTOS** (cada producto es un bloque `{ ... }`; copia uno, pégalo y edítalo)
- Nombre, categoría, descripción, detalle, edades, material, área, etiqueta, tabla de datos y características.
- Las categorías, materiales y contadores de los filtros se generan solos a partir de estos datos.
- Imágenes: `imagenes: ["img/mi-juego-1.jpg", "img/mi-juego-2.jpg"]`. La primera es la principal; todas salen como miniaturas en la tarjeta y como galería al hacer clic.
  Recomendado: JPG/WebP de 1200×900 px (4:3), fondo claro, menos de 200 KB cada una.

**Productos que no son juegos (sillas, mesas, libros, extintores…)**
- `edades`, `edadMin`, `edadMax` y `area` son opcionales: si no los pones, no se muestran, y los filtros de edad y área se ocultan solos cuando ningún producto los usa.
- `meta` es una línea corta bajo la descripción de la tarjeta (ej. `"Disponible en 4 colores"`).
- Un mismo modelo en varios colores = **un solo producto** con una foto por color en `imagenes`. Las miniaturas de la tarjeta y la galería muestran cada color.
- **Mobiliario** es una sola categoría (sillas, armarios, y luego mesas y lockers). Para muebles con medidas, usa `ficha` con las filas `Largo`, `Ancho`, `Alto`, `Peso` y `Color` (o `Colores`).
- Un mismo mueble que se muestra dentro de una foto de grupo: recorta una imagen por producto (proporción 4:3) y agrega la foto del grupo como segunda imagen.
- Si la foto se ve cortada en la tarjeta: `ajuste: "contain"` la muestra completa (con `fondo: "#f6f6f6"` para igualar el fondo) o `posicion: "50% 60%"` mueve el encuadre.

> Todos los textos, medidas, datos de contacto y fotos actuales son **ejemplos**. Reemplázalos por los reales.

## 2. Configurar la vista previa de WhatsApp (Open Graph)

En el `<head>` de `index.html` cambia `TU-DOMINIO.vercel.app` por tu dominio real en:
`canonical`, `og:url`, `og:image`, `og:image:secure_url` y `twitter:image`.

Reglas de WhatsApp para la imagen:
- URL **absoluta** con `https://`.
- 1200×630 px, JPG o PNG, **menos de 300 KB** (la incluida pesa ~100 KB).
- Título y descripción cortos (el título se corta cerca de 60 caracteres).

La `og-image.jpg` incluida es de ejemplo (lleva un símbolo genérico): diseña la tuya con tu logo. Para cambiarla: reemplaza `og-image.jpg` y sube el número de versión (`?v=1` → `?v=2`) en los metadatos.

## 3. Publicar en Vercel

**Opción A: arrastrar y soltar**
1. Sube esta carpeta a un repositorio de GitHub.
2. En vercel.com → *Add New → Project* → importa el repositorio.
3. *Framework Preset*: **Other**. No hay build ni carpeta de salida. Pulsa *Deploy*.

**Opción B: por terminal**
```bash
npm i -g vercel
cd gardenkids-catalogo
vercel --prod
```

Después de publicar, copia la URL final, ponla en las etiquetas Open Graph (paso 2) y vuelve a desplegar.

## 4. Probar la vista previa

1. Abre https://developers.facebook.com/tools/debug/ , pega tu URL y pulsa *Scrape Again* (WhatsApp usa el mismo lector que Facebook).
2. Envíate el enlace por WhatsApp para verlo en el chat.
3. Si WhatsApp muestra una imagen vieja, agrega `?v=2` al final del enlace que compartes; WhatsApp guarda la vista previa en caché.

## Notas

- **Enlace directo a un producto**: al abrir un producto se agrega `#p-id-del-producto` al enlace (por ejemplo `tudominio.com/#p-castillo-magico`), y el botón *Compartir* del producto lo copia o lo envía. Ese enlace abre el producto directamente. La vista previa de WhatsApp será la misma imagen general de la página, porque WhatsApp no lee el `#`.
- **Sin precios**: cada tarjeta muestra área requerida y rango de edad; el botón *Cotizar por WhatsApp* envía el nombre del producto ya escrito.
