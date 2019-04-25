---
title: Cómo crear un procedimiento almacenado mediante sqlrutils - SQL Server Machine Learning Services
description: Usar el paquete sqlrutils R en SQL Server para incluir código de lenguaje R en una sola función que puede pasarse como argumento a un procedimiento almacenado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 014fb8344a0b2cf93dc7f375fffc717663f53a46
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641845"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Crear un pProcedure almacenado mediante sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe los pasos para convertir el código de R para ejecutarlo como un procedimiento almacenado de T-SQL. Para obtener el mejor resultado posible, es posible que sea necesario modificar ligeramente el código a fin de garantizar que todas las entradas se puedan parametrizar.

## <a name="bkmk_rewrite"></a>Paso 1. Vuelva a escribir el Script de R

Para obtener resultados óptimos, debe volver a escribir el código de R para encapsular como una sola función.

Todas las variables usadas por la función deben definirse dentro de la función, o deben definirse como parámetros de entrada. Consulte la [código de ejemplo](#samples) en este artículo.

Además, dado que los parámetros de entrada para la función de R se convertirá en los parámetros de entrada de SQL de procedimiento almacenan, debe asegurarse de que sus entradas y salidas se ajustan a los siguientes requisitos de tipo:

### <a name="inputs"></a>Entradas

Entre los parámetros de entrada puede haber como mucho una trama de datos.

Los objetos de dentro de la trama de datos, así como todos los demás parámetros de entrada de la función, deben ser de los siguientes tipos de datos de R:
- POSIXct
- NUMERIC
- character
- integer
- lógicos
- raw

Si un tipo de entrada no es uno de los tipos anteriores, tiene que serializarse y pasarse a la función como *raw*. En este caso, la función también debe incluir código para deserializar la entrada.

### <a name="outputs"></a>Resultados

La función puede generar uno de los siguientes:

- Una trama de datos que contenga los tipos de datos admitidos. Todos los objetos de la trama de datos deben usar uno de los tipos de datos admitidos.
- Una lista con nombre que contenga como máximo una trama de datos. Todos los miembros de la lista deben usar uno de los tipos de datos admitidos.
- Un valor NULL si la función no devuelve ningún resultado

## <a name="step-2-generate-required-objects"></a>Paso 2. Generar objetos necesarios

Después de que el código de R que se ha limpiado y pueda llamarse como una sola función, usará las funciones en el **sqlrutils** paquete para preparar las entradas y salidas en un formulario que puede pasarse al constructor que genera el procedimiento almacenado.

**sqlrutils** proporciona funciones que definen el esquema de datos de entrada y el tipo y definen el esquema de datos de salida y el tipo. También incluye funciones que pueden convertir objetos de R en el tipo de salida requerida. Puede realizar varias llamadas de función para crear los objetos necesarios, dependiendo de los tipos de datos que usa el código.

### <a name="inputs"></a>Entradas

Si la función toma las entradas, para cada entrada, llame a las funciones siguientes:

- `setInputData` Si la entrada es una trama de datos
- `setInputParameter` para todos los demás tipos de entrada

Cuando se llamar a cada función, se crea un objeto de R que pasará posteriormente como argumento a `StoredProcedure`, para crear el procedimiento almacenado completo.

### <a name="outputs"></a>Resultados

**sqlrutils** proporciona varias funciones para convertir de R de objetos, como se enumeran en la trama de datos necesarios para SQL Server.
Si la función genera una trama de datos directamente, sin ajustar primero en una lista, puede omitir este paso.
También puede omitir la conversión en este paso si la función devuelve NULL.

Al convertir una lista u obtener un elemento determinado de una lista, elegir entre estas funciones:

- `setOutputData` Si la variable a obtener de la lista es una trama de datos
- `setOutputParameter` para todos los demás miembros de la lista

Cuando se llamar a cada función, se crea un objeto de R que pasará posteriormente como argumento a `StoredProcedure`, para crear el procedimiento almacenado completo.

## <a name="step-3-generate-the-stored-procedure"></a>Paso 3. Generar el procedimiento almacenado

Cuando todos los parámetros de entrada y salidos estén listos, realice una llamada a la `StoredProcedure` constructor.

**Usage**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Para ilustrarlo, supongamos que desea crear un procedimiento almacenado denominado **sp_rsample** con estos parámetros:

- Usa una función existente **foosql**. La función se basa en el código existente en función de R **foo**, pero tiene la función para cumplir los requisitos como se describe en [en esta sección](#bkmk_rewrite)y con el nombre de la función actualizada como  **foosql**.
- Usa la trama de datos **queryinput** como entrada
- Una trama de datos con el nombre de variable de R, se genera como salida **sqloutput**
- Para crear el código de Transact-SQL como un archivo en el `C:\Temp` carpeta, por lo que puede ejecutarlo con SQL Server Management Studio más adelante

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Dado que está escribiendo el archivo en el sistema de archivos, puede omitir los argumentos que definen la conexión de base de datos.

El resultado de la función es un procedimiento almacenado de T-SQL que se puede ejecutar en una instancia de SQL Server 2016 (requiere R Services) o SQL Server 2017 (requiere servicios de Machine Learning con R). 

Para obtener ejemplos adicionales, consulte la Ayuda del paquete, mediante una llamada a `help(StoredProcedure)` desde un entorno de R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Paso 4. Registrar y ejecutar el procedimiento almacenado

Hay dos formas que puede ejecutar el procedimiento almacenado:

- Con Transact-SQL, desde cualquier cliente que admite conexiones a la instancia de SQL Server 2016 o SQL Server 2017
- Desde un entorno de R

Ambos métodos requieren que se registre el procedimiento almacenado en la base de datos donde se va a usar el procedimiento almacenado.

### <a name="register-the-stored-procedure"></a>Registrar el procedimiento almacenado

Puede registrar el procedimiento almacenado con R, o puede ejecutar la instrucción CREATE PROCEDURE de Transact-SQL.

- Con Transact-SQL.  Si se siente más cómodo con T-SQL, abra SQl Server Management Studio (o cualquier otro cliente que se puede ejecutar comandos de DDL de SQL) y ejecute la instrucción CREATE PROCEDURE con el código elaborado por el `StoredProcedure` función.
- Con R. Mientras está todavía en el entorno de R, puede usar el `registerStoredProcedure` funcionando en **sqlrutils** para registrar el procedimiento almacenado con la base de datos.

  Por ejemplo, puede registrar el procedimiento almacenado **sp_rsample** en la instancia y base de datos definida en *sqlConnStr*, al realizar esta llamada R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Independientemente de si usa R o SQL, debe ejecutar la instrucción con una cuenta que tenga permisos para crear nuevos objetos de base de datos.

### <a name="run-using-sql"></a>Ejecutar mediante SQL

Una vez creado el procedimiento almacenado, abrir una conexión a la base de datos SQL con cualquier cliente que admita T-SQL y pasar los valores para los parámetros requeridos por el procedimiento almacenado.

### <a name="run-using-r"></a>Ejecutar con R

Si desea ejecutar el procedimiento almacenado desde el código de R, en lugar de SQL Server, se necesita una preparación adicional. Por ejemplo, si el procedimiento almacenado requiere valores de entrada, debe establecer los parámetros de entrada antes de que se puede ejecutar la función y, a continuación, pasar esos objetos al procedimiento almacenado en el código de R.

El proceso general de una llamada al procedimiento almacenado de SQL preparado es como sigue:

1. Llame a `getInputParameters` para obtener una lista de objetos de parámetro de entrada.
2. Defina `$query` o establezca `$value` para cada parámetro de entrada.
3. Use `executeStoredProcedure` para ejecutar el procedimiento almacenado desde el entorno de desarrollo de R, pasando la lista de objetos de parámetro de entrada que establezca.

## <a name = "samples"></a>Ejemplo

Este ejemplo se muestra el antes y después de las versiones de un script de R que obtiene los datos de una base de datos de SQL Server, realiza algunas transformaciones en los datos y lo guarda en otra base de datos.

Este sencillo ejemplo se utiliza únicamente para demostrar cómo se puede reorganizar el código de R para que resulte más fácil convertir a un procedimiento almacenado.

### <a name="before-code-preparation"></a>Antes de la elaboración de código


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> Cuando se usa una conexión ODBC en lugar de invocar el *RxSqlServerData* función, debe abrir la conexión con *rxOpen* para poder realizar operaciones en la base de datos.


### <a name="after-code-preparation"></a>Después de la preparación de código

En la versión actualizada, la primera línea define el nombre de función. El código restante de la solución de R original se convierte en una parte de esa función.

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> Aunque no es necesario abrir la conexión ODBC de forma explícita como parte del código, se sigue necesitando una conexión ODBC para usar **sqlrutils**.

## <a name="see-also"></a>Vea también

[sqlrutils (SQL)](ref-r-sqlrutils.md)


