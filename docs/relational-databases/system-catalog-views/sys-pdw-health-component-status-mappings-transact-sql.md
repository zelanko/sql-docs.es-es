---
title: Sys. pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ec631e9008cc37a7b4f91ed3f530e5388bdf9c0d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127497"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>Sys. pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Define la asignación entre los [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Estados de componente y los nombres de componentes definidos por el fabricante.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador único de la propiedad.<br /><br /> property_id, component_id y physical_name forman la clave de esta vista.|NOT NULL|  
|component_id|**int**|IDENTIFICADOR del componente. Vea [Sys. pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id, component_id y physical_name forman la clave de esta vista.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nombre de propiedad definido por el fabricante.<br /><br /> property_id, component_id y physical_name forman la clave de esta vista.|NOT NULL|  
|logical_name|**nvarchar(255)**|Nombre de la propiedad tal [!INCLUDE[ssDW](../../includes/ssdw-md.md)]y como se define en.|NOT NULL<br /><br /> 0: la instancia del dispositivo es única.<br /><br /> 1: la instancia del dispositivo no es única.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
