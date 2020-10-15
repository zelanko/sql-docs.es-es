---
title: Creación de flujos de trabajo de SSIS y SSRS con R
description: Escenarios de integración en los que se combina SQL Server Machine Learning Services y R Services, Reporting Services (SSRS) y SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/28/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ea99f736af30fb1989bd8728896bed3f12c4c59c
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956640"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Creación de flujos de trabajo de SSIS y SSRS con R en SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

En este artículo se explica cómo usar scripts insertados de R y Python mediante las capacidades de ciencia de datos y lenguaje de SQL Server Machine Learning Services, con dos características de SQL Server importantes: SQL Server Integration Services (SSIS) y SQL Server Reporting Services (SSRS). Las bibliotecas de R y Python en SQL Server proporcionan funciones estadísticas y predictivas. SSIS y SSRS proporcionan de manera coordinada transformaciones de ETL y visualizaciones, respectivamente. En este artículo se explica cómo aglutinar todas estas características en este patrón de flujo de trabajo:

> [!div class="checklist"]
> * Crear un procedimiento almacenado que contenga R o Python ejecutable
> * Ejecutar el procedimiento almacenado desde SSIS o SSRS

Los ejemplos de este artículo se centran principalmente en R y SSIS, pero los conceptos y los pasos son igualmente válidos en Python. En la segunda sección se facilitan instrucciones y vínculos relativos a las visualizaciones de SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Uso de SSIS para la automatización

Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro lenguaje. Pero ejecutar estos flujos de trabajo con datos empresariales requiere una integración perfecta con procesos y herramientas de ETL.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite realizar operaciones complejas en R a través de Transact-SQL y de procedimientos almacenados, se pueden integrar tareas de ciencia de datos con los procesos de ETL existentes. En lugar de realizar una cadena de tareas que usan mucha memoria, la preparación de datos puede optimizarse a través de las herramientas más eficaces, incluyendo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Estas son algunas ideas de cómo automatizar las canalizaciones de modelado y procesamiento de datos mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Extraer datos de orígenes locales o de la nube para generar datos de entrenamiento 
+ Compilar y ejecutar modelos de R o de Python como parte de un flujo de trabajo de integración de datos
+ Volver a entrenar modelos de forma periódica (programada)
+ Cargar resultados desde el script de R o de Python en otros destinos como, entre otros, Excel, Power BI, Oracle y Teradata
+ Usar tareas de SSIS para crear características de datos en la base de datos SQL
+ Usar bifurcaciones condicionales para alternar el contexto de ejecución de trabajos de R y de Python

## <a name="ssis-example"></a>Ejemplo de SSIS

En el siguiente ejemplo se extrae de una publicación de blog de MSDN ya retirada que creó Jimmy Wong en esta dirección URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

En él se muestra cómo automatizar tareas mediante SSIS. Hay que crear procedimientos almacenados con R insertado mediante SQL Server Management Studio y, después, ejecutar esos procedimientos almacenados desde [tareas Ejecutar instrucción T-SQL](../../integration-services/control-flow/execute-t-sql-statement-task.md) en un paquete SSIS.

Para realizar este ejemplo paso a paso, hay que estar familiarizado con Management Studio, SSIS, el Diseñador SSIS, el diseño de paquetes y T-SQL. El paquete SSIS usa tres [tareas Ejecutar instrucción T-SQL](../../integration-services/control-flow/execute-t-sql-statement-task.md) que insertan datos de entrenamiento en una tabla, modelan los datos y los puntúan para obtener la salida de predicción.

### <a name="load-training-data"></a>Carga de los datos de entrenamiento

Ejecute el siguiente script en SQL Server Management Studio para crear una tabla donde almacenar los datos. En este ejercicio, conviene crear y usar una base de datos de prueba. 

```T-SQL
Use test-db
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO
```

Cree un procedimiento almacenado que cargue datos de entrenamiento en el tramo de datos. En este ejemplo se usa el conjunto de datos de Iris integrado. 

```T-SQL
Create procedure load_iris
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'iris_df <- iris;'
        , @input_data_1 = N''
        , @output_data_1_name = N'iris_df'
    with result sets (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100)));
end;
```

En el Diseñador SSIS, cree una [tarea Ejecutar SQL](../../integration-services/control-flow/execute-sql-task.md) que ejecute el procedimiento almacenado que acaba de definir. El script de **SQLStatement** quita los datos existentes, especifica qué datos deben insertarse y, después, llama al procedimiento almacenado para que se faciliten los datos.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Inserción de datos](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "Insertar datos")

### <a name="generate-a-model"></a>Generación de un modelo

