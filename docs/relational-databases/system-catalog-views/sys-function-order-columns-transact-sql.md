---
title: Sys. function_order_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: stevestein
ms.author: sstein
ms.openlocfilehash: a2a51cc56b37325d760ca77f014594496c8ab6b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68122746"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada columna que forma parte de una expresión de **orden** de una función con valores de tabla de Common Language Runtime (CLR).  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto (función con valores de tabla de CLR) en el que se define el orden.|  
|**order_column_id**|**int**|Identificador de la columna de orden. **order_column_id** es único solo dentro de **object_id**.<br /><br /> **order_column_id** representa la posición de esta columna en la ordenación.|  
|**column_id**|**int**|IDENTIFICADOR de la columna en **object_id**.<br /><br /> **column_id** es único solo dentro de **object_id**.|  
|**is_descending**|**bit**|1 = La columna de ordenación tiene una dirección descendente.<br /><br /> 0 = La columna de ordenación tiene una dirección ascendente.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
