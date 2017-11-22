---
title: MSarticles (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs: TSQL
helpviewer_keywords: MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 458e353da5dd67489565948892b8a51025658fd8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSarticles** tabla contiene una fila por cada artículo replicado por un publicador. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**iddeeditor**|**smallint**|El identificador del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**artículo**|**sysname**|El nombre del artículo.|  
|**article_id**|**int**|Id. del artículo.|  
|**destination_object**|**sysname**|Nombre de la tabla creada en el suscriptor.|  
|**source_owner**|**sysname**|Nombre del esquema de la tabla de origen en el publicador.|  
|**source_object**|**sysname**|El nombre del objeto de origen desde el que se va a agregar el artículo.|  
|**Descripción**|**nvarchar(255)**|Descripción del artículo.|  
|**destination_owner**|**sysname**|Nombre del esquema de la tabla creada en el suscriptor.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
