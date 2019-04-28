---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f1d2bd9bd3ee1cc26c0bd488af0dd7891d2a8741
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868866"
---
# <a name="mssqlserver2527"></a>MSSQLSERVER_2527
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2527|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Texto del mensaje|No se puede procesar el índice I_NAME de la tabla O_NAME porque el grupo de archivos F_NAME se encuentra en modo sin conexión.|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje informativo indica que no se puede comprobar el índice porque uno de los grupos de archivos que almacena datos para él se encuentra en modo sin conexión. El estado de los archivos en un grupo de archivos determina la disponibilidad de todo el grupo de archivos. Para que un grupo de archivos esté disponible, todos los archivos del grupo de archivos deben estar en línea. Si no hay ningún otro problema, todos los demás índices del mismo objeto se comprobarán.  
  
## <a name="user-action"></a>Acción del usuario  
 Para ver el estado de los archivos correspondientes al grupo de archivos especificado, consulte la vista de catálogo **sys.database_files** o **sys.master_files**.  
  
 Restaure el archivo sin conexión a partir de una copia de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
