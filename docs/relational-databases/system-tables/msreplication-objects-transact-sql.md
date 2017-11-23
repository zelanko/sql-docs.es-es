---
title: MSreplication_objects (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs: TSQL
helpviewer_keywords: MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf9eef9834dca254f153c8f7a984f77a1ad33c0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationobjects-transact-sql"></a>MSreplication_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplication_objects** tabla contiene una fila por cada objeto que está asociado con la replicación de la base de datos de suscriptor. Esta tabla se almacena en la base de datos de suscripción.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|El nombre del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**object_name**|**sysname**|Nombre del objeto.|  
|**object_type**|**Char(2)**|El tipo de objeto:<br /><br /> **u** = tabla.<br /><br /> **t** = desencadenador.<br /><br /> **p** = procedimiento almacenado.|  
|**artículo**|**sysname**|Nombre del artículo con el que está asociado el objeto.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
