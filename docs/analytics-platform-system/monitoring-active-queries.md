---
title: Supervisar consultas activas - almacenamiento de datos paralelos | Documentos de Microsoft
description: Utilice las vistas de sistema de la consola de administración y almacenamiento de datos paralelos para supervisar consultas activas en el sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 057e5448b68ea7a7f8f23bc57d1a3b0308b300d2
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538705"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Supervisión de consultas activas - almacenamiento de datos paralelos
Este artículo muestra cómo utilizar la consola de administración y las vistas del sistema PDW de SQL Server para supervisar consultas activas. Vea [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) y [vistas del sistema](tsql-system-views.md) para obtener información sobre estas herramientas.  
  
## <a name="prerequisites"></a>Requisitos previos  
Independientemente del método utilizado para supervisar consultas activas, el inicio de sesión debe tener los permisos descritos en "Usar todos los de la consola de administración" en [conceder permisos para usar la consola de administración](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="PermsAdminConsole"></a>Consultas activas del Monitor  
La consola de administración y las vistas del sistema PDW de SQL Server pueden usarse para supervisar las consultas activas. Siga las instrucciones siguientes.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Para supervisar consultas activas mediante la consola de administración  
  
1.  Inicie sesión en la consola de administración. Vea [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) para obtener instrucciones.  
  
2.  En el menú superior, haga clic en **consultas**. Verá una tabla con información básica acerca de las consultas más reciente en el dispositivo, incluido el inicio de sesión que envió la consulta, los tiempos de inicio y finalización para la consulta y el estado actual de la consulta.  
  
3.  Para ver el comando de consulta, mantenga el puntero del mouse sobre el identificador de la consulta en la columna izquierda para esa fila.  
  
    Para ver que información más detallada sobre una consulta determinada, haga clic en el identificador de la consulta. Verá información como la consulta completa y el plan de consulta con información de estado de cada paso de la ejecución de la consulta. Si se devuelven los errores, también puede ver información detallada sobre los errores. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Para supervisar las consultas activas con las vistas del sistema  
Es la vista del sistema principal utilizada para supervisar consultas [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Utilice esta vista de sistema para encontrar el `request_id` para una consulta activa o reciente, basándose en el texto de consulta.  
  
Por ejemplo, la siguiente consulta busca el `request_id` y actual `status` para cualquier consulta que selecciona todas las columnas de la `memberAddresses` tabla.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE ‘%SELECT * FROM db1..memberAddresses%’;  
```  
  
Después de la `request_id` ha sido identificada para una consulta, use la otra información de la `dm_pdw_exec_requests` de tabla para obtener información sobre el procesamiento de la consulta o usar [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) para ver el estado de la consulta individual pasos para la ejecución de la consulta.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
