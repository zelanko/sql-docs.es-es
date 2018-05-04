---
title: Sys.partition_functions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.partition_functions_TSQL
- partition_functions
- sys.partition_functions
- partition_functions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_functions catalog view
ms.assetid: 96515727-728b-4bea-804a-36ce915b8b75
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5605fa1b5ef261083c8e26205de92c3f76b10256
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syspartitionfunctions-transact-sql"></a>sys.partition_functions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contiene una fila por cada función de partición en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la función de partición. Es único en la base de datos.|  
|**function_id**|**int**|Identificador de función de partición Es único en la base de datos.|  
|**Tipo**|**char(2)**|Tipo de función.<br /><br /> R = Intervalo|  
|**type_desc**|**nvarchar(60)**|Tipo de función.<br /><br /> RANGE|  
|**nodos secundarios**|**int**|Número de particiones creadas por la función.|  
|**boundary_value_on_right**|**bit**|Para la creación de particiones por intervalos.<br /><br /> 1 = El valor de límite está incluido en el intervalo RIGHT del límite.<br /><br /> 0 = LEFT.|  
|**is_system**||**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = El objeto se usa para los fragmentos de índice de texto completo.<br /><br /> 0 = El objeto no se usa para los fragmentos de índice de texto completo.|  
|**create_date**|**datetime**|Fecha de creación de la función.|  
|**modify_date**|**datetime**|Fecha de la última modificación de la función mediante una instrucción ALTER.|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de la función de partición &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [Sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
