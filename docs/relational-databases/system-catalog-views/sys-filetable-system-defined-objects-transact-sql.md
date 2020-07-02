---
title: Sys. filetable_system_defined_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0232a635267dc97f53f67309fb59d06651d918ce
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786437"
---
# <a name="sysfiletable_system_defined_objects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Muestra una lista de los objetos definidos por el sistema relacionados con objetos FileTable. Contiene una fila por cada objeto definido por el sistema.  
  
 Cuando se crea un objeto FileTable, los objetos relacionados como restricciones e índices se crean al mismo tiempo. No puede modificar ni quitar estos objetos; desaparecen solo cuando se quita el propio objeto FileTable.  
  
 Para más información sobre FileTables, vea [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
|Columna|Tipo de datos|Descripción|  
|------------|---------------|-----------------|  
|**object_id**|**int**|Identificador de objeto del objeto definido por el sistema relacionado con una tabla FileTable.<br /><br /> Hace referencia al objeto de **Sys. Objects**.|  
|**parent_object_id**|**int**|Identificador de objeto de la tabla FileTable primaria.<br /><br /> Hace referencia al objeto de **Sys. Objects**.|  
  
## <a name="see-also"></a>Consulte también  
 [Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
