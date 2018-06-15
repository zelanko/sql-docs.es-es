---
title: Predecir y trazar de modelo (R en Inicio rápido de SQL) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3809b8f6dbf84de04b84c7f4a6bdd5c492e2bdcd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202837"
---
# <a name="predict-and-plot-from-model-r-in-sql-quickstart"></a>Predecir y trazar de modelo (R en Inicio rápido de SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para realizar _puntuación_ con los nuevos datos, uno de los modelos entrenados obtener de la tabla y, a continuación, llamar a un nuevo conjunto de datos en el que se va a basar las predicciones. La puntuación es un término utilizado en la ciencia de datos a veces significa generar predicciones, las probabilidades u otros valores basadas en datos que se pasa a un modelo entrenado.

## <a name="create-the-table-of-new-speeds"></a>Crear la tabla de nuevas velocidades

¿Se ha dado cuenta de que los datos de entrenamiento originales se detienen a una velocidad de 25 millas por hora? Eso se debe a que los datos originales se basan en un experimento realizado en... ¡1920!

Quizás se pregunte, ¿cuánto tiempo tardaría un automóvil de los años 20 en detenerse, suponiendo que pueda alcanzar una velocidad de 60 o de incluso 100 millas por hora? Para responder a esta pregunta, debe proporcionar algunos nuevos valores de velocidad.

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

En este ejemplo, dado que el modelo se basa en el **rxLinMod** algoritmo que se proporcionan como parte de la **RevoScaleR** paquete, se llama a la [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) función, en lugar de la R genérico `predict` función.

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
    , @input_data_1 = N' SELECT speed FROM [dbo].[NewCarSpeed] '
    , @input_data_1_name = N'NewCarData'
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ Use una instrucción SELECT para obtener un único modelo de la tabla y páselo como un parámetro de entrada.
+  Después de recuperar el modelo de la tabla, llame a la función `unserialize` en el modelo.

    > [!TIP] 
    > También consulte el nuevo [funciones de serialización](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) proporcionada por RevoScaleR, que son compatibles con [en tiempo real de puntuación](../../advanced-analytics/real-time-scoring.md).
+  Use la función `rxPredict` con los argumentos adecuados para el modelo y proporcione los nuevos datos de entrada.
+  En el ejemplo, el `str` se agrega la función durante la fase de prueba, para comprobar el esquema de datos que se devuelven desde R. Puede quitar la instrucción más tarde.
+ Los nombres de columna utilizados en el script de R no son necesariamente pasa a la salida del procedimiento almacenado. Aquí hemos usado la cláusula con resultados para definir algunos nombres de columna nueva.

**Resultado**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>Realizar la puntuación en paralelo

Las predicciones se obtuvieron con bastante rapidez en este pequeño conjunto de datos. Pero ¿y si necesita realizar una gran cantidad de predicciones a gran velocidad? Hay muchas maneras de acelerar las operaciones de SQL Server, más si las operaciones se pueden procesar en paralelo. Para puntuar en particular, una forma muy sencilla de hacerlo consiste en agregar el parámetro *@parallel* a `sp_execute_external_script` y establecer el valor en **1**.

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

+ La ejecución en paralelo suele proporciona ventajas solamente cuando se trabaja con datos muy grandes. El motor de base de datos SQL podría decidir que no es necesaria la ejecución en paralelo. Además, la consulta SQL que obtiene los datos debe ser capaz de generar un plan de consulta paralelo.

+ Si usa la opción de ejecución en paralelo, **debe** especificar el esquema de resultados de salida de antemano con la cláusula WITH RESULT SETS. Especificar el esquema de salida de antemano permite a SQL Server agregar los resultados de varios conjuntos de datos en paralelo que, de otro modo, podrían tener esquemas desconocidos.

+ Si está *entrenamiento* un modelo en lugar de *puntuación*, este parámetro no tiene a menudo un efecto. Según el tipo de modelo, la creación del modelo puede requerir que se deban leer todas las filas para poder crear resúmenes.

+ Para obtener las ventajas del procesamiento en paralelo cuando se entrena el modelo, se recomienda que realice uno de los **RevoScaleR** algoritmos. Estos algoritmos están diseñados para distribuir el procesamiento de forma automática, incluso si no se especifica <code>@parallel =1</code> en la llamada a `sp_execute_external_script`. Para obtener instrucciones sobre cómo obtener el mejor rendimiento con RevoScaleR algoritmos, vea [distribuida y la informática en paralelo con ScaleR en Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).

## <a name="create-an-r-plot-of-the-model"></a>Crear un trazado de R del modelo

Muchos clientes, incluido SQL Server Management Studio, no pueden mostrar directamente los trazados creados con [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). En su lugar, el proceso general para la generación de trazados de R es crear el gráfico como parte del código R y, a continuación, escribir la imagen en un archivo.

Como alternativa, puede devolver el objeto de trazado binario serializado para cualquier aplicación que pueda mostrar imágenes.

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
+ Argumentos de `tempfile`, puede especificar un prefijo y extensión de archivo, así como el directorio. Para comprobar el nombre completo del archivo y ruta de acceso, imprimir un mensaje utilizando `str()`.
+ La función `jpeg` crea un dispositivo de R con los parámetros especificados.
+ Después de crear el gráfico, puede agregar más características visuales a él. En este caso, se agrega una línea de regresión mediante `abline`.
+ Cuando termine de agregar características de trazado, debe cerrar el dispositivo de gráficos con la función `dev.off()`.
+ La función `readBin` toma un archivo para leerlo, una especificación de formato y el número de registros. El `rb`**' palabra clave indica que el archivo es binario en lugar de texto.

**Resultado**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

Si quiere obtener unos trazados más elaborados, usando para ello algunos de los fantásticos paquetes de gráficos de R, le recomendamos estos artículos. En ambos se requiere el popular paquete **ggplot2**.

+ [Loan Classification using SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/) (Clasificación de préstamos con SQL Server 2016 R Services): escenario completo basado en datos sobre seguros. Requiere la **cambiar la forma de** paquete.
+ [Crear gráficos y los gráficos con R](../../advanced-analytics/tutorials/walkthrough-create-graphs-and-plots-using-r.md)

## <a name="conclusions"></a>Conclusiones

La integración de R con SQL Server hace que sea más fácil implementar soluciones de R a escala (gracias a las mejores características de R y de las bases de datos relacionales) para controlar los datos de alto rendimiento y los análisis rápidos de R. 

Consulte estos recursos adicionales para ver más ejemplos de R:

+  [Tutoriales de SQL Server R](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Seguir obteniendo información acerca de las soluciones con R con SQL Server, a través de los escenarios de extremo a extremo creados por los equipos de desarrollo de ciencia de datos de Microsoft y R Services.

+ [Tutoriales de SQL Server Python](../../advanced-analytics/tutorials/sql-server-python-tutorials.md)

    Para SQL Server 2017, use las posibilidades de contexto de proceso remoto y el algoritmo escalable con el lenguaje de Python.

+ [Tutoriales y los datos de ejemplo de Microsoft R](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    Obtenga información acerca de cómo usar los nuevos paquetes de RevoScaleR para crear modelos y transformar datos.

+ [Empezar a trabajar con MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

    Más información acerca de la máquina rápida y escalable algoritmos de Microsoft Research de aprendizaje.
