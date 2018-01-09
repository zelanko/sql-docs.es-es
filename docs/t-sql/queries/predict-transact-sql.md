---
title: PREDECIR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs: TSQL
helpviewer_keywords: PREDICT clause
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 5f2ed3582341ff2824943a432e5877602b0b9ee7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="predict-transact-sql"></a>PREDECIR (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Genera un valor de predicción o puntuaciones basadas en un modelo almacenado.  

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

El `MODEL` parámetro se utiliza para especificar el modelo que se usa para la puntuación o la predicción. El modelo se especifica como una variable o un literal o una expresión escalar.

El objeto de modelo puede crearse mediante el uso de R o Python u otra herramienta.

**data**

El parámetro de datos se utiliza para especificar los datos usados para puntuar o la predicción. Datos se especifican en forma de un origen de tabla en la consulta. Origen de tabla puede ser una tabla, los alias de tabla, los alias CTE, vista o función con valores de tabla.

**parámetros**

Los parámetros se utilizan para especificar los parámetros de definido por el usuario opcionales que se usa para la puntuación o la predicción.

El nombre de cada parámetro es específico del tipo de modelo. Por ejemplo, la función rxPredict en RevoScaleR admite el parámetro  _@computeResiduals bits_ para admitir el cálculo de los valores residuales cuando un modelo de regresión logística de puntuación. Podría pasar que el nombre del parámetro y valor para el `PREDICT` función.

> [NOTA] Esta opción no se admite en la versión preliminar de SQL Server 2017 y se incluye únicamente con fines de compatibilidad de avance.

**CON ( \<result_set_definition >)**

Se utiliza la cláusula WITH para especificar el esquema de la salida devuelta por la `PREDICT` (función).

Además de las columnas devueltas por la `PREDICT` propia función, todas las columnas que forman parte de los datos de entrada están disponibles para su uso en la consulta.

### <a name="return-values"></a>Valores devueltos

Ningún esquema predefinido está disponible; SQL Server no valida el contenido del modelo y no valida los valores de columna devuelta.  
- El `PREDICT` función pasa a través de las columnas como entrada  
- El `PREDICT` función también genera nuevas columnas, pero el número de columnas y sus tipos de datos depende del tipo de modelo que se usó para la predicción.  

Los mensajes de error relacionados con los datos, el modelo o el formato de columna se devuelven mediante la función de predicción subyacente asociada con el modelo.  
- Para RevoScaleR, la función equivalente es [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)  
- Para MicrosoftML, la función equivalente es [rxPredict.mlModel](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxpredict)  

No es posible ver la estructura de modelo interno con `PREDICT`. Si desea entender el contenido del modelo de sí mismo, debe cargar el objeto de modelo, deserializarlo y utilizar código de R adecuado para analizar el modelo.

## <a name="remarks"></a>Comentarios

El `PREDICT` función se admite en todas las ediciones de SQL Server, como Linux.

No es necesario que R, Python u otra máquina aprendizaje idioma esté instalado en el servidor para usar el `PREDICT` función. Puede entrenar el modelo en otro entorno y guárdelo en una tabla de SQL Server para su uso con `PREDICT`, o llamar el modelo desde otra instancia de SQL Server que contiene el modelo guardado.

### <a name="supported-algorithms"></a>Algoritmos admitidos

El modelo que usa se debe haber creado mediante uno de los algoritmos admitidos desde el paquete RevoScaleR. Para obtener una lista de los modelos admitidos actualmente, consulte [de puntuación en tiempo real](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Permissions

No se requieren para permisos `PREDICT`; sin embargo, las necesidades de usuario `EXECUTE` permiso en la base de datos y permiso para consultar los datos que se usan como entradas. El usuario también debe ser capaz de leer el modelo de una tabla, si el modelo se ha almacenado en una tabla.

## <a name="examples"></a>Ejemplos

Los ejemplos siguientes muestran la sintaxis para llamar a `PREDICT`.

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>Llamar a un modelo almacenado y usarlo para la predicción

Este ejemplo llama a un modelo de regresión logística existente almacenado en la tabla [models_table]. Obtiene el último modelo entrenado, mediante una instrucción SELECT y, a continuación, pasa el modelo de binario a la función de PREDICCIÓN. Los valores de entrada representan características; el resultado representa la clasificación asignada por el modelo.

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 @model from [models_table]";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>Uso de PREDICCIÓN en una cláusula FROM

Este ejemplo hace referencia el `PREDICT` funcionando en el `FROM` cláusula de una `SELECT` instrucción:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

El alias **d.** especificado para la tabla de origen en el _datos_ parámetro se usa para hacer referencia a las columnas que pertenecen a dbo.mytable. El alias **p** especificado para la **PREDICT** función se utiliza para hacer referencia a las columnas devueltas por la función de PREDICCIÓN.

### <a name="combining-predict-with-an-insert-statement"></a>La combinación de PREDICCIÓN con una instrucción INSERT

Uno de los casos de uso común para la predicción es generar una puntuación de datos de entrada y, a continuación, insertar los valores de predicción en una tabla. En el siguiente ejemplo se da por supuesto que la aplicación que realiza la llamada usa un procedimiento almacenado para insertar una fila que contiene el valor de predicción en una tabla:

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

Si el procedimiento toma varias filas a través de un parámetro con valores de tabla, a continuación, puede escribirse como sigue:

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

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Crear un modelo de R y generando puntuaciones mediante parámetros del modelo opcional

> [!NOTE]
> Uso del argumento de parámetros no se admite en la versión Release Candidate 1.

En este ejemplo se da por supuesto que ha creado un modelo de regresión logística equipado con una matriz de covarianza, mediante una llamada a RevoScaleR como este:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Si almacena el modelo en SQL Server en formato binario, puede usar la función de PREDICCIÓN para generar no sólo las predicciones, sino información adicional compatible con el tipo de modelo, por ejemplo, error o intervalos de confianza.

El código siguiente muestra la llamada equivalente de R a rxPredict:

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

La llamada a equivalente con el `PREDICT` función también proporciona la puntuación (predecir el valor), error y los intervalos de confianza:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```


