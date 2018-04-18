---
title: sp_showrowreplicainfo (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87857390035273ca2350f90175cc4254f182bb7c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información acerca de una fila en una tabla que se utiliza como un artículo en la replicación de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@ownername**=] **'***ownername***'**  
 Es el nombre del propietario de la tabla. *ownername* es **sysname**, su valor predeterminado es null. Este parámetro resulta útil para diferenciar las tablas en caso de que la base de datos contenga varias tablas con el mismo nombre pero con propietarios distintos.  
  
 [  **@tablename =**] **'***tablename***'**  
 Es el nombre de la tabla que contiene la fila para la cual se devuelve la información. *TableName* es **sysname**, su valor predeterminado es null.  
  
 [  **@rowguid =**] *rowguid*  
 Es el identificador único de la fila. *ROWGUID* es **uniqueidentifier**, no tiene ningún valor predeterminado.  
  
 [ **@show**=] **'***mostrar***'**  
 Determina la cantidad de información que se devuelve en el conjunto de resultados. *Mostrar* es **nvarchar (20)** con un valor predeterminado es BOTH. Si **fila**, se devuelve solo información de versión de fila. Si **columnas**, se devuelve solo información de versión de columna. Si **ambos**, filas y se devuelve información de columna.  
  
## <a name="result-sets-for-row-information"></a>Conjuntos de resultados para información de fila  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nombre del servidor que hospeda la base de datos que realizó la entrada de versión de fila.|  
|**db_name**|**sysname**|Nombre de la base de datos que realizó esta entrada.|  
|**db_nickname**|**binary(6)**|Alias de la base de datos que realizó esta entrada.|  
|**version**|**int**|Versión de la entrada.|  
|**current_state**|**nvarchar(9)**|Devuelve información sobre el estado actual de la fila.<br /><br /> **y** -datos de la fila representan el estado actual de la fila.<br /><br /> **n** -datos de la fila no representan el estado actual de la fila.<br /><br /> **\<n / >** : no es aplicable.<br /><br /> **\<desconocido >** -no se puede determinar el estado actual.|  
|**rowversion_table**|**nchar(17)**|Indica si las versiones de fila se almacenan en la [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabla o la [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabla.|  
|**Comentario**|**nvarchar(255)**|Información adicional acerca de esta entrada de versión de fila. Este campo suele estar vacío.|  
  
## <a name="result-sets-for-column-information"></a>Conjuntos de resultados para información de columna  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|Nombre del servidor que hospeda la base de datos que realizó la entrada de versión de columna.|  
|**db_name**|**sysname**|Nombre de la base de datos que realizó esta entrada.|  
|**db_nickname**|**binary(6)**|Alias de la base de datos que realizó esta entrada.|  
|**version**|**int**|Versión de la entrada.|  
|**colname**|**sysname**|Nombre de la columna del artículo que representa la entrada de la versión de columna.|  
|**Comentario**|**nvarchar(255)**|Información adicional acerca de esta entrada de versión de columna. Este campo suele estar vacío.|  
  
## <a name="result-set-for-both"></a>Conjuntos de resultados para ambos  
 Si el valor **ambos** elegido para *mostrar*, a continuación, se devuelven los conjuntos de resultados de la fila y la columna.  
  
## <a name="remarks"></a>Comentarios  
 **sp_showrowreplicainfo** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permissions  
 **sp_showrowreplicainfo** sólo se puede ejecutar los miembros de la **db_owner** rol fijo de base en la base de datos de publicación o los miembros de la lista de acceso de publicación (PAL) en la base de datos de publicación.  
  
## <a name="see-also"></a>Vea también  
 [Detectar y resolver los conflictos de replicación de mezcla](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
