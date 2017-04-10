---
title: "Inclusi&#243;n valores Null en la salida JSON con la opci&#243;n INCLUDE_NULL_VALUES (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "INCLUDE_NULL_VALUES (para JSON)"
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# Inclusi&#243;n valores Null en la salida JSON con la opci&#243;n INCLUDE_NULL_VALUES (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para incluir valores NULL en la salida JSON de la cláusula **FOR JSON**, especifique la opción **INCLUDE_NULL_VALUES**.  
  
 Si no especifica la opción **INCLUDE_NULL_VALUES**, la salida JSON no incluye propiedades para valores NULL en los resultados de consulta.  
  
## Ejemplos  
 En el ejemplo siguiente se muestra la salida de la cláusula **FOR JSON** con y sin la opción **INCLUDE_NULL_VALUES**.  
  
|Sin la opción **INCLUDE_NULL_VALUES**|Con la opción **INCLUDE_NULL_VALUES**|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 Este es otro ejemplo de una cláusula **FOR JSON** con la opción **INCLUDE_NULL_VALUES**.  
  
 **Query**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES  
```  
  
 **Resultado**  
  
```json  
[   
   {"name": "John",  "surname": null },  
   {"name": "Jane",  "surname": "Doe"}  
]  
```  
  
## Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  