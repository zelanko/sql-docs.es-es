---
title: 'En tiempo real de puntuación mediante el procedimiento sp_rxPredict almacenados: SQL Server Machine Learning Services'
description: Generar predicciones con sp_rxPredict, puntuación de entradas de datos en un modelo previamente entrenado escritas en R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: cccbae1e1957baedaba665e68a3a058db69f4885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962375"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Puntuación con sp_rxPredict en aprendizaje automático de SQL Server en tiempo real
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Usos de puntuación en tiempo real la [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) sistema procedimiento almacenado y las funciones de extensión CLR en SQL Server para las predicciones de alto rendimiento o las puntuaciones de la previsión de las cargas de trabajo. Puntuación en tiempo real es independiente del lenguaje y se ejecuta sin depender de R o Python tiempos de ejecución. Suponiendo que un modelo crea y entrena con las funciones de Microsoft y, a continuación, se serializa a un formato binario en SQL Server, puede usar la puntuación en tiempo real para generar los resultados predichos en nuevas entradas de datos en instancias de SQL Server que no tienen el complemento de R o Python instalado.

## <a name="how-real-time-scoring-works"></a>En tiempo real cómo funciona la puntuación

Puntuación en tiempo real se admite en SQL Server 2017 y SQL Server 2016, en tipos de modelos concretos según las funciones de RevoScaleR o MicrosoftML como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Usa las bibliotecas nativas de C++ para generar puntuaciones, basadas en la entrada de usuario proporcionado a un modelo almacenado en un formato binario especial de aprendizaje automático.

Dado que puede usar un modelo entrenado para puntuar sin tener que llamar en tiempo de ejecución de un lenguaje externo, se reduce la sobrecarga de varios procesos. Esto es compatible con un rendimiento de predicción mucho más rápido para escenarios de puntuación de producción. Dado que los datos nunca abandonan el SQL Server, se pueden generar resultados e inserta una nueva tabla sin sufrir ninguna traducción de datos entre R y SQL.

Puntuación en tiempo real es un proceso de varios pasos:

1. El procedimiento almacenado que realiza la puntuación debe estar habilitado en bases de datos.
2. Cargar el modelo previamente entrenado en formato binario.
3. Proporcionar nuevos datos de entrada puntuarse, filas tabulares o únicas, como entrada para el modelo.
4. Para generar puntuaciones, llame a la [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) procedimiento almacenado.

## <a name="prerequisites"></a>Requisitos previos

