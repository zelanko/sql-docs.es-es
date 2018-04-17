---
title: Sys.pdw_health_component_properties (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 628432368c30d81f8a89b97baf1534ce9502403b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
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
  
  
