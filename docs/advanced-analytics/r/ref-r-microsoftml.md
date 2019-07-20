---
title: Biblioteca de funciones de R de MicrosoftML
description: Introducción a la biblioteca de funciones de MicrosoftML en SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2cf89b26ffad2902223a84e19ccaf425aa6f8b2d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344898"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (biblioteca de R en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** es una biblioteca de funciones de R de Microsoft que proporciona algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, la puntuación, el análisis de texto y de imagen, y la extracción de características para derivar valores a partir de datos existentes.

Microsoft desarrolló las API de machine learning para aplicaciones de aprendizaje automático internas y se han perfeccionado durante los años para admitir un alto rendimiento en macrodatos, mediante el procesamiento de varios núcleos y el streaming de datos rápido. MicrosoftML también incluye numerosas transformaciones para el procesamiento de texto e imágenes.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

La biblioteca **MicrosoftML** se distribuye en varios productos de Microsoft, pero el uso es el mismo si se obtiene la biblioteca en SQL Server u otro producto. Dado que las funciones son iguales, la [documentación de las funciones individuales de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft machine learning Server. Si hay algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

La biblioteca **MicrosoftML** se basa en R 3.4.3 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Cliente de Microsoft R](set-up-a-data-science-client.md)

> [!NOTE]
> Las versiones completas del producto son solo de Windows, empezando por SQL Server 2017. La compatibilidad con Linux para **MicrosoftML** es nueva en [SQL Server vista previa de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependencias de paquetes

Los algoritmos de **MicrosoftML** dependen de [RevoScaleR](ref-r-revoscaler.md) para:

+ Objetos de origen de datos. Los datos consumidos por las funciones de **MicrosoftML** se crean mediante las funciones de **RevoScaleR** .
+ Informática remota (cambio de la ejecución de la función a una instancia de SQL Server remota). La biblioteca **RevoScaleR** proporciona funciones para crear y activar un contexto de cálculo remoto para SQL Server.

En la mayoría de los casos, los paquetes se cargarán juntos siempre que se use **MicrosoftML**.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría para darle una idea de cómo se usa cada una de ellas. También puede usar la [tabla de contenido](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para buscar funciones en orden alfabético.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1: algoritmos de aprendizaje automático

| Nombre de función | Descripción |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Una implementación de FastRank, una implementación eficaz del algoritmo de impulso de gradiente MART.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Un bosque aleatorio y una implementación de bosque de regresión de por cuantiles con [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regresión logística mediante L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Una clase admite máquinas de vectores.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Red neuronal binaria, de varias clases y de regresión.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Optimización de ascenso de coordenada doble de estocástico para la regresión y clasificación binaria lineal. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Entrena varios modelos de diversos tipos para obtener un mejor rendimiento predictivo que el que se puede obtener a partir de un único modelo.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2: funciones de transformación

| Nombre de función | Descripción |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Transformación para crear una columna de valor vectorial única a partir de varias columnas.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Cree un vector de indicador mediante la transformación de categorías con el diccionario.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Convierte el valor de categoría en una matriz de indicador mediante un algoritmo hash. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Genera un contenedor de recuentos de secuencias de palabras consecutivas, denominadas n-gramas, de un corpus de texto determinado. Ofrece detección de idioma, tokenización, eliminación de palabras irrelevantes, normalización de texto y generación de características.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Puntua texto en lenguaje natural y crea una columna que contiene las probabilidades de que las opiniones del texto sean positivas.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | permite definir argumentos para la extracción de características basada en recuentos y en hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Selecciona un conjunto de columnas para volver a entrenar, quitando todas las demás. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Selecciona las características de las variables especificadas mediante un modo especificado.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carga los datos de la imagen.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Cambia el tamaño de una imagen a una dimensión especificada utilizando un método de cambio de tamaño especificado.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Extrae los valores de píxeles de una imagen.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Featurizes una imagen mediante un modelo de red neuronal en profundidad previamente entrenado.|


## <a name="3-scoring-and-training-functions"></a>3-funciones de puntuación y aprendizaje

| Nombre de función | Descripción |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Ejecuta la biblioteca de puntuación desde SQL Server, mediante el procedimiento almacenado o desde código R, lo que permite una puntuación en tiempo real para proporcionar un rendimiento de predicción mucho más rápido.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Transforma los datos de un conjunto de datos de entrada en un conjunto de datos de salida.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Proporciona un resumen de un modelo de Machine Learning de Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-funciones de pérdida de clasificación y regresión

| Nombre de función | Descripción |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación exponencial. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de registro.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de bisagras. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de clasificación de bisagras suaves.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de regresión de Poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificaciones de la función de pérdida de regresión cuadrada.   |   

## <a name="5-feature-selection-functions"></a>5: funciones de selección de características

| Nombre de función | Descripción |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Especificación de la selección de características en el modo de recuento. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Especificación de la selección de características en modo de información mutua. |

## <a name="6-ensemble-modeling-functions"></a>funciones de modelado de 6 conjuntos

| Nombre de función | Descripción |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de árbol rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de bosque rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo lineal rápido con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo de regresión logística con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Crea una lista que contiene el nombre de la función y los argumentos para entrenar un modelo OneClassSvm con [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>7: funciones de red neuronal

| Nombre de función | Descripción |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Especifica los algoritmos de optimización para el algoritmo de aprendizaje automático de [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) .|


## <a name="8-package-state-functions"></a>8: funciones de estado de paquete

| Nombre de función | Descripción |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Objeto de entorno que se usa para almacenar el estado de todo el paquete. |


## <a name="how-to-use-microsoftml"></a>Cómo usar MicrosoftML

Las funciones de **MicrosoftML** se pueden llamar en código R encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones **MicrosoftML** localmente y, después, migran el código R finalizado a procedimientos almacenados como un ejercicio de implementación.

El paquete **MicrosoftML** para R está instalado de forma preconfigurada en SQL Server 2017. También está disponible para su uso con SQL Server 2016 si actualiza los componentes de R para la instancia: [Actualizar una instancia de SQL Server mediante enlace](../install/upgrade-r-and-python.md)

El paquete no se carga de forma predeterminada. Como primer paso, cargue el paquete **MicrosoftML** y, a continuación, cargue **RevoScaleR** si necesita usar contextos de cálculo remotos o los objetos de origen de datos o la conectividad relacionada. A continuación, haga referencia a las funciones individuales que necesite.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Vea también

+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Aprenda a usar contextos de cálculo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: Entrenar y poner en funcionamiento un modelo](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Ejemplos de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referencia de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 