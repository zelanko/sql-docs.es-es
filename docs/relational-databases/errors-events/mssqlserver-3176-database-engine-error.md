---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cca32f5a1a2947dc65cf85976874ce1043de0e3d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|3176|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_FILE_CLAIM|  
|Texto del mensaje|El archivo '%ls' fue reclamado por '%ls'(%d) y '%ls'(%d). Se puede utilizar la cláusula WITH MOVE para cambiar la ubicación de uno o más archivos.|  
  
## <a name="explanation"></a>Explicación  
Se ha intentado utilizar un archivo para más de un propósito.  
  
### <a name="possible-causes"></a>Posibles causas  
Otra base de datos ya está utilizando el nombre de archivo.  
  
## <a name="user-action"></a>Acción del usuario  
Restaure los archivos de la base de datos en otra ubicación. En una instrucción RESTORE, utilice una cláusula WITH MOVE para mover cada archivo. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], cambie las ubicaciones de los archivos en la cuadrícula **Restaurar los archivos de base de datos como** del cuadro de diálogo **Opciones de Restaurar base de datos**.  
  
## <a name="see-also"></a>Vea también  
[Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  

