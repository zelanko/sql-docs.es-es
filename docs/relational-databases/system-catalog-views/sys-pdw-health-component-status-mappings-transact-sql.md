---
title: Sys. pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: def9dc4a7601e4d5a89794e85f4e209036966f73
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87397125"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>Sys. pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Define la asignación entre los [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Estados de componente y los nombres de componentes definidos por el fabricante.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador único de la propiedad.<br /><br /> property_id, component_id y physical_name forman la clave de esta vista.|NOT NULL|  
|component_id|**int**|IDENTIFICADOR del componente. Vea [Sys. pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id, component_id y physical_name forman la clave de esta vista.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nombre de propiedad definido por el fabricante.<br /><br /> property_id, component_id y physical_name forman la clave de esta vista.|NOT NULL|  
|logical_name|**nvarchar(255)**|Nombre de la propiedad tal y como se define en [!INCLUDE[ssDW](../../includes/ssdw-md.md)] .|NOT NULL<br /><br /> 0: la instancia del dispositivo es única.<br /><br /> 1: la instancia del dispositivo no es única.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
