---
title: Copias de seguridad parciales (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4213bcee1d17d27bf63da9eb286b21dea4cc5a02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921935"
---
# <a name="partial-backups-sql-server"></a>Copias de seguridad parciales (SQL Server)
  Todos los modelos de recuperación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten copias de seguridad parciales, por lo que este tema es aplicable a todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, las copias de seguridad parciales están diseñadas para usarse con el modelo de recuperación simple a fin de mejorar la flexibilidad al realizar copias de seguridad de bases de datos de gran tamaño que contienen uno o varios grupos de archivos de solo lectura.  
  
 Las copias de seguridad parciales resultan útiles cuando desea excluir grupos de archivos de solo lectura. Una *copia de seguridad parcial* es similar a una copia de seguridad de base de datos completa, pero no contiene todos los grupos de archivos. En lugar de ello, en el caso de una base de datos de lectura y escritura, una copia de seguridad parcial contiene todos los datos del grupo de archivos principal, todos los grupos de archivos de lectura/escritura y, de manera opcional, uno o varios archivos de solo lectura. Una copia de seguridad parcial de una base de datos de solo lectura contiene únicamente el grupo de archivos principal.  
  
> [!NOTE]  
>  Si después de una copia de seguridad parcial se modifica el permiso de una base de datos de solo lectura a lectura y escritura, es posible que se creen grupos de archivos secundarios de lectura y escritura que no figuren en la copia de seguridad parcial. En este caso, si intenta realizar una copia de seguridad diferencial parcial, el proceso producirá un error. Antes de poder efectuar una copia de seguridad diferencial parcial de la base de datos, es preciso crear otra copia de seguridad parcial. La nueva copia de seguridad parcial contiene todos los grupos de archivos secundarios de lectura /escritura y puede servir como base para las copias de seguridad diferenciales parciales.  
  
 Las copias de seguridad de archivos de los grupos de archivos de solo lectura se pueden combinar con copias de seguridad parciales. Para obtener información sobre las copias de seguridad de archivos, vea [Copias de seguridad de archivos completas &#40;SQL Server&#41;](full-file-backups-sql-server.md).  
  
 Una copia de seguridad parcial puede utilizarse como *base diferencial* para realizar copias de seguridad diferenciales parciales. Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
> [!NOTE]  
>  Las copias de seguridad parciales no son compatibles con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ni con el Asistente para planes de mantenimiento.  
  
 **Para crear una copia de seguridad parcial**  
  
-   [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) (READ_WRITE_FILEGROUPS; opción FILEGROUP, si es necesario)  
  
 **Para usar una copia de seguridad parcial en una secuencia de restauración**  
  
-   [Ejemplo: restauración por etapas de la base de datos &#40;modelo de recuperación simple&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación simple&#41;](file-restores-simple-recovery-model.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
