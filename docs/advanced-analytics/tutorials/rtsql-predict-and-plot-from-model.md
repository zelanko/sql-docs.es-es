---
title: Guía de inicio rápido para predecir y trazar desde el modelo mediante R en SQL Server Machine Learning | Microsoft Docs
description: En este tutorial, obtenga información sobre la puntuación mediante un modelo creado previamente en los datos de R y SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 60e152948945f4e86cc1114ae7b20c0e48b403bf
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086657"
---
# <a name="quickstart-predict-and-plot-from-model-using-r-in-sql-server"></a>Inicio rápido: Predecir y trazar desde el modelo mediante R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial, use el modelo que creó en el tutorial anterior para puntuar predicciones basadas en datos actualizados. Para realizar _puntuación_ con nuevos datos, obtener uno de los modelos entrenados de la tabla y, a continuación, llamar a un nuevo conjunto de datos en el que se va a basar las predicciones. La puntuación es un término usado en ocasiones, ciencia de datos significa generar predicciones, las probabilidades u otros valores según los nuevos datos que se introducen en un modelo entrenado.

## <a name="prerequisites"></a>Requisitos previos

Este inicio rápido es una extensión de [crear un modelo predictivo](rtsql-create-a-predictive-model-r.md).

## <a name="create-the-table-of-new-speeds"></a>Crear la tabla de nuevas velocidades

¿Se ha dado cuenta de que los datos de entrenamiento originales se detienen a una velocidad de 25 millas por hora? Eso se debe a que los datos originales se basan en un experimento realizado en... ¡1920!

Quizás se pregunte, ¿cuánto tiempo tardaría un automóvil de los años 20 en detenerse, suponiendo que pueda alcanzar una velocidad de 60 o de incluso 100 millas por hora? Para responder esta pregunta, debe proporcionar algunos valores de velocidad nuevos.

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>Predecir la distancia de parada

En este momento, la tabla puede contener varios modelos de R, todos creados con parámetros o algoritmos diferentes o entrenados a partir de distintos subconjuntos de datos.

![rsql_basictut_listofmodels](media/rsql-basictut-listofmodels.png)

Para obtener predicciones basadas en un modelo específico, debe escribir un script SQL que hace lo siguiente:

1. Obtener el modelo que quiere
2. Obtener los nuevos datos de entrada
3. Llamar a una función de predicción de R que sea compatible con ese modelo

En este ejemplo, porque el modelo se basa en el **rxLinMod** algoritmo proporcionada como parte de la **RevoScaleR** paquete, se llama a la [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) función, en lugar de R genérico `predict` función.

