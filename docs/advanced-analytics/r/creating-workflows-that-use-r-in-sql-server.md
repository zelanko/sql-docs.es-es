---
title: Creación de flujos de trabajo de SSIS y SSRS con R
description: Escenarios de integración combinados SQL Server Machine Learning Services y R Services, Reporting Services (SSRS) y SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b8d55e95991437e4d76911fd26afb5b1bc9c550
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715173"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>Creación de flujos de trabajo de SSIS y SSRS con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se explica cómo usar scripts incrustados de R y Python con las funcionalidades de ciencia de datos y lenguaje de SQL Server Machine Learning Services con dos características SQL Server importantes: SQL Server Integration Services (SSIS) y SQL Server Reporting Services SSRS. Las bibliotecas de R y Python en SQL Server proporcionan funciones estadísticas y de predicción. SSIS y SSRS proporcionan una transformación y visualizaciones ETL coordinadas, respectivamente. En este artículo se explica cómo poner todas estas características juntas en este patrón de flujo de trabajo:

> [!div class="checklist"]
> * Crear un procedimiento almacenado que contenga R o Python ejecutable
> * Ejecutar el procedimiento almacenado desde SSIS o SSRS

Los ejemplos de este artículo son principalmente de R y SSIS, pero los conceptos y los pasos se aplican igualmente a Python. En la segunda sección se proporcionan instrucciones y vínculos para las visualizaciones de SSRS.

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>Usar SSIS para la automatización

Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro lenguaje. Pero ejecutar estos flujos de trabajo con datos empresariales requiere una integración perfecta con procesos y herramientas de ETL.

Dado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que le permite ejecutar operaciones complejas en R a través de Transact-SQL y procedimientos almacenados, puede integrar las tareas de ciencia de datos con los procesos ETL existentes. En lugar de realizar una cadena de tareas con un uso intensivo de la memoria, la preparación de los datos se puede [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] optimizar [!INCLUDE[tsql](../../includes/tsql-md.md)]con las herramientas más eficaces, incluidos y. 

A continuación se muestran algunas ideas sobre cómo automatizar el procesamiento de datos y las canalizaciones [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]de modelado mediante:

+ Extraer datos de orígenes locales o en la nube para generar datos de entrenamiento 
+ Compilar y ejecutar modelos de R o Python como parte de un flujo de trabajo de integración de datos
+ Reciclaje de modelos de forma regular (programada)
+ Cargue los resultados del script de R o Python en otros destinos como Excel, Power BI, Oracle y Teradata, por nombrar algunos
+ Usar tareas de SSIS para crear características de datos en SQL Database
+ Usar bifurcaciones condicionales para cambiar el contexto de proceso para trabajos de R y Python

## <a name="ssis-example"></a>Ejemplo de SSIS

