---
title: Implementar la funcionalidad MERGE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80dd5a9fc01d6577e67e2bed6ad0b934a6652af1
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394125"
---
# <a name="implementing-merge-functionality"></a>Implementar la funcionalidad MERGE
  Una base de datos puede necesitar realizar una inserción o una actualización, dependiendo de si una fila determinada ya existe en la base de datos.  
  
 Sin usar el `MERGE` instrucción, el siguiente es un enfoque que puede usar en [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```tsql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 Otro método para implementar una combinación en [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
```tsql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE….  
ELSE  
    INSERT  
```  
  
 Para un procedimiento almacenado compilado de forma nativa:  
  
```tsql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT….  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
