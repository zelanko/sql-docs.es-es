---
title: 'paquete de Python microsoftml: SQL Server Machine Learning Services'
description: Modelos de Python, con respecto a las cargas de trabajo de SQL Server machine learning y presenta lo algoritmos de aprendizaje automático de Microsoft.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 618c4b127c42aae6a5b8d7570f1962f8c8e38e9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642363"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (módulo de Python en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml** es un módulo Python35 compatible de Microsoft que proporciona los algoritmos de aprendizaje automático de alto rendimiento. Incluye funciones para el entrenamiento y las transformaciones, puntuación, análisis de texto e imagen y extracción de características para derivar valores de datos existentes.

El aprendizaje automático de las API desarrolladas por Microsoft para aplicaciones de aprendizaje automático interno y se han perfeccionado en los años para admitir de alto rendimiento en macrodatos, con el procesamiento de varios núcleos y la transmisión de datos rápida. Este paquete se originó como un equivalente de una versión de R, Python [MicrosoftML](../r/ref-r-microsoftml.md), que tiene funciones similares. 

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El **microsoftml** library se distribuye en varios productos de Microsoft, pero el uso es el mismo si obtener la biblioteca de SQL Server u otro producto. Dado que las funciones son los mismos, [documentación para las funciones de microsoftml individuales](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) se publica en una sola ubicación en la [referencia de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Debe cualquier producto específico comportamientos existen, se anotará discrepancias en la página de Ayuda de la función.

## <a name="versions-and-platforms"></a>Las versiones y plataformas

El **microsoftml** módulo se basa en Python 3.5 y está disponible solo al instalar uno de los siguientes productos de Microsoft o descargas:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente de Python para un cliente de ciencia de datos](setup-python-client-tools-sql.md)

> [!NOTE]
> Versiones de lanzamiento de producto completo son sólo Windows, a partir de SQL Server 2017. Linux support para **microsoftml** es nuevo en [versión preliminar de SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependencias de paquetes

Los algoritmos en **microsoftml** dependen [revoscalepy](ref-py-revoscalepy.md) para:

+ Objetos de origen de datos. Consumen datos **microsoftml** las funciones se crean mediante **revoscalepy** funciones.
+ Informática (ejecución cambiante de la función a una instancia remota de SQL Server) remoto. El **revoscalepy** biblioteca proporciona funciones para crear y activar un control remoto de proceso de contexto para SQL server.

En la mayoría de los casos, cargará los paquetes entre sí cuando se usen **microsoftml**.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumera las funciones por categoría para darle una idea de cómo se usa cada uno de ellos. También puede usar el [tabla de contenido](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para buscar las funciones en orden alfabético.

## <a name="1-training-functions"></a>Funciones de aprendizaje de 1

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Entrenar un conjunto de modelos. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Bosque aleatorio. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modelo lineal. con el ascenso estocástico de coordenadas Dual. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Árboles impulsados. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regresión logística. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Red neuronal. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Detección de anomalías. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>Funciones de transformación de 2

### <a name="categorical-variable-handling"></a>Control de variables de categorías

| Función | Descripción |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Convierte una columna de texto en categorías. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Aplica un algoritmo hash y convierte una columna de texto en categorías. |

### <a name="schema-manipulation"></a>Manipulación de esquema

| Función | Descripción |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena varias columnas en un vector único. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Quita las columnas de un conjunto de datos. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Conserva las columnas de un conjunto de datos. |


### <a name="variable-selection"></a>Selección de variables

| Función | Descripción |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Selección de características según los recuentos. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Selección de características según la información mutua. |


### <a name="text-analytics"></a>Análisis de texto

| Función | Descripción |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Convierte columnas de texto en características numéricas. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Análisis de opiniones. |


### <a name="image-analytics"></a>Análisis de imágenes 

| Función | Descripción |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carga una imagen. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Cambia el tamaño de una imagen. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Extrae los píxeles de una imagen. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Convierte una imagen en las características. |

### <a name="featurization-functions"></a>Funciones de características

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Transformación de datos para orígenes de datos |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>Funciones de puntuación de 3

| Función | Descripción |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Puntuaciones mediante un modelo de aprendizaje automático de Microsoft |

## <a name="how-to-call-microsoftml"></a>Cómo llamar a microsoftml

Las funciones de **microsoftml** son invocables en código de Python encapsulada en procedimientos almacenados. La mayoría de los desarrolladores crear **microsoftml** soluciones localmente, y, a continuación, migrar código de Python terminado a los procedimientos almacenados como un ejercicio de implementación.

El **microsoftml** para Python está instalado de forma predeterminada, pero, a diferencia del paquete **revoscalepy**, no se cargan de forma predeterminada al iniciar una sesión de Python mediante los archivos ejecutables de Python instalados con SQL Server.

Como primer paso, importar el **microsoftml** empaquetar e importar **revoscalepy** si debe usar contextos de cálculo remoto u objetos de origen de conectividad o los datos relacionados. A continuación, hacer referencia a las funciones individuales que necesita.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vea también

+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Insertar código de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referencia de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

