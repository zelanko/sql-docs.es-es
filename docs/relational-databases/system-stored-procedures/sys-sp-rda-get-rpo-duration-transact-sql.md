---
title: Sys. sp_rda_get_rpo_duration (Transact-SQL) | Microsoft Docs
description: Use sys. sp_rda_get_rpo_duration para obtener el número de horas de datos migrados que SQL Server conserva en una tabla de almacenamiento provisional para restaurar completamente la base de datos de Azure remota.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b3b52298861da031dc5eab6b3a32135eec9d26cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538474"
---
# <a name="syssp_rda_get_rpo_duration-transact-sql"></a>Sys. sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Obtiene el número de horas de datos migrados que SQL Server conserva en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos remota de Azure, en caso de que sea necesaria una restauración a un momento dado. 
  
  Para obtener más información, consulte [Stretch Database reduce el riesgo de pérdida de datos en los datos de Azure al conservar temporalmente las filas migradas](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxis    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>Parámetro de salida    
 *\@durationinhours*    
  Es el número de horas (valor entero no NULL) de los datos migrados que SQL Server conserva para la base de datos habilitada para Stretch actual.    
    
## <a name="permissions"></a>Permisos    
 Requiere permisos de db_owner.    
    
## <a name="remarks"></a>Observaciones    
 Cambie el valor ejecutando [Sys. sp_rda_set_rpo_duration &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Consulte también    
 [Sys. sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [Restaurar bases de datos habilitadas para Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
