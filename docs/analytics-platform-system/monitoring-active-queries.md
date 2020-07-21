---
title: Supervisión de consultas activas
description: Use la consola de administración y las vistas del sistema de almacenamiento de datos paralelos para supervisar las consultas activas en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400911"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Supervisión de consultas activas: almacenamiento de datos paralelos
En este artículo se muestra cómo usar la consola de administración de y las vistas del sistema de PDW de SQL Server para supervisar las consultas activas. Consulte [supervisión del dispositivo mediante la consola de administración y las](monitor-the-appliance-by-using-the-admin-console.md) [vistas del sistema](tsql-system-views.md) para obtener información sobre estas herramientas.  
  
## <a name="prerequisites"></a>Prerrequisitos  
Independientemente del método que se use para supervisar las consultas activas, el inicio de sesión debe tener los permisos descritos en "usar toda la consola de administración" en [conceder permisos para usar la consola de administración](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="monitor-active-queries"></a><a name="PermsAdminConsole"></a>Supervisión de consultas activas  
Tanto la consola de administración como la PDW de SQL Server vistas del sistema se pueden usar para supervisar las consultas activas. Siga las instrucciones que se describen a continuación.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Para supervisar las consultas activas mediante la consola de administración  
  
1.  Inicie sesión en la consola de administración de. Consulte [supervisión del dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) para obtener instrucciones.  
  
2.  En el menú superior, haga clic en **consultas**. Verá una tabla con información básica sobre las consultas más recientes en el dispositivo, incluido el inicio de sesión que envió la consulta, las horas de inicio y finalización de la consulta y el estado actual de la consulta.  
  
3.  Para ver el comando de consulta, mantenga el puntero del mouse sobre el identificador de la consulta en la columna izquierda de esa fila.  
  
    Para ver información más detallada de una consulta determinada, haga clic en el identificador de la consulta. Verá información que incluye la consulta completa y el plan de consulta, con información de estado para cada paso de la ejecución de la consulta. Si se devolvieron errores, también puede ver información detallada sobre los errores. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Para supervisar las consultas activas mediante las vistas del sistema  
La vista del sistema principal utilizada para supervisar consultas es [Sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Utilice esta vista del sistema para buscar `request_id` el para una consulta activa o reciente, en función del texto de la consulta.  
  
Por ejemplo, la siguiente consulta busca el `request_id` y el actual `status` de cualquier consulta que seleccione todas las columnas de `memberAddresses` la tabla.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
Una vez `request_id` identificado el para una consulta, use la otra información de la `dm_pdw_exec_requests` tabla para averiguar el procesamiento de la consulta o use [Sys. dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) para ver el estado de los pasos de consulta individuales para la ejecución de la consulta.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
