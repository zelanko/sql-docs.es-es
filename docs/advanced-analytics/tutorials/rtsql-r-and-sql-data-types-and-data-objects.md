---
title: Guía de inicio rápido sobre los tipos de datos SQL y R y objetos (SQL Server Machine Learning) | Microsoft Docs
description: En este tutorial, obtenga información sobre cómo trabajar con tipos de datos y objetos de datos en R y SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2e861bf2d8daf2460fbffcf2d92fcd33f859cd78
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699131"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server"></a>Inicio rápido: Controlar los tipos de datos y objetos con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial, obtenga una introducción práctica a problemas comunes que se producen al mover datos entre R y SQL Server. La experiencia que obtenga a través de este ejercicio proporciona esencial en segundo plano cuando se trabaja con datos en su propio script.

Problemas comunes de saber anticipado incluyen:

+ A veces, los tipos de datos no coinciden
+ Pueden que se produzcan conversiones implícitas
+ A veces, se requieren operaciones de conversión
+ R y SQL usan objetos de datos distintos

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [Hello World en R y SQL](rtsql-using-r-code-in-transact-sql-quickstart.md), proporciona información y vínculos para configurar el entorno de R necesario para este inicio rápido.

## <a name="always-return-a-data-frame"></a>Siempre devuelve una trama de datos

Cuando el script devuelve resultados de R a SQL Server, debe devolverlos como una trama de datos (**data.frame**). Cualquier otro tipo de objeto que se genere en el script (sea una lista, un factor, un vector o datos binarios) debe convertirse en una trama de datos si se quiere incluir en los resultados del procedimiento almacenado. Por suerte, existen varias funciones de R con las que se pueden cambiar objetos en tramas de datos. Se puede incluso serializar un modelo binario y devolverlo en una trama de datos, algo que haremos más adelante en este tutorial.

En primer lugar, vamos a experimentar con algunos objetos básicos de R, vectores, matrices y listas y ver cómo la conversión a una trama de datos cambia el resultado pasado a SQL Server.

Comparar estos dos scripts de "Hello World" en R. Las secuencias de comandos son casi idénticos, pero el primero devuelve una sola columna de tres valores, mientras que el segundo devuelve tres columnas con un solo valor de cada uno.

**Ejemplo 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**Ejemplo 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identify-schema-and-data-types"></a>Identificar esquemas y tipos de datos

¿Por qué los resultados tan diferentes? 

La respuesta se suele hallar con el comando de R `str()`. Agregue la función `str(object_name)` en cualquier parte del script de R para que el esquema de datos del objeto de R especificado se devuelva como un mensaje informativo. Para ver los mensajes, consulte el panel **Mensajes** de Visual Studio Code o la pestaña **Mensajes** de SSMS.

Para averiguar por qué los resultados son diferentes en Example 1 y Example 2, inserte la línea `str(OutputDataSet)` al final de la definición de la variable _@script_ en cada instrucción, del modo siguiente:

**Ejemplo 1 con la función str agregado**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Ejemplo 2 con la función str agregado**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

Ahora, revise el texto en el panel **Mensajes** para ver por qué el resultado es diferente.

**Resultados de Example 1**

