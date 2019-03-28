---
title: sp_check_join_filter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02c46d74a1e68af322aa50c7b0ac1c3d4f96ee49
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531757"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza para comprobar un filtro de combinación entre dos tablas a fin de determinar si la cláusula del filtro de combinación es válida. Este procedimiento almacenado también devuelve información sobre el filtro de combinación proporcionado, incluso si se puede utilizar con particiones precalculadas para la tabla dada. Este procedimiento almacenado se ejecuta en el publicador de la publicación. Para obtener más información, vea [Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filtered_table = ] 'filtered_table'` Es el nombre de una tabla filtrada. *filtered_table* es **nvarchar (400)**, no tiene ningún valor predeterminado.  
  
`[ @join_table = ] 'join_table'` Es el nombre de una tabla que se combina con *filtered_table*. *join_table* es **nvarchar (400)**, no tiene ningún valor predeterminado.  
  
`[ @join_filterclause = ] 'join_filterclause'` Se está probando la cláusula de filtro de combinación. *join_filterclause* es **nvarchar (1000)**, no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Es si la publicación es apta para las particiones precalculadas; donde **1** significa que se pueden usar particiones precalculadas, y **0** significa que no puede utilizarse.|  
|**has_dynamic_filters**|**bit**|Si la cláusula de filtro suministrada incluye al menos una función de filtrado con parámetros; donde **1** significa que se utiliza una función de filtrado con parámetros, y **0** significa que no se utiliza una función de ese tipo.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Lista de las funciones de la cláusula de filtro que definen un filtro con parámetros para un artículo; las funciones están separadas por puntos y comas.|  
|**uses_host_name**|**bit**|Si el [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) función se utiliza en la cláusula de filtro, donde **1** significa que esta función está presente.|  
|**uses_suser_sname**|**bit**|Si el [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) función se utiliza en la cláusula de filtro, donde **1** significa que esta función está presente.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_check_join_filter** se utiliza en la replicación de mezcla.  
  
 **sp_check_join_filter** se puede ejecutar en cualquier tabla relacionada, incluso si no se publican. Este procedimiento almacenado se puede utilizar para comprobar una cláusula de filtro de combinación antes de definir un filtro de combinación entre dos artículos.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_check_join_filter**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
