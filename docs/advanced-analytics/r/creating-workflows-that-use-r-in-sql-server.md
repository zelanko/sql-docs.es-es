---
title: Crear flujos de trabajo SSIS y de SSRS con R - SQL Server Machine Learning Services
description: Escenarios de integración de combinación de SQL Server Machine Learning Services y R Services, Reporting Services (SSRS) y SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5d480b7cd24200b051fa2626fc41fa757703eaf8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642642"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Crear flujos de trabajo SSIS y de SSRS con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo usar el script de R y Python incrustado utilizando las capacidades de ciencia de datos y lenguaje de SQL Server Machine Learning Services con dos características importantes de SQL Server: SQL Server Integration Services (SSIS) y SQL Server Reporting Services SSRS. Bibliotecas de R y Python en SQL Server proporcionan funciones estadísticas y predictivas. SSIS y SSRS proporcionan coordinada transformación de ETL y visualizaciones, respectivamente. En este artículo se explica cómo colocar todas estas características conjuntamente en este patrón de flujo de trabajo:

> [!div class="checklist"]
> * Crear un procedimiento almacenado que contiene el ejecutable de R o Python
> * Ejecutar el procedimiento almacenado desde SSIS o en SSRS

Los ejemplos de este artículo son principalmente sobre R y SSIS, pero los conceptos y pasos se aplican igualmente a Python. La segunda sección proporciona instrucciones y vínculos para las visualizaciones de SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Usar SSIS para la automatización

Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro lenguaje. Pero ejecutar estos flujos de trabajo con datos empresariales requiere una integración perfecta con procesos y herramientas de ETL.

Dado que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] le permite realizar operaciones complejas en R a través de Transact-SQL y procedimientos almacenados, puede integrar las tareas de ciencia de datos con los procesos ETL existentes. En lugar de realizar una cadena de tareas de gran cantidad de memoria, preparación de datos puede optimizarse mediante las herramientas más eficaces, incluidas [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Estas son algunas ideas sobre cómo automatizar el procesamiento de datos y modelado de canalizaciones mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Extraer los datos en el entorno local o en la nube orígenes para generar datos de entrenamiento 
+ Compilar y ejecutar los modelos de R o Python como parte de un flujo de trabajo de integración de datos
+ Volver a entrenar modelos de forma regular (programado)
+ Cargar resultados del script de R o Python a otros destinos, como Excel, Power BI, Oracle y Teradata, por nombrar algunos
+ Utilice las tareas SSIS para crear características de datos en la base de datos SQL
+ Usar bifurcaciones condicionales para cambiar el contexto de proceso para trabajos de R y Python

## <a name="ssis-example"></a>Ejemplo SSIS

El ejemplo siguiente se origina desde una entrada de blog MSDN ya retirado creada por Jimmy Wong en esta dirección URL: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

En este ejemplo se muestra cómo automatizar las tareas con SSIS. Crear procedimientos almacenados con incrustado R con SQL Server Management Studio y, a continuación, ejecute los procedimientos almacenados de [tareas Ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) en un paquete SSIS.

Para seguir los pasos de este ejemplo, debe estar familiarizado con Management Studio, SSIS, Diseñador SSIS, diseño de paquete y T-SQL. El paquete SSIS usa tres [tareas Ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) que insertar los datos de entrenamiento en una tabla, los datos de modelo y puntuar los datos para obtener un resultado de predicción.

### <a name="load-training-data"></a>Cargar datos de entrenamiento

Ejecute el siguiente script en SQL Server Management Studio para crear una tabla para almacenar los datos. Debe crear y usar una base de datos de prueba para este ejercicio. 

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

Crear un procedimiento almacenado que carga los datos de entrenamiento en la trama de datos. Este ejemplo usa el conjunto de datos de Iris integrado. 

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

En el Diseñador SSIS, cree un [tarea Ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que ejecuta el procedimiento almacenado que acaba de definir. La secuencia de comandos para **SQLStatement** quita los datos existentes, especifica los datos que se va a insertar y, a continuación, llama al procedimiento almacenado para proporcionar los datos.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Insertar datos](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "insertar datos")

### <a name="generate-a-model"></a>Generar un modelo

Ejecute el siguiente script en SQL Server Management Studio para crear una tabla que almacena un modelo. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

Crear un procedimiento almacenado que genera un modelo lineal con [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Bibliotecas de RevoScaleR y revoscalepy están disponibles automáticamente en las sesiones de R y Python en SQL Server, por lo que no es necesario para importar la biblioteca.

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

En el Diseñador SSIS, cree un [tarea Ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) para ejecutar el **generate_iris_rx_model** procedimiento almacenado. El modelo se serializa y se guarda en la tabla ssis_iris_models. La secuencia de comandos para **SQLStatement** es como sigue:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Genera un modelo lineal](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "genera un modelo lineal")

Como un punto de control, una vez finalizada esta tarea, puede consultar el ssis_iris_models que contiene un modelo binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Predecir los resultados (puntuación) mediante el modelo de "aprendizaje"

Ahora que tiene código que carga los datos de entrenamiento y genera un modelo, el único paso izquierda es usar el modelo para generar predicciones. 

Para ello, coloque el script de R en la consulta SQL para desencadenar la [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) función integrada de R en ssis_iris_model. Llama un procedimiento almacenado **predict_species_length** lleva a cabo esta tarea.

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

En el Diseñador SSIS, cree un [tarea Ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que se ejecuta el **predict_species_length** procedimiento almacenado para generar la longitud del pétalo previstos.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Generar predicciones](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "generar predicciones")

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