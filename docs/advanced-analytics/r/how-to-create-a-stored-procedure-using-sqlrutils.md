---
title: "Cómo crear un procedimiento almacenado mediante sqlrutils | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: c86b39e8c6c9aad23c9059482f1e33ec7ba3621b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>Crear un procedimiento almacenado mediante sqlrutils

En este tema se detallan los pasos para convertir el código R de modo que se ejecute como un procedimiento almacenado de T-SQL. Para obtener el mejor resultado posible, es posible que sea necesario modificar ligeramente el código a fin de garantizar que todas las entradas se puedan parametrizar.

## <a name="bkmk_rewrite"></a>Paso 1. Vuelva a escribir el Script de R

Para obtener mejores resultados, debe volver a escribir el código de R para encapsular como una única función.

Todas las variables utilizadas por la función deben definirse dentro de la función, o deben definirse como parámetros de entrada. Consulte el [código de ejemplo](#samples) de este tema.

Además, dado que los parámetros de entrada para la función de R se convertirá en procedimiento almacenan de los parámetros de entrada de la instrucción SQL, debe asegurarse de que sus entradas y salidas se ajustan a los siguientes requisitos de tipo:

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

### <a name="outputs"></a>Resultados

La función puede generar uno de los siguientes:

- Una trama de datos que contenga los tipos de datos admitidos. Todos los objetos de la trama de datos deben usar uno de los tipos de datos admitidos.
- Una lista con nombre que contenga como máximo una trama de datos. Todos los miembros de la lista deben usar uno de los tipos de datos admitidos.
- Un valor NULL si la función no devuelve ningún resultado

## <a name="step-2-generate-required-objects"></a>Paso 2. Generar objetos necesarios

Después de que el código de R se ha limpiado y se pueda llamar como una sola función, se utilizarán las funciones en el **sqlrutils** paquete para preparar las entradas y salidas en un formulario que puede pasarse al constructor que genera el procedimiento almacenado.

**sqlrutils** proporciona funciones que definen el esquema de datos de entrada y el tipo y definen el esquema de datos de salida y el tipo. También incluye funciones que pueden convertir objetos de R en el tipo de salida requerida. Puede realizar varias llamadas de función para crear los objetos necesarios, dependiendo de los tipos de datos que utiliza el código.

### <a name="inputs"></a>Entradas

Si la función toma la entrada, para cada entrada, llame a las funciones siguientes:

- `setInputData`Si la entrada es una trama de datos
- `setInputParameter`para todos los demás tipos de entrada

Al realizar llamadas cada función, se crea un objeto de R que más adelante se pasará como argumento a `StoredProcedure`, para crear el procedimiento almacenado completo.

### <a name="outputs"></a>Resultados

**sqlrutils** proporciona varias funciones para convertir R de objetos, como listas para el data.frame requerido por SQL Server.
Si la función genera una trama de datos directamente, sin ajustar primero en una lista, puede omitir este paso.
También puede omitir la conversión en este paso si la función devuelve NULL.

Al convertir una lista u obtener un elemento determinado de una lista, elegir entre estas funciones:

- `setOutputData`Si la variable para obtener de la lista es una trama de datos
- `setOutputParameter`para todos los demás miembros de la lista

Al realizar llamadas cada función, se crea un objeto de R que más adelante se pasará como argumento a `StoredProcedure`, para crear el procedimiento almacenado completo.

## <a name="step-3-generate-the-stored-procedure"></a>Paso 3. Generar el procedimiento almacenado

Cuando todos los parámetros de entrada y salidos están listos, realizar una llamada a la `StoredProcedure` constructor.

**Uso**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Como ejemplo, suponga que desea crear un procedimiento almacenado denominado **sp_rsample** con estos parámetros:

- Utiliza una función existente **foosql**. La función se basa en código existente en función de R **foo**, pero se ha reescrito la función para que se ajuste a los requisitos como se describe en [en esta sección](#bkmk_rewrite)y con el nombre de la función actualizada como  **foosql**.
- Utiliza la trama de datos **queryinput** como entrada
- Genera como resultado una trama de datos con el nombre de variable de R **sqloutput**
- Para crear el código de T-SQL como un archivo en el `C:\Temp` carpeta, por lo que puede ejecutarlo mediante SQL Server Management Studio más adelante

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Dado que está escribiendo el archivo en el sistema de archivos, puede omitir los argumentos que definen la conexión de base de datos.

El resultado de la función es un procedimiento almacenado de T-SQL que se pueden ejecutar en una instancia de SQL Server 2016 (requiere servicios de R) o SQL Server 2017 (requiere servicios de aprendizaje de máquina con R). 

Para obtener ejemplos adicionales, vea la Ayuda del paquete, mediante una llamada a `help(StoredProcedure)` desde un entorno de R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Paso 4. Registrar y ejecutar el procedimiento almacenado

Hay dos modos que se puede ejecutar el procedimiento almacenado:

- Mediante T-SQL, desde cualquier cliente que admite las conexiones a la instancia de SQL Server 2016 o SQL Server 2017
- Desde un entorno de R

Ambos métodos requieren que el procedimiento almacenado se ha registrado en la base de datos donde piensa usar el procedimiento almacenado.

### <a name="register-the-stored-procedure"></a>Registrar el procedimiento almacenado

Puede registrar el procedimiento almacenado con R, o puede ejecutar la instrucción CREATE PROCEDURE en T-SQL.

- Mediante T-SQL.  Si está más familiarizado con T-SQL, abra SQl Server Management Studio (o cualquier otro cliente que se puede ejecutar comandos de DDL de SQL) y ejecute la instrucción CREATE PROCEDURE con el código preparado la `StoredProcedure` función.
- Uso de R. Mientras está todavía en el entorno de R, puede usar el `registerStoredProcedure` funcionando en **sqlrutils** para registrar el procedimiento almacenado con la base de datos.

  Por ejemplo, puede registrar el procedimiento almacenado **sp_rsample** en la instancia y la base de datos definida en *sqlConnStr*, mediante la realización de esta llamada R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Independientemente de si utiliza R o SQL, debe ejecutar la instrucción con una cuenta que tenga permisos para crear nuevos objetos de base de datos.

### <a name="run-using-sql"></a>Ejecutar con SQL

Una vez creado el procedimiento almacenado, abrir una conexión a la base de datos SQL con cualquier cliente que admite código T-SQL y pasar los valores para los parámetros requeridos por el procedimiento almacenado.

### <a name="run-using-r"></a>Ejecutar con R

Preparación adicional es necesario si desea ejecutar el procedimiento almacenado desde el código de R, en lugar de SQL Server. Por ejemplo, si el procedimiento almacenado requiere valores de entrada, debe establecer los parámetros de entrada antes de que la función se puede ejecutar y, a continuación, pasar esos objetos al procedimiento almacenado en el código de R.

El proceso general de una llamada al procedimiento almacenado de SQL preparado es como sigue:

1. Llame a `getInputParameters` para obtener una lista de objetos de parámetro de entrada.
2. Defina `$query` o establezca `$value` para cada parámetro de entrada.
3. Use `executeStoredProcedure` para ejecutar el procedimiento almacenado desde el entorno de desarrollo de R, pasando la lista de objetos de parámetro de entrada que establezca.

## <a name = "samples"></a>Ejemplo

Este ejemplo se muestra el antes y después de las versiones de un script de R que obtiene datos de una base de datos de SQL Server, realiza algunas transformaciones en los datos y lo guarda en otra base de datos.

Este sencillo ejemplo se usa únicamente para demostrar cómo puede reorganizar el código de R para que resulten más fáciles de convertir a un procedimiento almacenado.

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
> Cuando se usa una conexión ODBC, en lugar de invocar el *RxSqlServerData* función, debe abrir la conexión con *rxOpen* para poder realizar operaciones en la base de datos.


### <a name="after-code-preparation"></a>Después de la preparación de código

En la versión actualizada, la primera línea define el nombre de función. El código restante de la solución R original se convierte en una parte de esa función.

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

[Generating a Stored Procedure using sqlrutils (Generación de un procedimiento almacenado con sqlrutils)](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)


