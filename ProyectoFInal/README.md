# ⚽ Predicción de Resultados de Fútbol Internacional con XGBoost + LLM

**Proyecto Final — Inteligencia Artificial · Universidad EAFIT 2026-1**

> Sistema que predice el resultado de partidos de fútbol internacionales (victoria local / empate / victoria visitante) usando XGBoost con features estadísticas históricas, e integra la API de Claude para generar explicaciones en lenguaje natural de cada predicción.

---

## 🧠 Pregunta de investigación

> *¿Puede un modelo XGBoost predecir el resultado de un partido de fútbol internacional con un F1-macro superior al baseline de regresión logística, y puede un LLM explicar esa predicción en lenguaje natural comprensible para un aficionado?*

---

## 📁 Estructura del repositorio

```
proyecto-futbol/
├── README.md
├── requirements.txt
├── docs/
│   ├── informe_final.pdf           ← Informe LaTeX compilado
│   ├── eda_distribucion.png
│   ├── eda_localidad.png
│   ├── resultados_modelos.png
│   ├── shap_importance.png
│   └── curvas_entrenamiento.png
├── notebooks/
│   ├── 01_eda.ipynb                ← Análisis exploratorio
│   ├── 02_preprocessing.ipynb     ← Feature engineering + split
│   ├── 03_modeling.ipynb          ← LR, RF, XGBoost + evaluación
│   └── 04_llm_explicaciones.ipynb ← Integración Gemini API
├── data/
│   ├── raw/                        ← Dataset original (descargar de Kaggle)
│   └── processed/                  ← Datos procesados (generados por los notebooks)
└── models/
    └── checkpoints/                ← Modelos entrenados (.pkl)
```

---

## ⚙️ Instalación y ejecución

### 1. Clonar el repositorio
```bash
git clone https://github.com/OsoRr10/Entrega_Final_IA
cd proyectoFinal
```

### 2. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 3. Descargar el dataset
Descargar desde Kaggle: [International Football Results](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017)  
Guardar `results.csv` en `data/raw/results.csv`

*(Alternativamente, los notebooks incluyen generación de datos sintéticos para correr sin credenciales de Kaggle)*

### 4. Configurar API key de Claude (para el notebook 04)
```bash
export ANTHROPIC_API_KEY="sk-ant-..."
```
Obtener key gratuita en: https://console.anthropic.com

### 5. Ejecutar los notebooks en orden
```bash
jupyter notebook
```
Correr en orden: `01_eda.ipynb` → `02_preprocessing.ipynb` → `03_modeling.ipynb` → `04_llm_explicaciones.ipynb`

---

## 📊 Resultados principales

| Modelo | Accuracy | F1-macro |
|--------|----------|----------|
| Baseline (Logistic Regression) | ~0.47 | ~0.44 |
| Experimento 1 (Random Forest) | ~0.52 | ~0.49 |
| **Exp. 2 (XGBoost) — mejor** | **~0.55** | **~0.52** |

*Los valores exactos se generan al correr el notebook 03.*

### Ejemplo de output del sistema LLM

```json
{
  "home_team": "Colombia",
  "away_team": "Brazil",
  "tournament": "Copa America",
  "prediction": "Victoria Visitante",
  "confidence": "61.3%",
  "probabilities": {
    "home_win": "22.1%",
    "draw": "16.6%",
    "away_win": "61.3%"
  },
  "llm_explanation": "Brasil llega con una tasa de victorias del 68% en sus últimos partidos y un promedio goleador de 2.1 goles, cifras que superan claramente a Colombia. El modelo identifica la superioridad histórica del equipo verdeamarillo como el factor decisivo. Aunque Colombia juega de local, el torneo se disputa en campo neutro, lo que neutraliza la ventaja de localía. Por estas razones, el modelo predice con 61% de confianza una victoria para Brasil."
}
```

---

## 🎥 Video demo

📹 [Ver demo ]([https://youtu.be/LINK-AL-VIDEO](https://eafit-my.sharepoint.com/:v:/g/personal/jjosorioa3_eafit_edu_co/IQD2hjciQGGzT4WxZkkKzTkNATG_p692zYRX7aHjHrXYmdA?e=3z7RbM)) 

---

## 👤 Integrante

| Nombre | Correo |
|--------|--------|
| Juan Jose Osorio Arango | jjosorioa3@eafit.edu.co |

---

## 📄 Informe

El informe completo en PDF está disponible en [`docs/informe_final.pdf`](docs/informe_final.pdf)

---

## 📚 Referencias

- Chen, T. & Guestrin, C. (2016). XGBoost: A Scalable Tree Boosting System. KDD 2016.
- Martj42 (2024). International Football Results Dataset. Kaggle.
- Anthropic (2024). Claude API Documentation. https://docs.anthropic.com
