---
title: Usar OPENJSON con el esquema predeterminado (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: OPENJSON, with default schema
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0795006b2ec1b6dbc0f222f9513bf9d6ce9a17ac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="use-openjson-with-the-default-schema-sql-server"></a>Uso de OPENJSON con el esquema predeterminado (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Use **OPENJSON** con el esquema predeterminado para devolver una tabla con una fila por cada propiedad del objeto o por cada elemento de la matriz.  
  
 Estos son algunos ejemplos que utilizan **OPENJSON** con el esquema predeterminado. Para obtener más información y más ejemplos, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="example---return-each-property-of-an-object"></a>Ejemplo: Devolución de cada propiedad de un objeto  
 **Query**  
  
```sql  
SELECT *
FROM OPENJSON('{"name":"John","surname":"Doe","age":45}') 
```  
  
 **Resultado**  
  
|Key|Valor|  
|---------|-----------|  
|name|John|  
|surname|Doe|  
|age|45|  
  
## <a name="example---return-each-element-of-an-array"></a>Ejemplo: Devolución de cada elemento de una matriz  
 **Query**  
  
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Más información sobre la compatibilidad integrada de JSON en SQL Server  
Para obtener una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte las [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en Azure SQL Database ofrecidas por el director de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  
