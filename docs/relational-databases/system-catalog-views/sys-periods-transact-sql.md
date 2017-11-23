---
title: Sys.Periods (Transact-SQL) | Documentos de Microsoft
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
dev_langs: TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58e8428bc016975594105b842c75fca1304d0695
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysperiods-transact-sql"></a>Sys.Periods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada tabla para la que se han definido períodos.  
  
|Encabezado de columna|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|period_type|**sysname**|Nombre del período|  
|period_type_desc|**tinyint**|El valor numérico que representa el tipo de período:<br /><br /> 1 = período de tiempo del sistema|  
|object_id|**nvarchar (60)**|La descripción del tipo de columna:<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|El identificador de la tabla que contiene la columna period_type|  
|start_column_id|**int**|El identificador de la columna que define el límite inferior de periodo|  
|end_column_id|**int**|El identificador de la columna que define el límite superior de periodo|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys.ALL_COLUMNS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys.system_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)  
  
  
