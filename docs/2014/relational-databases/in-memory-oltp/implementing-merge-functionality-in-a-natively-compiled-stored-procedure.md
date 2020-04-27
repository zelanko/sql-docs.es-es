---
title: Implementar la funcionalidad de combinación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0e108f70f66aef1ed88ea202ddb326bd0757c10
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63015926"
---
# <a name="implementing-merge-functionality"></a>Implementar la funcionalidad MERGE
  Una base de datos puede necesitar realizar una inserción o una actualización, dependiendo de si una fila determinada ya existe en la base de datos.  
  
 Es posible usar el siguiente método en [!INCLUDE[tsql](../../includes/tsql-md.md)] sin hacer uso de la instrucción `MERGE`:  
  
```sql  
UPDATE mytable SET col=@somevalue WHERE myPK = @parm  
IF @@ROWCOUNT = 0  
    INSERT mytable (columns) VALUES (@parm, @other values)  
```  
  
 Otro método para implementar una combinación en [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
```sql  
IF EXISTS (SELECT 1 FROM mytable WHERE myPK = @parm)  
    UPDATE....  
ELSE  
    INSERT  
```  
  
 Para un procedimiento almacenado compilado de forma nativa:  
  
```sql  
DECLARE @i  int  = 0  -- or whatever your PK data type is  
UPDATE mytable SET @i=myPK, othercolums = other values WHERE myPK = @parm  
IF @i = 0  
   INSERT....  
```  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones de Transact-SQL no admitidas en In-Memory OLTP.](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
