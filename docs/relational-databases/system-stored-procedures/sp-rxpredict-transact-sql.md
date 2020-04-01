---
title: sp_rxPredict Microsoft Docs
ms.date: 03/30/2020
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
ms.openlocfilehash: 752d9655096bc929ea9175577c7705dc58955652
ms.sourcegitcommit: 5c28603dd51d907544ebf8a50b678675d5414eaf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2020
ms.locfileid: "80471837"
---
# <a name="sp_rxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

Genera un valor predicho para una entrada determinada que consta de un modelo de aprendizaje automático almacenado en un formato binario en una base de datos de SQL ServerSQL Server .

Proporciona puntuación en modelos de aprendizaje automático de R y Python casi en tiempo real. `sp_rxPredict`es un procedimiento almacenado proporcionado `rxPredict` como contenedor para la función R en [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) y [MicrosoftML,](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)y la [función rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python en [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Está escrito en C++ y está optimizado específicamente para operaciones de puntuación.

Aunque el modelo se debe crear mediante R o Python, una vez que se serializa y almacena en un formato binario en una instancia del motor de base de datos de destino, se puede consumir desde esa instancia del motor de base de datos incluso cuando la integración de R o Python no está instalada. Para obtener más información, consulte [Puntuación en tiempo real con sp_rxPredict](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="syntax"></a>Sintaxis

```syntaxsql
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**model**

Un modelo previamente entrenado en un formato compatible. 

**input**

Una consulta SQL válida

### <a name="return-values"></a>Valores devueltos

Se devuelve una columna de puntuación, así como cualquier columna de paso a través del origen de datos de entrada.
Se pueden devolver columnas de puntuación adicionales, como el intervalo de confianza, si el algoritmo admite la generación de dichos valores.

## <a name="remarks"></a>Observaciones

Para habilitar el uso del procedimiento almacenado, SQLCLR debe estar habilitado en la instancia.

> [!NOTE]
> Hay implicaciones de seguridad para enestablecer esta opción. Use una implementación alternativa, como la función PREDICT de [Transact-SQLTransact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) , si SQLCLR no se puede habilitar en el servidor.

El usuario `EXECUTE` necesita permiso en la base de datos.

### <a name="supported-algorithms"></a>Algoritmos admitidos

Para crear y entrenar modelos, utilice uno de los algoritmos admitidos para R o Python, proporcionado por [SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017), SQL Server [2016 R Server (independiente),](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016) [SQL Server 2017 Machine Learning Services (R o Python)](../../advanced-analytics/what-is-sql-server-machine-learning.md?view=sql-server-2017)o [SQL Server 2017 Server (Standalone) (R o Python).](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017)

#### <a name="r-revoscaler-models"></a>R: Modelos RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree)
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)

#### <a name="r-microsoftml-models"></a>R: Modelos de MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: Transformaciones suministradas por MicrosoftML

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


#### <a name="python-microsoftml-models"></a>Python: modelos de microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: transformaciones proporcionadas por microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>Tipos de modelos no admitidos

No se admiten los siguientes tipos de modelo:

+ Modelos que `rxGlm` `rxNaiveBayes` utilizan los algoritmos o en RevoScaleR
+ Modelos de PMML en R
+ Modelos creados con otras bibliotecas de terceros 

## <a name="examples"></a>Ejemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
  @inputData = N'SELECT * FROM data';
```

Además de ser una consulta SQL válida, los datos de entrada de * \@inputData* deben incluir columnas compatibles con las columnas del modelo almacenado.

`sp_rxPredict`Solo admite los siguientes tipos de columnas de .NET: double, float, short, ushort, long, ulong y string. Es posible que deba filtrar los tipos no admitidos en los datos de entrada antes de usarlos para la puntuación en tiempo real. 

  Para obtener información sobre los tipos de SQL correspondientes, vea [Asignación de tipos de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [Asignación de datos de parámetros de CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

