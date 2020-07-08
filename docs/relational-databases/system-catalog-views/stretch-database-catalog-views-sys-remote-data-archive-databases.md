---
title: Sys. remote_data_archive_databases (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: a4d7717a6e89b156cd66ea96a44383d28cbecfb3
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053637"
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
  
  
