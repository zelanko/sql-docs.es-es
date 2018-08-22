---
title: Puntuación en tiempo real en el aprendizaje automático de SQL Server | Microsoft Docs
description: Generar predicciones con sp_rxPredict, puntuación de entradas de dta en un modelo previamente entrenado escritas en R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d5a3d0318f925918ef98ae18744e4287d6b81108
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "40394170"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Puntuación con sp_rxPredict en aprendizaje automático de SQL Server en tiempo real
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo puntuación en funciona casi en tiempo real para datos relacionales de SQL Server, mediante el aprendizaje automático modela escritas en R. 

> [!Note]
> Puntuación nativa es una implementación especial de puntuación en tiempo real que usa la función nativa de T-SQL para PREDECIR para puntuar muy rápido. Para obtener más información y la disponibilidad, consulte [puntuación nativa](sql-native-scoring.md).

## <a name="how-real-time-scoring-works"></a>En tiempo real cómo funciona la puntuación

Puntuación en tiempo real se admite en SQL Server 2017 y SQL Server 2016, en tipos de modelos concretos según las funciones de RevoScaleR o MicrosoftML como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) o [rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Usa las bibliotecas nativas de C++ para generar puntuaciones, basadas en la entrada de usuario proporcionado a un modelo almacenado en un formato binario especial de aprendizaje automático.

Dado que puede usar un modelo entrenado para puntuar sin tener que llamar en tiempo de ejecución de un lenguaje externo, se reduce la sobrecarga de varios procesos. Esto es compatible con un rendimiento de predicción mucho más rápido para escenarios de puntuación de producción. Dado que los datos nunca abandonan el SQL Server, se pueden generar resultados e inserta una nueva tabla sin sufrir ninguna traducción de datos entre R y SQL.

Puntuación en tiempo real es un proceso de varios pasos:

1. El procedimiento almacenado que realiza la puntuación debe estar habilitado en bases de datos.
2. Cargar el modelo previamente entrenado en formato binario.
3. Proporcionar nuevos datos de entrada, las filas tabulares o únicas, como entrada para el modelo.
4. Para generar puntuaciones, llame al procedimiento almacenado de sp_rxPredict.

## <a name="get-started"></a>Introducción

Para obtener ejemplos de código e instrucciones, consulte [cómo realizar la puntuación nativa o puntuación en tiempo real](r/how-to-do-realtime-scoring.md).

Para obtener un ejemplo de cómo se puede usar rxPredict para la puntuación, vea [End final préstamos incobrables predicción creado utilizando Azure HDInsight clústeres de Spark y R Services de SQL Server 2016](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> Si está trabajando exclusivamente en el código de R, también puede usar el [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) función para la puntuación rápida.

## <a name="requirements"></a>Requisitos

Puntuación en tiempo real es compatible con estas plataformas:

+ SQL Server 2017 Machine Learning Services
+ SQL Server R Services 2016, con una actualización de componentes de R a 9.1.0 o posterior

En SQL Server, debe habilitar la característica de puntuación en tiempo real de antemano agregar las bibliotecas de CLR para SQL Server.

Para obtener información sobre la puntuación en tiempo real en un entorno distribuido basado en Microsoft R Server, consulte el [publishService](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice) disponibles en función del [paquete mrsDeploy](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package), que es compatible con publicación de modelos para puntuar en tiempo real como un nuevo un servicio web que se ejecutan en el servidor de R.

### <a name="restrictions"></a>Restrictions

+ Se debe entrenar el modelo de antemano con una de las **rx** algoritmos. Para obtener más información, consulte [admite algoritmos](#bkmk_rt_supported_algos). Puntuación en tiempo real con `sp_rxPredict` admite algoritmos RevoScaleR y MicrosoftML.

+ El modelo debe guardarse con las nuevas funciones de serialización: [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R, y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

+ Puntuación en tiempo real no utiliza un intérprete; por lo tanto, no se admite ninguna funcionalidad que puede requerir un intérprete durante el paso de puntuación.  Entre ellas se incluyen:

  + Los modelos utilizando la `rxGlm` o `rxNaiveBayes` actualmente no se admiten los algoritmos

  + Modelos de RevoScaleR que usan una función de transformación de R o una fórmula que contenga una transformación, tales como <code>A ~ log(B)</code> no se admiten para determinar la puntuación en tiempo real. Para usar un modelo de este tipo, se recomienda realizar la transformación en el que los datos de entrada antes de pasar los datos para puntuar en tiempo real.

+ Puntuación en tiempo real está optimizado actualmente para las predicciones rápidas en conjuntos de datos más pequeños, que abarcan desde unas pocas filas hasta cientos de miles de filas. En grandes conjuntos de datos, mediante [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) puede ser más rápido.

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-real-time-scoring"></a><a name="bkmk_rt_supported_algos">Algoritmos que admiten la puntuación en tiempo real

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Marcan de modelos con \* también admiten la puntuación nativa con la función PREDICT.

+ Modelos de MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ Transformaciones proporcionadas por MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorías](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelo no admitido

Puntuación en tiempo real no se admite para las transformaciones de R que no sean los explícitamente de la lista en la sección anterior. 

Para los desarrolladores acostumbrados a trabajar con RevoScaleR y otras bibliotecas específicas de Microsoft R, incluyen funciones no admitidas `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR, los modelos PMML y otros modelos creados mediante otras bibliotecas de R desde CRAN o otros repositorios.

### <a name="known-issues"></a>Problemas conocidos

+ `sp_rxPredict` Devuelve un mensaje incorrecto cuando se pasa un valor NULL como el modelo: "System.Data.SqlTypes.SqlNullValueException:Data en Null".

## <a name="next-steps"></a>Pasos siguientes

[Cómo realizar la puntuación en tiempo real](r/how-to-do-realtime-scoring.md)
