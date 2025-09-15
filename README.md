# Naive-Bayes-Ghostbusters

[![Repo](https://img.shields.io/badge/GitHub-Naive--Bayes--Ghostbusters-181717?logo=github)](https://github.com/goveaangel/Naive-Bayes-Ghostbusters.git)

---

## Resumen

Este proyecto desarrolla un **clasificador Naive Bayes** aplicado a relatos de *Your Ghost Stories*.  
Se comparan distintas **representaciones de texto** —**BOW completo**, **BOW Top-800**, **NRC** (emociones) y **combinaciones**— evaluando su impacto en **accuracy**, **precision**, **recall** y **F1**.  

El mejor desempeño general se obtuvo con **BOW Top-800 + NRC** (~**0.77** de accuracy).  
Con *cross-validation* de Laplace, el **BOW completo** alcanzó la mayor *accuracy* (**0.7845**).

---

## Objetivo

Explorar cómo la **reducción de dimensionalidad** (vocabulario Top-N) y la **incorporación de rasgos semánticos** (emociones NRC) impactan la clasificación automática de relatos narrativos en dos categorías:

- Haunted Places  
- Old Hags / Sleep Paralysis  

---

## Metodología

1. **Web Scraping**
   - `robotstxt::paths_allowed()` para verificar acceso.  
   - Extracción con **rvest**: título, fecha, país, categoría y texto.  
   - Dataset final: miles de relatos.

2. **Procesamiento**
   - Limpieza de texto, tokenización, eliminación de *stopwords*.  
   - Variantes: **BOW completo**, **BOW Top-800**.  
   - Cálculo de emociones con **NRC**.  
   - Construcción de **Document–Term Matrix**.

3. **Modelado**
   - **e1071::naiveBayes** (baseline).  
   - **naivebayes::naive_bayes** (con y sin `usepoisson`).  
   - **Cross-Validation de Laplace** para elegir el mejor suavizado.  

4. **Evaluación**
   - Split **70/30** estratificado.  
   - Métricas: **accuracy**, **precision**, **recall**, **F1**.  
   - Matrices de confusión + gráficas comparativas.  

---

## Resultados principales

### e1071 (baseline)
- **Mejor dataset:** BOW Top-800  
- `accuracy = 0.7716`, `precision = 0.8178`, `recall = 0.7231`, `F1 = 0.7675`.

### naivebayes (Poisson opcional)
- Poisson ≈ sin Poisson (mínimas diferencias).  
- Nuevamente, **Top-800** fue el más equilibrado.

### e1071 + Cross-Validation Laplace
- CV eligió siempre **Laplace = 0**.  
- **Mejor dataset:** BOW completo  
- `accuracy = 0.7845`, `precision = 0.8413`, `recall = 0.7231`, `F1 = 0.7778`.

---


---

## Requisitos

- **R ≥ 4.2.0**
- Instalar dependencias:
  ```R
  install.packages(c(
    "robotstxt","rvest","purrr","dplyr","stringr","lubridate",
    "parallel","tidytext","tm","naivebayes","syuzhet",
    "caret","tibble","janitor","ggplot2","tidyr",
    "e1071","discrim","klaR","scales"
  ))

