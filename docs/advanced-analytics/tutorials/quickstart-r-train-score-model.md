---
title: Crear y puntuar un modelo predictivo en R
titleSuffix: SQL Server Machine Learning Services
description: Cree un modelo predictivo simple en R mediante SQL Server Machine Learning Services y, a continuación, prediga un resultado con nuevos datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc968c9364f23826b366721590f72ac1b0af0391
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005977"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>Inicio rápido: Crear y puntuar un modelo predictivo en R con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, creará y entrenará un modelo predictivo con R, guardará el modelo en una tabla en la instancia de SQL Server y, a continuación, usará el modelo para predecir valores de datos nuevos con [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

El modelo que usará en esta guía de inicio rápido es un modelo lineal generalizado simple (GLM) que predice la probabilidad de que un vehículo se haya equipado con una transmisión manual. Usará el conjunto de **mtcars** que se incluye con R.

> [!TIP]
> Si necesita un actualizador en modelos lineales, pruebe este tutorial, en el que se describe el proceso de ajuste de un modelo mediante rxLinMod:  [Fitting Linear Models](/machine-learning-server/r/how-to-revoscaler-linear-model) (Ajuste de modelos lineales)

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el lenguaje R instalado.

  La instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripting externo está deshabilitada de forma predeterminada, por lo que es posible que tenga que [Habilitar el scripting externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y comprobar que **SQL Server Launchpad servicio** se está ejecutando antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de R. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-the-model"></a>Crear el modelo

Para crear el modelo, debe crear los datos de origen para el entrenamiento, crear el modelo y entrenarlo usando los datos y, a continuación, almacenar el modelo en una base de datos SQL, donde se puede usar para generar predicciones con nuevos datos.

### <a name="create-the-source-data"></a>Crear el origen de datos

1. Abra **SQL Server Management Studio** y conéctese a su instancia de SQL Server.

1. Cree una tabla para guardar los datos de entrenamiento.

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

1. Inserte los datos del conjunto de datos integrado `mtcars`.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > El runtime de R incluye muchos conjuntos de datos, pequeños y grandes. Para obtener una lista de los conjuntos de valores instalados con R, escriba `library(help="datasets")` desde un símbolo del sistema de R.

### <a name="create-and-train-the-model"></a>Crear y entrenar el modelo

Los datos de velocidad del automóvil contienen dos columnas, numéricas: potencia (`hp`) y peso (`wt`). A partir de estos datos, creará un modelo lineal generalizado (GLM) que calcula la probabilidad de que un vehículo se haya equipado con una transmisión manual.

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

- El primer argumento de `glm` es el parámetro de *fórmula* , que define `am` como dependiente de `hp + wt`.
- Los datos de entrada se almacenan en la variable `MTCarsData`, que se rellena con la consulta SQL. Si no asigna un nombre específico a los datos de entrada, el nombre predeterminado de la variable sería _InputDataSet_.

### <a name="store-the-model-in-the-sql-database"></a>Almacenar el modelo en la base de datos SQL

A continuación, almacene el modelo en una base de datos SQL para que pueda usarlo para la predicción o para volver a entrenarlo. 

1. Cree una tabla para almacenar el modelo.

   La salida de un paquete de R que crea un modelo suele ser un objeto binario. Por lo tanto, la tabla en la que se almacena el modelo debe proporcionar una columna de tipo **varbinary (Max)** .

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. Ejecute la siguiente instrucción Transact-SQL para llamar al procedimiento almacenado, generar el modelo y guardarlo en la tabla que creó.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > Si ejecuta este código por segunda vez, obtendrá este error: "Infracción de la restricción de clave principal... No se puede insertar una clave duplicada en el objeto DBO. stopping_distance_models ". Una opción para evitar este error consiste en actualizar el nombre de cada nuevo modelo. Por ejemplo, podría cambiar el nombre por algo más descriptivo e incluir el tipo de modelo, el día en que lo creó, etc.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>Puntuar nuevos datos con el modelo entrenado

La *puntuación* es un término que se usa en la ciencia de datos para hacer referencia a la generación de predicciones, probabilidades u otros valores basados en nuevos datos que se introducen en un modelo entrenado. Usará el modelo que creó en la sección anterior para puntuar las predicciones con los nuevos datos.

### <a name="create-a-table-of-new-data"></a>Crear una tabla de datos nuevos

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

### <a name="predict-manual-transmission"></a>Predicción de la transmisión manual

Para obtener las predicciones basadas en el modelo, escriba un script SQL que hace lo siguiente:

1. Obtener el modelo que quiere
1. Obtener los nuevos datos de entrada
1. Llamar a una función de predicción de R que sea compatible con ese modelo

Con el tiempo, la tabla puede contener varios modelos de R, todos creados con distintos parámetros o algoritmos, o entrenado en distintos subconjuntos de datos. En este ejemplo, usaremos el modelo denominado `default model`.

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

- Use una instrucción SELECT para obtener un único modelo de la tabla y páselo como un parámetro de entrada.

- Después de recuperar el modelo de la tabla, llame a la función `unserialize` en el modelo.

- Use la función `predict` con los argumentos adecuados para el modelo y proporcione los nuevos datos de entrada.

> [!NOTE]
> En el ejemplo, se agrega la función `str` durante la fase de prueba para comprobar el esquema de los datos que se devuelven desde R. Puede quitar la instrucción más adelante.
>
> Los nombres de columna utilizados en el script de R no se pasan necesariamente a la salida del procedimiento almacenado. Aquí se usa la cláusula WITH RESULTs para definir algunos nombres de columna nuevos.

**Resultado**

![Conjunto de resultados para predecir properbility de la transmisión manual](./media/r-predict-am-resultset.png)

También es posible usar la instrucción [PREDICT (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) para generar un valor de predicción o una puntuación basada en un modelo almacenado.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server Machine Learning Services, consulte:

- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
