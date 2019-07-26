---
title: sp_rxPredict | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9cd9bb481ec54f9d99c80aba54241827c2a118cf
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471073"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

Genera un valor de predicción para una entrada determinada que consta de un modelo de aprendizaje automático almacenado en un formato binario en una base de datos de SQL Server.

Proporciona puntuación en los modelos de aprendizaje automático de R y Python casi en tiempo real. `sp_rxPredict`es un procedimiento almacenado que se proporciona como un contenedor `rxPredict` para la función de R en [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) y [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package), y la función de Python [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) en [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Está escrito en C++ y está optimizado específicamente para las operaciones de puntuación.

Aunque el modelo se debe crear mediante R o Python, una vez que se serializa y se almacena en un formato binario en una instancia del motor de base de datos de destino, se puede usar desde esa instancia del motor de base de datos aunque no esté instalada la integración de R o Python. Para obtener más información, vea [puntuación en tiempo real con sp_rxPredict](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="syntax"></a>Sintaxis

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**model**

Modelo previamente entrenado en un formato admitido. 

**input**

Una consulta SQL válida

### <a name="return-values"></a>Valores devueltos

Se devuelve una columna de puntuación, así como todas las columnas de paso a través del origen de datos de entrada.
Se pueden devolver columnas de puntuación adicionales, como el intervalo de confianza, si el algoritmo admite la generación de estos valores.

## <a name="remarks"></a>Comentarios

Para habilitar el uso del procedimiento almacenado, SQLCLR debe estar habilitado en la instancia.

> [!NOTE]
> Hay implicaciones de seguridad para enabing esta opción. Use una implementación alternativa, como la función de predicción de [Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) , si SQLCLR no se puede habilitar en el servidor.

El usuario necesita `EXECUTE` el permiso en la base de datos.

### <a name="supported-algorithms"></a>Algoritmos admitidos

Para crear y entrenar el modelo, use uno de los algoritmos admitidos para R o Python, proporcionado por [SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017), [SQL Server 2016 R Server (independiente)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016), [SQL Server 2017 Machine Learning Services (R o Python)](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017)o [SQL Server 2017 Servidor (independiente) (R o Python)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017).

#### <a name="r-revoscaler-models"></a>R: Modelos RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: Modelos MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: Transformaciones proporcionadas por MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: modelos revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit)
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees)
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree)
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest)


#### <a name="python-microsoftml-models"></a>Python: modelos microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python Transformaciones proporcionadas por microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>Tipos de modelo no admitidos

No se admiten los siguientes tipos de modelo:

+ Modelos que usan `rxGlm` los `rxNaiveBayes` algoritmos o en RevoScaleR
+ Modelos PMML en R
+ Modelos creados con otras bibliotecas de terceros 

## <a name="examples"></a>Ejemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Además de ser una consulta SQL válida, los datos de entrada de *@inputData* deben incluir columnas compatibles con las columnas del modelo almacenado.

`sp_rxPredict`solo admite los siguientes tipos de columna de .NET: Double, Float, Short, ushort, Long, ulong y String. Es posible que tenga que filtrar los tipos no admitidos en los datos de entrada antes de usarlo para la puntuación en tiempo real. 

  Para obtener información sobre los tipos SQL correspondientes, consulte [asignación de tipos de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [asignación de datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

