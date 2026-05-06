Laboratorio 7 — Aprendizaje No Supervisado
Estudiante: Jhonn Wilder Llanos Rojas
Carrera: Ciencias de la Computación
Universidad: Universidad San Francisco Xavier de Chuquisaca (USFX)
Dataset: Garbage Classification (12 classes)
Fuente: Kaggle — mostafaabla

📁 Descripción del Dataset
El dataset Garbage Classification es una colección de imágenes de residuos domésticos del hogar, diseñado para el desarrollo de modelos de aprendizaje automático orientados a la clasificación automática de basura, con el objetivo de apoyar procesos de reciclaje y gestión de residuos sólidos. Las imágenes fueron recopiladas de diversas fuentes web y representan objetos reales de uso cotidiano fotografiados en distintos fondos, ángulos e iluminaciones.
CaracterísticaValorTotal de imágenes~15,515 imágenesNúmero de clases12FormatoJPG / PNG (color RGB)Tamaño originalVariable (se redimensionan a 64×64 px)Peso total~250 MBFuenteKaggle

🗂️ Estructura del Dataset
El dataset no tiene filas ni columnas como un CSV — está organizado en 12 carpetas, una por cada clase. Cada carpeta contiene imágenes JPG/PNG de objetos de esa categoría.
garbage_classification/
├── battery/        →  945 imágenes  — Pilas y baterías
├── biological/     →  985 imágenes  — Residuos orgánicos (cáscaras, restos de comida)
├── brown-glass/    →  607 imágenes  — Vidrio de color marrón (botellas de cerveza, etc.)
├── cardboard/      →  891 imágenes  — Cartón y cajas
├── clothes/        → 5325 imágenes  — Ropa y textiles
├── green-glass/    →  629 imágenes  — Vidrio de color verde
├── metal/          →  769 imágenes  — Latas, objetos metálicos
├── paper/          → 1050 imágenes  — Papel, periódicos, hojas
├── plastic/        →  865 imágenes  — Botellas y envases plásticos
├── shoes/          → 1977 imágenes  — Calzado
├── trash/          →  697 imágenes  — Basura general no clasificada
└── white-glass/    →  775 imágenes  — Vidrio blanco / transparente

Nota: En este laboratorio las etiquetas de carpeta se ignoran completamente durante el entrenamiento (aprendizaje no supervisado). Solo se usan al final para evaluación.


⚙️ Preprocesamiento aplicado
Cada imagen pasa por el siguiente proceso antes de ser usada en el modelo:

Carga desde su carpeta correspondiente con PIL/OpenCV
Redimensionado a 64×64 píxeles (RGB)
Aplanado → vector de 64 × 64 × 3 = 12,288 features por imagen
Normalización dividiendo entre 255.0 → valores entre [0, 1]
Reducción de dimensionalidad con PCA antes de aplicar KMeans


🧠 Técnicas aplicadas
Punto 1 — KMeans sobre dataset aleatorio

Generador de dataset aleatorio con centroides entre 1 y 20, con distancia importante entre ellos para verificación visual
Método del Codo para encontrar el k óptimo
Silhouette Score para evaluar la calidad del clustering

Punto 2 — Dataset de imágenes reales (Garbage Classification)
Aprendizaje No Supervisado

KMeans con k=12 (igual al número de clases reales)
Visualización de clusters con PCA 2D

Aprendizaje Semi-supervisado

Solo el 10% de las imágenes tienen etiqueta
El modelo propaga etiquetas al 90% restante usando KMeans
Se evalúa la precisión de la propagación

Aprendizaje Activo

Se empieza con solo el 5% de etiquetas
El modelo selecciona las imágenes más inciertas para etiquetar (mayor distancia al centroide)
Se itera: etiquetar → reentrenar → seleccionar nuevas inciertas
Se grafica cómo mejora el accuracy en cada iteración

Predicción con imagen propia

Se puede pasar cualquier foto de basura al modelo
El modelo predice a qué cluster pertenece visualmente


📋 Requisitos
numpy
pandas
matplotlib
scikit-learn
Pillow
tqdm

▶️ Cómo ejecutar

Clonar o descargar el repositorio
Colocar la carpeta garbage_classification/ en el mismo directorio que el notebook
Instalar dependencias: pip install numpy pandas matplotlib scikit-learn Pillow tqdm
Abrir y ejecutar: lab7_jhonn_llanos.ipynb


🗑️ ¿Qué predice el modelo?
Dada cualquier imagen de basura (tomada con el celular, descargada de internet, etc.), el modelo la asigna al cluster visual más cercano entre los 12 aprendidos. Por ejemplo:

Una foto de una botella plástica → cluster similar a plastic
Una foto de una lata → cluster similar a metal
Una foto de ropa vieja → cluster similar a clothes


Laboratorio desarrollado para el curso de Inteligencia Artificial — USFX
