---
title: Usar el paquete MicrosoftML con SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a75ed22e46576c701e281f495d5bc123ca489526
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348466"
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>Usar el paquete MicrosoftML con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El [ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) paquete que se proporciona con Microsoft R Server y SQL Server 2017 incluye varios algoritmos de aprendizaje automático. Estas API se han desarrollado por Microsoft para aplicaciones de aprendizaje de automático interno y se han perfeccionado en los años para admitir de alto rendimiento en macrodatos, con el procesamiento de varios núcleos y la transmisión de datos rápida. MicrosoftML incluye también numerosas transformaciones para el procesamiento de imagen y texto.

En SQL Server 2017, se agregó compatibilidad para el lenguaje Python. El **microsoftml** del paquete de Python contiene funciones equivalentes a las que en el paquete MicrosoftML para R. 

+ **MicrosoftML para R**

    Referencia de paquete e Introducción: [MicrosoftML: machine algoritmos de aprendizaje de R](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    Porque R distingue entre mayúsculas y minúsculas, asegúrese de que hace referencia al nombre correctamente al cargar el paquete.

+ **microsoftml para Python**

    Referencia de paquete e Introducción: [microsoftml (biblioteca de funciones para Python)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package). 

## <a name="whats-in-microsoftml"></a>¿Qué es en MicrosoftML

MicrosoftML contiene una variedad de transformaciones que se han optimizado para rendimiento y los algoritmos de aprendizaje automático.

### <a name="machine-learning-algorithms"></a>Algoritmos de aprendizaje automático

-  Los modelos lineales: `rxFastLinear` aprendiz lineal según estocástico ascenso dual de coordenadas que puede usarse para clasificación binaria o de regresión. El modelo admite regularización L1 y L2.

- Modelos de bosque de decisión y de árbol de decisión: `rxFastTree` es un algoritmo de árbol de decisión incrementado originalmente conocido como FastRank que se desarrolló para su uso en Bing. Es uno de los aprendices más rápidos y populares. Admite la regresión y la clasificación binarias.

  `rxFastForest` es un modelo de regresión logística se basa en el método de bosque aleatorio. Es similar a la función `rxLogit` de RevoScaleR, aunque admite la regularización L1 y L2. Admite la regresión y la clasificación binarias.

- Regresión logística: `rxLogisticRegression` es similar a un modelo de regresión logística el `rxLogit` función de RevoScaleR, con compatibilidad adicional para la regularización L1 y L2. Admite la clasificación multiclase o binaria.

- Las redes neuronales: el `rxNeuralNet` admite la función de clasificación binaria, clasificación multiclase y regresión con redes neuronales. Redes intrincadas personalizables y admite la aceleración de GPU, con una sola GPU.

- Detección de anomalías.  El `rxOneClassSvm` función se basa en el método SVM pero está optimizada para la clasificación binaria en conjuntos de datos desequilibrados.

### <a name="transformation-functions"></a>Funciones de transformación

MicrosoftML incluye numerosas funciones especializadas que son útiles para transformar los datos y extraer características.

- Las capacidades de procesamiento de texto incluyen el `featurizeText` y `getSentiment` funciones. Puede contar los n-gramas, detectar el idioma empleado o realizar la normalización de texto. También puede realizar la limpieza de operaciones como la eliminación de palabras irrelevantes de texto comunes o generar características con hash o basada en recuento de texto.

- Selección de características y funciones de transformación, la característica como `selectFeatures` o `getSentiment`, analizar datos y crear las características que son más útiles para el modelado.

- Trabajar con variables de categorías mediante como `categorical` o `categoricalHash`, que convertir los valores de categorías en las matrices indizadas para mejorar el rendimiento.

- Las funciones específicas de procesamiento de imágenes y análisis, como `extractPixels` o `featurizeImage`, permiten obtener más información acerca de las imágenes y las imágenes se procesan más rápido.

Para más información, vea [MicrosoftML functions](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml) (Funciones de MicrosoftML).

## <a name="how-to-use-microsoftml"></a>Cómo usar MicrosoftML

En esta sección se describe cómo buscar y cargar el paquete en el código de R y Python.

+ El paquete MicrosoftML para R se instala de forma predeterminada con Microsoft R Server 9.1.0 y en SQL Server 2017.

    También está disponible para su uso con SQL Server 2016, si actualiza los componentes de R para la instancia, mediante el instalador de Microsoft R Server como se describe aquí: [actualizar una instancia de SQL Server mediante el enlace](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ El **microsoftml** del paquete de Python se instala de forma predeterminada con SQL Server 2017 

   Para usar este paquete, se recomienda que actualice a Release Candidate 2 o posterior. Se lanzó una versión temprana con RC1, pero la biblioteca ha sometido a revisiones considerable, incluidos los cambios en los nombres de función. 

Sin embargo, R y Python, el paquete no está cargado de forma predeterminada; por lo tanto, debe cargar explícitamente el paquete como parte de su código para utilizar sus funciones.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>Llamar a funciones de MicrosoftML desde R en SQL Server

En el código de R, cargar el paquete MicrosoftML y llame a sus funciones, al igual que cualquier otro paquete.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**Notas**

+ El paquete MicrosoftML está totalmente integrado con la canalización de procesamiento de datos proporcionada por el paquete RevoScaleR. Por lo tanto, puede usar el paquete MicrosoftML en cualquier contexto de proceso basados en Windows, incluida una instancia de SQL Server que tiene habilitadas las extensiones de aprendizaje de máquina.

    Sin embargo, MicrosoftML requiere una referencia a RevoScaleR y sus funciones para poder usar remoto contextos de cálculo.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>Llamar a funciones de microsoftml desde Python en SQL Server

Para llamar a funciones del paquete, en el código de Python, importar el **microsoftml** empaquetar e importar **revoscalepy** si necesita usar contextos de cálculo remoto o relacionado conectividad u origen de datos objetos. A continuación, hacer referencia a las funciones individuales que necesita.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Notas**

+ En SQL Server 2017, **microsoftml** es un módulo Python35 compatible. 

+ Las funciones de **microsoftml** se integran con los orígenes de datos y contextos de proceso que son compatibles con **revoscalepy**. Por lo tanto, puede usar el **microsoftml** paquete de Python para crear y puntuación de modelos en cualquier contexto de proceso basados en Windows, incluida una instancia de SQL Server que tiene extensiones de machine learning. habilitada.

    Sin embargo, **microsoftml** para Python requiere una referencia a **revoscalepy** y contextos de cálculo de sus funciones para poder usar remoto.

Para obtener más información acerca de revoscalepy, consulte:

+ [¿Qué es revoscalepy](python/what-is-revoscalepy.md)

+ [biblioteca de revoscalepy (función)](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
