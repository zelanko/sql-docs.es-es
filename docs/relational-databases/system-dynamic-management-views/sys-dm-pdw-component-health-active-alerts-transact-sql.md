---
title: Sys. dm_pdw_component_health_active_alerts (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 90531889d3e510d342ff39abdf069f75f3c371aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401708"
---
# <a name="sysdm_pdw_component_health_active_alerts-transact-sql"></a>Sys. dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena alertas activas en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] componentes de.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodo.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|component_id|**int**|IDENTIFICADOR del componente. Vea [Sys. pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|alert_id|**int**|IDENTIFICADOR del tipo de alerta. Vea [Sys. pdw_health_alerts &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|Identifica una instancia de una alerta determinada.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|current_value|**nvarchar(255)**|Se usa cuando la alerta es de tipo StatusChange. Este es el estado actual del componente. El valor es NULL para las alertas de tipo umbral. Vea [Sys. pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|previous_value|**nvarchar(255)**|Se usa cuando la alerta es de tipo StatusChange. Este es el estado anterior del componente. El valor es NULL para las alertas de tipo umbral. Vea [Sys. pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|create_time|**datetime**|Fecha y hora en que se generó la alerta.|NOT NULL|  
  
 Para obtener información acerca de las filas máximas retenidas en esta vista, vea "valores mínimos [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]y máximos" en la.  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
