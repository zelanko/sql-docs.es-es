---
title: Puntuación nativa en el aprendizaje automático de SQL Server | Microsoft Docs
description: Generar predicciones mediante la función T-SQL PREDECIR, puntuación de entradas de dta en un modelo previamente entrenado escritas en R o Python en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf8f9a6362b72efddccbf5c2b0e54096c6e86aa7
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "40392672"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Puntuación nativa mediante la función de PREDICCIÓN de Transact-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Una vez que un modelo previamente entrenado, puede pasar nuevos datos de entrada a la función para generar valores de predicción o *puntuaciones*. En SQL Server 2017 Windows o Linux, o en Azure SQL Database, puede usar la función PREDICT de Transact-SQL para admitir la puntuación nativa. Sólo requiere que tienen un modelo ya entrenado, que puede llamar mediante T-SQL. 

+ What ' s nativa frente a la puntuación en tiempo real de puntuación
+ Funcionamiento
+ Requisitos y plataformas admitidas

## <a name="what-is-native-scoring-and-how-is-it-different-from-real-time-scoring"></a>¿Qué es la puntuación nativa y cómo se diferencia de puntuación en tiempo real?

En SQL Server 2016, Microsoft creó un marco de extensibilidad que permite que los scripts de R que se ejecutará desde T-SQL. Este marco de trabajo admite cualquier operación que podría realizar en R, comprendido entre funciones sencillas y entrenamiento complejos modelos de machine learning. Sin embargo, la arquitectura de doble proceso requiere invocar un proceso de R externo para cada llamada, independientemente de la complejidad de la operación. Si va a cargar un modelo previamente entrenado de una tabla y de puntuación en el mismo en los datos ya incluidos en SQL Server, la sobrecarga que supone el proceso de R externo de llamada representa un costo de rendimiento innecesaria.

_Puntuación_ es un proceso en dos pasos. En primer lugar, especifique un modelo previamente entrenado para cargar desde una tabla. En segundo lugar, pase nuevos datos de entrada en la función para generar valores de predicción (o _puntuaciones_). La entrada puede ser tabulares o solo las filas. Puede elegir como resultado un valor de columna única que representa una probabilidad, o pueden generar varios valores, como un intervalo de confianza, error u otro complemento útil para la predicción.

Cuando la entrada incluye muchas filas de datos, es normalmente más rápido insertar los valores de predicción en una tabla como parte del proceso de puntuación.  Generar una puntuación única es más habitual en un escenario donde obtener los valores de entrada de una solicitud de formulario o de usuario y devolver la puntuación a una aplicación cliente. Para mejorar el rendimiento al generar puntuaciones sucesivas, SQL Server puede almacenar en caché el modelo para que se puede volver a cargar en la memoria.

Para admitir la puntuación rápido, SQL Server Machine Learning Services (y Microsoft Machine Learning Server) proporcionan bibliotecas de puntuación integradas que trabajan en R o en T-SQL. Existen diferentes opciones dependiendo de qué versión tiene.

**Puntuación nativa**

+ La función PREDICT de Transact-SQL admite _puntuación nativa_ en cualquier instancia de SQL Server 2017. Sólo requiere que tienen un modelo ya entrenado, que puede llamar mediante T-SQL. Puntuación nativa con Transact-SQL tiene las siguientes ventajas:

    + No se requiere ninguna configuración adicional.
    + No se llama al runtime de R. No es necesario para instalar R.

**Puntuación en tiempo real**

+ **sp_rxPredict** es un procedimiento almacenado para puntuar en tiempo real que se puede usar para genera las puntuaciones de cualquier tipo de modelo admitidos, sin llamar al runtime de R.

  Este procedimiento almacenado también está disponible en SQL Server 2016, si actualiza los componentes de R mediante el instalador independiente de Microsoft R Server. sp_rxPredict también se admite en SQL Server 2017. Por lo tanto, puede usar esta función al generar las puntuaciones con un tipo de modelo no admitido por la función PREDICT.

+ Puede usar la función rxPredict para puntuar rápida dentro del código de R.

Para todos estos métodos de puntuación, debe usar un modelo que se ha entrenado mediante uno de los algoritmos RevoScaleR o MicrosoftML admitidos.

Para obtener un ejemplo de puntuación en tiempo real en acción, consulte [End final préstamos incobrables predicción creado utilizando Azure HDInsight clústeres de Spark y R Services de SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Nativo cómo funciona la puntuación

Puntuación nativa usa las bibliotecas nativas de C++ de Microsoft que puede leer el modelo desde un formato binario especial y generar puntuaciones. Debido a un modelo se puede publicar y usar para puntuar sin tener que llamar el intérprete de R, se reduce la sobrecarga de las interacciones de varios procesos. Por lo tanto, puntuación nativa es compatible con un rendimiento de predicción mucho más rápido en escenarios de producción corporativo.

Para generar puntuaciones mediante esta biblioteca, llame a la función de puntuación y pasar las entradas necesarias siguientes:

+ Un modelo compatible. Consulte la [requisitos](#Requirements) sección para obtener más información.
+ Datos de entrada, que normalmente se define como una consulta SQL

La función devuelve las predicciones para los datos de entrada, junto con las columnas de datos de origen que se van a pasar a través.

Para obtener ejemplos de código, así como instrucciones sobre cómo preparar los modelos en el formato binario necesario, consulte este artículo:

+ [Cómo realizar la puntuación en tiempo real](r/how-to-do-realtime-scoring.md)

Para una solución completa que incluye la puntuación nativa, vea estos ejemplos desde el equipo de desarrollo de SQL Server:

+ Implementar la secuencia de comandos de ML: [mediante un modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implementar la secuencia de comandos de ML: [mediante un modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>Requisitos

Las plataformas admitidas son como sigue:

+ SQL Server 2017 Machine Learning Services (incluye Microsoft R Server 9.1.0)
    
    Puntuación nativa mediante PREDICT requiere SQL Server 2017.
    Funciona en cualquier versión de SQL Server 2017, incluido Linux.

    También puede realizar sp_rxPredict de puntuación en tiempo real. Para utilizar este procedimiento almacenado requiere que habilite [integración CLR de SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ SQL Server 2016

   En tiempo real de puntuación mediante sp_rxPredict es posible con SQL Server 2016 y también se puede ejecutar en Microsoft R Server. Esta opción requiere SQLCLR esté habilitado y que instale la actualización a Microsoft R Server.
   Para obtener más información, consulte [de puntuación en tiempo real](Real-time-scoring.md)

### <a name="model-preparation"></a>Preparación del modelo

+ Se debe entrenar el modelo de antemano con una de las **rx** algoritmos. Para obtener más información, consulte [admite algoritmos](#bkmk_native_supported_algos).
+ El modelo debe guardarse con la nueva función de serialización proporcionada en Microsoft R Server 9.1.0. La función de serialización está optimizada para admitir la puntuación rápida.

### <a name="bkmk_native_supported_algos"></a> Algoritmos que admiten la puntuación nativa

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Si necesita usar modelos de MicrosoftML, utilice la puntuación en tiempo real con sp_rxPredict.

### <a name="restrictions"></a>Restrictions

No se admiten los siguientes tipos de modelo:

+ Modelos que contienen otros tipos de transformaciones de R no admitidos
+ Los modelos utilizando la `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR
+ Modelos PMML
+ Modelos creados mediante otras bibliotecas de R de CRAN u otros repositorios
+ Modelos que contienen cualquier otra transformación de R

## <a name="see-also"></a>Vea también

[Puntuación en el aprendizaje automático de SQL Server en tiempo real ](real-time-scoring.md)