---
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 08f8ea872ef58a42b07254417db0a19a5dfd9fd7
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3156"></a>MSSQLSERVER_3156
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|3156|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_CANT_WRITE|  
|Texto del mensaje|El archivo '%ls' no se puede restaurar en '%ls'. Utilice WITH MOVE para identificar una ubicación válida para el archivo.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje general identifica los nombres lógicos o físicos de los archivos que no se pudieron restaurar debido a un problema con la ubicación especificada.  
  
### <a name="possible-causes"></a>Posibles causas  
Entre las posibles causas figuran las siguientes:  
  
-   Es posible que necesite acceso al directorio de Windows especificado.  
  
-   Es posible que haya escrito incorrectamente la ruta de acceso o que haya especificado una que no existe.  
  
-   Es posible que un archivo que no se puede sobrescribir esté utilizando el nombre de archivo.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe si en los registros de errores existen otros mensajes que proporcionen más información.  
  
Corrija el problema relacionado con la ubicación especificada. Por ejemplo, conceda acceso o utilice la opción WITH MOVE en la instrucción RESTORE para colocar el archivo en otra ubicación.  
  
## <a name="see-also"></a>Vea también  
[Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  

