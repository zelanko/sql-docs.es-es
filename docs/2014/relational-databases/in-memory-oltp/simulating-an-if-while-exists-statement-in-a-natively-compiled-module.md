---
title: Simular una cláusula EXISTS en un procedimiento almacenado compilado de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac041e19aeb5948a644a9fcf82b3e687472b7259
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535627"
---
# <a name="simulating-an-exists-clause-in-a-natively-compiled-stored-procedure"></a>Simular una cláusula EXISTS en un procedimiento almacenado compilado de forma nativa
  Los procedimientos almacenados compilados de forma nativa no admiten la cláusula `EXISTS`, pero existe una solución:  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
