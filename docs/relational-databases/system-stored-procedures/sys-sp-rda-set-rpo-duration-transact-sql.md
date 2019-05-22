---
title: sys.sp_rda_set_rpo_duration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f46dd0bbedfebec5e21800b477a23d664446bf24
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982957"
---
# <a name="syssprdasetrpoduration-transact-sql"></a>sys.sp_rda_set_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Establece el número de horas de datos migrados que conserva de SQL Server en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos de Azure remota, si es necesario un punto de restauración a un momento dado.    
    
 Para obtener más información, consulte [Stretch Database reduce el riesgo de pérdida de datos para los datos de Azure al conservar filas migradas temporalmente](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>Sintaxis    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>Argumentos    
 [ @duration_hrs =] *duration_hrs*    
 Es el número de horas (un valor entero distinto de null) de los datos migrados que desee que SQL Server para conservar la base de datos habilitadas para Stretch actual. El valor predeterminado y el valor mínimo es de 8 horas.    
 
 > [!NOTE]
 > Los valores más altos requieren más espacio de almacenamiento en SQL Server.
    
## <a name="permissions"></a>Permisos    
 Se requieren permisos db_owner.    
    
## <a name="remarks"></a>Comentarios    
 Obtener el valor actual mediante la ejecución de [sys.sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Vea también    
 [sys.sp_rda_get_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [Restaurar bases de datos habilitadas para Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
