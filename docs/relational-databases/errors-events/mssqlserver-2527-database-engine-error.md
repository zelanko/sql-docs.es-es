---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bc2b1094a4ea7f8f6c2d2d60c804260286c5f237
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68085991"
---
# <a name="mssqlserver_2527"></a>MSSQLSERVER_2527
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|2527|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Texto del mensaje|No se puede procesar el índice I_NAME de la tabla O_NAME porque el grupo de archivos F_NAME se encuentra en modo sin conexión.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje informativo indica que no se puede comprobar el índice porque uno de los grupos de archivos que almacena datos para él se encuentra en modo sin conexión. El estado de los archivos en un grupo de archivos determina la disponibilidad de todo el grupo de archivos. Para que un grupo de archivos esté disponible, todos los archivos del grupo de archivos deben estar en línea. Si no hay ningún otro problema, todos los demás índices del mismo objeto se comprobarán.  
  
## <a name="user-action"></a>Acción del usuario  
Para ver el estado de los archivos correspondientes al grupo de archivos especificado, consulte la vista de catálogo **sys.database_files** o **sys.master_files**.  
  
Restaure el archivo sin conexión a partir de una copia de seguridad.  
  
## <a name="see-also"></a>Consulte también  
[sys.database_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
