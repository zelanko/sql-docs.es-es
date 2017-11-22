---
title: Sys.sp_xtp_merge_checkpoint_files (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2034ab3fc7118a0e93aabaed345fa17407b7539
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **Sys.sp_xtp_merge_checkpoint_files** combina todos los archivos de datos y delta en el intervalo de transacción especificado.  
  
 Para obtener más información, consulte [crear y administrar el almacenamiento para los objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**Tenga en cuenta**: este procedimiento almacenado está en desuso en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Ya no es necesario y no se puede usar, a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos en la que se va a invocar la combinación. Si la base de datos no tiene tablas en memoria, este procedimiento devuelve un error de usuario. Si la base de datos está sin conexión, devuelve un error.  
  
 *lower_bound_Tid*  
 El límite inferior (bigint) de las transacciones de un archivo de datos tal como se muestra en [sys.dm_db_xtp_checkpoint_files &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) correspondiente al archivo de punto de comprobación de inicio de la combinación. Se genera un error si se especifica un valor no válido para transactonId.  
  
 *upper_bound_Tid*  
 El límite superior (bigint) de las transacciones de un archivo de datos tal como se muestra en [sys.dm_db_xtp_checkpoint_files &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md). Se genera un error si se especifica un valor no válido para transactonId.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Ninguno  
  
## <a name="cursors-returned"></a>Cursores devueltos  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Requiere el rol fijo de servidor sysadmin y el rol fijo de base de datos db_owner.  
  
## <a name="remarks"></a>Comentarios  
 Combina todos los archivos delta y de datos del intervalo válido para generar un único archivo delta y de datos. Este procedimiento no respeta la directiva de combinación.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
