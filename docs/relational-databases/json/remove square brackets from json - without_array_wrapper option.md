---
title: "Quitar corchetes de la salida JSON con la opci&#243;n WITHOUT_ARRAY_WRAPPER (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WITHOUT_ARRAY_WRAPPER"
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Quitar corchetes de la salida JSON con la opci&#243;n WITHOUT_ARRAY_WRAPPER (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para quitar los corchetes que rodean la salida JSON de la cláusula **FOR JSON** de manera predeterminada, especifique la opción **WITHOUT_ARRAY_WRAPPER**. Use esta opción para generar un objeto JSON único como salida.  
  
 Si no especifica esta opción, la salida JSON aparecerá entre corchetes.  
  
## Ejemplos  
 En el ejemplo siguiente se muestra la salida de la cláusula **FOR JSON** con y sin la opción **WITHOUT_ARRAY_WRAPPER**.  
  
 **Query**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 **Resultado** Con la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{ "year":2015, "month":12, "day":15 }  
```  
  
 **Resultado** Sin la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[ { "year":2015, "month":12, "day":15 } ]  
```  
  
 Este es otro ejemplo de una cláusula **FOR JSON** con la opción **WITHOUT_ARRAY_WRAPPER**.  
  
 **Query**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 **Resultado** Con la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{  
    "SalesOrderNumber":"SO43660",  
    "OrderDate":"2011-05-31T00:00:00",  
    "Status":5  
}  
```  
  
 **Resultado** Sin la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[  
    {  
        "SalesOrderNumber":"SO43660",  
        "OrderDate":"2011-05-31T00:00:00",  
        "Status":5  
    }  
]  
```  
  
## Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  