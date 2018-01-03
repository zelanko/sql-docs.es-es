---
title: "Puntuación nativo | Documentos de Microsoft"
ms.custom: 
ms.date: 09/19/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 9fdd033a2e3ad05e06acb64ad38587782153a7c0
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="native-scoring"></a>Nativo de puntuación

Este tema describe las características de SQL Server 2017 que proporcionan la puntuación en modelos de aprendizaje automático en casi en tiempo real.

+ ¿Qué es nativo puntuación frente a la puntuación en tiempo real
+ Funcionamiento
+ Requisitos y plataformas admitidas

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>¿Qué es la puntuación nativo y cómo se diferencia de puntuación en tiempo real?

En SQL Server 2016, Microsoft ha creado un marco de extensibilidad que permite a los scripts de R se ejecuten desde el código T-SQL. Este marco de trabajo admite cualquier operación que puede realizar en R, comprendido entre funciones sencillas y modelos de aprendizaje de automático complejas de entrenamiento. Sin embargo, la arquitectura de doble proceso requiere invocar un proceso de R externo para cada llamada, independientemente de la complejidad de la operación. Si va a cargar un modelo previamente entrenado de una tabla y de puntuación en el mismo en datos ya incluidos en SQL Server, la sobrecarga de llamar al proceso de R externo representa un costo de rendimiento innecesarios.

_Puntuación_ es un proceso de dos pasos. En primer lugar, especifique un modelo previamente entrenado para cargar desde una tabla. En segundo lugar, pase nuevos datos de entrada en la función, para generar valores de predicción (o _puntuaciones_). La entrada puede ser tabulares o solo filas. Puede elegir como resultado un valor de columna única que representa una probabilidad, o pueden generar varios valores, como un intervalo de confianza, error u otro complemento útil para la predicción.

Cuando la entrada incluye muchas filas de datos, normalmente es más rápido insertar los valores de predicción en una tabla como parte del proceso de puntuación.  Generar una puntuación única es más habitual en un escenario donde obtener valores de entrada de una solicitud de formulario o de usuario y devolver la puntuación a una aplicación cliente. Para mejorar el rendimiento al generar puntuaciones sucesivas, SQL Server puede almacenar en caché el modelo para que se puede volver a cargar en la memoria.

Para admitir la puntuación rápido, servicios de aprendizaje de máquina de SQL Server (y el servidor de aprendizaje de máquina de Microsoft) proporcionan las bibliotecas de puntuación integradas que funcionan en R o en T-SQL. Hay diferentes opciones dependiendo de qué versión tiene.

**Puntuación nativa**

+ La función de PREDICCIÓN en Transact-SQL admite _puntuación nativo_ en cualquier instancia de SQL Server 2017. Solo requiere que haya un modelo ya está entrenado, que puede llamar mediante T-SQL. Puntuación nativo con código T-SQL presenta las siguientes ventajas:

    + No se requiere ninguna configuración adicional.
    + No se llama al runtime de R. No es necesario para instalar R.

**En tiempo real de puntuación**

+ **sp_rxPredict** es un procedimiento almacenado para en tiempo real de puntuación que se puede usar para generar puntuaciones de cualquier tipo de modelo admitidos, sin llamar al runtime de R.

  Este procedimiento almacenado también está disponible en SQL Server 2016, si actualiza los componentes de R mediante el instalador independiente de Microsoft R Server. sp_rxPredict también se admite en SQL Server 2017. Por lo tanto, puede usar esta función al generar puntuaciones con un tipo de modelo no admitido por la función de PREDICCIÓN.

+ La función rxPredict puede usarse para puntuar rápido dentro del código de R.

Para todos estos métodos de puntuación, debe usar un modelo que se entrenó con uno de los algoritmos admitidos RevoScaleR o MicrosoftML.

Para obtener un ejemplo de en tiempo real de puntuación en acción, vea [final al final préstamo ChargeOff predicción creado utilizando Azure HDInsight Spark clústeres y el servicio de R de SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Modo nativo funciona de puntuación

Puntuación nativo usa las bibliotecas de C++ nativas de Microsoft que puede leer el modelo desde un formato binario especial y para generar puntuaciones. Dado que un modelo se pueden publicar y usar para puntuar sin tener que llamar el intérprete de R, se reduce la sobrecarga de las interacciones de procesos múltiples. Por lo tanto, la puntuación nativo admite un rendimiento mucho más rápido predicción en escenarios de producción de la empresa.

Para generar puntuaciones mediante esta biblioteca, llame a la función de puntuación y pasar las entradas necesarias siguientes:

+ Un modelo compatible. Consulte la [requisitos](#Requirements) sección para obtener más información.
+ Datos de entrada, que normalmente se define como una consulta SQL

La función devuelve las predicciones para los datos de entrada, junto con las columnas de datos de origen que se van a pasar a través de.

Para obtener ejemplos de código, así como instrucciones sobre cómo preparar los modelos en el formato binario requerido, consulte este artículo:

+ [Cómo realizar la puntuación en tiempo real](r/how-to-do-realtime-scoring.md)

Para una solución completa que incluye la puntuación nativo, vea estos ejemplos desde el equipo de desarrollo de SQL Server:

+ Implementar la secuencia de comandos de aprendizaje automático: [con un modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implementar la secuencia de comandos de aprendizaje automático: [mediante un modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>Requisitos

Plataformas admitidas son los siguientes:

+ SQL Server de 2017 Machine Learning Services (incluye Microsoft R Server 9.1.0)
    
    Puntuación nativo utilizando PREDICT requiere SQL Server 2017.
    Funciona en cualquier versión de SQL Server de 2017, incluidos Linux.

    También puede realizar en tiempo real de puntuación mediante sp_rxPredict. Para utilizar este procedimiento almacenado requiere que se habilite [integración CLR de SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ SQL Server 2016

   En tiempo real utilizando sp_rxPredict la puntuación es posible con SQL Server 2016 y también se puede ejecutar en Microsoft R Server. Esta opción requiere SQLCLR esté habilitado y que se instala la actualización de Microsoft R Server.
   Para obtener más información, vea [en tiempo real de puntuación](Real-time-scoring.md)

### <a name="model-preparation"></a>Preparación de modelo

+ Debe entrenar el modelo de antemano con uno de los admitidos **rx** algoritmos. Para obtener más información, consulte [admite algoritmos](#bkmk_native_supported_algos).
+ El modelo debe guardarse con la nueva función de serialización que se proporcionan en Microsoft R Server 9.1.0. La función de serialización está optimizada para admitir la puntuación rápida.

### <a name="bkmk_native_supported_algos"></a>Algoritmos que admiten la puntuación nativo

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Si necesita usar modelos de MicrosoftML, use en tiempo real con sp_rxPredict de puntuación.

### <a name="restrictions"></a>Restrictions

No se admiten los siguientes tipos de modelo:

+ Modelos que contienen otros tipos de transformaciones de R no compatibles
+ Modelos mediante el `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR
+ Modelos PMML
+ Modelos creados mediante otras bibliotecas de R de CRAN u otros repositorios
+ Modelos que contienen cualquier otra transformación de R
