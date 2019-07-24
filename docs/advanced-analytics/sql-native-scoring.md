---
title: Puntuación nativa mediante la instrucción de T-SQL de predicción
description: Generar predicciones mediante la función de T-SQL de predicción, puntuar las entradas DTA en un modelo entrenado previamente escrito en R o Python en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b148bd1ca51a7121ae043e2b616100e295c008aa
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344761"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Puntuación nativa mediante la función de T-SQL de predicción
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La puntuación nativa usa la función de predicción de [T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) y las capacidades de extensión nativa C++ en SQL Server 2017 para generar valores de predicción o *puntuaciones* para nuevas entradas de datos casi en tiempo real. Esta metodología ofrece la velocidad de procesamiento más rápida posible de las cargas de trabajo de previsión y predicción, pero incluye requisitos de plataforma y de biblioteca: solo las funciones C++ de RevoScaleR y revoscalepy tienen implementaciones.

La puntuación nativa requiere que ya tenga un modelo entrenado. En SQL Server 2017 Windows o Linux, o en Azure SQL Database, puede llamar a la función PREDICT en Transact-SQL para invocar la puntuación nativa con los nuevos datos que proporcione como parámetro de entrada. La función PREDICT devuelve las puntuaciones de las entradas de datos proporcionadas.

## <a name="how-native-scoring-works"></a>Cómo funciona la puntuación nativa

La puntuación nativa usa C++ bibliotecas nativas de Microsoft que pueden leer un modelo ya entrenado, almacenado previamente en un formato binario especial o guardado en el disco como flujo de bytes sin formato, y generar puntuaciones para las nuevas entradas de datos que proporcione. Dado que el modelo está entrenado, publicado y almacenado, se puede usar para la puntuación sin tener que llamar al intérprete de R o Python. Como tal, se reduce la sobrecarga de varias interacciones de proceso, lo que da lugar a un rendimiento de predicción mucho más rápido en escenarios de producción empresarial.

Para usar la puntuación nativa, llame a la función de T-SQL de predicción y pase las siguientes entradas obligatorias:

+ Modelo compatible basado en un algoritmo compatible.
+ Datos de entrada, normalmente definidos como una consulta SQL.

La función devuelve las predicciones para los datos de entrada, junto con las columnas de datos de origen que desea pasar.

## <a name="prerequisites"></a>Requisitos previos

PREDICT está disponible en todas las ediciones de SQL Server motor de base de datos 2017 y está habilitada de forma predeterminada, incluido SQL Server 2017 Machine Learning Services en Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) o Azure SQL Database. No es necesario instalar R, Python ni habilitar características adicionales.

+ El modelo se debe entrenar de antemano con uno de los algoritmos **RX** admitidos que se enumeran a continuación.

+ Serialice el modelo con [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmos admitidos

+ modelos revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Modelos RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Si necesita usar modelos de MicrosoftML o MicrosoftML, use [la puntuación en tiempo real con sp_rxPredict](real-time-scoring.md).

Entre los tipos de modelo no admitidos se incluyen los siguientes:

+ Modelos que contienen otras transformaciones
+ Modelos que usan `rxGlm` los `rxNaiveBayes` algoritmos o en RevoScaleR o revoscalepy equivalentes
+ Modelos PMML
+ Modelos creados con otras bibliotecas de código abierto o de terceros

## <a name="example-predict-t-sql"></a>Ejemplo: PREDICCIÓN (T-SQL)

En este ejemplo, se crea un modelo y, a continuación, se llama a la función de predicción en tiempo real desde T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Paso 1. Preparar y guardar el modelo

Ejecute el código siguiente para crear la base de datos de ejemplo y las tablas necesarias.

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

Use la instrucción siguiente para rellenar la tabla de datos con datos del conjunto de datos de **iris** .

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Ahora, cree una tabla para almacenar los modelos.

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

En el código siguiente se crea un modelo basado en el conjunto de elementos de **iris** y se guarda en la tabla denominada **Models**.

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> Asegúrese de usar la función [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) de RevoScaleR para guardar el modelo. La función estándar `serialize` de R no puede generar el formato requerido.

Puede ejecutar una instrucción como la siguiente para ver el modelo almacenado en formato binario:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Paso 2. Ejecutar predecir en el modelo

La siguiente instrucción de predicción simple obtiene una clasificación del modelo de árbol de decisión mediante la función de **puntuación nativa** . Predice las especies del iris en función de los atributos proporcionados, la longitud y el ancho del pétalo.

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

Si aparece el error "error durante la ejecución de la función PREDICT. El modelo está dañado o no es válido ", normalmente significa que la consulta no devolvió un modelo. Compruebe si escribió correctamente el nombre del modelo, o si la tabla de modelos está vacía.

> [!NOTE]
> Dado que las columnas y los valores  devueltos por predicción pueden variar según el tipo de modelo, debe definir el esquema de los datos devueltos mediante una cláusula **with** .

## <a name="next-steps"></a>Pasos siguientes

Para obtener una solución completa que incluye la puntuación nativa, consulte estos ejemplos del equipo de desarrollo de SQL Server:

+ Implemente el script de ML: [Usar un modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implemente el script de ML: [Usar un modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)