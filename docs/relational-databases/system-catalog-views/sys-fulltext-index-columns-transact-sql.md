---
description: sys.fulltext_index_columns (Transact-SQL)
title: sys.fulltext_index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c514fbfd5d82038995bb6db006a9013c28674202
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472986"
---
# <a name="sysfulltext_index_columns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Contiene una fila para cada columna que forma parte de un índice de texto completo.    
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. del objeto del que forma parte.|  
|**column_id**|**int**|Id. de la columna que forma parte del índice de texto completo.|  
|**type_column_id**|**int**|ID. de la columna de tipo que almacena la extensión de archivo de documento proporcionada por el usuario (". doc", ". xls", etc.) del documento en una fila determinada. La columna de tipo solo se especifica para las columnas cuyos datos requieren el filtrado durante la indización de texto completo. NULL si no es aplicable. Para obtener más información, vea [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md).|  
|**language_id**|**int**|LCID de idioma cuyo separador de palabras se utiliza para indizar esta columna de texto completo.<br /><br /> 0 = Neutro.<br /><br /> Para obtener más información, vea [sys.fulltext_languages &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).|  
|**statistical_semantics**|**int**|1 = La columna tiene habilitada la indización semántica estadística además de la indización de texto completo.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
