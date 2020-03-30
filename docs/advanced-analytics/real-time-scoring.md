---
title: Puntuación en tiempo real con sp_rxPredict
description: Genere predicciones mediante sp_rxPredict y puntúe las entradas de datos en un modelo entrenado previamente escrito en R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/26/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 746a9cadfca28aae3bd2781a3daf71aabb8d6e5b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727327"
---
# <a name="real-time-scoring-with-sp_rxpredict-in-sql-server-machine-learning"></a>Puntuación en tiempo real con sp_rxPredict en SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La puntuación en tiempo real usa el procedimiento almacenado del sistema [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) y las funciones de extensión de CLR en SQL Server para las puntuaciones o predicciones de alto rendimiento en cargas de trabajo de predicción. La puntuación en tiempo real es independiente del lenguaje y se ejecuta sin dependencias en los tiempos de ejecución de R o Python. Suponiendo que el modelo se haya creado y entrenado con las funciones de Microsoft y, después, se haya serializado a un formato binario en SQL Server, se puede usar la puntuación en tiempo real para generar resultados previstos en nuevas entradas de datos en instancias de SQL Server que no tienen instalado el complemento de R o Python.

## <a name="how-real-time-scoring-works"></a>Funcionamiento de la puntuación en tiempo real

La puntuación en tiempo real se admite en determinados tipos de modelo basados en funciones de RevoScaleR o MicrosoftML, como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Usa bibliotecas de C++ nativas para generar puntuaciones, según los datos introducidos por el usuario que se proporcionan a un modelo de aprendizaje automático almacenado en un formato binario especial.

Como los modelos entrenados se pueden usar para la puntuación sin tener que llamar a un entorno de tiempo de ejecución de lenguaje externo, se reduce la sobrecarga de varios procesos. Esto admite un rendimiento de predicción mucho más rápido para escenarios de puntuación de producción. Los datos nunca salen de SQL Server. Por eso, los resultados se pueden generar e insertar en una nueva tabla sin realizar ninguna conversión de datos entre R y SQL.

La puntuación en tiempo real es un proceso que consta de varios pasos:

1. Es necesario habilitar en cada base de datos el procedimiento almacenado que realiza la puntuación.
2. Hay que cargar el modelo previamente entrenado en formato binario.
3. Se proporcionan nuevos datos de entrada para puntuarlos, ya sea mediante tablas o en filas individuales, como entrada para el modelo.
4. Para generar puntuaciones, se llama al procedimiento almacenado [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql).

## <a name="prerequisites"></a>Prerequisites

