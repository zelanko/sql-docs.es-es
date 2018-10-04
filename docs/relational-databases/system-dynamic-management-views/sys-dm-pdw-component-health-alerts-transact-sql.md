---
title: Sys.dm_pdw_component_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 652467f0f40b27f35b4c805a9d646e537d51f040
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662903"
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>Sys.dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacenes de alertas en los componentes del dispositivo ha emitido anteriormente.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodo.<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|IdComponente|**int**|El identificador del componente. Consulte [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|alert_id|**int**|El identificador para el tipo de alerta. Consulte [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifica una instancia de una alerta dada.<br /><br /> pdw_node_id, IdComponente, component_instance_id, alert_id y alert_instance_id forman la clave para esta vista.|NOT NULL|  
|previous_value|**nvarchar(255)**|Se utiliza cuando la alerta es de tipo StatusChange. Este es el estado del componente anterior. Valor es NULL para las alertas de umbral de tipo. Consulte [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|current_value|**nvarchar(255)**|Se utiliza cuando la alerta es de tipo StatusChange. Este es el estado actual del componente. Valor es NULL para las alertas de umbral de tipo. Consulte [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) para obtener una lista de tipos de alerta.|NULL|  
|create_time|**datetime**|Hora y fecha cuando se generó la alerta.|NOT NULL|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
