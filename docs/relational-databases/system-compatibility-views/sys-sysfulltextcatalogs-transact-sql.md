---
title: Sys.sysfulltextcatalogs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysfulltextcatalogs
- sys.sysfulltextcatalogs_TSQL
- sysfulltextcatalogs_TSQL
- sys.sysfulltextcatalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysfulltextcatalogs compatibility view
- sysfulltextcatalogs system table
ms.assetid: 18ac6ad5-01e8-428f-8422-a9ca29626977
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 871604113ffcb98b84a70a142c7312871922fc05
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="syssysfulltextcatalogs-transact-sql"></a>sys.sysfulltextcatalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Contiene información sobre los catálogos de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**ftcatid**|**smallint**|Identificador del catálogo de texto completo.|  
|**Nombre**|**sysname**|Nombre del catálogo de texto completo especificado por el usuario.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**path**|**nvarchar(260)**|Ruta raíz especificada por el usuario.<br /><br /> NULL = Ruta no especificada. Se utiliza la ruta predeterminada (instalación).|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
