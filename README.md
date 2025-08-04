
https://diegomezapy.github.io/usewebcam/

# SeCien 2025 – Laboratorio de Emociones

## Descripción  
**SeCien 2025 – Laboratorio de Emociones** es una aplicación web estática (HTML/CSS/JavaScript) que combina visión por computador y análisis estadístico en tiempo real. Utiliza las librerías de MediaPipe Tasks Vision y Chart.js para:

- Capturar el feed de vídeo del usuario.
- Detectar rostros, manos y pose corporal.
- Estimar emociones faciales (feliz, sorprendido, triste, enojado, neutro) aplicando blendshapes y un filtro EMA.
- Contar dedos levantados y calibrar la escala de píxeles a centímetros usando la apertura de la mano.
- Medir estatura y peso aproximados a partir de landmarks de pose.
- Representar estadísticas y gráficos interactivos (distribución de emociones, conteo de dedos, regresión estatura-peso).

---

## Características principales  

1. **Captura de cámara**  
   - Solo necesita navegador moderno con `getUserMedia`.  
   - Resolución mínima 640×360 px, ideal 1280×720 px.

2. **Detección y estimación**  
   - **Rostro**: Landmarks + expresiones faciales.  
   - **Manos**: Landmarks + conteo de dedos + calibración de escala.  
   - **Pose**: Landmarks para medir estatura y ancho corporal.

3. **Visualización**  
   - Gráficos de pastel (`pie`) para emociones y barras (`bar`) para dedos (Chart.js).  
   - Gráfico de dispersión y línea de regresión para estatura vs. peso.  
   - Panel lateral con KPIs: FPS, caras, manos, dedos, emoción actual, estadísticas agregadas.

4. **Calibración automática**  
   - Pulso de calibración al detectar 5 dedos levantados, asumiendo una longitud de mano de 15 cm.

5. **Estadísticas acumuladas**  
   - Historial de emociones y conteo de dedos (máximo 1000 muestras).  
   - Duración promedio, frecuencia, último cambio.  
   - Promedio, máximo, mínimo y total de dedos.

---

## Tecnologías empleadas  

- **HTML5 + CSS3**: Diseño responsivo con CSS Grid y animaciones `@keyframes`.  
- **JavaScript ES6+**: Módulos dinámicos, async/await.  
- **MediaPipe Tasks Vision v0.10.7**:  
  - `FaceLandmarker` (detección de rostros y blendshapes)  
  - `HandLandmarker` (detección de manos y landmarks)  
  - `PoseLandmarker` (detección de pose corporal)  
- **Chart.js**: Visualización de datos (pie, bar, scatter, line).  
- **Fuentes y íconos**:  
  - Google Fonts (Comic Neue, Nunito)  
  - Font Awesome 6.4.0

---

## Estructura del proyecto  

/index.html
├─ /assets/
│ ├─ robot.svg ← Icono embebido en base64
│ └─ ... ← Imágenes o recursos adicionales
├─ /README.md ← Esta documentación
└─ /LICENSE ← Licencia del proyecto

yaml
Copiar
Editar

> **Nota**: El HTML principal incluye todo el CSS y JS inline; no se requieren compiladores ni empaquetadores.

---

## Instalación y despliegue  

1. **Descarga o clona el repositorio**  
   ```bash
   git clone https://github.com/tu-usuario/SeCien-2025.git
   cd SeCien-2025
Servidor HTTP estático
Debido a los módulos ES y las importaciones de MediaPipe, debes servir los archivos mediante un servidor web (no basta abrir el archivo directamente en el navegador). Por ejemplo, con Python 3:

bash
Copiar
Editar
# Python 3.7+
python -m http.server 8000
Luego abre http://localhost:8000 en tu navegador.

Permisos de cámara
Concede acceso a la cámara cuando el navegador lo solicite.

Uso
Al cargar la página, haz clic en “Iniciar Laboratorio”.

Espera a que el estado avance:

“Solicitando cámara…”

“Importando @mediapipe/tasks-vision…”

“Cargando modelos y WASM…”

“Modelos listos. Laboratorio Activo”

Realiza gestos frente a la cámara:

Mira la sección principal para ver el vídeo superpuesto con landmarks.

Observa el panel lateral con FPS, número de caras, manos y dedos.

Consulta gráficos y KPIs que se actualizan cada 1.5 s.

Para calibrar la escala de píxeles a cm, extiende la mano con 5 dedos levantados:

El estado mostrará Calibrado: XX.XX px/cm.

A partir de entonces, se estimará estatura y peso.

Configuración avanzada
Intervalo de muestreo
Modifica const SAMPLE_INTERVAL_MS = 1500; en el <script> para cambiar la frecuencia de actualización de estadísticas.

Rangos de medición

Estatura: const HEIGHT_RANGE = [120, 200];

Peso: const WEIGHT_RANGE = [25, 150];

Blendshape thresholds
Ajusta los coeficientes y umbrales en la función estimateExpression() para refinar la detección de emoción.

Contribuciones
Las contribuciones son bienvenidas. Para proponer mejoras, correcciones o nuevas características:

Fork del repositorio.

Crea una branch para tu feature/bugfix.

Envía un Pull Request detallando los cambios y su justificación.

Licencia
Este proyecto se distribuye bajo la licencia MIT. Consulta el archivo LICENSE para más detalles.

