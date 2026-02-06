<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="Chino">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="Inglés">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Español">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Portugués">
  <img src="https://img.shields.io/badge/Model-SDTL-orange" alt="Modelo">
  <img src="https://img.shields.io/badge/Task-SOH_Estimation-blueviolet" alt="Tarea">
  
  <h1>📚 Notas de Lectura: SDTL——Estimación de SOH en línea basada en Aprendizaje de Transferencia Profundo y Autoatención</h1>
  <p>Paper: Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols</p>
  
  <div style="margin: 10px 0;">
    <a href="./" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">Español</a> | 
    <a href="README_pt.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Português</a>
  </div>
</div>

> **Título del Artículo**: Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols  
> **Revista**: Journal of Power Sources (2025, Vol. 650, 237503)  
> **Método Principal**: SDTL (Self-attention-based Deep Transfer Learning)  
> **Alcance**: Estimación de SOH con muestras pequeñas a través de materiales catódicos (NCM/NCA), temperaturas y tasas.

## 🔍 Problemas Centrales
La estimación en línea del Estado de Salud (SOH) para baterías de iones de litio enfrenta desafíos significativos:
- **Escasez de Datos**: Datos insuficientes de etapas tempranas para baterías nuevas o condiciones específicas.
- **Condiciones Variables**: Diferencias significativas de degradación debido a materiales catódicos (ej. NCM vs. NCA), temperaturas ambientales (ej. baja temperatura 4℃) y tasas de descarga.
- **Generalización del Modelo**: Los modelos tradicionales de aprendizaje profundo luchan por mantener la precisión en condiciones operativas no vistas sin un reentrenamiento extenso.

## 💡 Metodología: El Marco SDTL
El artículo propone un enfoque de Aprendizaje de Transferencia Profundo basado en Autoatención (SDTL). Utiliza grandes conjuntos de datos de un dominio fuente para el preentrenamiento y se adapta rápidamente a un dominio objetivo utilizando solo una pequeña cantidad de datos de ciclos tempranos mediante ajuste fino (fine-tuning).

> 📊 **Diagrama del Marco SDTL**
> ![Marco SDTL](assets/fig1.jpg)
> *Esta figura ilustra el flujo de trabajo de SDTL: desde la adquisición de datos bajo diversas condiciones, extracción y selección de Indicadores de Salud (HIs), preentrenamiento fuera de línea en el dominio fuente, hasta el ajuste fino en línea y evaluación utilizando el primer 10% de los datos del dominio objetivo.*

### Detalles Técnicos Clave
1.  **Ingeniería de Características**:
    -   Se extrajeron 18 Indicadores de Salud (HIs) de curvas de voltaje, corriente y capacidad incremental (IC).
    -   Se seleccionaron 3 HIs clave usando el Coeficiente de Correlación de Pearson (PCC): Tiempo de descarga a corriente constante (HI5), Entropía de corriente (HI17) y Pendiente de corriente (HI18).
2.  **Arquitectura del Modelo**:
    -   Emplea **Autoatención Multicabezal (Multi-Head Self-Attention)** para capturar dependencias a largo plazo en series temporales.
    -   Incorpora Codificación Posicional para preservar la información de la secuencia.
3.  **Estrategia de Transferencia**:
    -   **Preentrenamiento**: Entrenamiento de parámetros del modelo en datos del dominio fuente.
    -   **Ajuste Fino**: Congelación de capas de la red excepto la capa totalmente conectada, que se actualiza utilizando el primer 10% de los datos de la batería objetivo.

> 📊 **Estructura del Modelo de Autoatención**
> ![Estructura del Modelo](assets/fig5.jpg)
> *Diagrama de la red basada en autoatención, incluyendo Codificación Posicional, bloques de Atención Multicabezal, Normalización de Capa y Redes Feed-Forward (FFN).*

## 📈 Resultados Experimentales
El modelo fue validado en dos conjuntos de datos (Serie A: baterías NCM, Serie B: baterías NCA de NASA) cubriendo diferentes temperaturas ($24^{\circ}C, 4^{\circ}C$) y tasas (1C, 2C).

- **Precisión**: SDTL logró un RMSE y MAE más bajos en comparación con los modelos base Transformer y LSTM.
- **Adaptación con Pocas Muestras**: Capaz de una predicción precisa del ciclo de vida completo utilizando solo el 10% de los datos de ciclos tempranos de la batería objetivo.
- **Ventaja Comparativa**: Superó a otros métodos de aprendizaje de transferencia (como DAAP, DAAD) tanto en precisión como en estabilidad.

> 📊 **Visualización de Resultados de Estimación de SOH**
> ![Resultados de Estimación](assets/fig8.jpg)
> *La Figura (a) muestra los resultados de estimación en tres series de baterías; la Figura (b) destaca el rendimiento de ajuste en condiciones de baja temperatura ($4^{\circ}C$); la Figura (c) presenta la comparación de distribución de errores.*

## 📚 Referencias
- **Cita**: X. Li, M. Zhao*, S. Zhong, J. Li, S. Fu, Z. Yan. Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols[J]. Journal of Power Sources, 2025, 650: 237503.
- **Fuentes de Datos**: Conjunto de datos propio de baterías NCM y Repositorio de Pronósticos de NASA (NCA).

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Fuente: <a href="https://doi.org/10.1016/j.jpowsour.2025.237503">Journal of Power Sources</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="#readme">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
