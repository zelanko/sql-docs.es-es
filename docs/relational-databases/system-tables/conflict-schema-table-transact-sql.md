---
title: conflict_&lt;schema&gt;_&lt;table&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd226aef62c2d05eead5e2b5f72b2f358422025a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471084"
---
# <a name="conflictltschemagtlttablegt-transact-sql"></a>conflict_&lt;schema&gt;_&lt;table&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El conflict_\<esquema > _\<tabla > contiene información acerca de las filas conflictivas en la replicación punto a punto. En una publicación, cada tabla replicada posee una tabla de conflictos; el nombre de esta tabla de conflictos se anexa al nombre del artículo y esquema. Estas tablas de conflictos específicas del artículo existen en cada base de datos de publicación.  
  
 En el caso de la replicación punto a punto, el Agente de distribución genera un error de forma predeterminada cuando detecta un conflicto. Se registra un error de conflicto en el registro de errores, pero no se registra ningún dato de conflicto en la tabla de conflictos, por lo que no está disponible para verse. Si el Agente de distribución puede continuar, se registra un conflicto localmente en cada nodo donde se detectó. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|Identificador del nodo en el que se originó el cambio en conflicto. Para obtener una lista de identificadores, ejecute [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).|  
|__$origin_datasource|**int**|Nodo en el que se originó el cambio en conflicto.|  
|__$tranid|**nvarchar (40)**|Número de flujo de registro (LSN) del cambio en conflicto cuando se aplicó en __$origin_datasource.|  
|__$conflict_type|**int**|Tipo de conflicto, que puede ser uno de los valores siguientes:<br /><br /> 1: Una actualización porque cambió la fila local por otra actualización o se eliminó y, a continuación, volver a insertar.<br /><br /> 2: Se produce un error porque ya se ha eliminado la fila local.<br /><br /> 3: Una error porque se modificó la fila local por otra actualización o de eliminación se eliminó y, a continuación, volver a insertar.<br /><br /> 4: No se pudo eliminar porque ya se ha eliminado la fila local.<br /><br /> 5: Error en una inserción porque ya se insertó la fila local o se insertó y, a continuación, se actualiza.|  
|__$is_winner|**bit**|Indica si la fila de esta tabla fue la ganadora del conflicto, lo que significa que se aplicó al nodo local.|  
|__$pre_version|**varbinary (32)**|Versión de la base de datos en la que se originó el cambio en conflicto.|  
|__$reason_code|**int**|Código de la resolución del conflicto. Puede presentar uno de los siguientes valores:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> Para obtener más información, consulte **__ $reason_text**.|  
|__$reason_text|**nvarchar (720)**|Resolución del conflicto. Puede presentar uno de los siguientes valores:<br /><br /> Resuelto (1)<br /><br /> No resuelto (2)<br /><br /> Desconocido (0)|  
|__$update_bitmap|**varbinary (** *n* **)**. Tamaño varía en función de contenido.|Mapa de bits que indica qué columnas se actualizaron en el caso de un conflicto de actualizaciones.|  
|__$inserted_date|**datetime**|Fecha y hora en que la fila en conflicto se insertó en esta tabla.|  
|__$row_id|**timestamp**|Versión de fila que está asociada a la fila que ocasionó el conflicto.|  
|__$change_id|**binary (8)**|En una fila local, este valor es igual al valor __$row_id de la fila entrante que sufrió un conflicto con la fila local. Este valor es NULL para una fila entrante.|  
|\<basar los nombres de columna de tabla >|\<tipos de columna de tabla base >|La tabla de conflictos contiene una columna para cada columna de la tabla base.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
