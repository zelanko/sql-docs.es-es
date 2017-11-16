---
title: "Inclusión de valores Null en JSON - Opción INCLUDE_NULL_VALUES | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a44f712ecec89a1a5aae2f19f505c7a924b120d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="include-null-values-in-json---includenullvalues-option"></a>Inclusión de valores Null en JSON - Opción INCLUDE_NULL_VALUES
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Para incluir valores NULL en la salida JSON de la cláusula **FOR JSON** , especifique la opción **INCLUDE_NULL_VALUES** .  
  
 Si no especifica la opción **INCLUDE_NULL_VALUES** , la salida JSON no incluye propiedades para valores NULL en los resultados de consulta.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra la salida de la cláusula **FOR JSON** con y sin la opción **INCLUDE_NULL_VALUES** .  
  
|Sin la opción **INCLUDE_NULL_VALUES**|Con la opción **INCLUDE_NULL_VALUES**|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 Este es otro ejemplo de una cláusula **FOR JSON** con la opción **INCLUDE_NULL_VALUES** .  
  
 **Query**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES    
```  
  
 **Resultado**  
  
```json  
[{
    "name": "John",
    "surname": null
}, {
    "name": "Jane",
    "surname": "Doe"
}] 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Más información sobre la compatibilidad integrada de JSON en SQL Server  
Para obtener una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte las [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en Azure SQL Database ofrecidas por el director de programas de Microsoft Jovan Popovic.  

## <a name="see-also"></a>Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
