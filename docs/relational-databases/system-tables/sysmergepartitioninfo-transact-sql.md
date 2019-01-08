---
title: sysmergepartitioninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cea1f26a93627d2a3719ad362d2bd62ee1e3ba1e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802777"
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información sobre las particiones de cada artículo. Contiene una fila por cada artículo de mezcla definido en la base de datos local. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|El número de identificación único del artículo indicado.|  
|**pubid**|**uniqueidentifier**|Número de identificación único para esta publicación; se genera al agregarla.|  
|**partition_view_id**|**int**|El Id de la vista de partición de esta tabla. La vista muestra una asignación de cada fila del artículo a los diferentes Id. de partición a los que pertenece.|  
|**repl_view_id**|**int**|Se agregará.|  
|**partition_deleted_view_rule**|**nvarchar(4000)**|La instrucción SQL utilizada en un desencadenador de replicación de mezcla para recuperar el Id de partición de cada fila eliminada o actualizada según sus valores de columna antiguos.|  
|**partition_inserted_view_rule**|**nvarchar(4000)**|La instrucción SQL utilizada en un desencadenador de replicación de mezcla para recuperar el Id de partición de cada fila insertada o actualizada según sus valores de columna nuevos.|  
|**membership_eval_proc_name**|**sysname**|El nombre del procedimiento que se evalúa como el Id. de partición actual de filas de **MSmerge_contents**.|  
|**column_list**|**nvarchar(4000)**|La lista delimitada por comas de las columnas replicadas en un artículo.|  
|**column_list_blob**|**nvarchar(4000)**|La lista delimitada por comas de las columnas replicadas en un artículo, incluyendo las columnas de objetos binarios grandes.|  
|**expand_proc**|**sysname**|El nombre del procedimiento que vuelve a evaluar los Id. de partición de todas las filas secundarias de una fila principal recién insertada y de las filas principales que han experimentado un cambio de partición o han sido eliminadas.|  
|**logical_record_parent_nickname**|**int**|El alias del primario de nivel superior de un artículo dado de un registro lógico.|  
|**logical_record_view**|**int**|Una vista que produce el rowguid del artículo primario de nivel superior correspondiente a cada rowguid secundario.|  
|**logical_record_deleted_view_rule**|**nvarchar(4000)**|Similar a **logical_record_view**, excepto que muestra filas secundarias de la tabla "eliminada" en actualización y eliminación desencadenadores.|  
|**logical_record_level_conflict_detection**|**bit**|Indica si los conflictos se deben detectar en el nivel de registro lógico o en el nivel de fila o de columna.<br /><br /> **0** = o columna de nivel de fila se utiliza la detección de conflictos.<br /><br /> **1** = lógicos se utiliza la detección de conflictos de registro, donde un cambio en una fila en el publicador y el cambio en otra fila a la misma lógica se controla el registro en el suscriptor como un conflicto.<br /><br /> Cuando este valor es **1**, resolución de conflictos de nivel de registro lógico solo puede utilizarse.|  
|**logical_record_level_conflict_resolution**|**bit**|Indica si los conflictos se deben solucionar en el nivel de registros lógicos o en el nivel de fila o de columna.<br /><br /> **0** = o columna de nivel de fila se utiliza la resolución.<br /><br /> **1** = en caso de conflicto, el registro lógico completo del ganador sobrescribe el registro lógico completo de la parte perdedora.<br /><br /> Un valor de **1** puede utilizarse con ambos detección de nivel de registro lógico y con la detección de nivel de fila o columna.|  
|**partition_options**|**tinyint**|Define el modo en el que se realiza la partición de los datos en el artículo, lo que permite optimizaciones de rendimiento cuando todas las filas pertenecen solamente a una partición o solamente a una suscripción. *partition_options* puede ser uno de los siguientes valores.<br /><br /> **0** = el filtro del artículo es estático o no produce un único subconjunto de datos para cada partición, es decir, una partición "superpuesta".<br /><br /> **1** = las particiones se superponen y las actualizaciones DML realizadas en el suscriptor no pueden cambiar la partición a la que pertenece una fila.<br /><br /> **2** = el filtro del artículo produce particiones no superpuestas, pero varios suscriptores pueden recibir la misma partición.<br /><br /> **3** = el filtro del artículo produce particiones no superpuestas que son únicas para cada suscripción.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
