---
title: Cargas de monitor
description: Supervise las cargas activas y recientes mediante el uso de la consola de administración de Analytics Platform System (APS) o las vistas del sistema de almacenamiento de datos paralelo (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b67460528da7cac2e7d3d2d10dfbb4719b08d77f
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/17/2020
ms.locfileid: "97638074"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>Supervisión de cargas en almacenamiento de datos paralelos
Supervise las cargas [dwloaders](dwloader.md) activas y recientes mediante la consola de administración de Analytics Platform System (APS) o las [vistas del sistema](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)de almacenamiento de datos paralelo (PDW). 
  
> [!TIP]  
> Algunas cargas se inician mediante instrucciones INSERT o herramientas de inteligencia empresarial que usan instrucciones SQL para realizar la carga. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Prerrequisitos  
Independientemente del método utilizado para supervisar una carga, el inicio de sesión debe tener permiso de acceso a los orígenes de datos subyacentes. 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>Supervisión de cargas  
En las secciones siguientes se describe cómo supervisar cargas.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>Para supervisar las cargas mediante la consola de administración  
  
1.  Inicie sesión en la consola de administración de. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  En el menú superior, haga clic en **cargas**. Verá una tabla que se puede ordenar y que muestra todas las cargas recientes y activas más información adicional, por ejemplo, si la carga se ha completado o todavía está activa. Haga clic en los encabezados de columna para ordenar las filas.  
  
3.  Para ver detalles adicionales de una carga específica, haga clic en el **identificador** de carga en la columna izquierda. En la vista detallada, puede ver el progreso en cada paso de la carga.  
  
Consulte estas vistas del sistema para obtener información sobre los metadatos acerca de la carga que se muestra en la consola de administración:  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md?view=aps-pdw-2016-au7&preserve-view=true)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>Para supervisar las cargas mediante vistas del sistema  
Para supervisar las cargas activas y recientes mediante PDW de SQL Server vistas, siga los pasos que se indican a continuación. Para cada vista del sistema utilizada, vea la documentación de esa vista para obtener información sobre las columnas y los valores posibles devueltos por la vista.  
  
1.  Busque la `request_id` de la carga en la [Sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) vista buscando la línea de comandos del cargador en la `command` columna para esta vista.  
  
    Por ejemplo, el siguiente comando devuelve el texto del comando y el estado actual, más el `request_id` .  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  Utilice el `request_id` para recuperar información adicional para la carga mediante el [Sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) y las vistas de [Sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) . Por ejemplo, la consulta siguiente devuelve el `run_id` y la información sobre los tiempos de inicio, finalización y duración de la carga, más los errores e información sobre el número de filas procesadas:  
  
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
