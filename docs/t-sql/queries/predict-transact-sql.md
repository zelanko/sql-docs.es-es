---
title: PREDICT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=azuresqldb-current||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c97363e7f13c3b42cf447ecf69929171544f3a6b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907257"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Genera un valor de predicción o puntuaciones basadas en un modelo almacenado. Para obtener más información, vea [Puntuación nativa mediante la función PREDICT de T-SQL](../../advanced-analytics/sql-native-scoring.md).

## <a name="syntax"></a>Sintaxis

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

### <a name="arguments"></a>Argumentos

**model**

El parámetro `MODEL` se usa para especificar el modelo que se usa para la puntuación o predicción. El modelo se especifica como una variable o un literal, o bien una expresión escalar.

El objeto de modelo se puede crear mediante R, Python u otra herramienta.

**data**

El parámetro DATA se usa para especificar los datos que se usan para la puntuación o predicción. Los datos se especifican en forma de un origen de tabla en la consulta. El origen de tabla puede ser una tabla, un alias de tabla, alias de CTE, vista o función con valores de tabla.

**parameters**

El parámetro PARAMETERS se usa para especificar los parámetros opcionales definidos por el usuario que se usan para la puntuación o predicción.

El nombre de cada parámetro es específico del tipo de modelo. Por ejemplo, la función [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) en RevoScaleR admite el parámetro `@computeResiduals`, lo que indica si se deben calcular valores residuales al puntuar un modelo de regresión logística. Si se llama a un modelo compatible, se podría pasar ese nombre de parámetro y un valor TRUE o FALSE a la función `PREDICT`.

**WITH ( <definición_de_conjunto_de_resultados> )**

La cláusula WITH se usa para especificar el esquema de la salida devuelta por la función `PREDICT`.

Además de las columnas devueltas por la propia función `PREDICT`, todas las columnas que forman parte de los datos de entrada están disponibles para su uso en la consulta.

### <a name="return-values"></a>Valores devueltos

No hay ningún esquema predefinido disponible; SQL Server no valida el contenido del modelo ni los valores de columna devueltos.

- La función `PREDICT` se pasa a través de las columnas como entrada.
- La función `PREDICT` también genera columnas nuevas, pero el número de columnas y sus tipos de datos dependen del tipo de modelo que se usó para la predicción.

Los mensajes de error relacionados con los datos, el modelo o el formato de columna se devuelven mediante la función de predicción subyacente asociada con el modelo.

- Para RevoScaleR, la función equivalente es [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict).  
- Para MicrosoftML, la función equivalente es [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict).  

No es posible ver la estructura de modelo interna con `PREDICT`. Para entender el contenido del modelo en sí mismo, se debe cargar el objeto de modelo, deserializarlo y usar código de R adecuado para analizar el modelo.

## <a name="remarks"></a>Observaciones

La función `PREDICT` se admite en todas las ediciones de SQL Server 2017 o posteriores, en Windows y Linux. `PREDICT` también es compatible con Azure SQL Database en la nube. Todas estas compatibilidades están activas sin importar si hay habilitadas otras características de aprendizaje automático.

No es necesario instalar R, Python u otro lenguaje de aprendizaje automático en el servidor para usar la función `PREDICT`. Se puede entrenar el modelo en otro entorno y guardarlo en una tabla de SQL Server para su uso con `PREDICT`, o bien llamar al modelo desde otra instancia de SQL Server que contenga el modelo guardado.

### <a name="supported-algorithms"></a>Algoritmos admitidos

El modelo que se use se debe haber creado mediante uno de los algoritmos admitidos del paquete RevoScaleR. Para obtener una lista de los modelos admitidos actualmente, vea [Puntuación en tiempo real](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Permisos

No se requieren permisos para `PREDICT`; pero los usuarios necesitan el permiso `EXECUTE` en la base de datos y permiso para consultar los datos que se usan como entradas. Los usuarios también deben poder leer el modelo desde una tabla, si el modelo se ha almacenado en una tabla.

## <a name="examples"></a>Ejemplos

En los ejemplos siguientes se describe la sintaxis para llamar a `PREDICT`.

### <a name="using-predict-in-a-from-clause"></a>Uso de PREDICT en una cláusula FROM

Este ejemplo se hace referencia a la función `PREDICT` en la cláusula `FROM` de una instrucción `SELECT`:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

El alias **d** especificado para el origen de tabla en el parámetro `DATA` se usa para hacer referencia a las columnas que pertenecen a dbo.mytable. El alias **p** especificado para la función **PREDICT** se usa para hacer referencia a las columnas devueltas por la función PREDICT.

### <a name="combining-predict-with-an-insert-statement"></a>Combinación de PREDICT con una instrucción INSERT

Uno de los casos de uso comunes para la predicción consiste en generar una puntuación para los datos de entrada y después insertar los valores de predicción en una tabla. En el ejemplo siguiente se da por supuesto que la aplicación que realiza la llamada usa un procedimiento almacenado para insertar una fila que contiene el valor de predicción en una tabla:

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

Si el procedimiento toma varias filas a través de un parámetro con valores de tabla, se puede escribir de esta forma:

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Creación de un modelo de R y generación de puntuaciones con parámetros de modelo opcionales

En este ejemplo se da por supuesto que se ha creado un modelo de regresión logística equipado con una matriz de covarianza, mediante una llamada a RevoScaleR como esta:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Si el modelo se almacena en SQL Server en formato binario, se puede usar la función PREDICT para generar no solo las predicciones, sino información adicional compatible con el tipo de modelo, por ejemplo, los intervalos de error o confianza.

En el código siguiente se muestra la llamada equivalente de R a [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict):

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

La llamada equivalente con la función `PREDICT` también proporciona los intervalos de puntuación (el valor de predicción), error y confianza:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```

## <a name="next-steps"></a>Pasos siguientes

- [Puntuación nativa mediante la función PREDICT de T-SQL](../../advanced-analytics/sql-native-scoring.md)
