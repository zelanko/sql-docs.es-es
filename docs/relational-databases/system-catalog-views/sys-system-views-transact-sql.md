---
title: Sys. system_views (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dbfca799f3c3dc4b3930f487fb45413c7711af48
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821305"
---
# <a name="syssystem_views-transact-sql"></a>sys.system_views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada vista del sistema incluida en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Todas las vistas del sistema están contenidas en los esquemas denominados **Sys** o **INFORMATION_SCHEMA**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|\<columnas heredadas>||Para obtener una lista de las columnas que hereda esta vista, vea [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_replicated**|**bit**|1 = La vista está replicada.|  
|**has_replication_filter**|**bit**|1 = La vista tiene un filtro de replicación.|  
|**has_opaque_metadata**|**bit**|1 = Se ha especificado la opción VIEW_METADATA para la vista. Para obtener más información, vea [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).|  
|**has_unchecked_assembly_data**|**bit**|1 = La tabla contiene datos persistentes que dependen de un ensamblado cuya definición cambió durante el último ALTER ASSEMBLY. Se restablecerá en 0 tras la siguiente operación DBCC CHECKDB o DBCC CHECKTABLE correcta.|  
|**with_check_option**|**bit**|1 = Se ha especificado WITH CHECK OPTION en la definición de la vista.|  
|**is_date_correlation_view**|**bit**|1 = el sistema creó automáticamente la vista para almacenar la información de correlación entre las columnas de **fecha y hora** . La creación de esta vista se ha habilitado al establecer DATE_CORRELATION_OPTIMIZATION en ON.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
