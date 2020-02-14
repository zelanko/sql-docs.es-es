---
title: Realizar una copia de seguridad en un conjunto de medios reflejado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b498aaa0a5a82294bc68942a68859939aff0fb7f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67940857"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>Realizar una copia de seguridad en un conjunto de medios reflejado (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se explica cómo usar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) para especificar un conjunto de medios reflejado cuando se realiza una copia de seguridad de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En la instrucción BACKUP, especifique el primer reflejo en la cláusula TO. A continuación, especifique cada reflejo en su propia cláusula MIRROR TO. Las cláusulas TO y MIRROR TO deben especificar el mismo número y tipo de dispositivo de copia de seguridad.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se crea el conjunto de medios reflejado de la ilustración anterior y se realiza una copia de seguridad de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en ambos reflejos.  
  
```sql  
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
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