El ejemplo siguiente se origina en una publicación de blog de MSDN retirada ahora creada por Jimmy Wong en esta dirección URL:`https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

En este ejemplo se muestra cómo automatizar tareas mediante SSIS. Cree procedimientos almacenados con R incrustado mediante SQL Server Management Studio y, a continuación, ejecute esos procedimientos almacenados desde [ejecutar tareas de T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) en un paquete SSIS.

Para recorrer este ejemplo, debe estar familiarizado con Management Studio, SSIS, el diseñador SSIS, el diseño de paquetes y T-SQL. El paquete SSIS usa tres [tareas ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) que insertan datos de entrenamiento en una tabla, modelan los datos y puntuan los datos para obtener la salida de predicción.

### <a name="load-training-data"></a>Cargar datos de entrenamiento

Ejecute el siguiente script en SQL Server Management Studio para crear una tabla para almacenar los datos. Debe crear y utilizar una base de datos de prueba para este ejercicio. 

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

Cree un procedimiento almacenado que cargue datos de entrenamiento en la trama de datos. Este ejemplo utiliza el conjunto de datos de iris integrado. 

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

En el diseñador SSIS, cree una [tarea ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que ejecute el procedimiento almacenado que acaba de definir. El script para **SQLStatement** quita los datos existentes, especifica los datos que se van a insertar y, a continuación, llama al procedimiento almacenado para proporcionar los datos.

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![Insertar datos](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "Insertar datos")

### <a name="generate-a-model"></a>Generar un modelo

Ejecute el siguiente script en SQL Server Management Studio para crear una tabla que almacene un modelo. 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

Cree un procedimiento almacenado que genere un modelo lineal mediante [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod). Las bibliotecas RevoScaleR y revoscalepy están disponibles automáticamente en las sesiones de R y Python en SQL Server por lo que no es necesario importar la biblioteca.

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

En el diseñador SSIS, cree una [tarea ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) para ejecutar el procedimiento almacenado **generate_iris_rx_model** . El modelo se serializa y se guarda en la tabla ssis_iris_models. El script para **SQLStatement** es el siguiente:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![Genera un modelo lineal](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "Genera un modelo lineal")

Como punto de control, una vez completada esta tarea, puede consultar el ssis_iris_models para ver que contiene un modelo binario.

### <a name="predict-score-outcomes-using-the-trained-model"></a>Resultados de predicción (puntuación) mediante el modelo "entrenado"

Ahora que tiene código que carga los datos de entrenamiento y genera un modelo, el único paso que queda es usar el modelo para generar predicciones. 

Para ello, coloque el script de R en la consulta SQL para desencadenar la función integrada de R de [rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) en ssis_iris_model. Un procedimiento almacenado denominado **predict_species_length** lleva a cabo esta tarea.

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

En el diseñador SSIS, cree una [tarea ejecutar SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task) que ejecute el procedimiento almacenado **predict_species_length** para generar la longitud de pétalo previsto.

```T-SQL
exec predict_species_length 'rxLinMod';
```

![Generar predicciones](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "Generar predicciones")

### <a name="run-the-solution"></a>Ejecutar la solución

En el diseñador SSIS, presione F5 para ejecutar el paquete. Debería ver un resultado similar al de la captura de pantalla siguiente.

![F5 para ejecutar en modo de] depuración (../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 para ejecutar en modo de") depuración

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>Usar SSRS para visualizaciones

Aunque R puede crear gráficos y visualizaciones interesantes, no se integra bien con orígenes de datos externos, lo que significa que cada gráfico o grafo debe generarse individualmente. El uso compartido también puede ser difícil.

Mediante el [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]uso de, puede ejecutar operaciones complejas en R [!INCLUDE[tsql](../../includes/tsql-md.md)] a través de procedimientos almacenados, que se pueden usar fácilmente en una gran variedad de herramientas [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de informes empresariales, entre las que se incluyen y Power BI.

### <a name="ssrs-example"></a>Ejemplo de SSRS

[R Graphics Device for Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/) (Dispositivo gráfico de R para Microsoft Reporting Services [SSRS])

Este proyecto de CodePlex proporciona el código para ayudarle a crear un elemento de informe personalizado que representa la salida de gráficos de R como una imagen que se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] puede usar en los informes.  Mediante el elemento de informe personalizado se puede:

+ Publicar gráficos y trazados creados con el dispositivo gráfico de R en paneles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Pasar parámetros de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a trazados de R

> [!NOTE]
> En este ejemplo, el código que admite el dispositivo de gráficos de R para Reporting Services debe estar instalado en el servidor de Reporting Services, así como en Visual Studio. También se requiere la configuración y compilación manual.

## <a name="next-steps"></a>Pasos siguientes

Los ejemplos de SSIS y SSRS de este artículo muestran dos casos de ejecución de procedimientos almacenados que contienen scripts de R o Python incrustados. Una ventaja clave es que puede hacer que el script de R o Python esté disponible para cualquier aplicación o herramienta que pueda enviar una solicitud de ejecución en un procedimiento almacenado. Una ventaja adicional para SSIS es que puede crear paquetes que automaticen y programen una amplia gama de operaciones, como la adquisición de datos, la limpieza, la manipulación, etc., con la funcionalidad de ciencia de datos de R o Python incluida en la cadena de operaciones. Para obtener más información e ideas, consulte [operacionalización de código R mediante procedimientos almacenados en SQL Server Machine Learning Services](operationalizing-your-r-code.md).