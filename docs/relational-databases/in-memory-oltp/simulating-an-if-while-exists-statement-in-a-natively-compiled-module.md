---
title: "Simular una instrucción IF-WHILE EXISTS en un módulo compilado de forma nativa | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d509d0d749591a134a0b87aa457bb53d28901a99
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>Simular una instrucción IF-WHILE EXISTS en un módulo compilado de forma nativa
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Los procedimientos almacenados compilados de forma nativa no admiten la cláusula **EXISTS** en instrucciones condicionales como IF y WHILE.  
  
 En el ejemplo siguiente se muestra una solución mediante una variable BIT con una instrucción SELECT para simular una cláusula EXISTS:  
  
```tsql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones Transact-SQL no admitidas por OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
