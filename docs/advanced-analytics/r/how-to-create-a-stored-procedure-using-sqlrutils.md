---
title: Cómo crear un procedimiento almacenado mediante sqlrutils
description: Use el paquete sqlrutils R en SQL Server para agrupar el código del lenguaje R en una sola función que se pueda pasar como argumento a un procedimiento almacenado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a224bed65cd7d3fd1b6dda4ed10d56f79ecc12ee
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470149"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Creación de un pProcedure almacenado mediante sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los pasos necesarios para convertir el código de R para que se ejecute como un procedimiento almacenado de T-SQL. Para obtener el mejor resultado posible, es posible que sea necesario modificar ligeramente el código a fin de garantizar que todas las entradas se puedan parametrizar.

## <a name="bkmk_rewrite"></a>Paso 1. Reescribir script de R

Para obtener los mejores resultados, debe volver a escribir el código de R para encapsularlo como una sola función.

Todas las variables utilizadas por la función deben definirse dentro de la función o deben definirse como parámetros de entrada. Consulte el [código de ejemplo](#samples) de este artículo.

Además, dado que los parámetros de entrada de la función de R se convertirán en los parámetros de entrada del procedimiento almacenado de SQL, debe asegurarse de que las entradas y salidas cumplan los siguientes requisitos de tipo:

### <a name="inputs"></a>Entradas

Entre los parámetros de entrada puede haber como mucho una trama de datos.

Los objetos de dentro de la trama de datos, así como todos los demás parámetros de entrada de la función, deben ser de los siguientes tipos de datos de R:
- POSIXct
- numeric
- character
- integer
- lógicos
- raw

Si un tipo de entrada no es uno de los tipos anteriores, tiene que serializarse y pasarse a la función como *raw*. En este caso, la función también debe incluir código para deserializar la entrada.

### <a name="outputs"></a>Salidas

La función puede generar uno de los siguientes:

- Una trama de datos que contenga los tipos de datos admitidos. Todos los objetos de la trama de datos deben usar uno de los tipos de datos admitidos.
- Una lista con nombre que contenga como máximo una trama de datos. Todos los miembros de la lista deben usar uno de los tipos de datos admitidos.
- Un valor NULL si la función no devuelve ningún resultado

## <a name="step-2-generate-required-objects"></a>Paso 2. Generar objetos necesarios

Una vez que el código de R se ha limpiado y se puede llamar como una sola función, usará las funciones del paquete **sqlrutils** para preparar las entradas y salidas en un formulario que se puede pasar al constructor que crea realmente el procedimiento almacenado.

**sqlrutils** proporciona funciones que definen el tipo y el esquema de datos de entrada, y definen el tipo y el esquema de datos de salida. También incluye funciones que pueden convertir objetos de R en el tipo de salida necesario. Puede realizar varias llamadas de función para crear los objetos necesarios, en función de los tipos de datos que use el código.

### <a name="inputs"></a>Entradas

Si la función toma entradas, para cada entrada, llame a las siguientes funciones:

- `setInputData`Si la entrada es una trama de datos
- `setInputParameter`para el resto de tipos de entrada

Cuando realice una llamada de función, se creará un objeto de R que posteriormente pasará como argumento a `StoredProcedure`para crear el procedimiento almacenado completo.

### <a name="outputs"></a>Salidas

**sqlrutils** proporciona varias funciones para convertir objetos de R, como listas, a Data. Frame required by SQL Server.
Si la función genera una trama de datos directamente, sin ajustar primero en una lista, puede omitir este paso.
También puede omitir la conversión en este paso si la función devuelve NULL.

Al convertir una lista u obtener un elemento determinado de una lista, elija entre estas funciones:

- `setOutputData`Si la variable que se va a obtener de la lista es una trama de datos
- `setOutputParameter`para todos los demás miembros de la lista

Cuando realice una llamada de función, se creará un objeto de R que posteriormente pasará como argumento a `StoredProcedure`para crear el procedimiento almacenado completo.

## <a name="step-3-generate-the-stored-procedure"></a>Paso 3. Generar el procedimiento almacenado

Cuando todos los parámetros de entrada y salida estén listos, realice una llamada `StoredProcedure` al constructor.

**Uso**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Para ilustrar, supongamos que desea crear un procedimiento almacenado denominado **sp_rsample** con estos parámetros:

- Usa una función **foosql**existente. La función se basó en el código existente en la función **foo**de R, pero reescribió la función para cumplir los requisitos, tal y como se describe en [esta sección](#bkmk_rewrite), y llamó a la función Updated como **foosql**.
- Usa la trama de datos **queryinput** como entrada.
- Genera como salida una trama de datos con el nombre de variable de R, **SQLOutput**
- Desea crear el código T-SQL como un archivo en la `C:\Temp` carpeta, de modo que pueda ejecutarlo mediante SQL Server Management Studio posterior

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Dado que está escribiendo el archivo en el sistema de archivos, puede omitir los argumentos que definen la conexión a la base de datos.

La salida de la función es un procedimiento almacenado de T-SQL que se puede ejecutar en una instancia de SQL Server 2016 (requiere R Services) o SQL Server 2017 (requiere Machine Learning Services con R). 

Para obtener más ejemplos, consulte la ayuda del paquete llamando `help(StoredProcedure)` desde un entorno de R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Paso 4. Registrar y ejecutar el procedimiento almacenado

Puede ejecutar el procedimiento almacenado de dos maneras:

- Mediante T-SQL, desde cualquier cliente que admita conexiones a la instancia de SQL Server 2016 o SQL Server 2017
- Desde un entorno de R

Ambos métodos requieren que el procedimiento almacenado se registre en la base de datos en la que desea utilizar el procedimiento almacenado.

### <a name="register-the-stored-procedure"></a>Registrar el procedimiento almacenado

Puede registrar el procedimiento almacenado mediante R o puede ejecutar la instrucción CREATE PROCEDURE en T-SQL.

- Mediante T-SQL.  Si está más familiarizado con T-SQL, abra el Management Studio de SQL Server (o cualquier otro cliente que pueda ejecutar comandos DDL de SQL) y ejecute la instrucción CREATE PROCEDURE con el código `StoredProcedure` preparado por la función.
- Usar R. Mientras sigue en el entorno de R, puede usar la `registerStoredProcedure` función de **sqlrutils** para registrar el procedimiento almacenado en la base de datos.

  Por ejemplo, podría registrar el procedimiento almacenado **sp_rsample** en la instancia y la base de datos definidas en *sqlConnStr*, mediante esta llamada de R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Independientemente de si usa R o SQL, debe ejecutar la instrucción con una cuenta que tenga permisos para crear nuevos objetos de base de datos.

### <a name="run-using-sql"></a>Ejecutar con SQL

Una vez creado el procedimiento almacenado, abra una conexión a la base de datos SQL con cualquier cliente que admita T-SQL y pase los valores de los parámetros requeridos por el procedimiento almacenado.

### <a name="run-using-r"></a>Ejecutar con R

Se necesita una preparación adicional si desea ejecutar el procedimiento almacenado desde código R, en lugar de SQL Server. Por ejemplo, si el procedimiento almacenado requiere valores de entrada, debe establecer esos parámetros de entrada antes de que se pueda ejecutar la función y, a continuación, pasar esos objetos al procedimiento almacenado en el código de R.

El proceso general de llamada al procedimiento almacenado de SQL preparado es el siguiente:

1. Llame a `getInputParameters` para obtener una lista de objetos de parámetro de entrada.
2. Defina `$query` o establezca `$value` para cada parámetro de entrada.
3. Use `executeStoredProcedure` para ejecutar el procedimiento almacenado desde el entorno de desarrollo de R, pasando la lista de objetos de parámetro de entrada que establezca.

## <a name = "samples"></a>Ejemplo

En este ejemplo se muestran las versiones anterior y posterior de un script de R que obtiene datos de una base de datos de SQL Server, realiza algunas transformaciones en los datos y los guarda en una base de datos diferente.

Este sencillo ejemplo solo se usa para mostrar cómo se puede reorganizar el código de R con el fin de facilitar la conversión a un procedimiento almacenado.

### <a name="before-code-preparation"></a>Antes de la preparación del código


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
> Cuando se usa una conexión ODBC en lugar de invocar la función *RxSqlServerData* , debe abrir la conexión con *rxOpen* para poder realizar operaciones en la base de datos.


### <a name="after-code-preparation"></a>Después de la preparación del código

En la versión actualizada, la primera línea define el nombre de la función. El resto del código de la solución original de R pasa a formar parte de esa función.

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


