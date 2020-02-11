---
title: Sys. dm_pdw_component_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 770ddc4d1e182360b13d4f9e27d9e0bbf80cceee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899579"
---
# <a name="sysdm_pdw_component_health_alerts-transact-sql"></a>Sys. dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena las alertas emitidas previamente en los componentes del dispositivo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodo.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|component_id|**int**|IDENTIFICADOR del componente. Vea [Sys. pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|alert_id|**int**|IDENTIFICADOR del tipo de alerta. Vea [Sys. pdw_health_alerts &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|Identifica una instancia de una alerta determinada.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id y alert_instance_id forman la clave de esta vista.|NOT NULL|  
|previous_value|**nvarchar(255)**|Se usa cuando la alerta es de tipo StatusChange. Este es el estado anterior del componente. El valor es NULL para las alertas de tipo umbral. Vea [Sys. pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|current_value|**nvarchar(255)**|Se usa cuando la alerta es de tipo StatusChange. Este es el estado actual del componente. El valor es NULL para las alertas de tipo umbral. Vea [Sys. pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|create_time|**datetime**|Fecha y hora en que se generó la alerta.|NOT NULL|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
