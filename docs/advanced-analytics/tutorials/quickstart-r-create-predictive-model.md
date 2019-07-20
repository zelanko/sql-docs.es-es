---
title: Inicio rápido para crear un modelo predictivo mediante R
description: En esta guía de inicio rápido, aprenderá a crear un modelo en R con datos de SQL Server para trazar las predicciones.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 39310d935ddefe463b81af495f63304822035818
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345473"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>Inicio rápido: Creación de un modelo predictivo mediante R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta guía de inicio rápido, aprenderá a entrenar un modelo mediante R y, a continuación, guardará el modelo en una tabla en SQL Server. El modelo es un modelo lineal generalizado simple (GLM) que predice la probabilidad de que un vehículo se haya equipado con una transmisión manual. Usará el `mtcars` conjunto de DataSet incluido con R.

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Verify r existe en SQL Server](quickstart-r-verify.md), se proporciona información y vínculos para configurar el entorno de r necesario para esta guía de inicio rápido.

## <a name="create-the-source-data"></a>Crear el origen de datos

En primer lugar, cree una tabla para guardar los datos de entrenamiento.

```sql
CREATE TABLE dbo.MTCars(
    mpg decimal(10, 1) NOT NULL,
    cyl int NOT NULL,
    disp decimal(10, 1) NOT NULL,
    hp int NOT NULL,
    drat decimal(10, 2) NOT NULL,
    wt decimal(10, 3) NOT NULL,
    qsec decimal(10, 2) NOT NULL,
    vs int NOT NULL,
    am int NOT NULL,
    gear int NOT NULL,
    carb int NOT NULL
);
```

A continuación, inserte los datos de la compilación en `mtcars`el conjunto de datos.

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ A algunas personas les gusta usar tablas temporales, pero tenga en cuenta que algunos clientes de R desconectan las sesiones entre los lotes.

+ El runtime de R incluye muchos conjuntos de datos, pequeños y grandes. Para obtener una lista de los conjuntos de datos instalados en R, escriba `library(help="datasets")` desde un símbolo del sistema de R.

## <a name="create-a-model"></a>Crear un modelo

Los datos de velocidad del automóvil contienen dos columnas, numéricas,`hp`de potencia ()`wt`y ponderación (). A partir de estos datos, creará un modelo lineal generalizado (GLM) que calcula la probabilidad de que un vehículo se haya equipado con una transmisión manual.

Para compilar el modelo, debe definir la fórmula dentro del código de R y pasar los datos como un parámetro de entrada.

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

+ El primer argumento de `glm` es el parámetro de *fórmula* , que `am` define como dependiente `hp + wt`de.
+ Los datos de entrada se almacenan en la variable `MTCarsData`, que se rellena con la consulta SQL. Si no asigna un nombre específico a los datos de entrada, el nombre predeterminado de la variable sería _InputDataSet_.

## <a name="create-a-table-for-the-model"></a>Crear una tabla para el modelo

A continuación, almacene el modelo para que pueda volver a entrenarlo o usarlo para la predicción. El resultado de un paquete de R que crea un modelo suele ser un **objeto binario**. Por lo tanto, la tabla en la que se almacena el modelo debe proporcionar una columna de tipo **varbinary (Max)** .

```sql
CREATE TABLE GLM_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
```

## <a name="save-the-model"></a>Guardar el modelo

Para guardar el modelo, ejecute la siguiente instrucción de Transact-SQL para llamar al procedimiento almacenado, generar el modelo y guardarlo en una tabla.

```sql
INSERT INTO GLM_models(model)
EXEC generate_GLM;
```

Tenga en cuenta que si ejecuta este código por segunda vez, obtendrá este error:

```sql
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

Una opción para evitar este error consiste en actualizar el nombre de cada nuevo modelo. Por ejemplo, podría cambiar el nombre por algo más descriptivo e incluir el tipo de modelo, el día en que lo creó, etc.

```sql
UPDATE GLM_models
SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene un modelo, en la guía de inicio rápido final, aprenderá a generar predicciones a partir de él y a trazar los resultados.

> [!div class="nextstepaction"]
> [Inicio rápido: Predecir y trazar desde el modelo](quickstart-r-predict-from-model.md)