---
description: Sys. pdw_health_component_status_mappings (Transact-SQL)
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
ms.openlocfilehash: 2965fb53df87c09c1ccd99c42bed541272b91da7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490261"
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
  
  
