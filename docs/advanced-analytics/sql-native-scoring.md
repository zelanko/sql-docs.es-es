---
title: Puntuación nativa mediante la instrucción de T-SQL PREDECIR - SQL Server Machine Learning Services
description: Generar predicciones mediante la función T-SQL PREDECIR, puntuación de entradas de dta en un modelo previamente entrenado escritas en R o Python en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 65a7954aa18f9e8dbdfd814a6b0d189683e4606f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962312"
---
# <a name="native-scoring-using-the-predict-t-sql-function"></a>Puntuación nativa mediante la función de PREDICCIÓN de Transact-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Nativo de puntuación usa [función T-SQL PREDECIR](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) y las capacidades de extensión de C++ nativas en SQL Server 2017 para generar valores de predicción o *puntuaciones* para nuevas entradas de datos casi en tiempo real. Esta metodología ofrece la velocidad de procesamiento posibles más rápida de cargas de trabajo de previsión y la predicción, pero viene con los requisitos de plataforma y la biblioteca: solo las funciones de RevoScaleR y revoscalepy tienen implementaciones de C++.

Puntuación nativa requiere que tenga un modelo entrenado ya. En SQL Server 2017 Windows o Linux, o en Azure SQL Database, puede llamar a la función PREDICT de Transact-SQL para invocar nativo de puntuación con nuevos datos que se proporcionan como un parámetro de entrada. La función PREDICT devuelve las puntuaciones de las entradas de datos que proporcione.

## <a name="how-native-scoring-works"></a>Nativo cómo funciona la puntuación

Puntuación usa nativo C++ bibliotecas nativas de Microsoft que puede leer un modelo entrenado ya, previamente almacenados en un formato binario especial o guardado en el disco como secuencia de bytes sin procesar y generar puntuaciones para nuevas entradas de datos que proporcione. Dado que el modelo está entrenado, publicado y se almacenan, se puede usar para la puntuación sin tener que llamar el intérprete de R o Python. Por lo tanto, se reduce la sobrecarga de las interacciones de varios procesos, lo que el rendimiento de predicción mucho más rápido en escenarios de producción corporativo.

Para usar la puntuación nativa, llame a la función T-SQL PREDECIR y pase las siguientes entradas necesarias:

+ Un modelo compatible basado en un algoritmo compatible.
+ Datos de entrada, que normalmente se define como una consulta SQL.

La función devuelve las predicciones para los datos de entrada, junto con las columnas de datos de origen que se van a pasar a través.

## <a name="prerequisites"></a>Requisitos previos

PREDECIR está disponible en todas las ediciones del motor de base de datos de SQL Server 2017 y habilitado de forma predeterminada, incluido SQL Server 2017 Machine Learning Services en Windows, SQL Server 2017 (Windows), SQL Server 2017 (Linux) o Azure SQL Database. No es necesario instalar R, Python, o habilitar características adicionales.

+ Se debe entrenar el modelo de antemano con una de las **rx** algoritmos enumerados a continuación.

+ Serializar el modelo mediante [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R, y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

<a name="bkmk_native_supported_algos"></a> 

## <a name="supported-algorithms"></a>Algoritmos admitidos

+ modelos de revoscalepy

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

Si necesita usar modelos de MicrosoftML o microsoftml, use [puntuación en tiempo real con sp_rxPredict](real-time-scoring.md).

Tipos de modelos no admitidos incluyen los siguientes tipos:

+ Modelos que contienen otras transformaciones
+ Los modelos utilizando la `rxGlm` o `rxNaiveBayes` algoritmos en RevoScaleR o revoscalepy equivalentes
+ Modelos PMML
+ Modelos creados mediante otras bibliotecas de código abierto o de terceros

## <a name="example-predict-t-sql"></a>Ejemplo: PREDECIR (TRANSACT-SQL)

En este ejemplo, crear un modelo y, a continuación, llame a la función de predicción en tiempo real desde T-SQL.

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

Use la siguiente instrucción para rellenar la tabla de datos con los datos de la **iris** conjunto de datos.

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

El código siguiente crea un modelo basado en el **iris** conjunto de datos y lo guarda en la tabla denominada **modelos**.

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
> Asegúrese de usar el [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) función de RevoScaleR para guardar el modelo. El estándar de R `serialize` función no puede generar el formato requerido.

Puede ejecutar una instrucción como la siguiente para ver el modelo almacenado en formato binario:

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Paso 2. Ejecutar PREDICT en el modelo

La siguiente instrucción de PREDICCIÓN simple Obtiene una clasificación desde el modelo de árbol de decisión mediante el **puntuación nativa** función. Predice la especie de iris en función de los atributos proporcionados, la longitud del pétalo y ancho.

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

Si se produce un error, "Error durante la ejecución de la función PREDICT. Modelo está dañado o no válido", normalmente significa que la consulta no devolvió un modelo. Compruebe si ha escrito el nombre del modelo correctamente, o si la tabla de modelos está vacía.

> [!NOTE]
> Dado que las columnas y valores devuelven por **PREDICT** puede variar por tipo de modelo, debe definir el esquema de los datos devueltos mediante el uso de un **WITH** cláusula.

## <a name="next-steps"></a>Pasos siguientes

Para una solución completa que incluye la puntuación nativa, vea estos ejemplos desde el equipo de desarrollo de SQL Server:

+ Implemente la secuencia de comandos de ML: [Uso de un modelo de Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Implemente la secuencia de comandos de ML: [Uso de un modelo de R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)