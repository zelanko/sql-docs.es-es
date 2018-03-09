---
title: sp_check_dynamic_filters (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 096c6ff70b712b283191afeddbb7e9d9c6afd36a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre las propiedades del filtro de filas con parámetros para una publicación, en particular, las funciones utilizadas para generar una partición de datos filtrados para una publicación, y sobre si la publicación puede utilizar particiones previamente calculadas. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication** =] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Es si la publicación es apta para usar particiones precalculadas; donde **1** significa que las particiones precalculadas pueden estar usando, y **0** significa que no se puede usar.|  
|**has_dynamic_filters**|**bit**|Es si se ha definido el filtro de al menos una fila con parámetros en la publicación; donde **1** significa que existen uno o más filtros de fila con parámetros, y **0** significa que existe ningún filtro dinámico.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|Lista de funciones utilizadas para filtrar artículos en una publicación, donde las funciones se separan mediante puntos y coma.|  
|**validate_subscriber_info**|**nvarchar (500)**|Lista de funciones utilizadas para filtrar artículos en una publicación, donde las funciones se separan mediante signos más (+).|  
|**uses_host_name**|**bit**|Si el [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) función se utiliza en filtros de fila con parámetros, donde **1** significa que esta función se utiliza para filtrado dinámico.|  
|**uses_suser_sname**|**bit**|Si el [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) función se utiliza en filtros de fila con parámetros, donde **1** significa que esta función se utiliza para filtrado dinámico.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_check_dynamic_filters** se utiliza en la replicación de mezcla.  
  
 Si una publicación se ha definido para usar particiones precalculadas, **sp_check_dynamic_filters** comprueba si hay alguna infracción de las restricciones de las particiones precalculadas. Si se infringió alguna restricción, se devuelve un error. Para obtener más información, vea [Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 Si se ha definido que una publicación posee filtros de filas con parámetros, pero no se encuentra ninguno, se devuelve un error.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_check_dynamic_filters**.  
  
## <a name="see-also"></a>Vea también  
 [Administrar particiones para una publicación de mezcla con filtros con parámetros](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
