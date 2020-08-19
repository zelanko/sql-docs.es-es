---
description: sys.dm_fts_fdhosts (Transact-SQL)
title: Sys. dm_fts_fdhosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d282a4d64f82420a37a991d95e81422f019bc4d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489904"
---
# <a name="sysdm_fts_fdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve información sobre la actividad actual de los host de demonio de filtro en la instancia de servidor.  
  
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|Id. del host de demonio de filtro.|  
|**fdhost_name**|**nvarchar(120)**|Nombre del host de demonio de filtro.|  
|**fdhost_process_id**|**int**|Id. de proceso de Windows del host de demonio de filtro.|  
|**fdhost_type**|**nvarchar(120)**|Tipo de documento que procesa el host de demonio de filtro, que puede ser uno de los siguientes:<br /><br /> Subproceso único<br /><br /> Varios subprocesos<br /><br /> Documento gigante|  
|**max_thread**|**int**|Número máximo de subprocesos del host de demonio de filtro.|  
|**batch_count**|**int**|Número de lotes que se procesan en el host de demonio de filtro.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el  **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el nombre del host de demonio de filtro y el número máximo de subprocesos que contiene. También supervisa el número de lotes que se procesan actualmente en el demonio de filtro. Esta información se puede utilizar para evaluar el rendimiento.  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones y vistas de administración dinámica de la búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
