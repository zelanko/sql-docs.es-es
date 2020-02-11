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
ms.openlocfilehash: 41c3a6848d71d7ba8f22667c117686485bb569b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019976"
---
# <a name="sp_mergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una limpieza manual de los metadatos en las tablas del sistema [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)y [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) . Este procedimiento almacenado se ejecuta en cada publicador y suscriptor de la topología.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT`Devuelve el número de filas que se han limpiado de la tabla [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) . *num_genhistory_rows* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT`Devuelve el número de filas que se han limpiado de la tabla [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) . *num_contents_rows* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT`Devuelve el número de filas que se han limpiado de la tabla [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) . *num_tombstone_rows* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only`Solo para uso interno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
  
> [!IMPORTANT]  
>  Si hay varias publicaciones en una base de datos y cualquiera de estas publicaciones utiliza un período de retención de publicación infinita, la ejecución de **sp_mergemetadataretentioncleanup** no limpia los metadatos de seguimiento de cambios de la replicación de mezcla para la base de datos. Por ese motivo, debe utilizar con cuidado la retención infinita de publicaciones. Para determinar si una publicación tiene un período de retención infinito, ejecute [sp_helpmergepublication &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) en el publicador y anote las publicaciones del conjunto de resultados con un valor de **0** para la **retención**.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de base de datos **db_owner** o los usuarios de la lista de acceso a la publicación de una base de datos publicada pueden ejecutar **sp_mergemetadataretentioncleanup**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
