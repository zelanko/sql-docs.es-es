---
title: Inicio rápido para predecir el modelo mediante R
description: En esta guía de inicio rápido, obtendrá información sobre la puntuación mediante un modelo creado previamente en R y SQL Server datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4058725227deea1f6755c8e6272265ecdf91e59c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714786"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>Inicio rápido: Predicción del modelo mediante R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, use el modelo que ha creado en la guía de inicio rápido anterior para puntuar las predicciones con datos nuevos. Para realizar la _puntuación_ con datos nuevos, obtenga uno de los modelos entrenados de la tabla y, a continuación, llame a un nuevo conjunto de datos en el que basar las predicciones. La puntuación es un término que a veces se usa en la ciencia de datos para hacer referencia a la generación de predicciones, probabilidades u otros valores basados en nuevos datos que se introducen en un modelo entrenado.

## <a name="prerequisites"></a>Requisitos previos

Esta guía de inicio rápido es una extensión de [creación de un modelo predictivo](quickstart-r-create-predictive-model.md).

## <a name="create-the-table-of-new-data"></a>Crear la tabla de datos nuevos

En primer lugar, cree una tabla con nuevos datos. 

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

## <a name="predict-manual-transmission"></a>Predicción de la transmisión manual

En este momento, `dbo.GLM_models` es posible que la tabla contenga varios modelos de R, todos ellos compilados con diferentes parámetros o algoritmos, o entrenado en distintos subconjuntos de datos.

Para obtener las predicciones basadas en un modelo específico, debe escribir un script SQL que hace lo siguiente:

1. Obtener el modelo que quiere
2. Obtener los nuevos datos de entrada
3. Llamar a una función de predicción de R que sea compatible con ese modelo

En este ejemplo, usaremos el modelo denominado `default model`.

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

En el script anterior se realizan los pasos siguientes:

+ Use una instrucción SELECT para obtener un único modelo de la tabla y páselo como un parámetro de entrada.

+ Después de recuperar el modelo de la tabla, llame a la función `unserialize` en el modelo.

+ Use la función `predict` con los argumentos adecuados para el modelo y proporcione los nuevos datos de entrada.

+ En el ejemplo, la `str` función se agrega durante la fase de prueba para comprobar el esquema de datos devuelto desde R. Puede quitar la instrucción más adelante.

+ Los nombres de columna utilizados en el script de R no se pasan necesariamente a la salida del procedimiento almacenado. Aquí hemos usado la cláusula WITH RESULTs para definir algunos nombres de columna nuevos.

**Resultado**

![Conjunto de resultados para predecir properbility de la transmisión manual](./media/r-predict-am-resultset.png)

También es posible usar la predicción [en Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para generar un valor o una puntuación predichos basados en un modelo almacenado.

## <a name="next-steps"></a>Pasos siguientes

La integración de R con SQL Server hace que sea más fácil implementar soluciones de R a escala (gracias a las mejores características de R y de las bases de datos relacionales) para controlar los datos de alto rendimiento y los análisis rápidos de R. 

Siga aprendiendo sobre soluciones que usan R con SQL Server a través de escenarios de un extremo a otro creados por los equipos de desarrollo de ciencia de datos de Microsoft y de R Services.

> [!div class="nextstepaction"]
> [Tutoriales de SQL Server R](sql-server-r-tutorials.md)
