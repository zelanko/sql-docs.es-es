---
title: Sys.computed_columns (Transact-SQL) | Documentos de Microsoft
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
- sys.computed_columns_TSQL
- sys.computed_columns
- computed_columns_TSQL
- computed_columns
dev_langs: TSQL
helpviewer_keywords: sys.computed_columns catalog view
ms.assetid: c962c619-e18f-4315-9251-8d9862462299
caps.latest.revision: "48"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d8614fe85f562c9b3ffdbbb10e5451464564b9e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syscomputedcolumns-transact-sql"></a>sys.computed_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila para cada columna encontrada en **sys.columns** que es una columna calculada.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<Hereda columnas >**||El **sys.computed_columns** vista devuelve todas las columnas de la **sys.columns** vista. También devuelve las columnas adicionales descritas a continuación. Para obtener una descripción de las columnas que la **sys.computed_columns** vista se hereda de **sys.columns**, consulte [sys.columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md). El valor de la **is_computed** columna siempre se establece en 1 en el **sys.computed_columns** vista.|  
|**definición**|**nvarchar(max)**|Texto SQL que define esta columna calculada.|  
|**uses_database_collation**|**bit**|1 = La definición de columna depende de la intercalación predeterminada de la base de datos para su correcta evaluación; de lo contrario, 0. Esta dependencia evita el cambio de la intercalación predeterminada de la base de datos.|  
|**is_persisted**|**bit**|Se almacena la columna calculada.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
