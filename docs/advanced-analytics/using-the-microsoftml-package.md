---
title: Usar el paquete de MicrosoftML con SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4f94d2eaaaa9fc70014e5d333dede4919ca198f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>Usar el paquete de MicrosoftML con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El [ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) paquete que se proporciona con Microsoft R Server y SQL Server 2017 incluye varios algoritmos de aprendizaje de automático. Estas API desarrolladas por Microsoft para las aplicaciones de aprendizaje de automático interno y se han perfeccionado en los años para admitir el alto rendimiento de grandes cantidades de datos, mediante la transmisión por secuencias de datos rápidas y procesamiento de varios núcleos. MicrosoftML también incluye numerosas transformaciones de texto y procesamiento de imágenes.

En SQL Server de 2017 CTP 2.0, se agregó compatibilidad para el lenguaje de Python. El **microsoftml** del paquete de Python contiene funciones equivalentes a las del paquete MicrosoftML para R. 

+ **MicrosoftML para R**

    Referencia de introducción y paquete: [MicrosoftML: máquina algoritmos de aprendizaje R](https://docs.microsoft.com/en-us/r-server/r-reference/microsoftml/microsoftml-package)

    Dado que R distingue mayúsculas de minúsculas, asegúrese de que hace referencia al nombre correctamente al cargar el paquete.

+ **Microsoftml para Python**

    Referencia de introducción y paquete: [microsoftml (biblioteca de funciones para Python)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package). 

## <a name="whats-in-microsoftml"></a>¿Qué es MicrosoftML

MicrosoftML contiene una variedad de algoritmos y las transformaciones que se han optimizado para el rendimiento de aprendizaje automático.

### <a name="machine-learning-algorithms"></a>Algoritmos de aprendizaje automático

-  Modelos lineales: `rxFastLinear` es un aprendiz lineal según estocástico ascenso coordenada dual que puede usarse para clasificación binaria o de regresión. El modelo admite regularización L1 y L2.

- Modelos de bosque de decisión y de árbol de decisión: `rxFastTree` es un algoritmo de árbol de decisión impulsado originalmente denominado FastRank, que se desarrolló para su uso en Bing. Es uno de los aprendices más rápidos y populares. Admite la regresión y la clasificación binarias.

  `rxFastForest` es un modelo de regresión logística se basa en el método de bosque aleatorio. Es similar a la función `rxLogit` de RevoScaleR, aunque admite la regularización L1 y L2. Admite la regresión y la clasificación binarias.

- Regresión logística: `rxLogisticRegression` es similar a un modelo de regresión logística el `rxLogit` función en RevoScaleR, con compatibilidad adicional para la regularización L1 y L2. Es compatible con la clasificación binaria o multiclase.

- Redes neurales: el `rxNeuralNet` función admite clasificación binaria, la clasificación multiclase y regresión con redes neurales. Personalizables y es compatible con redes complicadas con aceleración de la GPU, el uso de una GPU única.

- Detección de anomalías.  El `rxOneClassSvm` función se basa en el método SVM pero está optimizada para clasificación binaria en conjuntos de datos no está equilibradas.

### <a name="transformation-functions"></a>Funciones de transformación

MicrosoftML incluye numerosas funciones especializadas que son útiles para transformar los datos y extraer características.

- Las capacidades de procesamiento de texto incluyen el `featurizeText` y `getSentiment` funciones. Puede contar n gramos, detectar el idioma usado o realizar la normalización de texto. También puede realizar la limpieza de operaciones como la eliminación de palabras irrelevantes de texto comunes, o generar características con hash o basadas en recuento de texto.

- Selección de características y funciones de transformación, de características como `selectFeatures` o `getSentiment`, analizar los datos y crear características que son muy útiles para el modelado.

- Trabajar con variables de categorías mediante como `categorical` o `categoricalHash`, que convertir los valores de categorías en las matrices indizadas para mejorar el rendimiento.

- Las funciones específicas de procesamiento de imágenes y análisis, como `extractPixels` o `featurizeImage`, permiten obtener más información acerca de las imágenes y procesan las imágenes con mayor rapidez.

Para más información, vea [MicrosoftML functions](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml) (Funciones de MicrosoftML).

## <a name="how-to-use-microsoftml"></a>Cómo usar MicrosoftML

En esta sección se describe cómo buscar y cargar el paquete en el código de R y Python.

+ El paquete MicrosoftML para R está instalado de forma predeterminada a Microsoft R Server 9.1.0 y en SQL Server 2017.

    También está disponible para su uso con SQL Server 2016, si actualiza los componentes de R para la instancia, con el instalador de Microsoft R Server tal como se describe aquí: [actualizar una instancia de SQL Server mediante el enlace](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ El **microsoftml** del paquete de Python se instala de forma predeterminada con SQL Server 2017 

   Para usar este paquete, se recomienda que actualice a Release Candidate 2 o posterior. Se lanzó una versión anterior con RC1, pero la biblioteca ha experimentado revisión considerable, incluidos los cambios en los nombres de función. 

Sin embargo, para R y Python, el paquete no está cargado de forma predeterminada; por lo tanto, debe cargar explícitamente el paquete como parte del código para utilizar sus funciones.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>Llamar a funciones de MicrosoftML de R en SQL Server

En el código de R, cargar el paquete de MicrosoftML y llamar a sus funciones, al igual que cualquier otro paquete.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**Notas**

+ El paquete MicrosoftML está totalmente integrado con la canalización de procesamiento de datos proporcionada por el paquete RevoScaleR. Por lo tanto, puede usar el paquete de MicrosoftML en cualquier contexto de proceso basadas en Windows, incluida una instancia de SQL Server que tiene habilitadas las extensiones de aprendizaje de máquina.

    Sin embargo, MicrosoftML requiere una referencia a RevoScaleR y sus funciones para poder usar remoto contextos de proceso.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>Llamar a funciones de microsoftml desde Python en SQL Server

Para llamar a funciones desde el paquete, en el código Python, importar la **microsoftml** empaquetar e importar **revoscalepy** si necesita usar contextos de proceso remoto o relacionado conectividad u origen de datos objetos. A continuación, hacer referencia a las funciones individuales que necesita.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Notas**

+ En SQL Server de 2017 **microsoftml** es un módulo Python35 compatible. 

+ Las funciones de **microsoftml** se integran con los orígenes de datos y contextos de proceso que son compatibles con **revoscalepy**. Por lo tanto, puede usar el **microsoftml** paquete de Python para crear y puntuación de modelos en cualquier contexto de proceso basadas en Windows, incluida una instancia de SQL Server que tiene extensiones de aprendizaje de máquina. habilitado.

    Sin embargo, **microsoftml** para Python requiere una referencia a **revoscalepy** y sus funciones para poder usar remoto contextos de proceso.

Para obtener más información sobre revoscalepy, consulte:

+ [¿Qué es revoscalepy](python/what-is-revoscalepy.md)

+ [biblioteca de funciones de revoscalepy](https://docs.microsoft.com/en-us/r-server/python-reference/revoscalepy/revoscalepy-package) 
