# Análisis de Video Deportivo con YOLO (Visión Computacional)

## Descripción del Proyecto
Este proyecto implementa un pipeline de aprendizaje profundo aplicado a la analítica deportiva. Mediante el uso del modelo de detección de objetos **YOLO** (por ejemplo, los pesos `yolo26n.pt`), el sistema es capaz de detectar y rastrear **jugadores** y **balones** dentro de un terreno de juego a partir de un video de entrada. 

Además de la detección estándar, el proyecto utiliza la biblioteca `supervision` para interactuar de forma inteligente con el video visualizando regiones clave de la cancha mediante polígonos (*Polygon Zones*):
- Delimitación general de la cancha.
- Zonas de punto penal (izquierda y derecha).
- Línea de medio campo.

El sistema fusiona estas áreas (con máscaras de transparencia) sobre los frames y genera un video final renderizado que permite interpretar analíticas directamente sobre la secuencia deportiva original. También se evalúa exhaustivamente el modelo (mAP, F1-score, Precision, Recall y Matriz de Confusión) sobre un conjunto de prueba para garantizar resultados precisos con falsos positivos minimizados.

## Instalación y Configuración (Clonar y Ejecutar)

Sigue estos pasos para clonar el proyecto, instalar sus dependencias de software y comenzar el análisis.

**1. Clonar el repositorio**  
Abre tu terminal y ejecuta el siguiente comando:
```bash
git clone <URL_DEL_REPOSITORIO>
cd <NOMBRE_DEL_REPOSITORIO>
```

**2. Instalar las dependencias**  
Se recomienda crear un entorno virtual para correr el proyecto. Una vez activado el entorno, instala los paquetes requiridos listados en el `requirements.txt`:
```bash
pip install -r requirements.txt
```

**3. Ejecutar y utilizar el proyecto**  
Todo el código y flujo de trabajo está contenido y explicado en el archivo de Jupyter Notebook principal: `FinalProject_SportsAnalytics_Using_DeepLearning.ipynb`. 
Para iniciarlo, ejecuta:
```bash
jupyter notebook FinalProject_SportsAnalytics_Using_DeepLearning.ipynb
```
O, si usas VS Code u otro editor que soporte Notebooks, simplemente abre `FinalProject_SportsAnalytics_Using_DeepLearning.ipynb` y ejecuta sus celdas una por una. La sección final en el Notebook es la responsable de cargar el video original, realizar las detecciones, aplicar las zonas y guardar el render final que se detalla en el siguiente paso.

## Ejemplo de Salida

Tras la ejecución de las celdas de inferencia en el notebook, se genera y exporta un video con el prefijo `demo_final_analytics.mp4` (o similar). En la salida visual obtenida, se observa:

* **Zonificación en Pantalla:** Polígonos de colores que demarcan áreas importantes (ej. bordes verdes en los laterales, áreas naranjas y rojas para zonas penales).
* **Detecciones (Cajas Delimitadoras):** Cada jugador detectado tendrá una caja delimitadora a su alrededor (usualmente con un umbral de confianza visible, por ejemplo, >= 0.30). De igual manera, se muestra el rastreo del balón.
* **Métricas y Estadísticas:** Análisis superpuestos en consola o frames sobre la cantidad de jugadores y posición según la zona delineada.

Un fotograma del video procesado resultante se verá con el trazado del fondo de la cancha y las correspondientes *bounding boxes* resaltando las entidades de clase `player` (1) y `ball` (0).
