---
title: Crear flujos de trabajo SSIS y de SSRS con R - SQL Server Machine Learning Services
description: Escenarios de integración de combinación de SQL Server Machine Learning Services y R Services, Reporting Services (SSRS) y SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76ddf3e3fdb43fea6bb8fd224f8199cda4134b64
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976305"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Crear flujos de trabajo SSIS y de SSRS con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo utilizar procedimientos almacenados en SQL Server Reporting Services SSRS, SQL Server Integration Services (SSIS) y dos características importantes de SQL Server de manera que combina datos relacionales, las funciones de ciencia de datos de las bibliotecas de Microsoft R y las características de BI para las transformaciones de datos coordinados y visualización. Obtenga información sobre qué funcionalidades de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se prestan a una solución de ciencia de datos. En este artículo también te recuerda que código y los datos en SQL Server, por ejemplo, el código R incrustado en procedimientos almacenados, se pueda usar fácilmente en las visualizaciones proporcionadas en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

## <a name="bring-compute-power-to-the-data"></a>Traiga la potencia de proceso a los datos

Ha sido un objetivo de diseño clave de la integración de R y Python con SQL Server genere análisis cerca de los datos. Esto ofrece varias ventajas:

+ Seguridad de datos. Volver a poner más cerca de R para el origen de datos evita el movimiento de datos de una pérdida de tiempo o no seguros.
+ Velocidad. Las bases de datos están optimizadas para operaciones basadas en conjuntos. Las recientes innovaciones realizadas en bases de datos como tablas en memoria los resúmenes y agregaciones con suma y están a un complemento perfecto para ciencia de datos.
+ Facilidad de integración e implementación. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el punto central de operaciones para muchas otras tareas de administración de datos y aplicaciones. Con datos que residen en la base de datos o el almacén de informes, se asegura de que los datos utilizados por las soluciones de aprendizaje automático son coherentes y están actualizados. 
+ Eficiencia en la nube y locales. En lugar de procesar datos en R, puede confiar en las canalizaciones de datos empresariales incluidos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y Azure Data Factory. Los informes de análisis o de resultados son sencillos a través de Power BI o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Si usan la combinación adecuada de SQL y R para distintas tareas de procesamiento y análisis de datos, los científicos de datos y los desarrolladores lograrán ser más productivos.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-data-transformation-and-automation"></a>Usar SSIS para la automatización y la transformación de datos

Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro lenguaje. Pero ejecutar estos flujos de trabajo con datos empresariales requiere una integración perfecta con procesos y herramientas de ETL.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite realizar operaciones complejas en R a través de Transact-SQL y de procedimientos almacenados, se pueden integrar las tareas específicas de R con los procesos de ETL existentes sin tener que emplear tiempo en volver a desarrollar. En lugar de seguir una cadena de tareas de gran cantidad de memoria de R, preparación de datos puede optimizarse mediante las herramientas más eficaces, incluyendo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Estas son algunas ideas sobre cómo automatizar el procesamiento de datos y modelado de canalizaciones mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tareas para crear características de los datos necesarios en la base de datos SQL
+ Usar bifurcaciones condicionales para alternar el contexto de ejecución de trabajos de R
+ Ejecutar trabajos de R que generan sus propios datos en la base de datos y compartir datos con aplicaciones
+ Cuando se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cargue el script de R guardado en una variable de texto y ejecutarlo en SQL Server

## <a name="ssis-example"></a>Ejemplo SSIS

El ejemplo siguiente se origina desde una entrada de blog MSDN ya retirado creada por Jimmy Wong en esta dirección URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`.

En este ejemplo se muestra cómo automatizar las tareas con SSIS. Crear procedimientos almacenados con incrustado R con SQL Server Management Studio y, a continuación, ejecute los procedimientos almacenados de [tareas Ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) en un paquete SSIS.

Para seguir los pasos de este ejemplo, debe estar familiarizado con Management Studio, SSIS, Diseñador SSIS, diseño de paquete y T-SQL. El paquete SSIS usa tres [tareas Ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) que insertar los datos de entrenamiento en una tabla, los datos de modelo y puntuar los datos para obtener un resultado de predicción.

### <a name="create-tables"></a>Crear tablas

Ejecute el siguiente script en SQL Server Management Studio para crear unas cuantas tablas: uno para almacenar los datos y otro para almacenar un modelo. El rol de la tabla ssis_iris es para que actúe como datos de entrenamiento en un escenario de puesta en marcha. 

```T-SQL
Use irissql
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

### <a name="create-a-stored-procedure-that-loads-training-data"></a>Crear un procedimiento almacenado que carga datos de entrenamiento

