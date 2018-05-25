---
title: Sys.dm_pdw_component_health_active_alerts (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f236e451d155c88b9ceda2b1b09bbed112b8f79b
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>Sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena las alertas activas en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] componentes.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodo.<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|IdComponente|**int**|El identificador del componente. Vea [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|alert_id|**int**|El identificador para el tipo de alerta. Vea [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifica una instancia de una alerta dada.<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|current_value|**nvarchar(255)**|Se utiliza cuando la alerta es de tipo StatusChange. Este es el estado actual del componente. Valor es NULL para las alertas de umbral de tipo. Vea [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|previous_value|**nvarchar(255)**|Se utiliza cuando la alerta es de tipo StatusChange. Este es el estado del componente anterior. Valor es NULL para las alertas de umbral de tipo. Vea [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|create_time|**datetime**|Hora y fecha cuando se generó la alerta.|NOT NULL|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea "Mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
