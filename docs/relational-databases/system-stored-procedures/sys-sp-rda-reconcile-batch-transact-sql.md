---
title: Sys.sp_rda_reconcile_batch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 29bd622dd82a223b235249b611c1bee5d98a5715
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717103"
---
# <a name="syssprdareconcilebatch-transact-sql"></a>Sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Concilia el identificador de lote que se almacenan en la tabla de SQL Server habilitada para Stretch con el identificador de lote que se almacenan en la tabla de Azure remota.  
  
 Normalmente, solo tiene que ejecutar **sp_rda_reconcile_batch** si se ha eliminado manualmente los datos migrados más recientemente de la tabla remota. Al eliminar manualmente los datos remotos que incluya el lote más reciente, los identificadores de lote no están sincronizados y detiene la migración.  
 
 Para eliminar los datos que ya se ha migrado a Azure, vea los comentarios en esta página.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 \@objname = '*\@objname*'  
 El nombre de la tabla de SQL Server habilitada para Stretch.  
  
## <a name="permissions"></a>Permisos  
 Se requieren permisos db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Si desea eliminar los datos que ya se ha migrado a Azure, realice lo siguiente.  
  
1.  Migración de datos de pausa. Para más información, vea [Pausa y reanudación de la migración de datos &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
2.  Eliminar los datos de la tabla de ensayo de SQL Server mediante la ejecución de un comando de eliminación con la sugerencia STAGE_ONLY. Para obtener más información, consulte [realizar actualizaciones administrativas y las eliminaciones](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints).
  
3.  Elimine los mismos datos de la tabla remota de Azure mediante la ejecución de un comando de eliminación con la sugerencia REMOTE_ONLY.  
  
4.  Ejecute **sp_rda_reconcile_batch**.  
  
5.  Reanudar la migración de datos. Para más información, vea [Pausa y reanudación de la migración de datos &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
## <a name="example"></a>Ejemplo  
 Para conciliar el Id. del lote, ejecute la siguiente instrucción.  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
