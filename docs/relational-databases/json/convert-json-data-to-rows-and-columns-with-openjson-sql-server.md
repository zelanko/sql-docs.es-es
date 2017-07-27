---
title: "Conversión de datos JSON en filas y columnas con OPENJSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 50ef4db2a3c9eebcdf63ec9329eb22f1e0f001c0
ms.openlocfilehash: a7229bfe9c6924d2d7a79c861fe10c48db4b0c15
ms.contentlocale: es-es
ms.lasthandoff: 07/20/2017

---
# <a name="convert-json-data-to-rows-and-columns-with-openjson-sql-server"></a>Convertir datos JSON en filas y columnas con OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

La función de conjunto de filas **OPENJSON** convierte texto JSON en un conjunto de filas y columnas. Una vez que transforma una colección de JSON en un conjunto de filas con **OPENJSON**, puede ejecutar cualquier consulta SQL en los datos devueltos o insertarlos en una tabla de SQL Server. 
  
La función **OPENJSON** toma un objeto JSON o una colección de objetos JSON y los transforma en una o varias filas. De manera predeterminada, la función **OPENJSON** devuelve los datos siguientes:
-   Desde un objeto JSON, la función devuelve todos los pares de clave-valor que encuentra en el primer nivel.
-   Desde una matriz JSON, la función devuelve todos los elementos de la matriz con sus índices.  

Puede agregar una cláusula **WITH** opcional para proporcionar un esquema que defina explícitamente la estructura de la salida.  
  
## <a name="option-1---openjson-with-the-default-output"></a>Opción 1: OPENJSON con la salida predeterminada
Cuando se usa la función **OPENJSON** sin proporcionar un esquema explícito para los resultados, es decir, sin una cláusula **WITH** después de **OPENJSON**, la función devuelve una tabla con las siguientes tres columnas:
1.  El **nombre** de la propiedad en el objeto de entrada (o el índice del elemento en la matriz de entrada).
2.  El **valor** de la propiedad o el elemento de matriz.
3.  El **tipo** (por ejemplo, cadena, número, booleano, matriz u objeto).

**OPENJSON** devuelve cada propiedad del objeto JSON o cada elemento de la matriz como una fila independiente.  

En el siguiente ejemplo rápido se usa **OPENJSON** con el esquema predeterminado, es decir, sin la cláusula **WITH** opcional, y devuelve una fila por cada propiedad del objeto JSON.  
 
**Ejemplo**
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

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

### <a name="more-info-about-openjson-with-the-default-schema"></a>Más información sobre OPENJSON con el esquema predeterminado

Para obtener más información y ejemplos, vea [Uso de OPENJSON con el esquema predeterminado &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md).

Para ver la sintaxis y el uso, consulte [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

    
## <a name="option-2---openjson-output-with-an-explicit-structure"></a>Opción 2: salida OPENJSON con una estructura explícita
Cuando se especifica el esquema de los resultados con la cláusula **WITH** de la función **JSON**, esta devuelve una tabla con las columnas definidas en la cláusula **WITH**. En la cláusula **WITH** opcional se puede especificar un conjunto de columnas de salida, sus tipos y las rutas de acceso de las propiedades de origen de JSON de cada valor de salida. **OPENJSON** iterará por la matriz de objetos JSON, leerá el valor en la ruta de acceso especificada para cada columna y convertirá el valor al tipo especificado.  

A continuación, se muestra un ejemplo rápido que usa **OPENJSON** con un esquema para la salida que especifica explícitamente en la cláusula **WITH**.  
  
**Ejemplo**
  
```sql  
DECLARE @json NVARCHAR(MAX)
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
  
-   Por cada elemento de la matriz JSON, **OPENJSON** genera una nueva fila en la tabla de salida. Los dos elementos de la matriz JSON se convierten en dos filas en la tabla devuelta.  
  
-   Para cada columna que se especifica mediante la sintaxis `colName type json_path`, **OPENJSON** convierte el valor que se encuentra en cada elemento de matriz en la ruta de acceso especificada al tipo especificado. En este ejemplo, se toman los valores de la columna `Date` de cada elemento en una ruta de acceso`$.Order.Date` y se convierten en valores de fecha y hora.  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>Más información sobre OPENJSON con un esquema explícito
Para obtener más información y ejemplos, vea [Uso de OPENJSON con un esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).

Para ver la sintaxis y el uso, consulte [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON requiere el nivel de compatibilidad 130
La función **OPENJSON** solo está disponible en el **nivel de compatibilidad 130**. Si el nivel de compatibilidad de la base de datos es inferior a 130, SQL Server no podrá encontrar ni ejecutar la función **OPENJSON** . Hay otras funciones integradas de JSON que sí están disponibles en todos los niveles de compatibilidad.

Puede comprobar el nivel de compatibilidad en la vista `sys.databases` o en las propiedades de la base de datos.

Puede cambiar el nivel de compatibilidad de una base de datos mediante el comando siguiente:   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  

