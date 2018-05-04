---
title: Sys.pdw_health_component_status_mappings (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: be811802c8c49a58eb55b7724863be86a3fa0ace
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>Sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Define la asignación entre el [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Estados de los componentes y los nombres definidos por el fabricante del componente.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador único de la propiedad.<br /><br /> identificador property_id e IdComponente, physical_name forman la clave para esta vista.|NOT NULL|  
|IdComponente|**int**|El identificador del componente. Vea [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> identificador property_id e IdComponente, physical_name forman la clave para esta vista.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nombre de la propiedad tal como se define por el fabricante.<br /><br /> identificador property_id e IdComponente, physical_name forman la clave para esta vista.|NOT NULL|  
|logical_name|**nvarchar(255)**|Nombre de la propiedad tal como se define por [!INCLUDE[ssDW](../../includes/ssdw-md.md)].|NOT NULL<br /><br /> 0 - instancia de dispositivo es único.<br /><br /> 1 - instancia de dispositivo no es único.|  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
