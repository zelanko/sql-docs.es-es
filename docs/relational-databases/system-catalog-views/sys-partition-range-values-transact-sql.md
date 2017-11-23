---
title: Sys.partition_range_values (Transact-SQL) | Documentos de Microsoft
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
- sys.partition_range_values
- partition_range_values_TSQL
- partition_range_values
- sys.partition_range_values_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.partition_range_values catalog view
ms.assetid: 9aee483e-61f3-4613-bec6-f084161f45ac
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f1fd5ab82c373dbc08edf7a901ccfee4d6eed34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionrangevalues-transact-sql"></a>sys.partition_range_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contiene una fila por cada valor de límite de intervalo de una función de partición de tipo R.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|Id. de la función de partición de este valor de límite de intervalo.|  
|**boundary_id**|**int**|Id. (ordinal de base 1) de la tupla del valor de límite. El límite situado más a la izquierda se inicia con un Id. de 1.|  
|**parameter_id**|**int**|Id. del parámetro de la función a la que corresponde este valor. Los valores de esta columna se corresponden con los de la **parameter_id** columna de la **sys.partition_parameters** vista para un determinado de catálogo **function_id**.|  
|**valor**|**sql_variant**|El valor de límite en sí.|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de función de partición &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys.partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [Sys.partition_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