Este script crea un procedimiento almacenado que carga Iris en una trama de datos mediante el conjunto de datos de R integrado.

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

### <a name="define-an-execute-sql-task-that-refreshes-the-model"></a>Definir una tarea Ejecutar SQL que actualiza el modelo

En el Diseñador SSIS, cree un [tarea Ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task).

![Insertar datos](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "insertar datos")

La secuencia de comandos para SQLStatement es como sigue. La secuencia de comandos quita los datos existentes y, a continuación, vuelve a cargar nuevos datos mediante la **load_iris** que creó en el paso anterior del procedimiento almacenado.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

### <a name="create-a-stored-procedure-that-generates-a-model"></a>Crear un procedimiento almacenado que genera un modelo

Este procedimiento almacenado es código que crea un modelo lineal con [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Bibliotecas de RevoScaleR y revoscalepy se cargan automáticamente en las sesiones de R y Python en SQL Server.

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

### <a name="define-an-execute-sql-task-that-runs-the-model-generation-stored-procedure"></a>Definir una tarea Ejecutar SQL que se ejecuta el procedimiento almacenado de generación de modelos

En este paso, [tarea Ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) ejecuta el **generate_iris_rx_model** procedimiento almacenado, crear el modelo e insertarlos en la tabla ssis_iris_models.

![Genera un modelo lineal](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "genera un modelo lineal")

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

Una vez finalizada esta tarea, puede consultar el ssis_iris_models que contiene un modelo binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Predecir los resultados (puntuación) mediante el modelo de "aprendizaje"

En este ejemplo sencillo, la suposición es que ssis_iris_model es un modelo entrenado. Puesto que es el propósito de un modelo entrenado generar predicciones, ahora estamos preparados ejecutar una predicción con él. 

Para ello, coloque el script de R en la consulta SQL para desencadenar la [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) función integrada de R en ssis_iris_model. Llama un procedimiento almacenado en SQL Server **predict_species_length** lleva a cabo esta tarea.

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

### <a name="define-an-execute-sql-task-that-predicts-outcomes"></a>Definir una tarea Ejecutar SQL que prediga los resultados

Uso de [tarea Ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task), ejecute el **predict_species_length** procedimiento almacenado para generar la longitud del pétalo predicho.

![Generar predicciones](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "generar predicciones")

```T-SQL
exec predict_species_length 'rxLinMod';
```

### <a name="run-the-solution"></a>Ejecutar la solución

En el Diseñador SSIS, presione F5 para ejecutar el paquete. Debería ver un resultado similar a la captura de pantalla siguiente.

![F5 para ejecutar en modo de depuración](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 para ejecutar en modo de depuración")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Usar SSRS para las visualizaciones

Aunque R puede crear gráficos y visualizaciones interesantes, no está bien integrada con orígenes de datos externos, lo que significa que cada gráfico debe representarse individualmente. El uso compartido también puede ser difícil.

Mediante el uso de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], puede ejecutar operaciones complejas en R a través [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados, que pueden utilizarse fácilmente en una variedad de herramientas, incluidas de informes empresariales [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y Power BI.

### <a name="ssrs-example"></a>Ejemplo SSRS

[R Graphics Device for Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/) (Dispositivo gráfico de R para Microsoft Reporting Services [SSRS])

Este proyecto CodePlex proporciona el código que le ayudarán a crear un elemento de informe personalizado que representa el resultado de gráficos de R como una imagen que se puede usar en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informes.  Mediante el elemento de informe personalizado se puede:

+ Publicar gráficos y trazados creados con el dispositivo gráfico de R en paneles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Pasar parámetros de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a trazados de R

> [!NOTE]
> Para este ejemplo, el código que admite el dispositivo de gráficos de R para Reporting Services debe instalarse en el servidor de Reporting Services, así como en Visual Studio. También se requiere la configuración y compilación manual.

## <a name="next-steps"></a>Pasos siguientes

Los ejemplos SSIS y SSRS en este artículo muestran dos casos de la ejecución de procedimientos almacenados que contengan scripts de R o Python incrustado. Un punto clave es que puede realizar el script de R o Python disponibles en cualquier aplicación o herramienta que puede enviar una solicitud de ejecución en un procedimiento almacenado. Una conclusión adicional para SSIS es que puede crear paquetes que automatizan y programación la amplia gama de operaciones, como la adquisición de datos, limpieza, manipulación y así sucesivamente, con R o Python funcionalidad de ciencia de datos incluida en la cadena de operaciones. Para obtener más información e ideas, consulte [código Operacionalización de R mediante procedimientos almacenados en SQL Server Machine Learning Services](operationalizing-your-r-code.md).