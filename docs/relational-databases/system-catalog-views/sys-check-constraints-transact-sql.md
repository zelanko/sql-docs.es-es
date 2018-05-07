---
title: Sys.CHECK_CONSTRAINTS (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4d223f9ffea455c995890bbac9758d7a24d71f67
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syscheckconstraints-transact-sql"></a>sys.check_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada objeto que es una restricción CHECK, con **sys.objects.type** = 'C'.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<Las columnas que se heredan de sys.objects >**||Para obtener una lista de columnas que hereda esta vista, consulte [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|La restricción CHECK está deshabilitada.|  
|**is_not_for_replication**|**bit**|La restricción CHECK ha sido creada con la opción NOT FOR REPLICATION.|  
|**is_not_trusted**|**bit**|La restricción CHECK no ha sido comprobada por el sistema para todas las filas.|  
|**parent_column_id**|**int**|0 indica una restricción CHECK de nivel de tabla.<br /><br /> Un valor distinto de cero indica que se trata de una restricción CHECK de nivel de columna definida en la columna con el valor de Id. especificado.|  
|**Definición**|**nvarchar(max)**|Expresión SQL que define esta restricción CHECK.|  
|**uses_database_collation**|**bit**|1 = La definición de la restricción depende de la intercalación predeterminada de la base de datos para la evaluación correcta; en caso contrario, 0. Esta dependencia evita el cambio de la intercalación predeterminada de la base de datos.|  
|**is_system_named**|**bit**|1 = El nombre ha sido generado por el sistema.<br /><br /> 0 = El usuario proporcionó el nombre.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
