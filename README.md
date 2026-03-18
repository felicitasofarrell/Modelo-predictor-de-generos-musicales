# TP3 — Clasificación de Géneros Musicales con CNN

Proyecto desarrollado para **Tecnología Digital 6**, orientado a la **clasificación automática de géneros musicales** a partir de audio.

El trabajo parte de un modelo base y explora distintas decisiones de diseño para mejorar su desempeño, incluyendo:

- arquitecturas densas y convolucionales,
- batch size y cantidad de épocas,
- funciones de activación,
- optimizadores y schedulers,
- técnicas de regularización,
- comparación entre **waveforms** y **espectrogramas** como input.

## Objetivo

Construir y optimizar un modelo capaz de predecir el género de una canción a partir de su representación en audio.

## Enfoque

A lo largo del proyecto se realizaron experimentos iterativos, eligiendo en cada etapa la mejor configuración para avanzar a la siguiente. Se evaluó el desempeño usando principalmente:

- **validation loss**
- **validation accuracy**
- **test accuracy**

## Principales experimentos

### 1. Arquitectura densa
Se probaron redes densas con distinta cantidad de capas ocultas y nodos.

**Mejor resultado:**
- 2 capas ocultas
- 64 neuronas por capa
- batch size = 20
- epochs = 5 

### 2. Arquitectura CNN
Luego se evaluaron CNN con distinta profundidad.

**Mejor resultado:**
- 4 capas convolucionales
- batch size = 20
- epochs = 5 

### 3. Entrenamiento
Se compararon distintos batch sizes y cantidades de épocas.

**Mejor resultado:**
- 4 capas convolucionales
- batch size = 10
- epochs = 10
- valid accuracy ≈ 0.49 

### 4. Funciones de activación
Se probaron:
- ReLU
- Leaky ReLU
- tanh
- sigmoid

**Mejor resultado:**
- activación **tanh**
- valid accuracy ≈ 0.62
- valid loss mínima ≈ 1.2134 

### 5. Optimizadores y schedulers
Se compararon:
- Adam
- SGD
- RMSprop
- Adam + ReduceLROnPlateau
- Adam + StepLR

**Mejor resultado:**
- **Adam + StepLR**
- valid accuracy ≈ 0.59
- valid loss mínima ≈ 1.0985 

### 6. Regularización
Se probaron:
- Dropout (0.4)
- weight decay

En este caso, la regularización **no mejoró** los resultados y redujo la accuracy del modelo. :contentReference[oaicite:6]{index=6}

## Input utilizado

Inicialmente se intentó trabajar con **waveforms**, pero surgieron problemas de compatibilidad debido al tamaño variable de las señales.  
Por eso, para las CNN se decidió usar **espectrogramas**, que resultaron más adecuados para este tipo de arquitectura. :contentReference[oaicite:7]{index=7}

## Modelo final

La configuración final elegida fue:

- **CNN de 4 capas convolucionales**
- **10 epochs**
- **batch size = 10**
- **función de activación: tanh**
- **optimizador: Adam**
- **learning rate: 0.0001**
- **scheduler: StepLR** 

## Resultado final

En el conjunto de test, el modelo obtuvo:

- **test accuracy = 0.54** 

Esto muestra un desempeño moderado y deja margen para seguir mejorando.

## Estructura del proyecto

```text
.
├── TP3_TD6_Grupo24.ipynb              # Notebook principal con experimentos y entrenamiento
├── Informe TP3 TD6 - Grupo 24.pdf     # Informe con análisis y resultados
└── README.md
