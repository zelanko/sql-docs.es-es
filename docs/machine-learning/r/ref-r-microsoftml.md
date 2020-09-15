---
title: Paquete MicrosoftML R
description: MicrosoftML es un paquete de R de Microsoft que proporciona algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, la puntuación, el análisis de texto y de imágenes, y la extracción de características para derivar valores a partir de datos existentes. El paquete se incluye en SQL Server Machine Learning Services y SQL Server 2016 R y admite un alto rendimiento en macrodatos, mediante el procesamiento de varios núcleos y un flujo de datos rápido. MicrosoftML también incluye numerosas transformaciones para el procesamiento de texto e imágenes.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/06/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d7b48e547d402e15404e39e849c262320c5ee59e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179952"
---
# <a name="microsoftml-r-package-in-sql-server-machine-learning-services"></a>MicrosoftML (paquete de R en SQL Server Machine Learning Services)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**MicrosoftML** es un paquete de R de Microsoft que proporciona algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, la puntuación, el análisis de texto y de imágenes, y la extracción de características para derivar valores a partir de datos existentes. El paquete se incluye en [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) y [SQL Server 2016 R](sql-server-r-services.md) y admite un alto rendimiento en macrodatos, mediante el procesamiento de varios núcleos y un flujo de datos rápido. MicrosoftML también incluye numerosas transformaciones para el procesamiento de texto e imágenes.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El paquete **MicrosoftML** se distribuye en varios productos de Microsoft, pero el uso es el mismo independientemente de si se obtiene el paquete en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

El paquete **MicrosoftML** se basa en R 3.4.3 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Cliente de Microsoft R](set-up-a-data-science-client.md)

> [!NOTE]
> En SQL Server 2017, las versiones completas del producto son solo para Windows. Para **MicrosoftML** en [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md), se admiten tanto Windows como Linux.

## <a name="package-dependencies"></a>Dependencias de paquetes

Los algoritmos de **MicrosoftML** dependen de [RevoScaleR](ref-r-revoscaler.md) para:

+ Objetos de origen de datos. Los datos consumidos por las funciones de **MicrosoftML** se crean mediante las funciones de **RevoScaleR**.
+ Informática remota (cambio de la ejecución de la función a una instancia de SQL Server remota). El paquete **RevoScaleR** proporciona funciones para crear y activar un contexto de cálculo remoto para SQL Server.

En la mayoría de los casos, los paquetes se cargarán juntos siempre que se use **MicrosoftML**.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría, para darle una idea del uso de cada una de ellas. También puede usar la [tabla de contenido](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para ver las funciones en orden alfabético.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1- Algoritmos de aprendizaje automático

| Nombre de función | Descripción |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Una implementación de FastRank, una implementación eficaz del algoritmo de impulso de gradiente MART.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Un bosque aleatorio y una implementación de bosque de regresión por cuantiles mediante [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regresión logística mediante L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Máquinas de vectores de soporte de una clase.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Red neuronal binaria, de varias clases y de regresión.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Optimización del ascenso estocástico dual de coordenadas para la regresión y clasificación binaria lineal. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Entrena varios modelos de diversos tipos para obtener un mejor rendimiento predictivo que el que se podría obtener a partir de un único modelo.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2- Funciones de transformación

| Nombre de función | Descripción |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Transformación para crear una columna de valor vectorial única a partir de varias columnas.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Cree un vector indicador mediante la transformación categórica con el diccionario.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Convierte el valor categórico en una matriz indicadora mediante un código hash. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Genera un contenedor de recuentos de secuencias de palabras consecutivas, denominadas n-gramas, a partir de un corpus de texto determinado. Ofrece detección de idioma, tokenización, eliminación de palabras irrelevantes, normalización de texto y generación de características.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Puntúa el texto en lenguaje natural y crea una columna que contiene las probabilidades de que las opiniones del texto sean positivas.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | Permite definir argumentos para la extracción de características basada en recuentos y en hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Selecciona un conjunto de columnas para volver a entrenar, y elimina todas las demás. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Selecciona las características de las variables especificadas mediante un modo especificado.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carga los datos de la imagen.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Cambia el tamaño de una imagen a una dimensión especificada mediante un método de cambio de tamaño determinado.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Extrae los valores de píxeles de una imagen.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Caracteriza una imagen mediante un modelo de red neuronal profunda previamente entrenado.|


## <a name="3-scoring-and-training-functions"></a>3- Funciones de puntuación y aprendizaje

| Nombre de función | Descripción |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Ejecuta la biblioteca de puntuación desde SQL Server, mediante el procedimiento almacenado, o bien desde código R, lo que permite una puntuación en tiempo real para proporcionar un rendimiento de predicción mucho más rápido.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Transforma los datos de un conjunto de datos de entrada en un conjunto de datos de salida.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Proporciona un resumen de un modelo de Machine Learning de Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4- Funciones de pérdida para clasificación y regresión

| Nombre de función | Descripción |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación exponencial. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de registros.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de bisagra. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de bisagra uniforme.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de regresión de Poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de regresión cuadrada.   |   

## <a name="5-feature-selection-functions"></a>5- Funciones de selección de características

| Nombre de función | Descripción |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Especificación de la selección de características en el modo de recuento. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Especificación de la selección de características en el modo de información mutua. |

## <a name="6-ensemble-modeling-functions"></a>6- Funciones de modelado de conjuntos

| Nombre de función | Descripción |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de árbol rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de bosque rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de lineal rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de regresión logística con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de OneClassSvm con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>7- Funciones de red neuronal

| Nombre de función | Descripción |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Especifica los algoritmos de optimización para el algoritmo de aprendizaje automático [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet).|


## <a name="8-package-state-functions"></a>8- Funciones de estado del paquete

| Nombre de función | Descripción |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Objeto de entorno que se usa para almacenar el estado de todo el paquete. |


## <a name="how-to-use-microsoftml"></a>Cómo usar MicrosoftML

Las funciones de **MicrosoftML** se pueden llamar en código R encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones de **MicrosoftML** localmente y, después, migran el código R final a los procedimientos almacenados como un ejercicio de implementación.

El paquete de **MicrosoftML** para R está instalado de forma preconfigurada en SQL Server 2017. También está disponible para su uso con SQL Server 2016 si actualiza los componentes de R para la instancia: [Actualizar una instancia de SQL Server mediante el enlace de datos](../install/upgrade-r-and-python.md)

El paquete no se carga de forma predeterminada. Como primer paso, cargue el paquete de **MicrosoftML** y, después, cargue **RevoScaleR** si necesita usar contextos de cálculo remotos o conectividad u objetos de origen de datos relacionados. Después, haga referencia a las funciones individuales que necesite.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Consulte también

+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Información sobre cómo usar contextos de cálculo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: Entrenar y hacer operativo un modelo](../tutorials/r-taxi-classification-introduction.md)
+ [Ejemplos de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referencia de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 