---
title: suspect_pages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70dffcbf2ac3eac13f7ef42e901c4fcd99dce769
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130551"
---
# <a name="suspectpages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada página que se produjo un error 823 secundario o un error 824. Se hace una lista de páginas en esta tabla porque se sospecha que estén dañadas, pero es posible que, en realidad, sean correctas. Cuando se repara una página sospechosa, su estado se actualiza en el **event_type** columna.  
  
 La tabla siguiente, que tiene un límite de 1.000 filas, se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de la base de datos a la que se aplica esta página.|  
|**file_id**|**int**|Id. del archivo en la base de datos.|  
|**page_id**|**bigint**|Id. de la página sospechosa. Cada página incluye un valor de 32 bits de Id. de página que identifica su ubicación en la base de datos. El **page_id** es el desplazamiento en el archivo de datos de la página de 8 KB. Los Id. de página son únicos en un archivo.|  
|**event_type**|**int**|Tipo de error; puede ser uno de los siguientes:<br /><br /> 1 = Un error 823 que produce una página sospechosa (como un error de disco) o un error 824 distinto de una suma de comprobación incorrecta o una página rasgada (como un Id. de página no válido).<br /><br /> 2 = Suma de comprobación incorrecta.<br /><br /> 3 = Página rasgada.<br /><br /> 4 = Restaurada (la página se restauró después de marcarse como incorrecta).<br /><br /> 5 = Reparada (DBCC ha reparado la página).<br /><br /> 7 = Desasignada por DBCC.|  
|**error_count**|**int**|Número de veces que ha ocurrido el error.|  
|**last_update_date**|**datetime**|Marca de fecha y hora de la última actualización.|  
  
## <a name="permissions"></a>Permisos  
 Cualquier persona con acceso a **msdb** puede leer los datos de la tabla **suspect_pages** . Cualquier persona con el permiso UPDATE en la tabla suspect_pages puede actualizar sus registros. Los miembros del rol fijo de base de datos **db_owner** de **msdb** o el rol fijo de servidor **sysadmin** pueden insertar, actualizar y eliminar registros.  
  
## <a name="see-also"></a>Vea también  
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Clase de eventos de página de datos sospechosos de base de datos](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [Las tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
