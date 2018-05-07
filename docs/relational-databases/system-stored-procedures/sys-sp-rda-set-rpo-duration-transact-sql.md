---
title: Sys.sp_rda_set_rpo_duration (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 47d9f65a37a772a7da80f575d644e0f096523ceb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdasetrpoduration-transact-sql"></a>sys.sp_rda_set_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Establece el número de horas de los datos migrados que SQL Server conserva en una tabla de ensayo para ayudar a garantizar una restauración completa de la base de datos de Azure remota, si es necesario realizar una restauración a un momento dado.    
    
 Para obtener más información, consulte [Stretch Database reduce el riesgo de pérdida de datos para los datos de Azure, pero se mantiene temporalmente filas migradas](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>Sintaxis    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>Argumentos    
 [ @duration_hrs =] *duration_hrs*    
 Es el número de horas (un valor entero distinto de null) de los datos migrados que desea que SQL Server para conservar la base de datos habilitada para Stretch actual. El valor predeterminado y el valor mínimo es de 8 horas.    
 
 > [!NOTE]
 > Los valores más altos requieren más espacio de almacenamiento en SQL Server.
    
## <a name="permissions"></a>Permissions    
 Se requieren permisos db_owner.    
    
## <a name="remarks"></a>Comentarios    
 Obtener el valor actual mediante la ejecución de [sys.sp_rda_set_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>Vea también    
 [sys.sp_rda_get_rpo_duration &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [Restaurar bases de datos habilitadas para Stretch (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