+ [Habilitación de la integración de SQL Server con CLR](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Habilitar la puntuación en tiempo real](#bkmk_enableRtScoring).

+ El modelo se debe entrenar de antemano con uno de los algoritmos **rx** admitidos. Para R, la puntuación en tiempo real con `sp_rxPredict` funciona con [algoritmos admitidos de RevoScaleR y MicrosoftML](#bkmk_rt_supported_algos). Para Python, vea [Algoritmos admitidos de revoscalepy y microsoftml](#bkmk_py_supported_algos)

+ Serialice el modelo mediante [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

+ Guarde el modelo en la instancia del motor de base de datos desde el que quiere llamarlo. No es necesario que esta instancia tenga la extensión en tiempo de ejecución de R o de Python.

> [!Note]
> En la actualidad, la puntuación en tiempo real está optimizada para predicciones rápidas en conjuntos de datos más pequeños, que van desde unas pocas filas hasta cientos de miles de filas. En conjuntos de datos grandes, el uso de [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) podría ser más rápido.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmos admitidos

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmos de Python con puntuación en tiempo real

+ Modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Los modelos marcados con \* también admiten la puntuación nativa con la función PREDICT.

+ Modelos de microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Transformaciones proporcionadas por microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmos de R con puntuación en tiempo real

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Los modelos marcados con \* también admiten la puntuación nativa con la función PREDICT.

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
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelos no admitidos

La puntuación en tiempo real no usa un intérprete; por eso, no se admiten aquellas funciones que puedan necesitar un intérprete durante el paso de puntuación.  Entre ellas se incluyen:

  + No se admiten los modelos que usen los algoritmos `rxGlm` o `rxNaiveBayes`.

  + Los modelos que usan una función de transformación o una fórmula que contiene una transformación, como <code>A ~ log(B)</code>, no se admiten en la puntuación en tiempo real. Para usar un modelo de este tipo, se recomienda realizar la transformación en los datos de entrada antes de pasar los datos a la puntuación en tiempo real.


## <a name="example-sp_rxpredict"></a>Ejemplo: sp_rxPredict

En esta sección se describen los pasos necesarios para configurar la predicción **en tiempo real** y se muestra un ejemplo en R de cómo llamar a la función desde T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Paso 1. Habilitar el procedimiento de puntuación en tiempo real

Debe habilitar esta característica para cada base de datos que quiera usar para la puntuación. El administrador del servidor debe ejecutar la utilidad de línea de comandos, RegisterRExt.exe, que se incluye con el paquete RevoScaleR.

> [!NOTE]
> Para que funcione la puntuación en tiempo real, es necesario habilitar la función CLR de SQL en la instancia; además, la base de datos debe estar marcada como de confianza. Al ejecutar el script, estas acciones se realizan automáticamente. Pero no olvide las implicaciones de seguridad adicionales antes de hacerlo.

1. Abra un símbolo del sistema con privilegios elevados y navegue hasta la carpeta donde se encuentra RegisterRExt.exe. Puede usar esta ruta de acceso en una instalación predeterminada:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Ejecute el siguiente comando, pero sustituya el nombre de la instancia y la base de datos de destino donde quiera habilitar los procedimientos almacenados extendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por ejemplo, para agregar el procedimiento almacenado extendido a la base de datos CLRPredict en la instancia predeterminada, escriba:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    El nombre de la instancia es opcional si la base de datos está en la instancia predeterminada. Si usa una instancia con nombre, debe especificar el nombre de la instancia.

3. RegisterRExt.exe crea estos objetos:

    + ensamblados de confianza;
    + el procedimiento almacenado `sp_rxPredict`,
    + un nuevo rol de base de datos, `rxpredict_users`. El administrador de bases de datos puede usar este rol para conceder permiso a los usuarios que usan la función de puntuación en tiempo real.

4. Agregue los usuarios que tengan que ejecutar `sp_rxPredict` en el nuevo rol.

> [!NOTE]
> 
> En SQL Server 2017, se aplican medidas de seguridad adicionales para evitar problemas con la integración de CLR. Estas medidas también imponen restricciones adicionales sobre el uso de este procedimiento almacenado. 

### <a name="step-2-prepare-and-save-the-model"></a>Paso 2. Preparar y guardar el modelo

El formato binario que sp\_rxPredict necesita es el mismo que el formato necesario para usar la función PREDICT. Por lo tanto, en el código de R, incluya una llamada a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) y asegúrese de especificar `realtimeScoringOnly = TRUE`, como en este ejemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sp_rxpredict"></a>Paso 3. Llamar a sp_rxPredict

Llame a sp\_rxPredict como lo haría con cualquier otro procedimiento almacenado. En la versión actual, el procedimiento almacenado solo toma dos parámetros: _\@model_ para el modelo en formato binario y _\@inputData_ para los datos que se van a usar en la puntuación, definidos como una consulta SQL válida.

Como el formato binario es el mismo que el que usa la función PREDICT, puede usar los modelos y la tabla de datos del ejemplo anterior.

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> Se produce un error en la llamada a sp\_rxPredict si los datos de entrada para la puntuación no incluyen columnas que coincidan con los requisitos del modelo. Actualmente, solo se admiten los siguientes tipos de datos de .NET: double, float, short, ushort, long, ulong y string.
> 
> Por tanto, es posible que tenga que filtrar los tipos no admitidos en los datos de entrada antes de usarlos para la puntuación en tiempo real.
> 
> Para obtener información sobre los tipos de SQL correspondientes, vea [Asignación de tipos de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [Asignación de datos de parámetros de CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Deshabilitar la puntuación en tiempo real

Para deshabilitar la función de puntuación en tiempo real, abra un símbolo del sistema con privilegios elevados y ejecute este comando: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Pasos siguientes

Para saber más sobre la puntuación en SQL Server, vea [Cómo generar previsiones y predicciones mediante modelos de aprendizaje automático en SQL Server](r/how-to-do-realtime-scoring.md).
