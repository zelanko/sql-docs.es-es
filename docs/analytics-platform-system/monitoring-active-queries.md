---
title: Supervisar consultas activas - almacenamiento de datos paralelos | Microsoft Docs
description: Use las vistas de consola de administración y almacenamiento de datos paralelos del sistema para supervisar las consultas activas en Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2b1ee84b2ae738d7790e1238176331a221ac473
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52409872"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Supervisión de consultas activas - almacenamiento de datos paralelos
En este artículo se muestra cómo usar la consola de administración y las vistas del sistema de PDW de SQL Server para supervisar las consultas activas. Consulte [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) y [vistas del sistema](tsql-system-views.md) para obtener información sobre estas herramientas.  
  
## <a name="prerequisites"></a>Requisitos previos  
Independientemente del método usado para supervisar las consultas activas, el inicio de sesión debe tener los permisos descritos en "Uso todas de la consola de administración" en [conceder permisos para usar la consola de administración](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="PermsAdminConsole"></a>Consultas activas del Monitor  
La consola de administración y las vistas del sistema de PDW de SQL Server pueden usarse para supervisar las consultas activas. Siga las instrucciones siguientes.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Para supervisar las consultas activas mediante la consola de administración  
  
1.  Inicie sesión en la consola de administración. Consulte [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) para obtener instrucciones.  
  
2.  En el menú superior, haga clic en **consultas**. Verá una tabla con información básica acerca de las consultas más reciente en el dispositivo, incluido el inicio de sesión que envió la consulta, los tiempos de inicio y finalización para la consulta y el estado actual de la consulta.  
  
3.  Para ver el comando de consulta, mantenga el puntero del mouse sobre el identificador de la consulta en la columna izquierda para esa fila.  
  
    Para ver que información más detallada sobre una consulta determinada, haga clic en el identificador de consulta. Verá información con la consulta completa y el plan de consulta, con información de estado de cada paso de la ejecución de consultas. Si se devolvieron los errores, también puede ver información detallada sobre los errores. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Para supervisar las consultas activas con las vistas del sistema  
La vista del sistema principal utilizada para supervisar las consultas es [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Use esta vista del sistema para encontrar el `request_id` para las consultas activas o reciente, según el texto de consulta.  
  
Por ejemplo, la siguiente consulta busca el `request_id` y actual `status` para cualquier consulta que selecciona todas las columnas de la `memberAddresses` tabla.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
Después de la `request_id` ha sido identificado para una consulta, use la otra información de la `dm_pdw_exec_requests` para obtener información sobre el procesamiento de la consulta de tabla o usar [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) para ver el estado de la consulta individual pasos para la ejecución de consultas.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
