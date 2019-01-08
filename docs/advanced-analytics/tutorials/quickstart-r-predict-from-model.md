---
title: Inicio rápido para la predicción de modelo mediante R - SQL Server Machine Learning
description: En este tutorial, obtenga información sobre la puntuación mediante un modelo creado previamente en los datos de R y SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 7175b99eb20710f5dd08689bd055d3a4ec93ae92
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046973"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>Inicio rápido: Predicción de modelo mediante R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial, use el modelo que creó en el tutorial anterior para puntuar predicciones basadas en datos actualizados. Para realizar _puntuación_ con nuevos datos, obtener uno de los modelos entrenados de la tabla y, a continuación, llamar a un nuevo conjunto de datos en el que se va a basar las predicciones. La puntuación es un término usado en ocasiones, ciencia de datos significa generar predicciones, las probabilidades u otros valores según los nuevos datos que se introducen en un modelo entrenado.

## <a name="prerequisites"></a>Requisitos previos

Este inicio rápido es una extensión de [crear un modelo predictivo](quickstart-r-create-predictive-model.md).

## <a name="create-the-table-of-new-data"></a>Crear la tabla de datos nueva

En primer lugar, cree una tabla con datos nuevos. 

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

## <a name="predict-manual-transmission"></a>Predecir una transmisión manual

En este momento, su `dbo.GLM_models` tabla puede contener varios modelos de R, todos creados con distintos parámetros o algoritmos o entrenado en distintos subconjuntos de datos.

Para obtener predicciones basadas en un modelo específico, debe escribir un script SQL que hace lo siguiente:

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

El script anterior lleva a cabo los pasos siguientes:

+ Use una instrucción SELECT para obtener un único modelo de la tabla y páselo como un parámetro de entrada.

+ Después de recuperar el modelo de la tabla, llame a la función `unserialize` en el modelo.

+ Use la función `predict` con los argumentos adecuados para el modelo y proporcione los nuevos datos de entrada.

+ En el ejemplo, el `str` se agrega la función durante la fase de pruebas para comprobar el esquema de datos que se devuelve desde R. Puede quitar la instrucción más tarde.

+ Los nombres de columna utilizados en el script de R no son necesariamente pasa a la salida del procedimiento almacenado. Aquí hemos usado la cláusula WITH RESULTS para definir algunos nuevos nombres de columna.

**Resultado**

![Conjunto de resultados para predecir properbility de transmisión manual](./media/r-predict-am-resultset.png)

También es posible usar el [PREDICT de Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para generar un valor de predicción o la puntuación basada en un modelo almacenado.

## <a name="next-steps"></a>Pasos siguientes

La integración de R con SQL Server hace que sea más fácil implementar soluciones de R a escala (gracias a las mejores características de R y de las bases de datos relacionales) para controlar los datos de alto rendimiento y los análisis rápidos de R. 

Continuar aprendiendo sobre las soluciones de uso de R con SQL Server a través de escenarios de extremo a otro creados por los equipos de desarrollo de ciencia de datos de Microsoft y R Services.

> [!div class="nextstepaction"]
> [Tutoriales de SQL Server R](sql-server-r-tutorials.md)
