---
title: Sys. all_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_sql_modules_TSQL
- sys.all_sql_modules
- all_sql_modules
- sys.all_sql_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_sql_modules catalog view
ms.assetid: 7477a3fe-afb3-44c8-bb2c-c6e1d9bdee6f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b21f7e2bbed731e29334be1a87f5089ccfc1145
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981841"
---
# <a name="sysall_sql_modules-transact-sql"></a>sys.all_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la Unión de **Sys. sql_modules** y **Sys. system_sql_modules**.  
  
 La vista devuelve una fila por cada función escalar definida por el usuario y compilada de forma nativa. Para más información, vea [Funciones escalares definidas por el usuario para OLTP en memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de objeto del objeto contenedor. Es único en una base de datos.|  
|**definir**|**nvarchar(max)**|Texto SQL que define este módulo.<br /><br /> NULL = Cifrado|  
|**uses_ansi_nulls**|**bit**|Módulo creado con SET ANSI_NULLS ON.|  
|**uses_quoted_identifier**|**bit**|Módulo creado con SET QUOTED_IDENTIFIER ON.|  
|**is_schema_bound**|**bit**|Módulo creado con la opción SCHEMABINDING.|  
|**uses_database_collation**|**bit**|1 = La definición del módulo enlazado a un esquema depende de la intercalación predeterminada de la base de datos para la evaluación correcta; en caso contrario, 0. Esta dependencia impide cambiar la intercalación predeterminada de la base de datos.|  
|**is_recompiled**|**bit**|Procedimiento creado con la opción WITH RECOMPILE.|  
|**null_on_null_input**|**bit**|Módulo declarado para generar una salida NULL en cualquier entrada NULL.|  
|**execute_as_principal_id**|**int**|Id. de la entidad de seguridad de base de datos EXECUTE AS.<br /><br /> NULL de manera predeterminada o si EXECUTE AS CALLER.<br /><br /> IDENTIFICADOR de la entidad de seguridad especificada si EXECUTe AS SELF o EXECUTe AS \<principal >.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|bit|**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.<br /><br /> 0 = no está compilado de forma nativa<br /><br /> 1 = está compilado de forma nativa<br /><br /> El valor predeterminado es 0.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  [Vistas de catálogo de objetos (Transact-SQL)]  
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys. system_sql_modules &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
