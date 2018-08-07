---
title: Usar OPENJSON con el esquema predeterminado (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: douglasl
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 33817a87f7fe4836cae7f9c5f4aabac9e2e0c218
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535045"
---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>Uso de OPENJSON con el esquema predeterminado (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Use **OPENJSON** con el esquema predeterminado para devolver una tabla con una fila por cada propiedad del objeto o por cada elemento de la matriz.  
  
 Estos son algunos ejemplos que utilizan **OPENJSON** con el esquema predeterminado. Para obtener más información y más ejemplos, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="example---return-each-property-of-an-object"></a>Ejemplo: Devolución de cada propiedad de un objeto  
 **Consulta**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **Resultado**  
  
|Key|Valor|  
|---------|-----------|  
|NAME|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>Ejemplo: Devolución de cada elemento de una matriz  
 **Consulta**  
  
```sql  
SELECT [key],value
FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]') 
```  
  
 **Resultado**  
  
|Key|Valor|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## <a name="example---convert-json-to-a-temporary-table"></a>Ejemplo: Convertir JSON a una tabla temporal  
 La siguiente consulta devuelve todas las propiedades del objeto **info** .  
  
```sql  
DECLARE @json NVARCHAR(MAX)

SET @json=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'

SELECT *
FROM OPENJSON(@json,N'lax $.info')
```  
  
 **Resultado**  
  
|Key|Valor|Tipo|  
|---------|-----------|----------|  
|Tipo|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|etiquetas|[ "Sport", "Water polo" ]|4|  
  
## <a name="example---combine-relational-data-and-json-data"></a>Ejemplo: Combinar datos relacionales y datos JSON  
 En el ejemplo siguiente, la tabla SalesOrderHeader tiene una columna de texto SalesReason que contiene una matriz de SalesOrderReasons en formato JSON. Los objetos de SalesOrderReasons contienen propiedades como "Manufacturer" y "Quality". En el ejemplo se crea un informe que combina todas las filas de pedidos de ventas y las razones de venta relacionadas expandiendo la matriz JSON de razones de venta como si las razones se almacenaran en una tabla secundaria independiente.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
 En este ejemplo, OPENJSON devuelve una tabla de razones de venta en la que las razones aparecen como la columna de valor. El operador CROSS APPLY combina cada fila de pedido de ventas con las filas devueltas por la función con valores de tabla OPENJSON.  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Más información sobre JSON en SQL Server y Azure SQL Database  
  
### <a name="microsoft-blog-posts"></a>Entrada de blog de Microsoft  
  
Para obtener soluciones específicas, casos de uso y recomendaciones, consulte estas [entradas de blog](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre la compatibilidad integrada de JSON en SQL Server y Azure SQL Database.  

### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)
  
## <a name="see-also"></a>Ver también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
