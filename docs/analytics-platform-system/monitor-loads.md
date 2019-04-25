---
title: Supervisar las cargas de almacenamiento de datos paralelos | Microsoft Docs
description: Supervisar las cargas activas y recientes mediante el uso de la consola de administración de Analytics Platform System (APS) o las vistas de sistema de (PDW) de almacenamiento de datos paralelo".
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cb840c64c2235a2f3902c45633aa5471655482dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639965"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>Supervisar las cargas de almacenamiento de datos paralelos
Monitor activa y reciente [dwloader](dwloader.md) carga mediante la consola de administración de Analytics Platform System (APS) o el almacenamiento de datos paralelos (PDW) [vistas del sistema](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/). 
  
> [!TIP]  
> Algunas de las cargas se inician mediante el uso de las instrucciones INSERT o herramientas de inteligencia empresarial que usar instrucciones SQL para realizar la carga. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Requisitos previos  
Independientemente del método usado para supervisar una carga, el inicio de sesión debe tener permiso para tener acceso a los orígenes de datos subyacente. 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>Supervisión de cargas  
Las secciones siguientes describen cómo supervisar las cargas.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>Para supervisar las cargas mediante el uso de la consola de administración  
  
1.  Inicie sesión en la consola de administración. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  En el menú superior, haga clic en **cargas**. Verá una tabla que se puede ordenar que muestra todos los recientes y cargas activas así como información adicional, por ejemplo, si la carga se ha completado o aún está activa. Haga clic en los encabezados de columna para ordenar las filas.  
  
3.  Para ver detalles adicionales para una carga específica, haga clic en la carga **ID** en la columna izquierda. En la vista detallada, puede ver el progreso en cada paso de la carga.  
  
Consulte estas vistas del sistema para obtener información sobre los metadatos acerca de la carga que se muestra en la consola de administración:  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>Para supervisar las cargas mediante el uso de vistas del sistema  
Para supervisar cargas activas y recientes mediante las vistas de SQL Server PDW, siga los pasos siguientes. Para cada vista del sistema que utiliza, consulte la documentación de esa vista para obtener información en las columnas y los posibles valores devueltos por la vista.  
  
1.  Buscar el `request_id` para la carga en el [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) vista mediante la búsqueda de la línea de comandos del cargador en la `command` columna para esta vista.  
  
    Por ejemplo, el siguiente comando devuelve el texto del comando y el estado actual, más el `request_id`.  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  Use la `request_id` para recuperar información adicional para la carga mediante el uso de la [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) , y [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) vistas. Por ejemplo, la consulta siguiente devuelve el `run_id` y obtener información acerca de las horas de inicio, final y duración de la carga, además de los errores e información sobre el número de filas procesadas:  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id='12738';  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
