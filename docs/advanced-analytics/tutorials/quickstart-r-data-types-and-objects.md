---
title: Inicio rápido sobre los tipos de datos y objetos de R y SQL
description: En esta guía de inicio rápido, aprenderá a trabajar con tipos de datos y objetos de datos en R y SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: e8c8ccd60417d4c1d492d53041280ab0c8e318af
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345426"
---
# <a name="quickstart-handle-data-types-and-objects-using-r-in-sql-server"></a>Inicio rápido: Administrar tipos de datos y objetos mediante R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta guía de inicio rápido, se ofrece una introducción práctica a los problemas comunes que se producen al mover datos entre R y SQL Server. La experiencia que se obtiene en este ejercicio proporciona información básica sobre el uso de datos en su propio script.

Algunos de los problemas más comunes son:

+ A veces, los tipos de datos no coinciden
+ Pueden producirse conversiones implícitas
+ A veces, se requieren operaciones de conversión
+ R y SQL usan objetos de datos distintos

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Verify r existe en SQL Server](quickstart-r-verify.md), se proporciona información y vínculos para configurar el entorno de r necesario para esta guía de inicio rápido.

## <a name="always-return-a-data-frame"></a>Devolver siempre una trama de datos

Cuando el script devuelve resultados de R a SQL Server, debe devolverlos como una trama de datos (**data.frame**). Cualquier otro tipo de objeto que se genere en el script, ya sea una lista, un factor, un vector o datos binarios, debe convertirse en una trama de datos si desea generarla como parte de los resultados del procedimiento almacenado. Por suerte, existen varias funciones de R con las que se pueden cambiar objetos en tramas de datos. Se puede incluso serializar un modelo binario y devolverlo en una trama de datos, algo que haremos más adelante en este tutorial.

En primer lugar, vamos a experimentar con algunos objetos básicos de R: vectores, matrices y listas, y ver cómo la conversión a una trama de datos cambia la salida pasada a SQL Server.

Compare estos dos scripts "Hola mundo" en R. Los scripts son casi idénticos, pero el primero devuelve una única columna de tres valores, mientras que el segundo devuelve tres columnas con un valor único cada una.

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

## <a name="identify-schema-and-data-types"></a>Identificar los tipos de datos y esquemas

¿Por qué los resultados tan diferentes? 

La respuesta se suele hallar con el comando de R `str()`. Agregue la función `str(object_name)` en cualquier parte del script de R para que el esquema de datos del objeto de R especificado se devuelva como un mensaje informativo. Para ver los mensajes, consulte el panel **Mensajes** de Visual Studio Code o la pestaña **Mensajes** de SSMS.

Para averiguar por qué los resultados son diferentes en Example 1 y Example 2, inserte la línea `str(OutputDataSet)` al final de la definición de la variable _@script_ en cada instrucción, del modo siguiente:

**Ejemplo 1 con la función Str agregada**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Ejemplo 2 con la función Str agregada**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

Ahora, revise el texto en el panel **Mensajes** para ver por qué el resultado es diferente.

