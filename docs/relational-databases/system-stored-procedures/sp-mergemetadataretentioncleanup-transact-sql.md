---
title: sp_mergemetadataretentioncleanup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1797200ce5369f49035f1a950d606e34e584edc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658422"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una limpieza manual de metadatos en el [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_ asignaciones](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), y [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) las tablas del sistema. Este procedimiento almacenado se ejecuta en cada publicador y suscriptor de la topología.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT` Devuelve el número de filas limpiado de la [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) tabla. *num_genhistory_rows* es **int**, su valor predeterminado es **0**.  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT` Devuelve el número de filas limpiado de la [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabla. *num_contents_rows* es **int**, su valor predeterminado es **0**.  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT` Devuelve el número de filas limpiado de la [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabla. *num_tombstone_rows* es **int**, su valor predeterminado es **0**.  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` Solo para uso interno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
  
> [!IMPORTANT]  
>  Si hay varias publicaciones en una base de datos y una de estas publicaciones utiliza un período de retención de publicación infinito, ejecutando **sp_mergemetadataretentioncleanup** no limpiará el seguimiento de cambios de replicación de mezcla metadatos de la base de datos. Por ese motivo, debe utilizar con cuidado la retención infinita de publicaciones. Para determinar si una publicación tiene un período de retención infinito, ejecute [sp_helpmergepublication &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) en el publicador y tenga en cuenta las publicaciones en el resultado se establece con un valor de **0** para **retención**.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **db_owner** rol fijo de base de datos o los usuarios en la lista de acceso de publicación para una base de datos publicada puede ejecutar **sp_mergemetadataretentioncleanup**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
