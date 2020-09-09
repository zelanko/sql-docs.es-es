---
description: Sys. dm_pdw_component_health_status (Transact-SQL)
title: Sys. dm_pdw_component_health_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 755ccebc287d001b6cd2aa3a2989444d510102a5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89531068"
---
# <a name="sysdm_pdw_component_health_status-transact-sql"></a>Sys. dm_pdw_component_health_status (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contiene información sobre el estado actual de los componentes del dispositivo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||Not NULL|  
|component_id|int|IDENTIFICADOR del componente. Vea [Sys. pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, property_id y component_instance_id forman la clave de esta vista.|Not NULL|  
|property_id|**int**|Identificador de la propiedad. Vea [Sys. pdw_health_component_properties &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md).|NOT NULL|  
|component_instance_id|**nvarchar(255)**|Identifica una instancia de un componente. Por ejemplo, una instancia de una CPU puede identificarse mediante component_instance_id = ' CPU1 '.<br /><br /> pdw_node_id, component_id, property_id y component_instance_id forman la clave de esta vista.|NOT NULL|  
|property_value|**nvarchar(255)**|Valor de propiedad actual.|NULL|  
|update_time|**datetime**|La última vez que se actualizó la métrica.|NOT NULL|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
