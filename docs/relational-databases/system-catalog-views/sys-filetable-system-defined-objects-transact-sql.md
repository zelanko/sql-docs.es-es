---
title: Sys.filetable_system_defined_objects (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a9d4cdb95349c9af9416caca7ca8dcf8893c0b4d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33178571"
---
# <a name="sysfiletablesystemdefinedobjects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra una lista de los objetos definidos por el sistema relacionados con objetos FileTable. Contiene una fila por cada objeto definido por el sistema.  
  
 Cuando se crea un objeto FileTable, los objetos relacionados como restricciones e índices se crean al mismo tiempo. No puede modificar ni quitar estos objetos; desaparecen solo cuando se quita el propio objeto FileTable.  
  
 Para más información sobre FileTables, vea [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
|Columna|Data type|Description|  
|------------|---------------|-----------------|  
|**object_id**|**int**|Identificador de objeto del objeto definido por el sistema relacionado con una tabla FileTable.<br /><br /> Hace referencia al objeto en **sys.objects**.|  
|**parent_object_id**|**int**|Identificador de objeto de la tabla FileTable primaria.<br /><br /> Hace referencia al objeto en **sys.objects**.|  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
