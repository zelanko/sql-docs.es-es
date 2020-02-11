---
title: MSdbms_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: fffa30d0e252392c41cee34c1875b12b5b7a53b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907490"
---
# <a name="msdbms_map-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSdbms_map** contiene información del tipo de datos de origen, así como un vínculo a la información del tipo de datos de destino predeterminado para los pares de DBMS de origen y de destino. Esta tabla se almacena en la base de datos **msdb** y se utiliza para la publicación heterogénea.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|Identifica de manera única una asignación de tipo de datos.|  
|**src_dbms_id**|**int**|Identifica el DBMS de origen especificando su **dbms_id** en la tabla [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) .|  
|**dest_dbms_id**|**int**|Identifica el DBMS de destino especificando su **dbms_id** en la tabla [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md) .|  
|**src_datatype_id**|**int**|Identifica el **datatype_id** de la tabla de [MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md) para el tipo de datos de origen.|  
|**src_len_min**|**BIGINT**|La longitud mínima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una longitud.|  
|**src_len_max**|**BIGINT**|La longitud máxima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una longitud.|  
|**src_prec_min**|**BIGINT**|La precisión mínima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una precisión.|  
|**src_prec_max**|**BIGINT**|La precisión máxima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una precisión.|  
|**src_scale_min**|**int**|La escala mínima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una escala.|  
|**src_scale_max**|**int**|La escala máxima del tipo de datos en el DBMS de origen, en la que un valor NULL indica que no se utiliza una escala.|  
|**src_nullable**|**bit**|Indica si la columna de destino en la asignación admite valores NULL, donde un valor NULL significa que no se requiere esta definición.|  
|**default_datatype_mapping_id**|**int**|Identifica la asignación de tipo de datos predeterminada especificando su **map_id** en la tabla [MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar asignaciones de tipos de datos para un publicador de Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
