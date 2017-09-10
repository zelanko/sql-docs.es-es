---
title: "Puntuación nativo | Documentos de Microsoft"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1cb06223e5274c1fa439eb9f7d82a005e93a47d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="native-scoring"></a>Nativo de puntuación

Este tema describe las características de SQL Server 2017 que proporcionan la puntuación en modelos de aprendizaje automático en casi en tiempo real.

+ ¿Qué es nativo puntuación frente a la puntuación en tiempo real
+ Funcionamiento
+ Requisitos y plataformas admitidas

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>¿Qué es la puntuación nativo y cómo se diferencia de puntuación en tiempo real?

En SQL Server 2016, Microsoft ha creado un marco de extensibilidad que permite a los scripts de R se ejecuten desde el código T-SQL. Este marco de trabajo admite cualquier operación que puede realizar en R, comprendido entre funciones sencillas y modelos de aprendizaje de automático complejas de entrenamiento. Sin embargo, la arquitectura de proceso de doble que empareja R con SQL Server significa que los procesos de R externos se deben invocar para cada llamada, independientemente de la complejidad de la operación. Si va a cargar un modelo previamente entrenado de una tabla y de puntuación en el mismo en datos ya incluidos en SQL Server, la sobrecarga de llamar al proceso de R externo representa un costo de rendimiento innecesarios.

_Puntuación_ es un proceso de dos pasos: un modelo previamente entrenado se carga desde una tabla, y nuevos datos de entrada, filas tabulares o únicos, se pasan al modelo, que genera valores nuevos (o _puntuaciones_). El resultado puede ser un valor de columna única que representa una probabilidad o varios valores, como un intervalo de confianza, error u otro complemento útil para la predicción.

Cuando realice la puntuación de varias filas de datos, los nuevos valores se insertan normalmente en una tabla como parte del procedimiento de puntuación.  Sin embargo, también puede recuperar una puntuación solo en tiempo real. Cuando realice la puntuación de entradas sucesivas, el modelo podría almacenará en caché para que se puede volver a cargar en memoria rápida.

Para admitir la puntuación rápido, servicios de aprendizaje de máquina de SQL Server (y el servidor de aprendizaje de máquina de Microsoft) proporcionan las bibliotecas de puntuación integradas que funcionan en R o en T-SQL. Hay diferentes opciones dependiendo de qué versión tiene.

**Nativo de puntuación**

+ La función de PREDICCIÓN en Transact-SQL puede utilizarse para _puntuación nativo_ desde cualquier instancia de SQL Server 2017. Solo requiere que haya un modelo ya ha entrenado y guardado en una tabla o se puede llamar a través de T-SQL. Es un tipo de puntuación en tiempo real que utiliza las funciones nativas de T-SQL; no requerida ninguna configuración adicional.

   El runtime de R no se llama y no deben instalarse.

**En tiempo real de puntuación**

+ **sp_rxPredict** es un procedimiento almacenado para en tiempo real de puntuación que se puede usar para generar puntuaciones de cualquier tipo de modelo admitidos, sin llamar al runtime de R.

  Esta opción para usar en tiempo real de puntuación también está disponible en SQL Server 2016, si actualiza los componentes de R mediante el instalador independiente de Microsoft R Server. sp_rxPredict también se admite en SQL Server 2017 y puede ser una buena opción si está puntuando en un tipo de modelo no admitido por la función de PREDICCIÓN.

+ La función rxPredict puede usarse para puntuar rápido dentro del código de R.

Para todos estos métodos de puntuación, debe usar un modelo que se entrenó con uno de los algoritmos admitidos RevoScaleR o MicrosoftML.

Para obtener un ejemplo de en tiempo real de puntuación en acción, vea [final al final préstamo ChargeOff predicción creado utilizando Azure HDInsight Spark clústeres y el servicio de R de SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Modo nativo funciona de puntuación

Puntuación nativo usa las bibliotecas de C++ nativas de Microsoft que puede leer el modelo desde un formato binario especial y para generar puntuaciones. Dado que un modelo se pueden publicar y usar para puntuar sin tener que llamar el intérprete de R, se reduce la sobrecarga de las interacciones de procesos múltiples. Esto es compatible con un rendimiento mucho más rápido predicción en escenarios de producción de la empresa.

Para generar puntuaciones mediante esta biblioteca, llame a la función de puntuación y pasar las entradas necesarias siguientes:

+ Un modelo compatible. Consulte la [requisitos](#Requirements) sección para obtener más información.
+ Datos de entrada, que normalmente se define como una consulta SQL

La función devuelve las predicciones para los datos de entrada, junto con las columnas de datos de origen que se van a pasar a través de.

Para obtener ejemplos de código, así como instrucciones sobre cómo preparar los modelos en el formato binario requerido, consulte este artículo:

+ [Cómo realizar la puntuación en tiempo real](r/how-to-do-realtime-scoring.md)

## <a name="requirements"></a>Requisitos

Plataformas admitidas son los siguientes:

+ SQL Server de 2017 Machine Learning Services (incluye Microsoft R Server 9.1.0)
    
    Puntuación nativo utilizando PREDICT requiere SQL Server 2017.
    Funciona en cualquier versión de SQL Server de 2017, incluidos Linux.

    También puede realizar en tiempo real de puntuación mediante sp_rxPredict, lo que requiere que esté habilitado el CLR de SQL.

+ SQL Server 2016

   En tiempo real con la puntuación sp_rxPredict es posible con SQL Server 2016 y también se puede ejecutar en Microsoft R Server. Esta opción requiere SQLCLR esté habilitado y que se instala la actualización de Microsoft R Server.
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
  + [rxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Si necesita usar modelos de MicrosoftML, use en tiempo real con sp_rxPredict de puntuación.

### <a name="restrictions"></a>Restricciones

No se admiten los siguientes tipos de modelo:

+ Modelos que contienen otros tipos de transformaciones de R no compatibles
+ Modelos mediante el `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR
+ Modelos PMML
+ Modelos creados mediante otras bibliotecas de R de CRAN u otros repositorios
+ Modelos que contienen cualquier otro tipo de transformación de R

