---
title: Simular una cláusula EXISTS en un procedimiento almacenado compilado de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6d13d9df9d511aed94332459ca4aef94fd6c68e
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395773"
---
# <a name="simulating-an-exists-clause-in-a-natively-compiled-stored-procedure"></a>Simular una cláusula EXISTS en un procedimiento almacenado compilado de forma nativa
  Los procedimientos almacenados compilados de forma nativa no admiten la cláusula `EXISTS`, pero existe una solución:  
  
```tsql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
