---
title: ":: (Resolución de ámbito) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
dev_langs: TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4fa0fa1cd5a86ab4dc736803f6d4926b98f4a30
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="-scope-resolution-transact-sql"></a>:: (Resolución de ámbito) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  El operador de resolución de ámbito **::** proporciona acceso a los miembros estáticos de un tipo de datos compuesto. Un tipo de datos compuesto es aquel que contiene varios tipos de datos simples y métodos, como los tipos integrados de CLR y tipos personalizados de SQLCLR User-Defined (UDT).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo usar el operador de resolución de ámbito para obtener acceso al miembro `GetRoot()` del tipo `hierarchyid`.  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
