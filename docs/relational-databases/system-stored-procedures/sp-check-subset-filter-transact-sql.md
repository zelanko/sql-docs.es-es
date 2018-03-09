---
title: sp_check_subset_filter (Transact-SQL) | Documentos de Microsoft
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
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3341c4f5fc6c637f74dabf913730e6c6e30dfcea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza para comprobar una cláusula de filtro en una tabla para determinar si es válida para esa tabla. Este procedimiento almacenado devuelve información sobre el filtro suministrado, incluso si el filtro es apto para su uso con particiones precalculadas. Este procedimiento almacenado se ejecuta en el publicador de la base de datos que contiene la publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@filtered_table** =] **'***filtered_table***'**  
 Es el nombre de una tabla filtrada. *filtered_table* es **nvarchar (400)**, no tiene ningún valor predeterminado.  
  
 [  **@subset_filterclause**  =] **'***subset_filterclause***'**  
 Es la cláusula de filtro que se comprueba. *subset_filterclause* es **nvarchar (1000)**, no tiene ningún valor predeterminado.  
  
 [  **@has_dynamic_filters** =] *has_dynamic_filters*  
 Especifica si la cláusula de filtro es un filtro de fila con parámetros. *has_dynamic_filters* es **bits**, su valor predeterminado es null y es un parámetro de salida. Devuelve un valor de **1** cuando la cláusula de filtro es un filtro de fila con parámetros.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Es si la publicación es apta para usar particiones precalculadas; donde **1** significa que las particiones precalculadas pueden estar usando, y **0** significa que no se puede usar.|  
|**has_dynamic_filters**|**bit**|Especifica si la cláusula de filtro suministrada incluye al menos un filtro de fila con parámetros; donde **1** significa que se utiliza un filtro de fila con parámetros, y **0** significa que esa función no se utiliza.|  
|**dynamic_filters_function_list**|**nvarchar (500)**|Lista de las funciones de la cláusula de filtro que filtran un artículo dinámicamente; las funciones están separadas por puntos y comas.|  
|**uses_host_name**|**bit**|Si el [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) función se utiliza en la cláusula de filtro, donde **1** significa que esta función está presente.|  
|**uses_suser_sname**|**bit**|Si el [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) función se utiliza en la cláusula de filtro, donde **1** significa que esta función está presente.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_check_subset_filter** se utiliza en la replicación de mezcla.  
  
 **sp_check_subset_filter** se puede ejecutar en cualquier tabla, incluso si no se publica la tabla. Este procedimiento almacenado se puede utilizar para comprobar una cláusula de filtro antes de definir un artículo filtrado.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_check_subset_filter**.  
  
## <a name="see-also"></a>Vea también  
 [Optimizar el rendimiento de filtro con parámetros con particiones precalculadas](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
