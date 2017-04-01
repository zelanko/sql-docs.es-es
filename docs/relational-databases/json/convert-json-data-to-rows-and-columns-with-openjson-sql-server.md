---
title: "Convertir datos JSON en filas y columnas con OPENJSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON"
  - "JSON, importar"
  - "importar JSON"
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Convertir datos JSON en filas y columnas con OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  La función de conjunto de filas **OPENJSON** permite convertir texto JSON en un conjunto de filas y columnas. Puede usar **OPENJSON** para ejecutar consultas SQL en colecciones de JSON o para importar texto JSON en tablas de SQL Server.  
  
> [!NOTE] La función **OPENJSON** solo está disponible en el **nivel de compatibilidad 130**. Si el nivel de compatibilidad de la base de datos es inferior a 130, SQL Server no podrá encontrar ni ejecutar la función **OPENJSON**. Hay otras funciones JSON que sí están disponibles en todos los niveles de compatibilidad. Puede comprobar el nivel de compatibilidad en la vista sys.databases o en las propiedades de la base de datos.
> 
>   Puede cambiar un nivel de compatibilidad de la base de datos mediante el comando siguiente:   
>   ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
  
 La función **OPENJSON** toma un objeto JSON o una colección de objetos JSON y los transforma en una o varias filas. De forma predeterminada, la función **OPENJSON** devuelve todos los pares clave-valor que se encuentran en el primer nivel del objeto JSON o todos los elementos de matrices JSON con sus índices.  
  
 Puede especificar el esquema de filas que se devolverá mediante la función **OPENJSON** con la cláusula WITH. Este esquema explícito define la estructura de la salida.  
  
## Usa OPENJSON sin el esquema de resultados

En el siguiente ejemplo rápido se usa **OPENJSON**  con el esquema predeterminado y se devuelve una fila por cada propiedad del objeto JSON.  
 
Cuando se usa la función **OPENJSON** sin un esquema especificado de resultados devueltos (es decir, sin una cláusula WITH después de OPENJSON), la función devuelve una tabla con tres columnas: el nombre de la propiedad del objeto de entrada (o índice del elemento de la matriz de entrada), el valor de propiedad o elemento de matriz y el tipo (por ejemplo, cadena, número, booleano, matriz u objeto). Las propiedades del objeto JSON (o elementos de matriz) se devuelven en filas independientes.  

-   Para obtener más información y ejemplos, vea [Uso de OPENJSON con el esquema predeterminado &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md).
-   Para ver la sintaxis y el uso, consulte [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

```tsql  
SET @json = '{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';  
  
SELECT *  
FROM OPENJSON(@json);  
```  
  
**Resultado**  
  
|Key|value|tipo|  
|---------|-----------|----------|  
|name|John|1|  
|surname|Doe|1|  
|age|45|2|  
|skills|["SQL","C#","MVC"]|4|
    
## Usa OPENJSON con un esquema explícito

A continuación se muestra un ejemplo rápido que usa **OPENJSON** con un esquema especificado de forma explícita.  
  
Cuando se especifica el esquema de los resultados devueltos en la cláusula WITH de la función **OPENJSON**, la función devuelve una tabla con las columnas definidas en la cláusula WITH. En la cláusula WITH se pueden especificar un conjunto de columnas de salida, sus tipos y las rutas de acceso de las propiedades de origen de JSON de cada valor de salida. **OPENJSON** iterará por la matriz de objetos JSON, leerá el valor en la ruta de acceso especificada para cada columna y convertirá el valor al tipo especificado.  

-   Para obtener más información y ejemplos, vea [Uso de OPENJSON con un esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).
-   Para ver la sintaxis y el uso, consulte [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).
  
```tsql  
SET @json =   
 N'[  
      {  
        "Order": {  
          "Number":"SO43659",  
          "Date":"2011-05-31T00:00:00"  
        },  
        "AccountNumber":"AW29825",  
        "Item": {  
          "Price":2024.9940,  
          "Quantity":1  
        }  
      },  
      {  
        "Order": {  
          "Number":"SO43661",  
          "Date":"2011-06-01T00:00:00"  
        },  
        "AccountNumber":"AW73565",  
        "Item": {  
          "Price":2024.9940,  
          "Quantity":3  
        }  
     }  
]'  
  
SELECT * FROM  
OPENJSON ( @json )  
WITH (   
             Number   varchar(200) '$.Order.Number' ,  
             Date     datetime     '$.Order.Date',  
             Customer varchar(200) '$.AccountNumber',  
             Quantity int          '$.Item.Quantity'  
)  
```  
  
**Resultado**  
  
|Number|Date|Customer|Cantidad|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 Esta función devuelve los elementos de una matriz JSON y les da formato.  
  
-   Por cada elemento de la matriz JSON, **OPENJSON** genera una nueva fila en la tabla de salida. Dos elementos de la matriz JSON se convierten en dos filas en la tabla devuelta.  
  
-   Para cada columna especificada mediante la sintaxis `colName type json_path`, la función **OPENJSON** convierte los valores que encuentra en los elementos de la matriz en la ruta de acceso especificada, los convierte al tipo especificado y rellena una celda de la tabla de salida. En este ejemplo, se toman los valores de la columna de fecha de cada objeto en una ruta de acceso `$.Order.Date` y se convierten en valores de fecha y hora.  
  
Una vez que la colección de JSON se ha transformado en un conjunto de filas, puede ejecutar cualquier consulta SQL en los datos devueltos o insertarlos en una tabla.  
  
## Más información sobre OPENJSON y la compatibilidad integrada de JSON en SQL Server  
 [Entradas de blog del administrador de programas de Microsoft Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## Vea también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  