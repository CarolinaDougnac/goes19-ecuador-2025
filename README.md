# Análisis Satelital realizado para un evento convectivo dentro del dominio de estudio (2025)

Este repositorio reúne el código, notebooks y ejemplos de productos gráficos utilizados para el **monitoreo y la evaluación de campañas de estimulación de nubes (cloud seeding)** durante 2025, a partir de imágenes satelitales **GOES-19 (banda 13)**.

El objetivo principal es mostrar mi forma de trabajo integrando:
- análisis meteorológico operativo,
- procesamiento de datos satelitales en Python,
- y generación de productos visuales para la toma de decisiones.

---

## ✨ Objetivos del proyecto

- Analizar la evolución temporal de sistemas convectivos.  
- Generar secuencias **antes–durante–después** de eventos seleccionados.  
- Integrar trayectorias georreferenciadas con datos satelitales.  
- Mantener una arquitectura modular mediante scripts en `src/`.

---

## 📂 Estructura del repositorio

```text
.
├── data/
│   ├── raw/          # Datos crudos GOES-19 (no incluidos)
│   └── processed/    # Datos preprocesados
├── figures/          # Figuras de ejemplo
├── notebooks/        # Notebooks del flujo de trabajo
├── src/              # Módulos reutilizables en Python
├── LICENSE
├── README.md
└── requirements.txt
```

---

## 📊 Ejemplo de análisis GOES-19: Evolución convectiva (caso de estudio)

<<<<<<< HEAD
A continuación se presenta un ejemplo detallado del análisis satelital realizado para el **Vuelo N° 51** en el dominio geográfico de estudio. Se muestra la evolución de la nube convectiva objetivo en tres momentos clave del proceso de siembra: **antes**, **durante** y **después** del vuelo, utilizando imágenes de la banda infrarroja **GOES-19 Band 13 (IR)**.

Estas figuras representan claramente:

- el desplazamiento y desarrollo convectivo del sistema,
- la ubicación de la trayectoria del avión (ida, siembra, regreso, pausa),
- y la interacción entre el vuelo y la estructura convectiva.
=======
A continuación se muestra la evolución de un sistema convectivo antes, durante y después del evento seleccionado.  
Las imágenes provienen de la banda infrarroja **GOES-19 B13**, utilizada para identificar núcleos fríos y evaluar desarrollo vertical.
>>>>>>> def67a1 (Actualizo README y aplico limpieza total del proyecto)

---

### 🟦 Antes — 18:50 UTC

![Figura 11](figures/Fig11_GOES19_B13_20250921_1850.png)

Núcleo convectivo inicial con temperaturas entre −50 °C y −60 °C.

---

### 🟪 Durante — 19:40 UTC

![Figura 16](figures/Fig16_GOES19_B13_20250921_1940.png)

Intensificación del sistema con expansión del núcleo frío y mayor desarrollo vertical.

---

### 🟧 Después — 20:30 UTC

![Figura 21](figures/Fig21_GOES19_B13_20250921_2030.png)

Estructura más madura, con nuevos máximos convectivos y mayor extensión espacial.

---

### ✨ Interpretación general

El análisis temporal evidencia:

- un **aumento progresivo del desarrollo vertical**,  
- intensificación del sistema convectivo durante el evento,  
- y expansión del núcleo frío posterior al máximo.

Este tipo de productos permite evaluar la evolución espacial y temporal de nubes convectivas utilizando datos satelitales y herramientas reproducibles.

---

## 🔄 Pipeline del proyecto

### 🛫 1. Selección del evento  
Definición de ventanas temporales **antes–durante–después**.

### 📥 2. Descarga de imágenes GOES-19  
Obtención automática de escenas satelitales B13.

### 🧭 3. Preprocesamiento geoespacial  
<<<<<<< HEAD
- Recorte al dominio geográfico de estudio  
- Reproyección de coordenadas  
- Conversión de formatos  
- Selección de la banda IR (B13)
=======
- Recorte del dominio de estudio  
- Reproyección  
- Selección de variable (temperatura de brillo)
>>>>>>> def67a1 (Actualizo README y aplico limpieza total del proyecto)

### 🔍 4. Análisis temporal  
Evaluación del desarrollo convectivo.

### ✈️ 5. Integración de trayectorias  
Superposición de tracks georreferenciados.

### 🎨 6. Visualización  
Mapas, composiciones temporales y productos gráficos.

### 📝 7. Documentación  
Elaboración de notas técnicas y figuras de interpretación.

---

## 📦 Organización del código (`src/`)

- `download_goes.py` → descarga robusta de archivos  
- `preprocess_goes.py` → apertura, selección y recorte  
- `plot_goes.py` → mapas y trayectorias

Estos módulos permiten mantener notebooks limpios y reutilizar funciones.

---

## 🧪 Ejemplo de uso desde notebook

```python
from src.preprocess_goes import prepare_scene
from src.plot_goes import plot_goes_scene

da_sub = prepare_scene(
    path="data/processed/GOES19_20250921_1940.nc",
    var_name="CMI",
    lat_bounds=(-5, 2),
    lon_bounds=(-82, -74),
    lat_name="lat",
    lon_name="lon",
)

plot_goes_scene(
    da_sub,
    extent=(-82, -74, -5, 2),
    title="Escena GOES-19 recortada con trayectoria",
    flight_track=([-80, -79.5, -79], [-1, -0.5, 0]),
    save_path="figures/ejemplo_scene_con_track.png",
    show=False,
)
```

