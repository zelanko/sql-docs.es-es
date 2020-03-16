---
title: Validar, consultar y cambiar datos JSON con funciones integradas
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ddc5fb198a62374fc43ebacb5fa7423ac9fadd5
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287899"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Validar, consultar y cambiar datos JSON con funciones integradas (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La compatibilidad integrada con JSON incluye las siguientes funciones integradas que se describen brevemente en este tema.  
  
-   [ISJSON](#ISJSON) prueba si una cadena contiene un valor JSON válido.  
  
-   [JSON_VALUE](#VALUE) extrae un valor escalar de una cadena JSON.  
  
-   [JSON_QUERY](#QUERY) extrae un objeto o una matriz de una cadena JSON.  
  
-   [JSON_MODIFY](#MODIFY) actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Texto de JSON para los ejemplos de esta página

En los ejemplos de esta página se usa el texto JSON similar al contenido que se muestra en el ejemplo siguiente:

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller",
         "givenName": "Lisa",
         "gender": "female",
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Este documento JSON, que contiene elementos complejos anidados, se almacena en la tabla de ejemplo siguiente:

```sql
CREATE TABLE Families (
   id int identity constraint PK_JSON_ID primary key,
   doc nvarchar(max)
)
``` 

##  <a name="ISJSON"></a> Validar texto JSON mediante la función ISJSON  
 La función **ISJSON** prueba si una cadena contiene un valor JSON válido.  
  
En el ejemplo siguiente, se devuelven las filas en las que la columna JSON contiene texto JSON válido. Tenga en cuenta que sin una restricción JSON explícita, puede escribir cualquier texto en la columna NVARCHAR:  
  
```sql  
SELECT *
FROM Families
WHERE ISJSON(doc) > 0 
```  

Para obtener más información, vea [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extraer un valor de texto JSON mediante la función JSON_VALUE  
La función **JSON_VALUE** extrae un valor escalar de una cadena JSON. La consulta siguiente devolverá los documentos en los que el campo JSON `id`coincida con el valor `AndersenFamily`, ordenados por y los campos JSON `city` y `state`:

```sql  
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       JSON_VALUE(f.doc, '$.address.county') AS County
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
ORDER BY JSON_VALUE(f.doc, '$.address.city') DESC, JSON_VALUE(f.doc, '$.address.state') ASC
```  

Los resultados de esta consulta se muestran en la tabla siguiente:

| Nombre | City | County |
| --- | --- | --- |
| AndersenFamily | NY | Manhattan |

Para obtener más información, vea [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extraer un objeto o una matriz de texto JSON mediante la función JSON_QUERY  

La función **JSON_QUERY** extrae un objeto o una matriz de una cadena JSON. En el ejemplo siguiente se muestra cómo devolver un fragmento de JSON en los resultados de la consulta.  
  
```sql
SELECT JSON_QUERY(f.doc, '$.address') AS Address,
       JSON_QUERY(f.doc, '$.parents') AS Parents,
       JSON_QUERY(f.doc, '$.parents[0]') AS Parent0
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
```  
Los resultados de esta consulta se muestran en la tabla siguiente:

| Dirección | Parents | Parent0 |
| --- | --- | --- |
| { "state": "NY", "county": "Manhattan", "city": "NY" } | [{ "familyName": "Wakefield", "givenName": "Robin" }, {"familyName": "Miller", "givenName": "Ben" } ]| { "familyName": "Wakefield", "givenName": "Robin" } |

Para obtener más información, vea [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  

## <a name="parse-nested-json-collections"></a>Análisis de colecciones JSON anidadas

La función `OPENJSON` permite transformar la submatriz JSON en el conjunto de filas y, después, combinarlo con el elemento primario. Como ejemplo, puede devolver todos los documentos de la familia y "unirlos" con sus objetos `children` que se almacenan como una matriz de JSON interna:

```sql
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       c.givenName, c.grade
FROM Families f
        CROSS APPLY OPENJSON(f.doc, '$.children')
            WITH(grade int, givenName nvarchar(100))  c
```

Los resultados de esta consulta se muestran en la tabla siguiente:

| Nombre | City | givenName | grade |
| --- | --- | --- | --- |
| AndersenFamily | NY | Jesse | 1 |
| AndersenFamily | NY | Lisa | 8 |

Se obtienen dos filas como resultado porque una fila primaria se combina con dos filas secundarias generadas mediante el análisis de dos elementos de la submatriz secundaria. La función `OPENJSON` analiza el fragmento `children` de la columna `doc` y devuelve `grade` y `givenName` de cada elemento como un conjunto de filas. Este conjunto de filas se puede combinar con el documento primario.
 
## <a name="query-nested-hierarchical-json-sub-arrays"></a>Consulta de submatrices JSON jerárquicas anidadas

Puede aplicar varias llamadas `CROSS APPLY OPENJSON` para consultar estructuras JSON anidadas. El documento JSON que se usa en este ejemplo tiene una matriz anidada denominada `children`, donde cada elemento secundario tiene una matriz anidada de `pets`. La consulta siguiente analizará los elementos secundarios de cada documento, devolverá cada objeto de matriz como una fila y, después, analizará la matriz `pets`:

```sql
SELECT  familyName,
    c.givenName AS childGivenName,
    c.firstName AS childFirstName,
    p.givenName AS petName 
FROM Families f 
    CROSS APPLY OPENJSON(f.doc) 
        WITH (familyName nvarchar(100), children nvarchar(max) AS JSON)
        CROSS APPLY OPENJSON(children) 
        WITH (givenName nvarchar(100), firstName nvarchar(100), pets nvarchar(max) AS JSON) as c
            OUTER APPLY OPENJSON (pets)
            WITH (givenName nvarchar(100))  as p
```

La primera llamada a `OPENJSON` devolverá un fragmento de la matriz `children` mediante la cláusula AS JSON. Este fragmento de matriz se proporcionará a la segunda función `OPENJSON` que devolverá `givenName`, `firstName` de cada elemento secundario, así como la matriz de `pets`. La matriz de `pets` se proporcionará a la tercera función `OPENJSON`, que devolverá el valor `givenName` de la mascota.
Los resultados de esta consulta se muestran en la tabla siguiente:

| familyName | childGivenName | childFirstName | petName |
| --- | --- | --- | --- |
| AndersenFamily | Jesse | Merriam | Goofy |
| AndersenFamily | Jesse | Merriam | Shadow |
| AndersenFamily | Lisa | Miller| `NULL` |

El documento raíz se combina con dos filas `children` devueltas por la primera llamada a `OPENJSON(children)`, lo que genera dos filas (o tuplas). Después, cada fila se combina con las filas nuevas generadas por `OPENJSON(pets)` mediante el operador `OUTER APPLY`. Jesse tiene dos mascotas, por lo que `(AndersenFamily, Jesse, Merriam)` se combina con dos filas generadas para Goofy y Shadow. Lisa no tiene mascotas, por lo que `OPENJSON(pets)` no devuelve filas para esta tupla. Pero como se usa `OUTER APPLY`, se obtiene `NULL` en la columna. Si se coloca `CROSS APPLY` en lugar de `OUTER APPLY`, Lisa no se devolverá en el resultado, porque no hay ninguna fila de mascotas que se pueda combinar con esta tupla.

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
  
|Path|**JSON_VALUE** devuelve|**JSON_QUERY** devuelve|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL o error|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL o error|  
|**$.b**|NULL o error|[1,2]|  
|**$.b[0]**|1|NULL o error|  
|**$.c**|hi|NULL o error|  
  
## <a name="test-json_value-and-json_query-with-the-adventureworks-sample-database"></a>Probar JSON_VALUE y JSON_QUERY con la base de datos de ejemplo AdventureWorks  
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
  
### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)
  
## <a name="see-also"></a>Consulte también  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [Expresiones de ruta de acceso JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
