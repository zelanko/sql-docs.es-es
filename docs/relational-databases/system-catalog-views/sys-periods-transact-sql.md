---
title: Sys. periods (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2263b06ff75f475cd09f8f7ee4a6c77a6390ad5a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831477"
---
# <a name="sysperiods-transact-sql"></a>Sys. periods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada tabla para la que se han definido períodos.  
  
|Encabezado de columna|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|name|**sysname**|Nombre del período|  
|period_type|**tinyint**|Valor numérico que representa el tipo de punto:<br /><br /> 1 = período de tiempo del sistema|  
|period_type_desc|**nvarchar(60)**|La descripción de texto del tipo de columna:<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|Identificador de la tabla que contiene la columna de period_type|  
|start_column_id|**int**|Identificador de la columna que define el límite del período inferior.|  
|end_column_id|**int**|Identificador de la columna que define el límite del período superior.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys. system_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [Preguntas más frecuentes sobre el catálogo del sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)  
  
  