+ [Habilitar la integración de CLR de SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Habilitar la puntuación en tiempo real](#bkmk_enableRtScoring).

+ Se debe entrenar el modelo de antemano con una de las **rx** algoritmos. Para R, en tiempo real de puntuación con `sp_rxPredict` funciona con [RevoScaleR y MicrosoftML admiten algoritmos](#bkmk_rt_supported_algos). Para Python, consulte [revoscalepy y microsoftml admiten algoritmos](#bkmk_py_supported_algos)

+ Serializar el modelo mediante [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R, y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

+ Guardar el modelo en la instancia del motor de base de datos desde el que desea llamar. Esta instancia no debe tener la extensión en tiempo de ejecución de R o Python.

> [!Note]
> Puntuación en tiempo real está optimizado actualmente para las predicciones rápidas en conjuntos de datos más pequeños, que abarcan desde unas pocas filas hasta cientos de miles de filas. En grandes conjuntos de datos, mediante [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) puede ser más rápido.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmos admitidos

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmos de Python con la puntuación en tiempo real

+ modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Marcan de modelos con \* también admiten la puntuación nativa con la función PREDICT.

+ modelos de microsoftml

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

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmos de R con la puntuación en tiempo real

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
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelo no admitido

Puntuación en tiempo real no utiliza un intérprete; por lo tanto, no se admite ninguna funcionalidad que puede requerir un intérprete durante el paso de puntuación.  Entre ellas se incluyen:

  + Los modelos utilizando la `rxGlm` o `rxNaiveBayes` no se admiten los algoritmos.

  + Modela el uso de una función de transformación o fórmula que contiene una transformación, tal como <code>A ~ log(B)</code> no se admiten para determinar la puntuación en tiempo real. Para usar un modelo de este tipo, se recomienda realizar la transformación de datos de entrada antes de pasar los datos para puntuar en tiempo real.


## <a name="example-sprxpredict"></a>Ejemplo: sp_rxPredict

En esta sección se describe los pasos necesarios para configurar **en tiempo real** predicción y proporciona un ejemplo de R de cómo llamar a la función desde T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Paso 1. Habilitar el procedimiento de puntuación en tiempo real

Debe habilitar esta característica para cada base de datos que desea usar para la puntuación. El administrador del servidor debe ejecutar la utilidad de línea de comandos, RegisterRExt.exe, que se incluye con el paquete RevoScaleR.

> [!NOTE]
> Para puntuar en tiempo real para que funcione, la funcionalidad de CLR de SQL debe habilitarse en la instancia; Además, la base de datos debe estar marcado como de confianza. Al ejecutar el script, estas acciones se realizan automáticamente. Sin embargo, tenga en cuenta las implicaciones de seguridad adicional antes de hacer esto!

1. Abra un símbolo del sistema con privilegios elevados y vaya a la carpeta donde se encuentra RegisterRExt.exe. La siguiente ruta de acceso puede usarse en una instalación predeterminada:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Ejecute el siguiente comando, sustituyendo el nombre de la instancia y la base de datos de destino donde desea habilitar los procedimientos almacenados extendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por ejemplo, para agregar el procedimiento almacenado extendido a la base de datos CLRPredict en la instancia predeterminada, escriba:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    El nombre de instancia es opcional si se encuentra la base de datos en la instancia predeterminada. Si usa una instancia con nombre, debe especificar el nombre de instancia.

3. RegisterRExt.exe crea los siguientes objetos:

    + Ensamblados de confianza
    + El procedimiento almacenado `sp_rxPredict`
    + Un nuevo rol de base de datos, `rxpredict_users`. El Administrador de base de datos puede usar esta función para conceder permiso a los usuarios que utilizan la funcionalidad de puntuación en tiempo real.

4. Agregar los usuarios que necesitan para ejecutar `sp_rxPredict` al nuevo rol.

> [!NOTE]
> 
> En SQL Server 2017, las medidas de seguridad adicionales están en vigor para evitar problemas con la integración CLR. Estas medidas imponen restricciones adicionales sobre el uso de este procedimiento almacenado también. 

### <a name="step-2-prepare-and-save-the-model"></a>Paso 2. Preparar y guardar el modelo

El formato binario requerido por el sp\_rxPredict es el mismo que el formato necesario para usar la función PREDICT. Por lo tanto, en el código de R, incluya una llamada a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)y no olvide especificar `realtimeScoringOnly = TRUE`, como en este ejemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Paso 3. Llamada sp_rxPredict

Llamar a sp\_rxPredict como haría con cualquier otro procedimiento almacenado. En la versión actual, el procedimiento almacenado solo acepta dos parámetros:  _\@modelo_ para el modelo en formato binario, y  _\@inputData_ para que los datos que se va a usar para determinar la puntuación, se definen como una consulta SQL válida.

Dado que el formato binario es el mismo que se usa la función de PREDICCIÓN, puede usar la tabla de datos y modelos del ejemplo anterior.

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
> La llamada a sp\_rxPredict se produce un error si los datos de entrada para la puntuación no incluyen columnas que coinciden con los requisitos del modelo. Actualmente, se admiten solo los siguientes tipos de datos. NET: double, float, short, ushort, long, ulong y cadena.
> 
> Por lo tanto, es posible que deba filtrar los tipos no compatibles en los datos de entrada antes de usarlo para puntuar en tiempo real.
> 
> Para obtener información acerca de los correspondientes tipos SQL, vea [asignación de tipos de CLR de SQL](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [asignación de datos de parámetros CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Deshabilitar la puntuación en tiempo real

Para deshabilitar la funcionalidad de puntuación en tiempo real, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la puntuación en SQL Server, vea [cómo generar predicciones de aprendizaje automático de SQL Server](r/how-to-do-realtime-scoring.md).
