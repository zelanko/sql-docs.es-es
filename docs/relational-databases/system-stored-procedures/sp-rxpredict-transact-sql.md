---
title: sp_rxPredict | Microsoft Docs
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
ms.openlocfilehash: dadaa5f51f359d9a6803d504d6b3a0da64f39852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126419"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Genera un valor de predicción para una entrada determinada que consta de un modelo de machine learning almacenado en un formato binario en una base de datos de SQL Server.

Proporciona la puntuación en R y Python modelos de machine learning en casi en tiempo real. `sp_rxPredict` es un procedimiento almacenado que se proporciona como un contenedor para el `rxPredict` función de R en [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) y [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)y el [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) función de Python en [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Está escrito en C++ y está optimizado específicamente para las operaciones de puntuación.

Aunque el modelo se debe crear mediante R o Python, una vez que se serializa y se almacena en un formato binario en una instancia del motor de base de datos de destino, se puede consumir desde esa instancia del motor de base de datos incluso cuando no está instalada la integración de R o Python. Para obtener más información, consulte [puntuación en tiempo real con sp_rxPredict](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring).

## <a name="syntax"></a>Sintaxis

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**model**

Un modelo previamente entrenado en un formato compatible. 

**input**

Una consulta SQL válida

### <a name="return-values"></a>Valores devueltos

Se devuelve una columna de puntuación, así como las columnas de paso a través del origen de datos de entrada.
Adicionales calificación columnas, como el intervalo de confianza, puede devolverse si el algoritmo admite la generación de estos valores.

## <a name="remarks"></a>Comentarios

Para habilitar el uso del procedimiento almacenado, SQLCLR debe habilitarse en la instancia.

> [!NOTE]
> Hay implicaciones de seguridad a enabing esta opción. Use una implementación alternativa, como el [PREDECIR Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql?view=sql-server-2017) funcione, si no se puede habilitar SQLCLR en el servidor.

El usuario debe `EXECUTE` permiso en la base de datos.

### <a name="supported-algorithms"></a>Algoritmos admitidos

Para crear y entrenar el modelo, use uno de los algoritmos admitidos para R o Python, proporcionada por [SQL Server 2016 R Services](https://docs.microsoft.com/sql/advanced-analytics/r/sql-server-r-services?view=sql-server-2017), [SQL Server 2016 R Server (independiente)](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2016), [máquina de SQL Server 2017 Servicios (R o Python) de aprendizaje](https://docs.microsoft.com//sql/advanced-analytics/what-is-sql-server-machine-learning?view=sql-server-2017), o [(independiente) (R o Python) del servidor de SQL Server 2017](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone?view=sql-server-2017).

#### <a name="r-revoscaler-models"></a>R: Modelos de RevoScaleR

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

#### <a name="r-transformations-supplied-by-microsoftml"></a>R: Transformaciones proporcionadas por MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

#### <a name="python-revoscalepy-models"></a>Python: modelos de revoscalepy

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

#### <a name="python-transformations-supplied-by-microsoftml"></a>Python: Transformaciones proporcionadas por microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)
  
### <a name="unsupported-model-types"></a>Tipos de modelo no admitido

No se admiten los siguientes tipos de modelo:

+ Los modelos utilizando la `rxGlm` o `rxNaiveBayes` algoritmos de RevoScaleR
+ Modelos PMML en R
+ Modelos creados mediante otras bibliotecas de terceros 

## <a name="examples"></a>Ejemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Además de ser una consulta SQL válida, los datos de entrada en *@inputData* debe incluir columnas compatibles con las columnas en el modelo almacenado.

`sp_rxPredict` admite solo los siguientes tipos de columna. NET: double, float, short, ushort, long, ulong y cadena. Es posible que deba filtrar los tipos no compatibles en los datos de entrada antes de usarlo para puntuar en tiempo real. 

  Para obtener información acerca de los correspondientes tipos SQL, vea [asignación de tipos de CLR de SQL](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [asignación de datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

