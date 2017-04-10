---
title: "Usar el paquete MicrosoftML con SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Usar el paquete MicrosoftML con SQL Server R Services
El paquete **MicrosoftML** incluido en Microsoft R Server y SQL Server vNext CTP 1.0 contiene varios algoritmos de aprendizaje automáticos desarrollados por Microsoft que admiten el procesamiento de varios núcleos y la transmisión de datos rápida. El paquete también incluye transformaciones para el procesamiento de texto y características.

### <a name="new-machine-learning-algorithms"></a>Nuevos algoritmos de aprendizaje automático


-  **Lineal rápido.** Aprendiz lineal basado en el ascenso estocástico dual de coordenadas que puede usarse para la clasificación o la regresión binarias. El modelo admite regularización L1 y L2.

- **Árbol rápido.** Un algoritmo de árbol de decisión incrementado originalmente conocido como FastRank que se desarrolló para su uso en Bing. Es uno de los aprendices más rápidos y populares. Admite la regresión y la clasificación binarias.

- **Bosque rápido.** Modelo de regresión logística basado en el método de bosque aleatorio. Es similar a la función `rxLogit` de RevoScaleR, aunque admite la regularización L1 y L2. Admite la regresión y la clasificación binarias.

- **Regresión logística.** Modelo de regresión logística similar a la función `rxLogit` de RevoScaleR, con compatibilidad adicional con la regularización L1 y L2. Admite la clasificación binaria o de varias clases.

- **Red neuronal.** Modelo de red neuronal para la clasificación binaria, la clasificación de varias clases y la regresión. Admite la aceleración GPU y las redes intrincadas personalizables.

- **SVM de una clase.** Modelo de detección de anomalías basado en el método SVM que puede usarse para la clasificación binaria en conjuntos de datos desequilibrados.

## <a name="transformation-functions"></a>Funciones de transformación

El paquete **MicrosoftML** también incluye las siguientes funciones que se pueden usar para transformar datos y extraer características.

- `featurizeText()`
 
  Genera recuentos de ngrams en una cadena de texto determinada. 

  La función incluye las opciones para detectar el idioma empleado, realiza la tokenización y la normalización del texto, quita las palabras irrelevantes y genera características a partir del texto. 

- `categorical()`

  Genera un diccionario de categorías y transforma cada categoría en un vector indicador. 
 
- `categoricalHash()`

  Convierte valores de categorías en una matriz indicadora al crear un hash a partir del valor y usar ese hash como un índice en la bolsa.  

- `selectFeatures()` 

  Selecciona un subconjunto de características de la variable determinada, ya sea al contar valores no predeterminados o al calcular una puntuación de información mutua con respecto a la etiqueta. 

Para obtener información detallada sobre estas nuevas características, consulte [MicrosoftML functions](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml) (Funciones de MicrosoftML).

## <a name="support-for-microsoftml-in-r-services"></a>Compatibilidad con MicrosoftML en R Services

El paquete **MicrosoftML** está totalmente integrado con la canalización de procesamiento de datos usada por el paquete **RevoScaleR**. Actualmente, se puede usar el paquete **MicrosoftML** en cualquier contexto de cálculo basado en Windows, incluido SQL Server R Services.



## <a name="see-also"></a>Vea también


[Referencia a la función RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)

