# Calculadora pVT PWA — Android + iPhone, offline

Esta es una conversión web instalable del proyecto Streamlit. Los cálculos se ejecutan localmente en el dispositivo; no se consulta un servidor para calcular. Las ecuaciones de Python fueron trasladadas a JavaScript conservando constantes, correlaciones, opciones y datos de referencia del archivo `app_pvt_corregido_final_v2.py` y del núcleo Kivy previo.

## Contenido
- `index.html`: interfaz responsive y cinco módulos.
- `app.js`: funciones de cálculo, tablas y gráficas de todos los módulos.
- `styles.css`: diseño adaptable a móvil.
- `manifest.webmanifest`: nombre, iconos y modo instalable.
- `sw.js`: caché de recursos para uso offline.
- `icons/`: iconos Android/PWA y Apple Touch Icon.

## Probar en Windows
Una PWA necesita `localhost` o HTTPS para que el service worker funcione; abrir `index.html` con doble clic no activa el modo offline instalable.

### Método con Python ya instalado
1. Extrae la carpeta del ZIP.
2. Abre PowerShell en esa carpeta.
3. Ejecuta `py -m http.server 8000`.
4. En la computadora, abre `http://localhost:8000` en Chrome o Edge.
5. Para probar en teléfono conectado a la misma Wi-Fi, consulta la IP local de la PC con `ipconfig`, y abre `http://IP_DE_TU_PC:8000` en el teléfono. Esta ruta HTTP por IP no siempre habilita service worker en móviles; para instalar en el móvil, usa una URL HTTPS.

### Publicar para instalar en Android y iPhone
Sube el contenido de esta carpeta a un hosting estático que sirva HTTPS (por ejemplo, GitHub Pages o Netlify). No requiere backend ni servidor de cálculos. Abre la URL HTTPS desde:
- **Android:** Chrome → menú ⋮ → “Instalar aplicación” o “Añadir a pantalla de inicio”.
- **iPhone:** Safari → botón Compartir → “Añadir a pantalla de inicio”.

Después de cargar la aplicación una vez con internet, el service worker guarda los archivos de la app para que vuelva a abrir sin conexión. Prueba explícitamente activar modo avión, cerrar y volver a abrir.

## Alcance y validación
- Módulos: gas, aceite, agua, validación del Ejemplo 1.1 y abatimiento Ejemplo 1.2.
- Gas, aceite y agua incluyen gráficas de sus propiedades frente a presión; la validación incluye gráfica del error relativo y el abatimiento compara Oistein, Standing y referencia.
- El Ejemplo 1.2 usa Rs y γgd transcritos como datos de entrada, no los predice a partir de presión.
- Se mantienen opciones para discrepancias documentadas de Bw, Rsw, Ccs y constante de Lee.
- Esta conversión inicial debe cotejarse con Streamlit usando los mismos datos de entrada antes de utilizarse como herramienta de ingeniería.

## Nota importante de instalación
Para que la PWA se instale con icono y tenga offline fiable en Android/iOS, sí se requiere publicar los archivos en un origen HTTPS (o usar `localhost` en el mismo dispositivo para pruebas de escritorio). El cálculo no necesita internet una vez cargados los archivos.
