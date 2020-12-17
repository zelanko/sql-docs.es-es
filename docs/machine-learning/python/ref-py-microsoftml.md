---
title: Paquete de Python microsoftml
description: microsoftml es un paquete de Python de Microsoft que proporciona algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, la puntuación, el análisis de texto y de imágenes, y la extracción de características para derivar valores a partir de datos existentes. El paquete se incluye en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15'
ms.openlocfilehash: ec421e1b0e112a535e3caa59cf83e01c4e02086c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470946"
---
# <a name="microsoftml-python-package-in-sql-server-machine-learning-services"></a>microsoftml (paquete de Python en SQL Server Machine Learning Services)
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

**microsoftml** es un paquete de Python de Microsoft que proporciona algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, la puntuación, el análisis de texto y de imágenes, y la extracción de características para derivar valores a partir de datos existentes. El paquete se incluye en [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) y admite un alto rendimiento en macrodatos, mediante el procesamiento de varios núcleos y un flujo de datos rápido.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El paquete de **microsoftml** se distribuye en varios productos de Microsoft, pero el uso es el mismo independientemente de si se obtiene el paquete en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) se publica en una sola ubicación en la [referencia de Python](/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

El módulo de **microsoftml** se basa en Python 3.5 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](/machine-learning-server/)
+ [Bibliotecas de cliente de Python para un cliente de ciencia de datos](setup-python-client-tools-sql.md)

> [!NOTE]
> En SQL Server 2017, las versiones completas del producto son solo para Windows. Para **microsoftml** en [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md), se admiten tanto Windows como Linux.

## <a name="package-dependencies"></a>Dependencias de paquetes

Los algoritmos de **microsoftml** dependen de [revoscalepy](ref-py-revoscalepy.md) para:

+ Objetos de origen de datos. Los datos consumidos por las funciones de **microsoftml** se crean mediante las funciones de **revoscalepy**.
+ Informática remota (cambio de la ejecución de la función a una instancia de SQL Server remota). El paquete de **revoscalepy** proporciona funciones para crear y activar un contexto de cálculo remoto para SQL Server.

En la mayoría de los casos, los paquetes se cargarán juntos siempre que se use **microsoftml**.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría, para darle una idea del uso de cada una de ellas. También puede usar la [tabla de contenido](/machine-learning-server/python-reference/introducing-python-package-reference) para ver las funciones en orden alfabético.

## <a name="1-training-functions"></a>1- Funciones de aprendizaje

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_ensemble](/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Entrena un conjunto de modelos. |
|[microsoftml.rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Bosque aleatorio. |
|[microsoftml.rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modelo lineal. con el ascenso estocástico dual de coordenadas. |
|[microsoftml.rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Árboles impulsados. |
|[microsoftml.rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regresión logística. |
|[microsoftml.rx_neural_network](/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Red neuronal. |
|[microsoftml.rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Detección de anomalías. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-Funciones de transformación

### <a name="categorical-variable-handling"></a>Control de variables de categorías

| Función | Descripción |
|----------|-------------|
|[microsoftml.categorical](/machine-learning-server/python-reference/microsoftml/categorical) | Convierte una columna de texto en categorías. |
|[microsoftml.categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash) | Aplica y convierte una columna de texto en categorías. |

### <a name="schema-manipulation"></a>Manipulación de esquemas

| Función | Descripción |
|----------|-------------|
|[microsoftml.concat](/machine-learning-server/python-reference/microsoftml/concat) | Concatena varias columnas en un único vector. |
|[microsoftml.drop_columns](/machine-learning-server/python-reference/microsoftml/drop-columns) | Quita columnas de un conjunto de datos. |
|[microsoftml.select_columns](/machine-learning-server/python-reference/microsoftml/select-columns) | Conserva las columnas de un conjunto de datos. |


### <a name="variable-selection"></a>Selección de variables

| Función | Descripción |
|----------|-------------|
|[microsoftml.count_select](/machine-learning-server/python-reference/microsoftml/count-select) |Selecciona características basadas en recuentos. |
|[microsoftml.mutualinformation_select](/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Selecciona características basadas en la información mutua. |


### <a name="text-analytics"></a>Análisis de texto

| Función | Descripción |
|----------|-------------|
|[microsoftml.featurize_text](/machine-learning-server/python-reference/microsoftml/featurize-text) | Convierte las columnas de texto en características numéricas. |
|[microsoftml.get_sentiment](/machine-learning-server/python-reference/microsoftml/get-sentiment) | Análisis de sentimiento. |


### <a name="image-analytics"></a>Análisis de imagen 

| Función | Descripción |
|----------|-------------|
|[microsoftml.load_image](/machine-learning-server/python-reference/microsoftml/load-image) | Carga una imagen. |
|[microsoftml.resize_image](/machine-learning-server/python-reference/microsoftml/resize-image) | Ajusta el tamaño de una imagen. |
|[microsoftml.extract_pixels](/machine-learning-server/python-reference/microsoftml/extract-pixels) | Extrae píxeles de una imagen. |
|[microsoftml.featurize_image](/machine-learning-server/python-reference/microsoftml/featurize-image) | Convierte una imagen en características. |

### <a name="featurization-functions"></a>Funciones de características

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_featurize](/machine-learning-server/python-reference/microsoftml/rx-featurize) | Transformación de datos para orígenes de datos |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-Funciones de puntuación

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_predict](/machine-learning-server/python-reference/microsoftml/rx-predict) | Puntuaciones mediante un modelo de aprendizaje automático de Microsoft |

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

+ [Tutoriales de Python](../tutorials/python-tutorials.md)
+ [Referencia de Python (Microsoft Machine Learning Server)](/machine-learning-server/python-reference/introducing-python-package-reference)