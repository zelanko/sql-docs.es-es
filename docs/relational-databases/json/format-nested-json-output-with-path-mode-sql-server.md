---
description: Formato de salida JSON anidada con el modo PATH (SQL Server)
title: Formato de salida JSON anidada con el modo PATH
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e95ffd1cf5e75f95cc79dc127ac154abc4253a0d
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595131"
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>Formato de salida JSON anidada con el modo PATH (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sqlserver2016-asdb.md)]

Para mantener el control total sobre la salida de la cláusula **FOR JSON**, especifique la opción **PATH**.  
  
El modo **PATH** le permite crear objetos contenedores y anidar propiedades complejas. Los resultados reciben el formato de una matriz de objetos JSON.  
  
La alternativa es usar la opción **AUTO** para aplicar formato a la salida automáticamente en función de la estructura de la instrucción **SELECT**.
 -   Para más información sobre la opción **AUTO**, vea [Aplicar formato a la salida JSON automáticamente con el modo AUTO](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).
 -   Para obtener información general sobre ambas opciones, consulte [Format Query Results as JSON with FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) (Aplicar formato a los resultados de la consulta como JSON con FOR JSON).
 
Estos son algunos ejemplos de la cláusula **FOR JSON** con la opción **PATH** . Aplique formato a los resultados anidados utilizando nombres de columna separados por puntos o consultas anidadas, tal como se muestra en los ejemplos siguientes. De forma predeterminada los valores null no se incluyen en la salida de **FOR JSON**.  [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) es el editor de consultas recomendado para las consultas JSON porque da formato automáticamente a los resultados JSON (como se muestra en este artículo), en lugar de mostrar una cadena plana.

## <a name="example---dot-separated-column-names"></a>Ejemplo: nombres de columna separados por puntos  
La siguiente consulta da formato a las cinco primeras filas de la tabla AdventureWorks `Person` como JSON.  

La cláusula **FOR JSON PATH** usa el alias de columna o el nombre de columna para determinar el nombre de clave en la salida de JSON. Si un alias que contiene puntos, la opción PATH crea objetos anidados.  

 **Consultar**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH   
```  
  
 **Resultado**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
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
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>Ejemplo: varias tablas  
Si se hace referencia a más de una tabla en una consulta, **FOR JSON PATH** anida cada columna mediante su alias. La siguiente consulta crea un objeto JSON por par (OrderHeader, OrderDetails) combinado en la consulta. 
  
 **Consultar**  
  
```sql  
SELECT TOP 2 H.SalesOrderNumber AS 'Order.Number',  
        H.OrderDate AS 'Order.Date',  
        D.UnitPrice AS 'Product.Price',  
        D.OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH   
```  
  
 **Resultado**  
  
```json  
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Más información sobre JSON en SQL Server y Azure SQL Database  
  
### <a name="microsoft-videos"></a>Vídeos de Microsoft

Para obtener una introducción visual a la compatibilidad integrada de JSON en SQL Server y Azure SQL Database, vea los siguientes vídeos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 y compatibilidad con JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso de JSON en SQL Server 2016 y Azure SQL Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON como puente entre los universos NoSQL y relacional)

## <a name="see-also"></a>Consulte también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
