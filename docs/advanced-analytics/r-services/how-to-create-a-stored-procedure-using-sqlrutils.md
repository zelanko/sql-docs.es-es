---
title: "C&#243;mo crear un procedimiento almacenado mediante sqlrutils | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# C&#243;mo crear un procedimiento almacenado mediante sqlrutils
En este tema se detallan los pasos para convertir el código R de modo que se ejecute como un procedimiento almacenado de T-SQL. Para obtener el mejor resultado posible, es posible que sea necesario modificar ligeramente el código a fin de garantizar que todas las entradas se puedan parametrizar.

## <a name="step-1-format-your-r-script"></a>Paso 1. Aplicar formato al script de R

1. Ajuste todo el código en una sola función.

   Esto significa que todas las variables usadas por la función tienen que definirse dentro de esta o que deben definirse como parámetros de entrada. Consulte el [código de ejemplo](#samples) de este tema.

## <a name="step-2-standardize-the-inputs-and-outputs"></a>Paso 2. Estandarizar las entradas y salidas

Los parámetros de entrada de la función se convertirán en los parámetros de entrada del procedimiento almacenado de SQL y, por tanto, deben cumplir los requisitos de tipo siguientes:
- Entre los parámetros de entrada puede haber como mucho una trama de datos.
- Los objetos de dentro de la trama de datos, así como todos los demás parámetros de entrada de la función, deben ser de los siguientes tipos de datos de R:
    - POSIXct
    - numeric
    - character
    - integer
    - lógicos
    - raw

- Si un tipo de entrada no es uno de los tipos anteriores, tiene que serializarse y pasarse a la función como *raw*. En este caso, la función también debe incluir código para deserializar la entrada.

La función puede generar uno de los siguientes:

- Una trama de datos que contenga los tipos de datos admitidos. Todos los objetos de la trama de datos deben usar uno de los tipos de datos admitidos.
- Una lista con nombre que contenga como máximo una trama de datos. Todos los miembros de la lista deben usar uno de los tipos de datos admitidos. 
- Un valor NULL si la función no devuelve ningún resultado

## <a name="step-3-make-calls-to-the-sqlrutils-package-to-generate-the-stored-procedure"></a>Paso 3. Realizar llamadas al paquete sqlrutils para generar el procedimiento almacenado

Después de que el código R se haya limpiado y pueda llamarse como una sola función, puede comenzar el proceso de usar las funciones de **sqlrutils** para convertir el código en un procedimiento almacenado.

Según los tipos de datos de los parámetros, usará funciones diferentes para capturar los datos y crear un objeto de parámetro.

1. Si la función toma parámetros de entrada, cree uno de los objetos siguientes para cada parámetro: 
    - Si el parámetro de entrada es una trama de datos, use `setInputData`.
    - Para los demás parámetros de entrada, use `setInputParameter`.

2. Si la función genera una lista, cree un objeto para controlar los datos deseados de la lista de la forma siguiente: 
    - Si la variable de la lista es una trama de datos, use `setOutputData`.
    - Para todos los demás miembros de la lista, use `setOutputParameter`.
    - Si la función genera una trama de datos directamente, sin ajustar primero en una lista, puede omitir este paso. 
    - Omita este paso si la función devuelve NULL.

3. Cuando todos los parámetros de entrada y salida estén listos, realice una llamada al constructor `StoredProcedure` para generar el procedimiento almacenado que contiene la función de R.
4. Para registrar inmediatamente el procedimiento almacenado en la base de datos, use `registerStoredProcedure`.

## <a name="step-4-execute-the-stored-procedure"></a>Paso 4. Ejecutar el procedimiento almacenado

1. Si quiere ejecutar el procedimiento almacenado desde el código R en lugar de hacerlo desde SQL Server y el procedimiento almacenado necesita una entrada, debe establecer esos parámetros de entrada para poder ejecutar la función: 
    - Llame a `getInputParameters` para obtener una lista de objetos de parámetro de entrada.
    - Defina `$query` o establezca `$value` para cada parámetro de entrada. 

2. Use `executeStoredProcedure` para ejecutar el procedimiento almacenado desde el entorno de desarrollo de R, pasando la lista de objetos de parámetro de entrada que establezca.

## <a name="a-name-samplesaexamples-prepare-your-code"></a><a name = "samples"></a>Ejemplos: preparar el código 

En este ejemplo, el código R lee de una base de datos, realiza algunas transformaciones en los datos y los guarda en otra base de datos. Este sencillo ejemplo se usa únicamente para demostrar cómo se puede reorganizar el código R para ofrecer una interfaz más sencilla para la conversión de procedimientos almacenados.

**Antes de aplicar formato**


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
Tenga en cuenta que si usa una conexión ODBC en lugar de invocar a la función *RxSqlServerData*, debe abrir la conexión con *rxOpen* para poder realizar operaciones en la base de datos.



**Después de aplicar formato**

En la versión con el nuevo formato, la primera línea define el nombre de la función.

El código restante de la solución original de R se convierte en una parte de esa función. 

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
Aunque no es necesario abrir la conexión ODBC de forma explícita como parte del código, se sigue necesitando una conexión ODBC para usar **sqlrutils**. 


## <a name="see-also"></a>Vea también

[Generating a Stored Procedure using sqlrutils (Generación de un procedimiento almacenado con sqlrutils)](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