```sql
DECLARE @speedmodel varbinary(max) = (SELECT model FROM [dbo].[stopping_distance_models] WHERE model_name = 'latest model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            str(predicted.distance);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N'SELECT speed FROM [dbo].[NewCarSpeed]'
    , @input_data_1_name = N'NewCarData'
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ Use una instrucción SELECT para obtener un único modelo de la tabla y páselo como un parámetro de entrada.
+ Después de recuperar el modelo de la tabla, llame a la función `unserialize` en el modelo.

    > [!TIP] 
    > Consulte también el nuevo [funciones de serialización](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) proporcionada por RevoScaleR, que son compatibles con [de puntuación en tiempo real](../real-time-scoring.md).
+  Use la función `rxPredict` con los argumentos adecuados para el modelo y proporcione los nuevos datos de entrada.
+  En el ejemplo, el `str` se agrega la función durante la fase de pruebas para comprobar el esquema de datos que se devuelve desde R. Puede quitar la instrucción más tarde.
+ Los nombres de columna utilizados en el script de R no son necesariamente pasa a la salida del procedimiento almacenado. Aquí hemos usado la cláusula WITH RESULTS para definir algunos nuevos nombres de columna.

**Resultado**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>Realizar la puntuación en paralelo

Las predicciones se obtuvieron con bastante rapidez en este pequeño conjunto de datos. Pero ¿y si necesita realizar una gran cantidad de predicciones a gran velocidad? Hay muchas maneras de acelerar las operaciones en SQL Server, más si las operaciones se pueden procesar en paralelo. Para puntuar en particular, una sencilla forma consiste en agregar el *@parallel* parámetro en sp_execute_external_script y establezca el valor en **1**.

Supongamos que ha obtenido una tabla mucho más grande de posibles velocidades de automóvil, con cientos de miles de valores. En la comunidad hay muchos scripts T-SQL de ejemplo con los que podrá generar tablas de números, de modo que no los reproduciremos aquí. Supongamos simplemente que tiene una columna con muchos enteros y quiere usar esto como entrada para `speed` en el modelo.

Para ello, simplemente ejecutar la misma consulta de predicción, pero sustituya el conjunto de datos mayor y agregue el `@parallel = 1` argumento.

```sql
DECLARE @speedmodel varbinary(max) = (select model from [dbo].[stopping_distance_models] where model_name = 'default model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT [speed] FROM [dbo].[HugeTableofCarSpeeds] '
    , @input_data_1_name = N'NewCarData'
    , @parallel = 1
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ Ejecución en paralelo suele ofrece ventajas solo cuando se trabaja con datos muy grandes. El motor de base de datos SQL podría decidir que no es necesaria la ejecución en paralelo. Además, la consulta SQL que obtiene los datos debe ser capaz de generar un plan de consulta paralelo.

+ Si usa la opción de ejecución en paralelo, **debe** especificar el esquema de resultados de salida de antemano con la cláusula WITH RESULT SETS. Especificar el esquema de salida de antemano permite a SQL Server agregar los resultados de varios conjuntos de datos en paralelo que, de otro modo, podrían tener esquemas desconocidos.

+ Si estás *entrenamiento* un modelo en lugar de *puntuación*, este parámetro a menudo no tendrá efecto. Según el tipo de modelo, la creación del modelo puede requerir que se deban leer todas las filas para poder crear resúmenes.

+ Para obtener las ventajas del procesamiento en paralelo al entrenar el modelo, se recomienda que utilice uno de los **RevoScaleR** algoritmos. Estos algoritmos están pensados para distribuir el procesamiento automáticamente, incluso si no se especifica <code>@parallel =1</code> en la llamada a `sp_execute_external_script`. Para obtener instrucciones sobre cómo obtener el mejor rendimiento con algoritmos RevoScaleR, vea [distribuida e informática en paralelo con ScaleR de Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).

## <a name="create-an-r-plot-of-the-model"></a>Crear un trazado de R del modelo

Muchos clientes, incluido SQL Server Management Studio, no pueden mostrar directamente los trazados creados con [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). En su lugar, el proceso general para generar trazados de R es crear el trazado como parte del código de R y, a continuación, escribir la imagen en un archivo.

Como alternativa, puede devolver el objeto de trazado binario serializado a cualquier aplicación que pueda mostrar imágenes.

Con el siguiente ejemplo se ilustra cómo crear un gráfico sencillo usando una función de trazado incluida de forma predeterminada con R. La imagen es la salida para el archivo especificado y, asimismo, la salida para una variable SQL por medio del procedimiento almacenado.

```sql
 EXECUTE sp_execute_external_script
 @language = N'R'
 , @script = N'
     imageDir <- ''C:\\temp\\plots'';
     image_filename = tempfile(pattern = "plot_", tmpdir = imageDir, fileext = ".jpg")
     print(image_filename);
     jpeg(filename=image_filename,  width=600, height = 800);
     print(plot(distance~speed, data=InputDataSet, xlab="Speed", ylab="Stopping distance", main = "1920 Car Safety"));
     abline(lm(distance~speed, data = InputDataSet));
     dev.off();
     OutputDataSet <- data.frame(data=readBin(file(image_filename, "rb"), what=raw(), n=1e6));
     '
  , @input_data_1 = N'SELECT speed, distance from [dbo].[CarSpeed]'
  WITH RESULT SETS ((plot varbinary(max)));
```

+ El `tempfile` función devuelve una cadena que puede usarse como un nombre de archivo, pero aún no ha generado el archivo.
+ Para los argumentos `tempfile`, puede especificar un prefijo y extensión de archivo, así como el directorio. Para comprobar el nombre completo del archivo y ruta de acceso, imprimir un mensaje mediante `str()`.
+ La función `jpeg` crea un dispositivo de R con los parámetros especificados.
+ Después de crear el trazado, puede agregar más características visuales a él. En este caso, se agrega una línea de regresión mediante `abline`.
+ Cuando termine de agregar características de trazado, debe cerrar el dispositivo de gráficos con la función `dev.off()`.
+ La función `readBin` toma un archivo para leerlo, una especificación de formato y el número de registros. El `rb`**' palabra clave indica que el archivo es binario, en lugar de texto.

**Resultado**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

Si quiere obtener unos trazados más elaborados, usando para ello algunos de los fantásticos paquetes de gráficos de R, le recomendamos estos artículos. En ambos se requiere el popular paquete **ggplot2**.

+ [Loan Classification using SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/) (Clasificación de préstamos con SQL Server 2016 R Services): escenario completo basado en datos sobre seguros. Requiere el **reshape** paquete.
+ [Crear gráficos y trazados con R](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="next-steps"></a>Pasos siguientes

La integración de R con SQL Server hace que sea más fácil implementar soluciones de R a escala (gracias a las mejores características de R y de las bases de datos relacionales) para controlar los datos de alto rendimiento y los análisis rápidos de R. 

Continuar aprendiendo sobre las soluciones de uso de R con SQL Server a través de escenarios de extremo a otro creados por los equipos de desarrollo de ciencia de datos de Microsoft y R Services.

> [!div class="nextstepaction"]
> [Tutoriales de SQL Server R](sql-server-r-tutorials.md)
