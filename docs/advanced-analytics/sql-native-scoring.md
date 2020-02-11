---
title: Puntuación nativa mediante PREDICT de T-SQL
description: Genere predicciones con la función PREDICT de T-SQL y puntúe las entradas de datos en un modelo entrenado previamente escrito en R o en Python en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 766adecbc91f88ed0796e4214b7e4074fc564f01
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727287"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Puntuación nativa mediante la función PREDICT de T-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La puntuación nativa usa la [función PREDICT de T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) y las capacidades de extensión nativas de C++ en SQL Server 2017 para generar valores de predicción o *puntuaciones* de las entradas de datos nuevas prácticamente en tiempo real. Esta metodología ofrece la velocidad de procesamiento más rápida posible de las cargas de trabajo de previsión y predicción, pero existen requisitos de plataforma y de biblioteca: solo las funciones de RevoScaleR y de revoscalepy tienen implementaciones de C++.

La puntuación nativa requiere que ya haya un modelo entrenado. En SQL Server 2017 (Windows o Linux) o en Azure SQL Database, se puede llamar a la función PREDICT en Transact-SQL para invocar la puntuación nativa con datos nuevos proporcionados como parámetro de entrada. La función PREDICT devuelve puntuaciones de las entradas de datos proporcionadas.

## <a name="how-native-scoring-works"></a>Cómo funciona la puntuación nativa

La puntuación nativa usa bibliotecas de C++ nativas de Microsoft capaces de leer un modelo ya entrenado (almacenado previamente en un formato binario especial o guardado en el disco como flujo de bytes sin formato) y de generar puntuaciones de las nuevas entradas de datos que se proporcionen. Como el modelo ya está entrenado, publicado y almacenado, se puede usar en la puntuación sin tener que llamar al intérprete de R o de Python. Esto reduce la sobrecarga de varias interacciones de procesos, lo que da lugar a un rendimiento de predicción mucho más rápido en escenarios de producción empresariales.

Para usar la puntuación nativa, llame a la función PREDICT de T-SQL y pase las siguientes entradas necesarias:

+ Un modelo compatible basado en un algoritmo compatible
+ Datos de entrada, normalmente definidos como una consulta SQL

La función devuelve predicciones de los datos de entrada, además de las columnas de datos de origen de paso a través.

## <a name="prerequisites"></a>Prerequisites

PREDICT está disponible en todas las ediciones del motor de base de datos de SQL Server 2017 y está habilitada de forma predeterminada, incluidos SQL Server Machine Learning Services en Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) o Azure SQL Database. No es necesario instalar R o Python, ni habilitar otras características.

+ El modelo se debe entrenar de antemano con uno de los algoritmos **rx** admitidos que se enumeran más abajo.

+ Serialice el modelo mediante [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmos admitidos

+ Modelos de revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ Modelos de RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Si necesita usar modelos de MicrosoftML o microsoftml, use [Puntuación en tiempo real con sp_rxPredict](real-time-scoring.md).

Los tipos de modelos no compatibles son los siguientes:

+ Modelos que contienen otras transformaciones
+ Modelos que usan los algoritmos `rxGlm` o `rxNaiveBayes` en los equivalentes de RevoScaleR o revoscalepy
+ Modelos de PMML
+ Modelos creados con otras bibliotecas de código abierto o de terceros

## <a name="example-predict-t-sql"></a>Ejemplo: PREDICT (T-SQL)

En este ejemplo, se crea un modelo y, después, se llama a la función de predicción en tiempo real desde T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Paso 1. Preparar y guardar el modelo

Ejecute el siguiente código para crear la base de datos de ejemplo y las tablas necesarias.

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

Use la siguiente instrucción para rellenar la tabla de datos con datos del conjunto de datos de **iris**.

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

El siguiente código crea un modelo basado en el conjunto de datos de **iris** y lo guarda en la tabla denominada **models**.

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
> Asegúrese de usar la función [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) de RevoScaleR para guardar el modelo. La función `serialize` de R estándar no puede generar el formato que necesitamos.

Puede ejecutar una instrucción como la siguiente para ver el modelo almacenado en formato binario:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Paso 2. Ejecutar PREDICT en el modelo

La siguiente instrucción PREDICT sencilla obtiene una clasificación del modelo de árbol de decisión mediante la función de **puntuación nativa**. Predice las especies de iris a partir de los atributos proporcionados y de la longitud y el ancho de pétalo.

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

Si aparece el error "Error durante la ejecución de la función integrada PREDICT. El modelo está dañado o no es válido", suele significar que la consulta no devolvió un modelo. Compruebe si escribió correctamente el nombre del modelo, o si la tabla de modelos está vacía.

> [!NOTE]
> Dado que las columnas y los valores devueltos por **PREDICT** pueden variar según el tipo de modelo, debe definir el esquema de los datos devueltos mediante una cláusula **WITH**.

## <a name="next-steps"></a>Pasos siguientes

Para obtener una solución completa que incluye puntuación nativa, vea estos ejemplos del equipo de desarrollo de SQL Server:

+ Implementación del script de ML [con un modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implementación del script de ML [con un modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)