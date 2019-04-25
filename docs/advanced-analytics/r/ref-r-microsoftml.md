---
title: Biblioteca de funciones de MicrosoftML R - SQL Server Machine Learning Services
description: Introducción a la biblioteca de funciones de MicrosoftML en SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 73d9dcf56c0eb5e69704adf169946f6aa28a432c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641825"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (biblioteca de R en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** es una biblioteca de funciones de R de Microsoft que proporciona los algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, puntuación, análisis de texto e imagen y extracción de características para derivar valores de datos existentes.

El aprendizaje automático de API se han desarrollado por Microsoft para aplicaciones de aprendizaje de automático interno y se han perfeccionado en los años para admitir de alto rendimiento en macrodatos, con el procesamiento de varios núcleos y la transmisión de datos rápida. MicrosoftML incluye también numerosas transformaciones para el procesamiento de imagen y texto.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El **MicrosoftML** library se distribuye en varios productos de Microsoft, pero el uso es el mismo si obtener la biblioteca de SQL Server u otro producto. Dado que las funciones son los mismos, [documentación para las funciones de RevoScaleR individuales](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Debe cualquier producto específico comportamientos existen, se anotará discrepancias en la página de Ayuda de la función.

## <a name="versions-and-platforms"></a>Las versiones y plataformas

El **MicrosoftML** biblioteca se basa en R 3.4.3 y disponibles solo al instalar uno de los siguientes productos de Microsoft o descargas:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> Versiones de lanzamiento de producto completo son sólo Windows, a partir de SQL Server 2017. Linux support para **MicrosoftML** es nuevo en [versión preliminar de SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependencias de paquetes

Los algoritmos en **MicrosoftML** dependen [RevoScaleR](ref-r-revoscaler.md) para:

+ Objetos de origen de datos. Consumen datos **MicrosoftML** las funciones se crean mediante **RevoScaleR** funciones.
+ Informática (ejecución cambiante de la función a una instancia remota de SQL Server) remoto. El **RevoScaleR** biblioteca proporciona funciones para crear y activar un control remoto de proceso de contexto para SQL server.

En la mayoría de los casos, cargará los paquetes entre sí cuando se usen **MicrosoftML**.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumera las funciones por categoría para darle una idea de cómo se usa cada uno de ellos. También puede usar el [tabla de contenido](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para buscar las funciones en orden alfabético.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>Algoritmos de aprendizaje automático de 1

| Nombre de función | Descripción |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Implementación de una implementación eficaz de gradiente mart. algoritmo de impulso FastRank.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Un bosque aleatorio y una implementación de bosque de regresión de Cuantil con [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regresión logística con L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Máquinas de vectores de soporte técnico de una clase.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Binario, varias clases y regresión Red neuronal.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Optimización de ascenso estocástico de coordenadas dual para lineal clasificación binaria y regresión. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Entrena un número de modelos de varias clases para obtener el mejor rendimiento predictivo que podría obtenerse a partir de un único modelo.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>Funciones de transformación de 2

| Nombre de función | Descripción |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Transformación para crear una sola columna con valores de vector de varias columnas.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Crear vector indicador mediante transformación categorías con el diccionario.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Convierte el valor de categoría en una matriz de indicador aplicando un algoritmo hash. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Genera un contenedor de los recuentos de secuencias de palabras consecutivas, que se llama n-gramas, desde un determinado corpus de texto. Ofrece la detección de idioma, la tokenización, eliminación de palabras irrelevantes, normalización de texto y generación de características.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Puntuaciones de texto de lenguaje natural y crea una columna que contiene las probabilidades de que las opiniones del texto son positivas.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | permite definir argumentos para la extracción de características basada en recuento y basado en hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Selecciona un conjunto de columnas que se va a reciclar, quitar todos los demás. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Selecciona las características de las variables especificadas mediante un modo especificado.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carga los datos de imagen.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Cambia el tamaño de una imagen a una dimensión especificada con un método de cambio de tamaño especificado.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Extrae los valores de píxel de una imagen.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Caracteriza una imagen mediante un modelo de red neuronal profunda ya entrenada.|


## <a name="3-scoring-and-training-functions"></a>Funciones de entrenamiento y puntuación de 3

| Nombre de función | Descripción |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Se ejecuta en la biblioteca de puntuación desde SQL Server, mediante el procedimiento almacenado, o desde código de R, lo cual permite puntuar en tiempo real proporcionar un rendimiento de predicción mucho más rápido.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Transforma los datos de un conjunto de datos de entrada a un conjunto de datos de salida.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Proporciona un resumen de un modelo de Machine Learning de Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>Funciones de pérdida de 4 para la clasificación y regresión

| Nombre de función | Descripción |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación exponencial. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de registro.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de bisagra de la clasificación. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de bisagra smooth clasificación.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de regresión de poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de regresión al cuadrado.   |   

## <a name="5-feature-selection-functions"></a>Funciones de selección de características de 5

| Nombre de función | Descripción |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Especificación de selección de características en modo de recuento. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Especificación de selección de características en el modo de información mutua. |

## <a name="6-ensemble-modeling-functions"></a>Funciones de modelado de conjunto de 6

| Nombre de función | Descripción |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de árbol rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de bosque rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo lineal rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de regresión logística con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo OneClassSvm con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>Las funciones de red neuronal de 7

| Nombre de función | Descripción |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Especifica los algoritmos de optimización para la [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) algoritmo de aprendizaje automático.|


## <a name="8-package-state-functions"></a>Funciones de estado del paquete de 8

| Nombre de función | Descripción |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Un objeto de entorno que se usa para almacenar el estado de todo el paquete. |


## <a name="how-to-use-microsoftml"></a>Cómo usar MicrosoftML

Las funciones de **MicrosoftML** son invocables en código R encapsulada en procedimientos almacenados. La mayoría de los desarrolladores crear **MicrosoftML** soluciones localmente, y, a continuación, migrar código de R terminado a los procedimientos almacenados como un ejercicio de implementación.

El **MicrosoftML** de paquetes de R es instaladas "de-la-listos para usar" en SQL Server 2017. También está disponible para su uso con SQL Server 2016 si actualiza los componentes de R para la instancia: [Actualizar una instancia de SQL Server mediante el enlace](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

No se carga el paquete de forma predeterminada. Como primer paso, cargue el **MicrosoftML** del paquete y, a continuación, cargar **RevoScaleR** si debe usar contextos de cálculo remoto u objetos de origen de conectividad o los datos relacionados. A continuación, hacer referencia a las funciones individuales que necesita.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Vea también

+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Aprenda a usar contextos de cálculo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: Entrenar y uso de modelos](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Muestras de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referencia de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 