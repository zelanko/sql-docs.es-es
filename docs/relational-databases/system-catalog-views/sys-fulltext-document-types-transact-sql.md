---
title: Sys.fulltext_document_types (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs: TSQL
helpviewer_keywords: sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3cda70f0c9ada37d6c805eefc7209a1ac7e0ca11
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysfulltextdocumenttypes-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada tipo de documento disponible para operaciones de indización de texto completo. Cada fila representa la interfaz IFilter registrada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|Extensión de archivo del tipo de documento admitido.<br /><br /> Este valor se puede usar para identificar el filtro que se usará durante la indización de texto completo de las columnas de tipo **varbinary (max)** o **imagen**.|  
|**class_id**|**uniqueidentifier**|GUID de la clase de IFilter que admite la extensión de archivo.|  
|**ruta de acceso**|**nvarchar (260)**|Ruta de acceso al archivo DLL de IFilter. La ruta de acceso solo es visible para los miembros del rol fijo de servidor **serveradmin** .|  
|**version**|**sysname**|Versión del archivo DLL de IFilter.|  
|**fabricante**|**sysname**|Nombre del fabricante de IFilter.<br /><br /> Nota: Solo los documentos con el fabricante como [!INCLUDE[msCoName](../../includes/msconame-md.md)] se admiten en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
