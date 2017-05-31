---
title: "Inclusión de valores Null en JSON - Opción INCLUDE_NULL_VALUES | Microsoft Docs"
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
- INCLUDE_NULL_VALUES (FOR JSON)
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 04389191586bf45a45a1771781858ec31e6f988a
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

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
  
```tsql  
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
  
## <a name="see-also"></a>Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

