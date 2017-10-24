---
title: "En tiempo real de puntuación | Documentos de Microsoft"
ms.custom: 
ms.date: 07/17/2017
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4d15a7f605f130ff4f93c7da66ca9a103195c17
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="realtime-scoring"></a>En tiempo real de puntuación

Este tema describe una característica disponible en SQL Server 2016 y de 2017 SQL Server que admita la puntuación en modelos de aprendizaje automático en casi en tiempo real.

> [!TIP]
> Puntuación nativo es una implementación especial de en tiempo real de puntuación que usa la función nativa de T-SQL PREDECIR para puntuar muy rápido y solo está disponible en SQL Server 2017. Para obtener más información, consulte [puntuación Native](sql-native-scoring.md).

## <a name="how-realtime-scoring-works"></a>Cómo funciona la puntuación en tiempo real

En tiempo real de puntuación se admite en 2017 de SQL Server y SQL Server 2016, en los tipos de modelo específico creados mediante el uso de algoritmos de RevoScaleR o MicrosoftML Evaluate. Usa las bibliotecas de C++ nativo para generar puntuaciones, en función de la entrada de usuario proporcionada a un modelo que se almacenan en un formato binario especial de aprendizaje automático.

Debido a un modelo entrenado puede utilizarse para la puntuación sin tener que llamar a un tiempo de ejecución de idiomas externos, se reduce la sobrecarga de varios procesos. Esto es compatible con un rendimiento mucho más rápido predicción para escenarios de puntuación de producción. Dado que los datos nunca dejan SQL Server, puede generar resultados e inserta una nueva tabla sin sufrir ninguna traducción de datos entre R y SQL.

En tiempo real de puntuación es un proceso de varios pasos:

1. El procedimiento almacenado que realiza la puntuación debe habilitarse para cada base de datos.
2. Cargar el modelo previamente entrenado en formato binario.
3. Proporcionar nuevos datos de entrada, filas tabulares o únicos, como entrada para el modelo.
4. Para generar puntuaciones, llame al procedimiento almacenado de sp_rxPredict.

## <a name="get-started"></a>Introducción

Para obtener ejemplos de código e instrucciones, consulte [cómo realizar la puntuación nativo o en tiempo real de puntuación](r/how-to-do-realtime-scoring.md).

Para un ejemplo de cómo puede rxPredict usados para puntuar, consulte [final al final préstamo ChargeOff predicción creado utilizando Azure HDInsight Spark clústeres y el servicio de R de SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> Si está trabajando exclusivamente en el código de R, también puede usar el [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) función para puntuar rápida.

## <a name="requirements"></a>Requisitos

En tiempo real de puntuación es compatible con estas plataformas:

+ SQL Server de 2017 Machine Learning Services (incluye Microsoft R Server 9.1.0)
+ SQL Server R Services 2016, con una actualización de la instancia de R Services para Microsoft R Server 9.1.0 o posterior
+ Microsoft Machine Learning Server (independiente)

En SQL Server, debe habilitar la característica de puntuación de antemano de en tiempo real. Esto es porque la característica requiere la instalación de bibliotecas basados en CLR en SQL Server.

Para obtener información sobre en tiempo real de puntuación en un entorno distribuido que se basa en Microsoft R Server, consulte el [publishService](https://msdn.microsoft.com/microsoft-r/mrsdeploy/packagehelp/publishservice) función disponible en la [mrsDeploy paquete](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy), que es compatible con publicación de modelos en tiempo real un servicio web que se ejecuta en el servidor de R de puntuación como una nueva.

### <a name="restrictions"></a>Restricciones

+ Debe entrenar el modelo de antemano con uno de los admitidos **rx** algoritmos. Para obtener más información, consulte [admite algoritmos](#bkmk_rt_supported_algos). En tiempo real de puntuación con sp_rxPredict admite algoritmos de RevoScaleR y MicrosoftML.

+ El modelo debe guardarse con la nueva función de serialización que se proporcionan en Microsoft R Server 9.1.0. El método de serialización se ha optimizado para admitir la puntuación rápida.

+ En tiempo real de puntuación no se usa un intérprete de R; por lo tanto, no se admite ninguna funcionalidad que requiera el intérprete de R durante el paso de puntuación.  Entre ellas se incluyen:

  + Modelos mediante el `rxGlm` o `rxNaiveBayes` algoritmos no son compatibles actualmente

  + Modelos de RevoScaleR que utilizan una función de transformación de R o una fórmula que contenga una transformación, como <code>A ~ log(B)</code> no se admiten para determinar la puntuación en tiempo real. Para usar un modelo de este tipo, se recomienda que lleva a cabo la transformación en la que los datos de entrada antes de pasar los datos a la puntuación en tiempo real.

+ En tiempo real de puntuación actualmente está optimizada para las predicciones rápidas en conjuntos de datos más pequeños, comprendido entre unas cuantas filas a cientos de miles de filas. En conjuntos de datos muy grandes, la puntuación en R utilizando rxPredict puede ser más rápida.

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-realtime-scoring"></a><a name="bkmk_rt_supported_algos">Algoritmos que admiten la puntuación en tiempo real

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)\*
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)\*
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)\*
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)\*
  + [rxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)\*
  
  Los modelos se marcan con \* también son compatibles con la puntuación nativo con la función de PREDICCIÓN.

+ Modelos de MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfastlinear)

+ Transformaciones proporcionadas por MicrosoftML

  + [featurizeText](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/r-server/r-reference/microsoftml/concat)
  + [categorías](https://docs.microsoft.com/r-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/r-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/r-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelo no admitido

No se admiten los siguientes tipos de modelo:

+ Modelos que contienen otros tipos de transformaciones de R no compatibles
+ Modelos mediante el `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR
+ Modelos PMML
+ Modelos creados mediante otras bibliotecas de R de CRAN u otros repositorios
+ Modelos que contienen cualquier otro tipo de transformación de R distintos de los mencionados aquí

### <a name="known-issues"></a>Problemas conocidos

+ `sp_rxPredict`Devuelve un mensaje correcta cuando se pasa un valor NULL como el modelo: "System.Data.SqlTypes.SqlNullValueException:Data en Null".

## <a name="next-steps"></a>Pasos siguientes

[Cómo llevar a cabo en tiempo real de puntuación](r/how-to-do-realtime-scoring.md)

