---
title: Sys.partition_parameters (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs: TSQL
helpviewer_keywords: sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea75798552d0521204e063663566b08b36a5797b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contiene una fila por cada parámetro de una función de partición.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|Id. de la función de partición a la que pertenece este parámetro.|  
|**parameter_id**|**int**|Id. del parámetro. Es único en la función de partición y empieza por 1.|  
|**system_type_id**|**tinyint**|Identificador del tipo de sistema del parámetro. Corresponde a la **system_type_id** columna de la **sys.types** vista de catálogo.|  
|**max_length**|**smallint**|Longitud máxima del parámetro en bytes.|  
|**precisión**|**tinyint**|Precisión del parámetro si está basado en numerales; de lo contrario es 0.|  
|**escala**|**tinyint**|Escala del parámetro si está basado en numerales; de lo contrario es 0.|  
|**collation_name**|**sysname**|Nombre de la intercalación del parámetro, si está basado en caracteres; en caso contrario, es NULL.|  
|**user_type_id**|**int**|Id. del tipo. Es único en la base de datos. Tipos de datos del sistema, **user_type_id** = **system_type_id**.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de función de partición &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys.partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [Sys.partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