**Resultados de Example 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Resultados de Example 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Como se puede observar, un cambio mínimo en la sintaxis de R ha tenido un gran efecto en el esquema de los resultados. No entraremos en el motivo, pero las diferencias en los tipos de datos de R se explican en los detalles de la sección de *estructuras de datos* en ["Advanced R" de Hadley Wickham](http://adv-r.had.co.nz).

Por ahora, basta con saber que hay que comprobar los resultados esperados cuando convirtamos objetos de R en tramas de datos.

> [!TIP]
> También puede usar funciones de identidad de R, como `is.matrix`, `is.vector`, para devolver información sobre la estructura de datos interna.

## <a name="implicit-conversion-of-data-objects"></a>Conversión implícita de objetos de datos

Cada objeto de datos de R tiene sus propias reglas sobre el tratamiento que se da a los valores cuando dicho objeto se combina con otro si ambos objetos de datos tienen el mismo número de dimensiones, o si cualquier objeto de datos contiene tipos de datos heterogéneos.

Por ejemplo, supongamos que ejecuta la siguiente instrucción para realizar la multiplicación de matrices mediante R. Puede multiplicar una matriz de una sola columna con los tres valores por una matriz con cuatro valores y esperar una matriz de 4x3 como resultado.

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
|1200|1300|1400|1\.500|

Sin embargo, tenga en cuenta lo que sucede cuando se cambia el `y`tamaño de la matriz.

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

¿Por qué? En este caso, dado que los dos argumentos se pueden controlar como vectores de la misma longitud, R devuelve el producto interno como una matriz.  Este es el comportamiento esperado según las reglas de álgebra lineal, pero podría causar problemas si la aplicación auxiliar espera que el esquema de salida no cambie nunca.

> [!TIP]
> 
> ¿Obtiene errores? En estos ejemplos se requiere la tabla **RTestData**. Si no ha creado la tabla de datos de prueba, vuelva a este tema para crear la tabla: [Controlar entradas y salidas](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Si ha creado la tabla pero sigue apareciendo un error, asegúrese de que está ejecutando el procedimiento almacenado en el contexto de la base de datos que contiene la tabla y no en la base de datos **maestra** o en otra.
> 
> Además, se recomienda evitar el uso de tablas temporales en estos ejemplos. Algunos clientes de R finalizarán una conexión entre lotes y eliminarán tablas temporales.

## <a name="merge-or-multiply-columns-of-different-length"></a>Combinar o multiplicar columnas de longitud diferente

R proporciona una gran flexibilidad para trabajar con vectores de diferentes tamaños y para combinar estas estructuras de tipo columna en tramas de datos. Las listas de vectores se pueden parecer a una tabla, pero no siguen todas las reglas que rigen las tablas de base de datos.

Por ejemplo, el siguiente script define una matriz numérica de longitud 6 y la almacena en la variable de R `df1`. A continuación, la matriz numérica se combina con los enteros de la tabla RTestData, que contiene tres (3) valores para crear una nueva trama de datos `df2`,.

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

- SQL Server insertar los datos de la consulta en el proceso de R administrado por el servicio Launchpad y lo convierte en una representación interna para mayor eficacia.
- El tiempo de ejecución de R carga los datos en una variable data.frame y realiza sus propias operaciones en los datos.
- El motor de base de datos devuelve los datos a SQL Server por medio de una conexión segura interna y los presenta como tipos de datos de SQL Server.
- Los datos se obtienen estableciendo una conexión a SQL Server con una biblioteca de red o de cliente capaz de emitir consultas SQL y tratar conjuntos de datos tabulares. Esta aplicación cliente posiblemente afecte a los datos de otras maneras.

Para ver cómo funciona esto, ejecute una consulta como esta en el almacenamiento de datos [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) . Esta vista devuelve los datos de ventas empleados en crear previsiones.

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
> Puede usar cualquier versión de AdventureWorks o crear una consulta diferente con una base de datos propia. El punto es tratar de tratar algunos datos que contienen valores de texto, DateTime y numérico.

Ahora, intente pegar esta consulta como entrada para el procedimiento almacenado.

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

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ La columna de fecha y hora se ha procesado con el tipo de datos de R, **POSIXct**.
+ La columna de texto "Products" se ha identificado como un **factor**, lo que significa una variable de categoría. Los valores de cadena se consideran factores de forma predeterminada. Si pasa una cadena a R, se convierte en un entero para uso interno y luego se asigna de nuevo a la cadena en la salida.

### <a name="summary"></a>Resumen

Incluso en estos breves ejemplos, puede ver la necesidad de comprobar los efectos de la conversión de datos al pasar consultas SQL como entrada. Dado que R no admite algunos tipos de datos SQL Server, tenga en cuenta estas maneras de evitar errores:

+ Pruebe los datos por adelantado y compruebe las columnas o valores del esquema que pueden ser un problema cuando se pasan a código de R.
+ Especifique las columnas en el origen de datos de entrada individualmente, en lugar de usar `SELECT *`, y sepa cómo se va a tratar cada columna.
+ Al preparar los datos de entrada, realice conversiones explícitas según sea necesario para evitar sorpresas.
+ Evite pasar columnas de datos (como GUID o ROWGUID) que causan errores y no son útiles para el modelado.

Para obtener más información sobre los tipos de datos admitidos y no admitidos, vea [bibliotecas y tipos de datos de R](../r/r-libraries-and-data-types.md).

Para obtener información sobre el impacto en el rendimiento de la conversión en tiempo de ejecución de cadenas en factores numéricos, vea [SQL Server R Services el ajuste del rendimiento](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-step"></a>Paso siguiente

En la siguiente guía de inicio rápido, aprenderá a aplicar funciones de R a los datos de SQL Server.

> [!div class="nextstepaction"]
> [Inicio rápido: Uso de funciones de R con datos de SQL Server](quickstart-r-functions.md)
