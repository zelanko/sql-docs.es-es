---
title: "Crear un modelo predictivo (R en Inicio rápido de SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 6eb78a80-5791-438f-9ca6-d142ab5d9bb1
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4e0d5dab1f737361a82191b6a3d74561e12722e1
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="create-a-predictive-model-r-in-sql-quickstart"></a>Crear un modelo predictivo (R en Inicio rápido de SQL)

En este paso, podrá aprender a entrenar un modelo con R y después guardar el modelo en una tabla de SQL Server. El modelo es un modelo de regresión simple que predice la distancia de detención de un automóvil en función de la velocidad. Usará el `cars` conjunto de datos incluido con R, porque es pequeño y fácil de entender.

## <a name="create-the-source-data"></a>Crear el origen de datos

En primer lugar, cree una tabla para guardar los datos de entrenamiento.

```sql
CREATE TABLE CarSpeed ([speed] int not null, [distance] int not null)
INSERT INTO CarSpeed
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'car_speed <- cars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'car_speed'
```

+ Algunas personas les gusta utilizar tablas temporales, pero tenga en cuenta que algunos clientes R desconectarán las sesiones entre los distintos lotes.

+ El runtime de R incluye muchos conjuntos de datos, pequeños y grandes. Para obtener una lista de los conjuntos de datos instalados en R, escriba `library(help="datasets")` desde un símbolo del sistema de R.

## <a name="create-a-regression-model"></a>Crear un modelo de regresión

Los datos de velocidad de automóvil contienen dos columnas, ambas numéricas, `dist` y `speed`. Hay diversas observaciones de algunas velocidades. Desde estos datos, podrá crear un modelo de regresión lineal que describe alguna relación entre la velocidad de automóvil y la distancia necesaria para detener un automóvil.

Los requisitos de un modelo lineal son sencillos:

+ Definir una fórmula que describa la relación entre la variable dependiente `speed` y la variable independiente `distance`

+ Proporcionar datos de entrada para usarlos en el entrenamiento del modelo

> [!TIP]
> Si necesita una actualización en los modelos lineales, se recomienda este tutorial, que describe el proceso de ajustar un modelo mediante rxLinMod: [ajustar modelos lineales](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

Para crear el modelo, defina la fórmula contenida en el código de R y pase los datos como un parámetro de entrada.

```sql
DROP PROCEDURE IF EXISTS generate_linear_model;
GO
CREATE PROCEDURE generate_linear_model
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'lrmodel <- rxLinMod(formula = distance ~ speed, data = CarsData);
        trained_model <- data.frame(payload = as.raw(serialize(lrmodel, connection=NULL)));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model varbinary(max)));
END;
GO
```

+ El primer argumento rxLinMod es el parámetro *formula*, que define la distancia como dependiente de la velocidad.
+ Los datos de entrada se almacenan en la variable `CarsData`, que se rellena con la consulta SQL. Si no asigna un nombre específico a los datos de entrada, el nombre predeterminado de la variable sería _InputDataSet_.

## <a name="create-a-table-for-storing-the-model"></a>Crear una tabla para almacenar el modelo

A continuación, almacenar el modelo para que pueda volver a entrenar o utilizarlo para la predicción. El resultado de un paquete de R que crea un modelo suele ser un **objeto binario**. Por tanto, la tabla donde se almacena el modelo debe incluir una columna de tipo **varbinary**.

```sql
CREATE TABLE stopping_distance_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null);
```

## <a name="save-the-model"></a>Guardar el modelo

Para guardar el modelo, ejecute la siguiente instrucción de Transact-SQL para llamar al procedimiento almacenado, generar el modelo y guardarlo en una tabla.

```sql
INSERT INTO stopping_distance_models (model)
EXEC generate_linear_model;
```

Tenga en cuenta que si se ejecuta este código en una segunda vez, obtendrá este error:

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

Una opción para evitar este error consiste en actualizar el nombre de cada nuevo modelo. Por ejemplo, podría cambiar el nombre por algo más descriptivo e incluir el tipo de modelo, el día en que lo creó, etc.

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>Generar variables adicionales

Por lo general, el resultado de R del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) se limita a una única trama de datos. (Es posible que esta limitación desaparezca en el futuro.)

En cambio, puede devolver resultados de otros tipos, como por ejemplo escalares, además de la trama de datos.

Por ejemplo, suponga que quiere entrenar un modelo, pero ver inmediatamente una tabla de coeficientes del modelo. Puede crear la tabla de coeficientes como el resultado principal y generar el modelo entrenado en una variable SQL. Podría inmediatamente volver a utilizar el modelo mediante una llamada a la variable, o puede guardar el modelo en una tabla como se muestra aquí.

```sql
DECLARE @model varbinary(max), @modelname varchar(30)
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
        speedmodel <- rxLinMod(distance ~ speed, CarsData)
        modelbin <- serialize(speedmodel, NULL)
        OutputDataSet <- data.frame(coefficients(speedmodel));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @params = N'@modelbin varbinary(max) OUTPUT'
    , @modelbin = @model OUTPUT
    WITH RESULT SETS (([Coefficient] float not null));

-- Save the generated model
INSERT INTO [dbo].[stopping_distance_models] (model_name, model)
VALUES (' latest model', @model)
```

**Resultado**

![rslq_basictut_coefficients](media/rslq-basictut-coefficients.PNG)

### <a name="summary"></a>Resumen

Recuerde estas reglas para trabajar con parámetros SQL y las variables de R en `sp_execute_external_script`:

+ Todos los parámetros SQL asignados a un script de R deben aparecer por nombre en el  _@params_  argumento.
+ Para generar uno de estos parámetros, agregue la palabra clave OUTPUT en la lista _@params_.
+ Después de enumerar los parámetros asignados, proporcione la asignación, línea por línea, de los parámetros de SQL a las variables de R, inmediatamente después de la lista _@params_.

## <a name="next-lesson"></a>Lección siguiente

Ahora que tiene un modelo, en el paso final, aprenderá a generar las predicciones a partir de él y a trazar los resultados.

[Predecir y trazar a partir del modelo](../tutorials/rtsql-predict-and-plot-from-model.md)


