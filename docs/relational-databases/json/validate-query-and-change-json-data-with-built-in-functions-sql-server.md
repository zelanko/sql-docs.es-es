---
title: Validar, consultar y cambiar datos JSON con funciones integradas (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d9cdb66be3f6831ad5c2a61258c25425f98c0988
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Validar, consultar y cambiar datos JSON con funciones integradas (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  La compatibilidad integrada con JSON incluye las funciones integradas que se describen en este tema.  
  
-   [ISJSON](#ISJSON) prueba si una cadena contiene un valor JSON válido.  
  
-   [JSON_VALUE](#VALUE) extrae un valor escalar de una cadena JSON.  
  
-   [JSON_QUERY](#QUERY) extrae un objeto o una matriz de una cadena JSON.  
  
-   [JSON_MODIFY](#MODIFY) actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Texto de JSON para los ejemplos de esta página
En los ejemplos de esta página se usa el siguiente texto de JSON, que contiene un elemento complejo.

```json  
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
  
 En el ejemplo siguiente se devuelve el texto JSON si la columna contiene un valor JSON válido.  
  
```tsql  
SELECT id,json_col
FROM tab1
WHERE ISJSON(json_col)>0 
```  
  
 Para obtener más información, vea [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extraer un valor de texto JSON mediante la función JSON_VALUE  
 La función **JSON_VALUE** extrae un valor escalar de una cadena JSON.  
  
 En el ejemplo siguiente se extrae el valor de una propiedad JSON en una variable local.  
  
```tsql  
SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')  
```  
  
 Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extraer un objeto o una matriz de texto JSON mediante la función JSON_QUERY  
 La función **JSON_QUERY** extrae un objeto o una matriz de una cadena JSON.  
 
 En el ejemplo siguiente se muestra cómo devolver un fragmento de JSON en los resultados de la consulta.  
  
```tsql  
SELECT FirstName,LastName,JSON_QUERY(jsonInfo,'$.info.address') AS Address
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
  
|Query|**JSON_VALUE** devuelve|**JSON_QUERY** devuelve|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL o error|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL o error|  
|**$.b**|NULL o error|[1,2]|  
|**$.b[0]**|1|NULL o error|  
|**$.c**|hi|NULL o error|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>Probar JSON_VALUE y JSON_QUERY con la base de datos de ejemplo AdventureWorks  
 Pruebe las funciones integradas que se describen en este tema ejecutando los ejemplos siguientes con la base de datos de ejemplo AdventureWorks, que contiene datos JSON. Para obtener la base de datos de ejemplo AdventureWorks, [haga clic aquí](http://www.microsoft.com/en-us/download/details.aspx?id=49502).  
  
 En los ejemplos siguientes, la columna Info de la tabla SalesOrder_json contiene texto JSON.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Ejemplo 1: devolver columnas estándar y datos JSON  
 La consulta siguiente devuelve columnas y valores estándar y relacionales de una columna JSON.  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,Status,ShipDate,Status,AccountNumber,TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info)>0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Ejemplo 2: agregar y filtrar valores JSON  
 La consulta siguiente agrega subtotales por nombre de cliente (almacenados en JSON) y estado (almacenado en una columna normal). A continuación, filtra los resultados por ciudad (almacenados en JSON) y OrderDate (almacenados en una columna normal).  
  
```tsql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info,'$.Customer.Name') AS Customer,Status,SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info,'$.ShippingInfo.City')=@city
 AND OrderDate>'1/1/2015'
GROUP BY JSON_VALUE(Info,'$.Customer.Name'),Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> Actualizar valores de propiedad en texto JSON mediante la función JSON_MODIFY  
 La función **JSON_MODIFY**  actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.  
  
 En el siguiente ejemplo se actualiza el valor de una propiedad de una variable que contiene JSON.  
  
```tsql  
SET @info=JSON_MODIFY(@jsonInfo,"$.info.address[0].town",'London')    
```  
  
 Para obtener más información, vea [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-built-in-json-support-in-sql-server"></a>Más información sobre la compatibilidad integrada de JSON en SQL Server  
 [Entradas de blog del administrador de programas de Microsoft Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>Vea también  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [Expresiones de ruta de acceso JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  

