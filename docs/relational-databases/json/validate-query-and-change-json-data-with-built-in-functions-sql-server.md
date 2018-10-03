---
title: Validar, consultar y cambiar datos JSON con funciones integradas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3ae0c36b766ce453998a88b347618f10e6cf3b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766523"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Validar, consultar y cambiar datos JSON con funciones integradas (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La compatibilidad integrada con JSON incluye las siguientes funciones integradas que se describen brevemente en este tema.  
  
-   [ISJSON](#ISJSON) prueba si una cadena contiene un valor JSON válido.  
  
-   [JSON_VALUE](#VALUE) extrae un valor escalar de una cadena JSON.  
  
-   [JSON_QUERY](#QUERY) extrae un objeto o una matriz de una cadena JSON.  
  
-   [JSON_MODIFY](#MODIFY) actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Texto de JSON para los ejemplos de esta página
En los ejemplos de esta página se usa el siguiente texto de JSON, que contiene un elemento complejo.

```sql 
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
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
``` 

##  <a name="ISJSON"></a> Validar texto JSON mediante la función ISJSON  
 La función **ISJSON** prueba si una cadena contiene un valor JSON válido.  
  
En el ejemplo siguiente, se devuelven las filas en las que la columna `json_col` contiene JSON válido.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  

Para obtener más información, vea [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extraer un valor de texto JSON mediante la función JSON_VALUE  
La función **JSON_VALUE** extrae un valor escalar de una cadena JSON.  
  
En el ejemplo siguiente, se extrae el valor de la propiedad JSON anidada `town` en una variable local.  
  
```sql  
SET @town = JSON_VALUE(@jsonInfo, '$.info.address.town')  
```  
  
Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extraer un objeto o una matriz de texto JSON mediante la función JSON_QUERY  
La función **JSON_QUERY** extrae un objeto o una matriz de una cadena JSON.  
 
En el ejemplo siguiente se muestra cómo devolver un fragmento de JSON en los resultados de la consulta.  
  
```sql  
SELECT FirstName, LastName, JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
Para obtener más información, vea [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
##  <a name="JSONCompare"></a> Comparación de JSON_VALUE y JSON_QUERY  
La diferencia clave entre **JSON_VALUE** y **JSON_QUERY** es que **JSON_VALUE** devuelve un valor escalar, mientras que **JSON_QUERY** devuelve un objeto o una matriz.  
  
Observe el siguiente ejemplo de texto JSON.  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
En este ejemplo de texto JSON, los miembros de datos "a" y "c" son valores de cadena, mientras que el miembro de datos "b" es una matriz. **JSON_VALUE** y **JSON_QUERY** devuelven los resultados siguientes:  
  
|Ruta de acceso|**JSON_VALUE** devuelve|**JSON_QUERY** devuelve|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL o error|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL o error|  
|**$.b**|NULL o error|[1,2]|  
|**$.b[0]**|1|NULL o error|  
|**$.c**|hi|NULL o error|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>Probar JSON_VALUE y JSON_QUERY con la base de datos de ejemplo AdventureWorks  
Pruebe las funciones integradas que se describen en este tema al ejecutar los ejemplos siguientes con la base de datos de ejemplo AdventureWorks. Para obtener información sobre dónde obtener AdventureWorks y sobre cómo agregar datos JSON para pruebas mediante la ejecución de un script, vea [Test drive built-in JSON support](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database) (Probar la compatibilidad integrada de JSON).
  
En los ejemplos siguientes, la columna `Info` de la tabla `SalesOrder_json` contiene texto JSON.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Ejemplo 1: devolver columnas estándar y datos JSON  
La consulta siguiente devuelve valores de las columnas relacionales estándar y de una columna JSON.  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Ejemplo 2: agregar y filtrar valores JSON  
La consulta siguiente agrega subtotales por nombre de cliente (almacenados en JSON) y estado (almacenado en una columna normal). Luego, filtra los resultados por ciudad (almacenados en JSON) y OrderDate (almacenados en una columna normal).  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> Actualizar valores de propiedad en texto JSON mediante la función JSON_MODIFY  
La función **JSON_MODIFY** actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.  
  
En el ejemplo siguiente, se actualiza el valor de una propiedad JSON en una variable que contiene JSON.  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 Para obtener más información, vea [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Más información sobre JSON en SQL Server y Azure SQL Database  
  
### <a name="microsoft-blog-posts"></a>Entrada de blog de Microsoft  
  
Para obtener soluciones específicas, casos de uso y recomendaciones, consulte estas [entradas de blog](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) sobre la compatibilidad integrada de JSON en SQL Server y Azure SQL Database.  

### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)
  
## <a name="see-also"></a>Ver también  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [Expresiones de ruta de acceso JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
