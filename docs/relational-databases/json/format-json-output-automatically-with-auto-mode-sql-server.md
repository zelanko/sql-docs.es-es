---
title: "Aplicar formato a la salida JSON automáticamente con el modo AUTO (SQL Server) | Microsoft Docs"
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
- FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: cba250a399bb3de87c9713ac600c9807527a1cd9
ms.contentlocale: es-es
ms.lasthandoff: 06/09/2017

---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>Aplicar formato a la salida JSON automáticamente con el modo AUTO (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Para aplicar formato a la salida de la cláusula **FOR JSON** automáticamente en función de la estructura de la instrucción **SELECT**, especifique la opción **AUTO**.  
  
Con la opción **AUTO** , el formato de la salida JSON se determina automáticamente según el orden de las columnas en la lista SELECT y sus tablas de origen. No se puede cambiar este formato.
 
 La alternativa consiste en usar la opción **PATH** para mantener el control sobre la salida.
 -   Para obtener más información sobre la opción **PATH**, consulte [Format Nested JSON Output with PATH Mode](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md) (Aplicar formato a la salida JSON anidada con el modo PATH).
 -   Para obtener información general sobre ambas opciones, consulte [Format Query Results as JSON with FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) (Aplicar formato a los resultados de la consulta como JSON con FOR JSON).
  
 Una consulta que usa la opción **FOR JSON AUTO** debe tener una cláusula **FROM** .  
  
 Estos son algunos ejemplos de la cláusula **FOR JSON** con la opción **AUTO** .  
  
## <a name="examples"></a>Ejemplos  
 **Consulta 1**  
  
Los resultados de la cláusula FOR JSON AUTO son similares a los de FOR JSON PATH cuando se usa solo una tabla en la consulta. En este caso, FOR JSON AUTO no crea objetos anidados. La única diferencia es que FOR JSON AUTO genera alias separados por puntos (por ejemplo, `Info.MiddleName` en el siguiente ejemplo) como claves con puntos, no como objetos anidados.  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **Resultado 1**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info.MiddleName": "J"
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info.MiddleName": "Lee"
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info.Title": "Ms.",
    "Info.MiddleName": "A"
}]
```  
  
 **Consulta 2**  
  
 Al unir tablas, las columnas de la primera tabla se generan como propiedades del objeto raíz. Las columnas de la segunda tabla se generan como propiedades de un objeto anidado. El nombre de tabla o alias de la segunda tabla (por ejemplo, `D` en el ejemplo siguiente) se usa como el nombre de la matriz anidada.  
  
```sql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
 **Resultado 2**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO43659",
    "D": [{
        "UnitPrice": 34.40
    }, {
        "UnitPrice": 134.24,
        "OrderQty": 5
    }]
}]
```  
 
 **Consulta 3**  
 En lugar de usar FOR JSON AUTO, puede anidar una subconsulta FOR JSON PATH en la instrucción SELECT, como se muestra en el ejemplo siguiente. Este ejemplo produce el mismo resultado que el ejemplo anterior.  
  
```sql  
SELECT TOP 2  
    SalesOrderNumber,  
    OrderDate,  
    (SELECT UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail AS D  
      WHERE H.SalesOrderID = D.SalesOrderID  
     FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
 **Resultado 3**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO4390",
    "D": [{
        "UnitPrice": 24.99
    }]
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.

## <a name="see-also"></a>Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  