```
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Resultados de Example 2**

```
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Como se puede observar, un cambio mínimo en la sintaxis de R ha tenido un gran efecto en el esquema de los resultados. No entraremos en los motivos, porque las diferencias en los tipos de datos de R se explican pormenorizadamente en este artículo de Hadley Wickham: [estructuras de datos de R](https://adv-r.had.co.nz/Data-structures.html).

Por ahora, basta con saber que hay que comprobar los resultados esperados cuando convirtamos objetos de R en tramas de datos.

> [!TIP]
> 
> También puede usar las funciones de identidad de R, como `is.matrix`, `is.vector`para devolver información sobre la estructura de datos internos.

## <a name="implicit-conversion-of-data-objects"></a>Conversión implícita de objetos de datos

Cada objeto de datos de R tiene sus propias reglas sobre el tratamiento que se da a los valores cuando dicho objeto se combina con otro si ambos objetos de datos tienen el mismo número de dimensiones, o si cualquier objeto de datos contiene tipos de datos heterogéneos.

Por ejemplo, suponga que ejecute la siguiente instrucción para realizar la multiplicación de matrices mediante R. Multiplicar una matrix de una sola columna con los tres valores por una matriz con cuatro valores y esperan como resultado una matriz de 4 x 3.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

En realidad, la única columna de tres valores se convierte en una matriz de una sola columna. Dado que este es simplemente un caso especial de matriz de R, la matriz `y` se convierte implícitamente en una matriz de una sola columna para que los dos argumentos se ajusten.

**Resultado**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

Sin embargo, tenga en cuenta lo que sucede cuando se cambia el tamaño de la matriz `y`.

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

Esta vez, R devuelve un solo valor como resultado.

**Resultado**
    
|Col1|
|---|
|1542|

¿Por qué? En este caso, porque los dos argumentos se pueden tratar como vectores de la misma longitud, R devuelve el producto interior como una matriz.  Este es el comportamiento esperado según las reglas de álgebra lineal, pero podría causar problemas si la aplicación auxiliar espera que el esquema de salida no cambie nunca.

> [!TIP]
> 
> ¿Mensajes de error? Estos ejemplos requieren la tabla **RTestData**. Si no ha creado la tabla de datos de prueba, vuelva a este tema para crear la tabla: [controlar entradas y salidas](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Si ha creado la tabla, pero sigue apareciendo un error, asegúrese de que se está ejecutando el procedimiento almacenado en el contexto de la base de datos que contiene la tabla y no en **maestro** o en otra base de datos.
> 
> Además, se recomienda evitar el uso de las tablas temporales para estos ejemplos. Algunos clientes R cerrará una conexión entre los lotes, eliminar las tablas temporales.

## <a name="merge-or-multiply-columns-of-different-length"></a>Combinar o multiplicar columnas de longitud diferente

R proporciona gran flexibilidad para trabajar con vectores de diferentes tamaños y de combinar estas estructuras de tipo de columna en tramas de datos. Las listas de vectores se pueden parecer a una tabla, pero no siguen todas las reglas que rigen las tablas de base de datos.

Por ejemplo, el siguiente script define una matriz numérica de longitud 6 y la almacena en la variable de R `df1`. La matriz numérica, a continuación, se combina con los enteros de la tabla RTestData, que contiene los valores de tres (3) para crear una nueva trama de datos, `df2`.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

Para rellenar la trama de datos, R repite los elementos recuperados de RTestData tantas veces como sea necesario, hasta coincidir con el número de elementos de la matriz `df1`.

**Resultado**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

Recuerde que una trama de datos solo es similar a una tabla en cuanto al aspecto. En realidad es una lista de vectores.

## <a name="cast-or-convert-sql-server-data"></a>Convertir datos de SQL Server

R y SQL Server no usan los mismos tipos de datos, de modo que cuando se ejecuta una consulta en SQL Server para obtener datos y luego se pasa al tiempo de ejecución de R, suele producirse algún tipo de conversión implícita. Otra serie de conversiones ocurre cuando se devuelven datos de R a SQL Server.

- SQL Server inserta los datos de la consulta en el proceso de R administrado por el servicio Launchpad y lo convierte en una representación interna para la mayor eficacia.
- El tiempo de ejecución de R carga los datos en una variable data.frame y realiza sus propias operaciones en los datos.
- El motor de base de datos devuelve los datos a SQL Server por medio de una conexión segura interna y los presenta como tipos de datos de SQL Server.
- Los datos se obtienen estableciendo una conexión a SQL Server con una biblioteca de red o de cliente capaz de emitir consultas SQL y tratar conjuntos de datos tabulares. Esta aplicación cliente posiblemente afecte a los datos de otras maneras.

Para ver cómo funciona esto, ejecute una consulta como esta el [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) almacenamiento de datos. Esta vista devuelve los datos de ventas empleados en crear previsiones.

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> Puede usar cualquier versión de AdventureWorks, o crear una consulta diferente con una base de datos de su elección. El punto es intentar controlar algunos datos que contiene texto, fecha y hora y valores numéricos.

Ahora, pruebe a pegar esta consulta como entrada para el procedimiento almacenado.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

Si se produce un error, probablemente necesite realizar algunas modificaciones en el texto de la consulta. Por ejemplo, el predicado de cadena en la cláusula WHERE debe estar delimitado por dos conjuntos de comillas simples.

Tras ejecutar la consulta, revise los resultados de la función `str` para ver cómo R trata los datos de entrada.

**Resultado**

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ La columna de fecha y hora se ha procesado con el tipo de datos de R, **POSIXct**.
+ La columna de texto "ProductSeries" se ha identificado como un **factor**, lo que significa que una variable de categoría. Los valores de cadena se consideran factores de forma predeterminada. Si pasa una cadena a R, se convierte en un entero para uso interno y luego se asigna de nuevo a la cadena en la salida.

### <a name="summary"></a>Resumen

Desde incluso estos ejemplos breves, puede ver la necesidad de comprobar los efectos de conversión de datos al pasar a SQL las consultas como entrada. Dado que no se admiten algunos tipos de datos de SQL Server mediante R, considere la posibilidad de estas formas de evitar errores:

+ Los datos de prueba de antemano y compruebe las columnas o valores en el esquema que podría ser un problema cuando se pasa al código de R.
+ Especifique las columnas en el origen de datos de entrada individualmente, en lugar de usar `SELECT *`, y sepa cómo se va a tratar cada columna.
+ Al preparar los datos de entrada, realice conversiones explícitas según sea necesario para evitar sorpresas.
+ Evite pasar columnas de datos (por ejemplo, ROWGUID o GUID) que provocan errores y que no son útiles para el modelado.

Para obtener más información sobre los tipos de datos admitidos y no admitidos, vea [tipos de datos y las bibliotecas de R](../r/r-libraries-and-data-types.md).

Para obtener información sobre el impacto de rendimiento de tiempo de ejecución de conversión de cadenas de factores numéricos, vea [optimización del rendimiento de SQL Server R Services](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-step"></a>Paso siguiente

En el siguiente tutorial, obtendrá información sobre cómo aplicar funciones de R a datos de SQL Server.

> [!div class="nextstepaction"]
> [Inicio rápido: Funciones uso de R con datos de SQL Server](rtsql-using-r-functions-with-sql-server-data.md)
