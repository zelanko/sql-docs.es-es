---
title: Base de datos (Transact-SQL) de procedimientos almacenados extendido de Stretch | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f71e898f656b1177c8b7ea0630b87babd5a0a82
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database (Transact-SQL) de procedimientos almacenados extendido
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Esta sección describen los procedimientos almacenados extendidos que están relacionados con la base de datos de Stretch.  
  
## <a name="in-this-section"></a>En esta sección  
[Sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) quita la conexión autenticada entre una base de datos habilitada para Stretch local y la base de datos de Azure remota.

[Sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) Obtiene el número de horas de los datos migrados que SQL Server conserva en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos de Azure remota, si es necesario realizar una restauración.
  
 [Sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) restaura la conexión autenticada entre una base de datos local habilitada para Stretch y la base de datos remota.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Concilia el identificador de lote que se almacenan en la tabla de SQL Server habilitada para Stretch para los datos migrados más recientemente con el identificador de lote que se almacenan en la tabla de Azure remota. 
 
[Sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) reconcilia las columnas de la tabla de Azure remota a las columnas de la en la tabla de SQL Server habilitada para Stretch.
 
 [Sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) pone en cola una tarea de esquema para conciliar los índices de la tabla remota.
 
 [Sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) especifica si las consultas realizadas en la base de datos habilitada para Stretch actual y sus tablas devuelven datos locales y remotos (valor predeterminado) o únicamente los datos locales.
 
 [Sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) establece el número de horas de los datos migrados que SQL Server conserva en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos de Azure remota, si es necesario realizar una restauración.
 
 [Sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) prueba la conexión de SQL Server para el servidor remoto de Azure y notifica problemas que podrían evitar la migración de datos.
 
## <a name="see-also"></a>Vea también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
