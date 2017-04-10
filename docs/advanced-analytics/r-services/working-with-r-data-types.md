---
title: "Trabajar con tipos de datos de R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Trabajar con tipos de datos de R
  Mientras que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varios tipos de docenas datos, R tiene un número limitado de tipos de datos escalares (entero, complejo, lógica, de carácter, numérico, de fecha y hora y sin formato). Por lo tanto, cuando use datos de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en scripts de R, pueden ocurrir varias cosas:  
  
-   Los datos se convierten implícitamente en un tipo de datos compatible.  
  
-   Los datos no se puede convertir implícitamente y se devuelve un error.  
  
 En general, siempre que tenga alguna duda sobre cómo se usa en R un tipo o una estructura de datos en concreto, use la función  `str()` para obtener la estructura interna y el tipo del objeto de R. El resultado de la función se imprime en la consola de R y también está disponible en los resultados de la consulta, en la pestaña **Mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Si una determinada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite el tipo de datos r, pero debe usar las columnas de datos en el script de R, se recomienda que utilice la [CAST y CONVERT & #40; Transact-SQL & #41;](../../t-sql/functions/cast-and-convert-transact-sql.md) funciones para asegurarse de que el tipo de datos las conversiones se realizan como se espera antes de utilizar los datos en el script de R.  
  
 Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos, vea [tipos de datos y 40 #; Transact-SQL & #41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
## Conversión de tipos de datos entre R y SQL Server  
 En la tabla siguiente se muestran los cambios que se producen en los tipos de datos y los valores cuando los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usan en un script de R y después se devuelven a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||||  
|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo|Clase de R|Tipo en **RESULT SET**|Comentarios|  
|**smalldatetime**|`POSIXct`|**Fecha y hora**|Se representa como GMT.|  
|**smallmoney**|`numeric`|**Float**||  
|**Fecha y hora**|`POSIXct`|**Fecha y hora**|Se representa como GMT.|  
|**money**|`numeric`|**Float**||  
|**uniqueidentifier**|`character`|**varchar(max)**||  
|**Numeric**|`numeric`|**Float**||  
|**decimal(p,s)**|`numeric`|**Float**||  
|**date**|`POSIXct`|**Fecha y hora**|Se representa como GMT.|  
|**tinyint**|`integer`|**int**||  
|**bit**|`logical`|**bit**||  
|**smallint**|`integer`|**int**||  
|**int**|`integer`|**int**||  
|**Float**|`numeric`|**Float**||  
|**real**|`numeric`|**Float**||  
|**bigint**|`numeric`|**Float**||  
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Solo se permite como parámetro de entrada y salida.|  
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary (n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Solo se permite como parámetro de entrada y salida.|  
|**varchar (n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary(max)**|`raw`|**varbinary(max)**|Solo se permite como parámetro de entrada y salida.|  
  
## Ejemplos de conversión de tipos de datos  
 La consulta siguiente obtiene una serie de valores de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabla y utiliza el procedimiento almacenado  [sp_execute_external_script & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para generar los valores con el tiempo de ejecución de R.  
  
```  
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```  
  
 **Resultado**  
  
||||||  
|-|-|-|-|-|  
||C1|C2|C3|C4|  
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|  
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|  
  
 Observe el uso de la función `str` en R para obtener el esquema de los datos de salida. Esta función devuelve la siguiente información:  
  
```  
'data.frame':2 obs. of  4 variables:   
 $ c1: int  1 -11   
 $ c2: Factor w/ 2 levels "Hello","world": 1 2   
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1   
 $ cR: num  4 2  
```  
  
 Aquí puede ver que las siguientes conversiones de tipos de datos se han realizado implícitamente como parte de esta consulta:  
  
-   **Columna C1**. La columna se representa como **int** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `integer` en R, y **int** conjunto de resultados de salida.  
  
     No se ha realizado ninguna conversión de tipo.  
  
-   **Columna C2**. La columna se representa como **varchar (10)** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `factor` en R, y **varchar (max)** en la salida.  
  
     Observe cómo cambia la salida; cualquier cadena de R (un factor o una cadena normal) se representarán como **varchar (max)**, independientemente de la longitud de las cadenas.  
  
-   **Columna C3**.  La columna se representa como **uniqueidentifier** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `character` en R, y **varchar (max)** en la salida.  
  
     Observe la conversión de tipo de datos que se ha producido. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la **uniqueidentifier** pero no R; por lo tanto, los identificadores se representan como cadenas.  
  
-   **Columna C4**. La columna contiene valores generados por el script de R que no están presentes en los datos originales.  
 
 ## Vea también
 [Características y tareas de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
  
  