Ejecute el siguiente script en SQL Server Management Studio para crear una tabla para almacenar un modelo. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

Use [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) para crear un procedimiento almacenado que genere un modelo. Las bibliotecas RevoScaleR y revoscalepy están disponibles automáticamente en las sesiones de R y de Python en SQL Server, por lo que no es necesario importarlas.

```T-SQL
Create procedure generate_iris_rx_model
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'
          irisLinMod <- rxLinMod(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = ssis_iris);
          trained_model <- data.frame(payload = as.raw(serialize(irisLinMod, connection=NULL)));'
        , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris'
        , @input_data_1_name = N'ssis_iris'
        , @output_data_1_name = N'trained_model'
    with result sets ((model varbinary(max)));
end;
GO
```

En el Diseñador SSIS, cree una [tarea Ejecutar SQL](../../integration-services/control-flow/execute-sql-task.md) para ejecutar el procedimiento almacenado **generate_iris_rx_model**. El modelo se serializa y se guarda en la tabla ssis_iris_models. El script de **SQLStatement** es el siguiente:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Generación de un modelo lineal](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "Generación de un modelo lineal")

Como punto de control, cuando esta tarea se complete, se puede consultar la tabla ssis_iris_models para comprobar si contiene un modelo binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Predicción (puntuación) de resultados a través del modelo "entrenado"

Ahora que ya tenemos código que carga los datos de entrenamiento y genera un modelo, el único paso que queda es usar ese modelo para generar predicciones. 

Para ello, coloque el script de R en la consulta SQL para desencadenar la función de R integrada [rxPredict](//machine-learning-server/r-reference/revoscaler/rxpredict) en ssis_iris_model. Un procedimiento almacenado llamado **predict_species_length** lleva a cabo esta tarea.

```T-SQL
Create procedure predict_species_length (@model varchar(100))
as
begin
    declare @rx_model varbinary(max) = (select model from ssis_iris_models where model_name = @model);
    -- Predict based on the specified model:
    exec sp_execute_external_script
        @language = N'R'
        , @script = N'
irismodel <-unserialize(rx_model);
irispred <- rxPredict(irismodel, ssis_iris[,2:6]);
OutputDataSet <- cbind(ssis_iris[1], irispred$Sepal.Length_Pred, ssis_iris[2]);
colnames(OutputDataSet) <- c("id", "Sepal.Length.Actual", "Sepal.Length.Expected");
#OutputDataSet <- subset(OutputDataSet, Species.Length.Actual != Species.Expected);
'
    , @input_data_1 = N'
    select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris
    '
    , @input_data_1_name = N'ssis_iris'
    , @params = N'@rx_model varbinary(max)'
    , @rx_model = @rx_model
    with result sets ( ("id" int, "Species.Length.Actual" float, "Species.Length.Expected" float)
        );
end;
```

En el Diseñador SSIS, cree una [tarea Ejecutar SQL](../../integration-services/control-flow/execute-sql-task.md) que ejecute el procedimiento almacenado **predict_species_length** para generar la longitud de pétalo prevista.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Generación de predicciones](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "Generación de predicciones")

### <a name="run-the-solution"></a>Ejecución de la solución

En el Diseñador SSIS, presione F5 para ejecutar el paquete. Debería aparecer un resultado similar al de la siguiente captura de pantalla.

![F5 para la ejecución en modo de depuración](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 para la ejecución en modo de depuración")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Uso de SSRS para visualizaciones

Aunque R puede crear gráficos y visualizaciones interesantes, no se integra bien con orígenes de datos externos, lo que significa que cada gráfico debe representarse individualmente. El uso compartido también puede ser difícil.

Con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se pueden ejecutar operaciones complejas en R mediante procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)], que muchas herramientas de informes empresariales pueden usar sin problemas, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y Power BI.

## <a name="next-steps"></a>Pasos siguientes

Los ejemplos de SSIS y de SSRS de este artículo muestran dos casos de ejecución de procedimientos almacenados que contienen scripts de R o de Python insertados. Una ventaja fundamental es que puede hacer que el script de R o de Python esté disponible para cualquier aplicación o herramienta capaz de enviar una solicitud de ejecución en un procedimiento almacenado. Una ventaja extra en el caso de SSIS es que puede crear paquetes que automaticen y programen una amplia gama de operaciones (como la adquisición, limpieza y manipulación de datos, entre otras), con la funcionalidad de ciencia de datos de R o de Python incluida en la cadena de operaciones. Para más información y obtener ideas, vea [Operacionalización de código de R con procedimientos almacenados en SQL Server Machine Learning Services](operationalizing-your-r-code.md).