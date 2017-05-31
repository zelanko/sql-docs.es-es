---
title: "Eliminación de corchetes de JSON: opción WITHOUT_ARRAY_WRAPPER | Microsoft Docs"
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
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea60d5a74c680e9c2aba571a76815f77913da471
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Eliminación de corchetes de JSON: opción WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para quitar los corchetes que rodean la salida JSON de la cláusula **FOR JSON** de manera predeterminada, especifique la opción **WITHOUT_ARRAY_WRAPPER** . Use esta opción para generar un objeto JSON único como resultado en lugar de una matriz.  
  
 Si no especifica esta opción, la salida JSON aparecerá entre corchetes.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra la salida de la cláusula **FOR JSON** con y sin la opción **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Resultado** con la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Resultado** sin la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  
  
 Este es otro ejemplo de una cláusula **FOR JSON** con y sin la opción **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Resultado** con la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Resultado** sin la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  
  
## <a name="see-also"></a>Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

