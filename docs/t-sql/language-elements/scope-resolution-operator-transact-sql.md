---
description: ':: (Resolución de ámbito)'
title: ':: (Resolución de ámbito) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c319d0e7e67605f09954e88434842be9b8ae1df
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124388"
---
# <a name="-scope-resolution-transact-sql"></a>:: (Resolución de ámbito)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  El operador de resolución de ámbito **::** proporciona acceso a los miembros estáticos de un tipo de datos compuesto. Un tipo de datos compuesto es aquel que contiene varios métodos y tipos de datos simples. En los tipos de datos compuestos, se incluyen los tipos de CLR integrados y los tipos definidos por el usuario de SQLCLR personalizados (UDT).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo usar el operador de resolución de ámbito para obtener acceso al miembro `GetRoot()` del tipo `hierarchyid`.  
  
```sql  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>Consulte también  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
 
