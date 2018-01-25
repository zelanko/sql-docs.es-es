---
title: "R y SQL datos y tipos de objetos de datos (R en Inicio rápido de SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: 1a17fc5b-b8c5-498f-b8b1-3b7b43a567e1
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b3c3a23cb44cc33a9257e4522be30cd3a8dd30ca
ms.sourcegitcommit: d7dcbcebbf416298f838a39dd5de6a46ca9f77aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2018
---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>R y SQL datos y tipos de objetos de datos (R en Inicio rápido de SQL)

En este paso, obtener información sobre algunos problemas comunes que surgen al mover datos entre R y SQL Server:

+ A veces, los tipos de datos no coinciden
+ Las conversiones implícitas pueden tener lugar
+ A veces, se requieren operaciones de conversión
+ R y SQL usan objetos de datos distintos

## <a name="always-return-r-data-as-a-data-frame"></a>Devolver siempre los datos de R como una trama de datos

Cuando el script devuelve resultados de R a SQL Server, debe devolverlos como una trama de datos (**data.frame**). Cualquier otro tipo de objeto que se genere en el script (sea una lista, un factor, un vector o datos binarios) debe convertirse en una trama de datos si se quiere incluir en los resultados del procedimiento almacenado. Por suerte, existen varias funciones de R con las que se pueden cambiar objetos en tramas de datos. Se puede incluso serializar un modelo binario y devolverlo en una trama de datos, algo que haremos más adelante en este tutorial.

En primer lugar, vamos a experimentar con algunos objetos de R básicas de R, vectores, matrices y listas y ver cómo cambia la conversión a una trama de datos de la salida que se pasan a SQL Server.

Compare estas dos secuencias de comandos de "Hello World" en R. Las secuencias de comandos son casi idénticos, pero el primero devuelve una sola columna de tres valores, mientras que el segundo devuelve tres columnas con un único valor de cada uno de ellos.

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

## <a name="identifying-the-schema-and-data-types-of-r-data"></a>Identificar el esquema y los tipos de datos de los datos de R

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

Como se puede observar, un cambio mínimo en la sintaxis de R ha tenido un gran efecto en el esquema de los resultados. No entraremos en por este motivo, ya que se explican las diferencias en los tipos de datos de R más exhaustivamente en este artículo por Hadley Wickham: [estructuras de datos de R](http://adv-r.had.co.nz/Data-structures.html).

Por ahora, basta con saber que hay que comprobar los resultados esperados cuando convirtamos objetos de R en tramas de datos.

> [!TIP]
> 
> También puede usar funciones de identidad de R, como `is.matrix`, `is.vector`, etcetera.

## <a name="implicit-conversion-of-data-objects"></a>Conversión implícita de objetos de datos

Cada objeto de datos de R tiene sus propias reglas sobre el tratamiento que se da a los valores cuando dicho objeto se combina con otro si ambos objetos de datos tienen el mismo número de dimensiones, o si cualquier objeto de datos contiene tipos de datos heterogéneos.

Por ejemplo, supongamos que ejecutamos la siguiente instrucción para multiplicar matrices mediante R. Una matriz de una sola columna con tres valores se multiplica por una matriz con cuatro valores, de lo que se espera como resultado una matriz 4x3.

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

Sin embargo, tenga en cuenta lo que ocurre cuando se cambia el tamaño de la matriz `y`.

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

¿Por qué? En este caso, porque los dos argumentos pueden controlarse como vectores de la misma longitud, R devuelve el producto interna como una matriz.  Este es el comportamiento esperado según las reglas de álgebra lineal, pero podría causar problemas si la aplicación auxiliar espera que el esquema de salida no cambie nunca.

> [!TIP]
> 
> ¿Mensajes de error? Estos ejemplos requieren la tabla **RTestData**. Si no ha creado la tabla de datos de prueba, vuelva a este tema: [trabajar con entradas y salidas](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Si ha creado la tabla pero sigue recibiendo un error, asegúrese de que está ejecutando el procedimiento almacenado en el contexto de la base de datos que contiene la tabla y no en **maestro** o en otra base de datos.
> 
> Además, se recomienda evitar el uso de tablas temporales para estos ejemplos. Algunos clientes de R cerrará una conexión entre los distintos lotes, eliminar las tablas temporales.

## <a name="merge-or-multiply-columns-of-different-length"></a>Combinar o multiplicar columnas de longitud diferente

R proporciona gran flexibilidad para trabajar con los vectores de tamaños diferentes y para combinar estas estructuras de tipo de columna en tramas de datos. Las listas de vectores se pueden parecer a una tabla, pero no siguen todas las reglas que rigen las tablas de base de datos.

Por ejemplo, el siguiente script define una matriz numérica de longitud 6 y la almacena en la variable de R `df1`. La matriz numérica, a continuación, se combina con los enteros de la tabla RTestData, que contiene los valores de tres (3), para realizar una nueva trama de datos, `df2`.

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

- SQL Server inserta los datos de la consulta en el proceso de R administrado por el servicio Launchpad y lo convierte en una representación interna para lograr una mayor eficacia.
- El tiempo de ejecución de R carga los datos en una variable data.frame y realiza sus propias operaciones en los datos.
- El motor de base de datos devuelve los datos a SQL Server por medio de una conexión segura interna y los presenta como tipos de datos de SQL Server.
- Los datos se obtienen estableciendo una conexión a SQL Server con una biblioteca de red o de cliente capaz de emitir consultas SQL y tratar conjuntos de datos tabulares. Esta aplicación cliente posiblemente afecte a los datos de otras maneras.

Para ver cómo funciona esto, ejecute una consulta como esta en el almacén de datos AdventureWorksDW. Esta vista devuelve los datos de ventas empleados en crear previsiones.

```sql
SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> Puede usar cualquier versión de AdventureWorks o crear una consulta diferente con una base de datos de su elección. El punto consiste en intentar controlar algunos datos que contienen valores numéricos, de texto y de fecha y hora.

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
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
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

En breves incluso estos ejemplos, puede ver la necesidad de comprobar los efectos de conversión de datos cuando pasan SQL las consultas como entrada. Dado que algunos tipos de datos de SQL Server no son compatibles con R, considere la posibilidad de estas formas de evitar errores:

+ Los datos de prueba de antemano y compruebe las columnas o valores en el esquema que podría ser un problema cuando se pasan a código R.
+ Especifique las columnas en el origen de datos de entrada individualmente, en lugar de usar `SELECT *`, y sepa cómo se va a tratar cada columna.
+ Al preparar los datos de entrada, realice conversiones explícitas según sea necesario para evitar sorpresas.
+ Evite pasar columnas de datos (por ejemplo, GUID o rowguid) que generan errores y no son útiles para el modelado.

Para obtener más información sobre los tipos de datos admitidos y no admitidos, vea [tipos de datos y las bibliotecas de R](../r/r-libraries-and-data-types.md).

Para obtener información sobre el impacto de rendimiento de tiempo de ejecución de conversión de cadenas de factores numéricos, vea [ajuste del rendimiento de SQL Server R Services](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-lesson"></a>Lección siguiente

En el siguiente paso, aprenderá a aplicar funciones de R a datos de SQL Server.

[Uso de funciones de R con datos de SQL Server](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
