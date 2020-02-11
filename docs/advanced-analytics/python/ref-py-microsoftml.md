---
title: Paquete de Python microsoftml
description: Presenta los algoritmos y modelos de aprendizaje automático de Microsoft para Python, relacionados con las cargas de trabajo de aprendizaje automático de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ecbfd2edd20a312fc8a6d451938f1407585ded5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "73706953"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (módulo de Python en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**microsoftml** es un módulo compatible con Python35 de Microsoft que proporciona algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, la puntuación, el análisis de texto y de imágenes, y la extracción de características para derivar valores a partir de datos existentes.

Microsoft desarrolló las API de aprendizaje automático para aplicaciones de aprendizaje automático internas, y las ha ido perfeccionando a lo largo de los años para que admitan un alto rendimiento en macrodatos, mediante el procesamiento de varios núcleos y la transmisión rápida de datos. Este paquete se originó como un equivalente de Python de una versión de R, [MicrosoftML](../r/ref-r-microsoftml.md), que tiene funciones similares. 

## <a name="full-reference-documentation"></a>Documentación de referencia completa

La biblioteca de **microsoftml** se distribuye en varios productos de Microsoft, pero el uso es el mismo, se obtenga la biblioteca en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) se publica en una sola ubicación en la [referencia de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

El módulo de **microsoftml** se basa en Python 3.5 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente de Python para un cliente de ciencia de datos](setup-python-client-tools-sql.md)

> [!NOTE]
> En SQL Server 2017, las versiones completas del producto son solo para Windows. Para **microsoftml** en [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md), se admiten tanto Windows como Linux.

## <a name="package-dependencies"></a>Dependencias de paquetes

Los algoritmos de **microsoftml** dependen de [revoscalepy](ref-py-revoscalepy.md) para:

+ Objetos de origen de datos. Los datos consumidos por las funciones de **microsoftml** se crean mediante las funciones de **revoscalepy**.
+ Informática remota (cambio de la ejecución de la función a una instancia de SQL Server remota). La biblioteca de **revoscalepy** proporciona funciones para crear y activar un contexto de cálculo remoto para SQL Server.

En la mayoría de los casos, los paquetes se cargarán juntos siempre que se use **microsoftml**.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría, para darle una idea del uso de cada una de ellas. También puede usar la [tabla de contenido](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para ver las funciones en orden alfabético.

## <a name="1-training-functions"></a>1- Funciones de aprendizaje

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Entrena un conjunto de modelos. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Bosque aleatorio. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modelo lineal. con el ascenso estocástico dual de coordenadas. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Árboles impulsados. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regresión logística. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Red neuronal. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Detección de anomalías. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-Funciones de transformación

### <a name="categorical-variable-handling"></a>Control de variables de categorías

| Función | Descripción |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Convierte una columna de texto en categorías. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Aplica y convierte una columna de texto en categorías. |

### <a name="schema-manipulation"></a>Manipulación de esquemas

| Función | Descripción |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena varias columnas en un único vector. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Quita columnas de un conjunto de datos. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Conserva las columnas de un conjunto de datos. |


### <a name="variable-selection"></a>Selección de variables

| Función | Descripción |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Selecciona características basadas en recuentos. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Selecciona características basadas en la información mutua. |


### <a name="text-analytics"></a>Análisis de texto

| Función | Descripción |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Convierte las columnas de texto en características numéricas. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Análisis de sentimiento. |


### <a name="image-analytics"></a>Análisis de imagen 

| Función | Descripción |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carga una imagen. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Ajusta el tamaño de una imagen. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Extrae píxeles de una imagen. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Convierte una imagen en características. |

### <a name="featurization-functions"></a>Funciones de características

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Transformación de datos para orígenes de datos |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-Funciones de puntuación

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Puntuaciones mediante un modelo de aprendizaje automático de Microsoft |

## <a name="how-to-call-microsoftml"></a>Cómo llamar a microsoftml

Las funciones de **microsoftml** se pueden llamar en código Python encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones de **microsoftml** localmente y, después, migran el código Python final a los procedimientos almacenados como un ejercicio de implementación.

El paquete **microsoftml** para Python está instalado de forma predeterminada, pero a diferencia de **revoscalepy**, no se carga de forma predeterminada cuando se inicia una sesión de Python con los ejecutables de Python instalados con SQL Server.

Como primer paso, importe el paquete de **microsoftml** e importe **revoscalepy** si necesita usar contextos de cálculo remotos o conectividad u objetos de origen de datos relacionados. Después, haga referencia a las funciones individuales que necesite.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Consulte también

+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Código de Python para insertar en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referencia de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

