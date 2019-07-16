---
title: MSdbms_datatype_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a1042bb3aa7b6113121693cc66440ebbf81ce1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907541"
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdbms_datatype_mapping** tabla contiene las asignaciones de tipos de datos permitido el tipo de datos en el sistema de administración de base de datos (DBMS) de origen a uno o varios tipos de datos específicos del DBMS de destino. Esta tabla se almacena en el **msdb** de base de datos y se usa para la replicación de base de datos heterogéneos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|Identifica cada asignación de tipo de datos única.|  
|**map_id**|**int**|Identifica el tipo de datos de origen.|  
|**dest_datatype_id**|**int**|Identifica el tipo de datos de destino.|  
|**dest_precision**|**bigint**|Define la precisión del tipo de datos de destino, donde un valor NULL significa que no se usará la precisión, y un valor de **-1** significa que se utiliza la precisión del tipo de datos de origen.|  
|**dest_scale**|**int**|Define la escala del tipo de datos de destino, donde un valor NULL significa que no se utiliza el escalado, y un valor de **-1** significa que se usa la escala del tipo de datos de origen.|  
|**dest_length**|**bigint**|Define la longitud del tipo de datos de destino, donde un valor NULL significa que no se utiliza la longitud, y un valor de **-1** significa que se utiliza la longitud del tipo de datos de origen.|  
|**dest_nullable**|**bit**|Indica si la columna de destino en la asignación admite valores NULL, donde un valor NULL significa que no se requiere esta definición.|  
|**dest_createparams**|**int**|Es el mapa de bits que describe qué combinación de longitud, precisión y escala es aplicable a cada tipo de datos, donde se incluye:<br /><br /> **0 x 1** = precisión.<br /><br /> **0 x 2** = escala.<br /><br /> **0 x 4** = longitud.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar asignaciones de tipo de datos para un publicador de Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
