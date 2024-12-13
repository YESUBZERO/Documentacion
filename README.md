# Documentación de Scripts

Este documento describe el funcionamiento de tres scripts utilizados para la detección, clasificación y organización de vehículos en videos.

---

## **1. `VehicleExtraction_tabgen_MAH00025.py`**

### **Descripción**
Este script procesa un video para detectar y rastrear vehículos utilizando un modelo YOLO. Calcula velocidades y extrae imágenes de los vehículos detectados.

### **Características Principales**
- **Detección y Rastreo:** Utiliza YOLO para rastrear vehículos.
- **Cálculo de Velocidad:** Calcula velocidades basadas en tiempos de entrada y salida.
- **Extracción de Imágenes:** Guarda imágenes de los vehículos en puntos específicos.

### **Configuraciones Clave**
- `dist`: Distancias medidas en metros para el cálculo de velocidades.
- `coords`: Coordenadas que definen las líneas de entrada y salida.
- `target_size`: Tamaño objetivo para las imágenes recortadas.
- `video_path`: Ruta al archivo de video.

### **Flujo del Script**
1. Carga un modelo YOLO y mueve el modelo a la GPU si está disponible.
2. Procesa cada cuadro del video, detectando vehículos y registrando sus datos.
3. Calcula velocidades basadas en las coordenadas de entrada/salida.
4. Extrae imágenes de los vehículos y las guarda organizadas.
5. Muestra resultados en video con superposiciones y guarda velocidades en consola.

---

## **2. `clasificador_tier1.py`**

### **Descripción**
Clasifica imágenes de vehículos extraídas utilizando un modelo YOLO personalizado y organiza los resultados en un archivo Excel.

### **Características Principales**
- **Clasificación de Imágenes:** Clasifica vehículos en tipos específicos.
- **Organización de Imágenes:** Agrupa imágenes en carpetas basadas en sus categorías.
- **Actualización de Excel:** Registra resultados en un archivo Excel.

### **Configuraciones Clave**
- `model_path`: Ruta del modelo YOLO personalizado (`best_cl_t1.pt`).
- `image_dir`: Carpeta que contiene las imágenes de entrada.
- `output_dir`: Carpeta para guardar imágenes clasificadas.
- `file_path`: Archivo Excel base.

### **Flujo del Script**
1. Carga un modelo YOLO para clasificación.
2. Procesa todas las imágenes en la carpeta de entrada.
3. Asigna categorías basadas en inferencias del modelo.
4. Organiza imágenes en carpetas por tipo.
5. Actualiza un archivo Excel con resultados de clasificación.

---

## **3. `clasification_PC.py`**

### **Descripción**
Procesa imágenes previamente clasificadas para refinar la clasificación en categorías adicionales y organiza resultados.

### **Características Principales**
- **Refinamiento de Clasificación:** Usa un modelo YOLO adicional para clasificaciones más detalladas.
- **Organización de Imágenes:** Agrupa imágenes en carpetas según nuevas categorías.
- **Actualización de Excel:** Añade nuevas etiquetas al archivo Excel existente.

### **Configuraciones Clave**
- `model_path`: Ruta del modelo YOLO (`best_PC.pt`).
- `input_folder`: Carpeta que contiene imágenes previamente clasificadas.
- `img_pre_ord_folder`: Subcarpeta para procesar imágenes.
- `excel_file`: Archivo Excel que contiene datos iniciales.

### **Flujo del Script**
1. Mueve las imágenes de entrada a una subcarpeta para procesamiento.
2. Clasifica las imágenes utilizando YOLO.
3. Organiza imágenes en carpetas basadas en las nuevas etiquetas.
4. Actualiza el archivo Excel con las etiquetas asignadas.
5. Genera advertencias si no encuentra imágenes en el Excel.

---

## **Relación entre Scripts**
1. **`VehicleExtraction_tabgen_MAH00025.py`:** Procesa videos y extrae imágenes.
2. **`clasificador_tier1.py`:** Clasifica las imágenes extraídas en categorías generales.
3. **`clasification_PC.py`:** Refina las clasificaciones de imágenes en categorías más específicas.

---

## **Requisitos de Instalación**
- Python 3.8 o superior.
- Librerías:
  - `torch`
  - `openpyxl`
  - `opencv-python`
  - `ultralytics`
- Modelos YOLO personalizados (`best.pt`, `best_cl_t1.pt`, `best_PC.pt`).

## **Ejemplo de Uso**
1. Ejecutar el script de extracción:
   ```bash
   python VehicleExtraction_tabgen_MAH00025.py
   ```
2. Clasificar imágenes extraídas:
   ```bash
   python clasificador_tier1.py <location> <video_name>
   ```
3. Refinar clasificación:
   ```bash
   python clasification_PC.py <location> <video_name>
   ```

---

## **Notas**
- Asegúrate de tener los modelos YOLO necesarios en las rutas especificadas.
- Los directorios deben estructurarse correctamente para evitar errores en el procesamiento.

