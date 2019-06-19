---
title: Realizar una copia de seguridad en un conjunto de medios reflejado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88ea15fabe8e8fd6630d3430417879c7104dff67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876993"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Realizar una copia de seguridad en un conjunto de medios reflejado (Transact-SQL)
  En este tema se describe cómo usar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)][de](/sql/t-sql/statements/backup-transact-sql) para especificar un conjunto de medios reflejado cuando se realiza una copia de seguridad de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En la instrucción BACKUP, especifique el primer reflejo en la cláusula TO. A continuación, especifique cada reflejo en su propia cláusula MIRROR TO. Las cláusulas TO y MIRROR TO deben especificar el mismo número y tipo de dispositivo de copia de seguridad.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se crea el conjunto de medios reflejado de la ilustración anterior y se realiza una copia de seguridad de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en ambos reflejos.  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 **Para restaurar a partir de una copia de seguridad reflejada**  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)  
  
  
