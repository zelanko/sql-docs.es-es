---
title: Sys.database_automatic_tuning_options (Transact-SQL) | Documentos de Microsoft
description: Obtenga información acerca de cómo ver las opciones de optimización automática en una base de datos de SQL
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 24
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 6b1ddbb9fd87c91182b3e43d9ac8e89465eb77f7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>Sys.Database\_automática\_tuning_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Devuelve las opciones de optimización automática de esta base de datos.  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**nvarchar(128)**|El nombre de la opción de optimización automática. Hacer referencia a [AUTOMATIC_TUNING del conjunto de base de datos de ALTER &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) opciones disponibles.|  
|**desired_state**|**smallint**|Indica el modo de operación para la opción de optimización automática, establece explícitamente por el usuario.<br />0 = OFF<br />1 = ON |  
|**desired_state_desc**|**nvarchar(60)**|Descripción textual del modo de operación de ajuste automático de la opción.<br />OFF<br />ON|  
|**actual_state**|**smallint**|Indica el modo de operación de ajuste automático de la opción.<br />0 = OFF<br />1 = ON |  
|**actual_state_desc**|**nvarchar(60)**|Descripción textual del modo de operación real de opción de optimización automática.<br />OFF<br />ON|  
|**Motivo**|**smallint**|Indica por qué estados reales y deseados son diferentes.<br />2 = DESHABILITADO<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|Descripción textual de la razón por qué estados reales y deseados son diferentes.<br />DESHABILITADO = opción está deshabilitada por sistema<br />QUERY_STORE_OFF = almacén de consultas está desactivado<br />QUERY_STORE_READ_ONLY = almacén de consultas está en modo de solo lectura<br />NOT_SUPPORTED = disponible solo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition| 
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso `VIEW DATABASE STATE`.  
  
## <a name="see-also"></a>Vea también  
 [El ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [AUTOMATIC_TUNING de conjunto de base de datos de ALTER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
