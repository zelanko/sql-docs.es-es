---
title: Procedimientos almacenados extendidos (Transact-SQL)
titleSuffix: SQL Server Stretch Database
ms.custom: seo-dt-2019
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d82b6cb9049bf5a41cfb987a55bb6d5a7147c9bd
ms.sourcegitcommit: add39e028e919df7d801e8b6bb4f8ac877e60e17
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119273"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database procedimientos almacenados extendidos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 En esta sección se describen los procedimientos almacenados extendidos relacionados con Stretch Database.  
  
## <a name="in-this-section"></a>En esta sección  
[Sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) Quita la conexión autenticada entre una base de datos habilitada para Stretch local y la base de datos de Azure remota.

[Sys. sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) Obtiene el número de horas de datos migrados que SQL Server conserva en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos remota de Azure, en caso de que sea necesaria una restauración.
  
 [Sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) Restaura la conexión autenticada entre una base de datos local habilitada para Stretch y la base de datos remota.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Concilia el identificador de lote almacenado en la tabla de SQL Server habilitada para Stretch los datos migrados más recientemente con el identificador de lote almacenado en la tabla remota de Azure. 
 
[Sys. sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) Concilia las columnas de la tabla remota de Azure con las columnas de la tabla SQL Server habilitada para Stretch.
 
 [Sys. sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) Pone en cola una tarea de esquema para conciliar los índices en la tabla remota.
 
 [Sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) Especifica si las consultas realizadas en la base de datos habilitada para Stretch actual y en sus tablas devuelven datos locales y remotos (el valor predeterminado) o solo los datos locales.
 
 [Sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) Establece el número de horas de datos migrados que SQL Server conserva en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos remota de Azure, en caso de que sea necesaria una restauración.
 
 [Sys. sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) Prueba la conexión desde SQL Server al servidor remoto de Azure e informa de los problemas que pueden impedir la migración de datos.
 
## <a name="see-also"></a>Vea también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
