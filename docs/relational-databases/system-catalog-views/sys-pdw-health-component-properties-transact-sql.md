---
title: Sys.pdw_health_component_properties (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 60e82089b66ff4a8a4263dd56b9ec2871a92869a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syspdwhealthcomponentproperties-transact-sql"></a>Sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena las propiedades que describen un dispositivo. Algunas propiedades muestran el estado del dispositivo y algunas propiedades describen el propio dispositivo.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador único de la propiedad de un componente.<br /><br /> identificador property_id e IdComponente forman la clave para esta vista.|NOT NULL|  
|IdComponente|**int**|El identificador del componente. Vea [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> identificador property_id e IdComponente forman la clave para esta vista.|NOT NULL|  
|property_name|**nvarchar(255)**|Nombre de la propiedad.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nombre de la propiedad tal como se define por el fabricante.|NOT NULL|  
|is_key|**bit**|Determina si la instancia de dispositivo es único o no.|NOT NULL<br /><br /> 0 - instancia de dispositivo es único.<br /><br /> 1 - instancia de dispositivo no es único.|  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
