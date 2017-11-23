---
title: Sys.function_order_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs: TSQL
helpviewer_keywords: sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 151d91a53092b9303f576d5b650abdc71a797039
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada columna que forma parte de un **orden** expresión de una función con valores de tabla de Common language runtime (CLR).  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto (función con valores de tabla de CLR) en el que se define el orden.|  
|**order_column_id**|**int**|Identificador de la columna de orden. **order_column_id** es único solo dentro de **object_id**.<br /><br /> **order_column_id** representa la posición de esta columna en la ordenación.|  
|**column_id**|**int**|Identificador de la columna en **object_id**.<br /><br /> **column_id** es único solo dentro de **object_id**.|  
|**is_descending**|**bit**|1 = La columna de ordenación tiene una dirección descendente.<br /><br /> 0 = La columna de ordenación tiene una dirección ascendente.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
