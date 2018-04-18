---
title: suspect_pages (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ca051495ebe4d429299243512b4952c4cd28111
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="suspectpages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada página que causó un error 823 secundario o un error 824. Se hace una lista de páginas en esta tabla porque se sospecha que estén dañadas, pero es posible que, en realidad, sean correctas. Cuando se repara una página sospechosa, su estado se actualiza en la **event_type** columna.  
  
 La tabla siguiente, que tiene un límite de 1.000 filas, se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de la base de datos a la que se aplica esta página.|  
|**file_id**|**int**|Id. del archivo en la base de datos.|  
|**page_id**|**bigint**|Id. de la página sospechosa. Cada página incluye un valor de 32 bits de Id. de página que identifica su ubicación en la base de datos. El **page_id** es el desplazamiento en el archivo de datos de la página de 8 KB. Los Id. de página son únicos en un archivo.|  
|**event_type**|**int**|Tipo de error; puede ser uno de los siguientes:<br /><br /> 1 = Un error 823 que produce una página sospechosa (como un error de disco) o un error 824 distinto de una suma de comprobación incorrecta o una página rasgada (como un Id. de página no válido).<br /><br /> 2 = Suma de comprobación incorrecta.<br /><br /> 3 = Página rasgada.<br /><br /> 4 = Restaurada (la página se restauró después de marcarse como incorrecta).<br /><br /> 5 = Reparada (DBCC ha reparado la página).<br /><br /> 7 = Desasignada por DBCC.|  
|**error_count**|**int**|Número de veces que ha ocurrido el error.|  
|**last_update_date**|**datetime**|Marca de fecha y hora de la última actualización.|  
  
## <a name="permissions"></a>Permissions  
 Cualquier persona con acceso a **msdb** puede leer los datos de la tabla **suspect_pages** . Cualquier persona con el permiso UPDATE en la tabla suspect_pages puede actualizar sus registros. Los miembros del rol fijo de base de datos **db_owner** de **msdb** o el rol fijo de servidor **sysadmin** pueden insertar, actualizar y eliminar registros.  
  
## <a name="see-also"></a>Vea también  
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Clase de eventos de página de datos sospechosa de base de datos](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
