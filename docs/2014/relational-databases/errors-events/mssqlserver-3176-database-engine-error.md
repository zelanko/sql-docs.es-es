---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f6ecd8482645db1cf8b070de8d82ed0012dae01f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417394"
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
 [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
