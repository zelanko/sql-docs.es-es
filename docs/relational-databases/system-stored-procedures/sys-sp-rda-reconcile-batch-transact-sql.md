---
title: sys.sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1df76c9b3107b5fbd45eb8a99eab1ec5baf5f4ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Concilia el identificador de lote que se almacenan en la tabla de SQL Server habilitada para Stretch con el identificador de lote que se almacenan en la tabla de Azure remota.  
  
 Normalmente sólo tendrá que ejecutar **sp_rda_reconcile_batch** si se han eliminado manualmente los datos migrados más recientemente de la tabla remota. Cuando elimine manualmente los datos remotos que incluya el lote más reciente, los identificadores de lote están sincronizados y detiene la migración.  
 
 Para eliminar los datos que ya se ha migrado a Azure, vea la sección comentarios en esta página.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 @objname = '*@objname*'  
 El nombre de la tabla de SQL Server habilitada para Stretch.  
  
## <a name="permissions"></a>Permissions  
 Se requieren permisos db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Si desea eliminar los datos que ya se ha migrado a Azure, haga lo siguiente.  
  
1.  Pause la migración de datos. Para obtener más información, consulte [pausar y reanudar la migración de datos &#40; Ajuste de la base de datos &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  Eliminar los datos de la tabla de ensayo de SQL Server mediante la ejecución de un comando de eliminación con la sugerencia STAGE_ONLY. Para obtener más información, consulte [realizar administrativas actualizaciones y eliminaciones](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints).
  
3.  Elimine los mismos datos de la tabla de Azure remota mediante la ejecución de un comando de eliminación con la sugerencia REMOTE_ONLY.  
  
4.  Run **sp_rda_reconcile_batch**.  
  
5.  Reanudar la migración de datos. Para obtener más información, consulte [pausar y reanudar la migración de datos &#40; Ajuste de la base de datos &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>Ejemplo  
 Para conciliar los ID de lote, ejecute la siguiente instrucción.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
