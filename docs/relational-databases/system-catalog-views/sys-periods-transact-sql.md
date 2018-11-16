---
title: Sys.Periods (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eed8badea9b7136cb71c5d89a76494aab190a0d2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655965"
---
# <a name="sysperiods-transact-sql"></a>Sys.Periods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada tabla para el que se han definido períodos.  
  
|Encabezado de columna|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|NAME|**sysname**|Nombre del período|  
|period_type|**tinyint**|El valor numérico que representa el tipo del período de:<br /><br /> 1 = período de tiempo del sistema|  
|period_type_desc|**nvarchar(60)**|La descripción de texto del tipo de columna:<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|El identificador de la tabla que contiene la columna period_type|  
|start_column_id|**int**|El identificador de la columna que define el límite inferior de período|  
|end_column_id|**int**|El identificador de la columna que define el límite superior de período|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys.ALL_COLUMNS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys.system_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)  
  
  
