---
title: Sys. remote_data_archive_databases (Transact-SQL) | Microsoft Docs
description: Obtenga información sobre cómo sys. remote_data_archive_databases contiene una fila por cada base de datos remota que almacena datos de una base de datos local habilitada para Stretch.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: e192a70c1d8f46b7ad89844a3b38019ab6364cc1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248154"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>Stretch Database vistas de catálogo: sys. remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Contiene una fila por cada base de datos remota que almacena datos de una base de datos local habilitada para Stretch.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|El identificador local generado automáticamente de la base de datos remota.|  
|**remote_database_name**|**sysname**|Nombre de la base de datos remota.|  
|**data_source_id**|**int**|Origen de datos utilizado para conectarse al servidor remoto.|  
  
## <a name="see-also"></a>Consulte también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
