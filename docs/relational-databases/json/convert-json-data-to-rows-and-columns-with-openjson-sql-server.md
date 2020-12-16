---
description: Análisis y transformación de datos JSON con OPENJSON (SQL Server)
title: Análisis y transformación de datos JSON con OPENJSON
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5a944c86280bd3fa756ecfe794b2270a778a0c71
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478176"
---
# <a name="parse-and-transform-json-data-with-openjson-sql-server"></a>Análisis y transformación de datos JSON con OPENJSON (SQL Server)
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

La función de conjunto de filas **OPENJSON** convierte texto JSON en un conjunto de filas y columnas. Una vez que transforma una colección de JSON en un conjunto de filas con **OPENJSON**, puede ejecutar cualquier consulta SQL en los datos devueltos o insertarlos en una tabla de SQL Server. 
  
La función **OPENJSON** toma un objeto JSON o una colección de objetos JSON y los transforma en una o varias filas. De manera predeterminada, la función **OPENJSON** devuelve los datos siguientes:
-   Desde un objeto JSON, la función devuelve todos los pares clave-valor que encuentra en el primer nivel.
-   Desde una matriz JSON, la función devuelve todos los elementos de la matriz con sus índices.  

Puede agregar una cláusula **WITH** opcional para proporcionar un esquema que defina explícitamente la estructura de la salida.  
  
## <a name="option-1---openjson-with-the-default-output"></a>Opción 1: OPENJSON con la salida predeterminada
Cuando se usa la función **OPENJSON** sin proporcionar un esquema explícito para los resultados (es decir, sin una cláusula **WITH** después de **OPENJSON**), la función devuelve una tabla con las siguientes tres columnas:
1.  **Nombre** de la propiedad en el objeto de entrada (o el índice del elemento en la matriz de entrada).
2.  **Valor** de la propiedad o el elemento de matriz.
3.  **Tipo** (por ejemplo, cadena, número, booleano, matriz u objeto).

**OPENJSON** devuelve cada propiedad del objeto JSON o cada elemento de la matriz como una fila independiente.  

En el siguiente ejemplo rápido se usa **OPENJSON** con el esquema predeterminado (es decir, sin la cláusula **WITH** opcional) y se devuelve una fila por cada propiedad del objeto JSON.  

**Ejemplo**

```sql
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**Resultados**
  
|key|value|type|  
|---------|-----------|----------|  
|name|John|1|  
|surname|Doe|1|  
|age|45|2|  
|skills|["SQL","C#","MVC"]|4|

### <a name="more-info-about-openjson-with-the-default-schema"></a>Más información sobre OPENJSON con el esquema predeterminado

Para obtener más información y ejemplos, vea [Uso de OPENJSON con el esquema predeterminado &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md).

Para ver la sintaxis y el uso, consulte [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

## <a name="option-2---openjson-output-with-an-explicit-structure"></a>Opción 2: Salida OPENJSON con una estructura explícita

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
  
**Resultados**
  
|Number|Date|Customer|Cantidad|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
Esta función devuelve los elementos de una matriz JSON y les da formato.  
  
-   Por cada elemento de la matriz JSON, **OPENJSON** genera una nueva fila en la tabla de salida. Los dos elementos de la matriz JSON se convierten en dos filas en la tabla devuelta.  
  
-   Para cada columna que se especifica mediante la sintaxis `colName type json_path`, **OPENJSON** convierte el valor que se encuentra en cada elemento de matriz en la ruta de acceso especificada al tipo especificado. En este ejemplo, se toman los valores de la columna `Date` de cada elemento en una ruta de acceso `$.Order.Date` y se convierten en valores de fecha y hora.  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>Más información sobre OPENJSON con un esquema explícito

Para obtener más información y ejemplos, vea [Uso de OPENJSON con un esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).

Para ver la sintaxis y el uso, consulte [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON requiere el nivel de compatibilidad 130

La función **OPENJSON** solo está disponible en el **nivel de compatibilidad 130**. Si el nivel de compatibilidad de la base de datos es inferior a 130, SQL Server no podrá encontrar ni ejecutar la función **OPENJSON**. Hay otras funciones integradas de JSON que sí están disponibles en todos los niveles de compatibilidad.

Puede comprobar el nivel de compatibilidad en la vista `sys.databases` o en las propiedades de la base de datos.

Puede cambiar el nivel de compatibilidad de una base de datos mediante el comando siguiente:   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Más información sobre JSON en SQL Server y Azure SQL Database  
  
### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

- [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

- [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

- [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)
  
## <a name="see-also"></a>Consulte también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
