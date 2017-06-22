---
title: "Solución de problemas de PolyBase | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
caps.latest.revision: 22
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bef55c15906ea76d2993d41e3eb7cbfd4bac9a4f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="polybase-troubleshooting"></a>Solución de problemas de PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para solucionar problemas de PolyBase, use las técnicas que aparecen en este tema.  
  
## <a name="catalog-views"></a>Vistas de catálogo  
 Use las vistas de catálogo que aparecen aquí para administrar las operaciones de PolyBase.  
  
|||  
|-|-|  
|Ver|Descripción|  
|[sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|Identifica tablas externas.|  
|[sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|Identifica orígenes de datos externos.|  
|[sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|Identifica formatos de archivo externos.|  
  
## <a name="dynamic-management-views"></a>Vistas de administración dinámica  
  
|||  
|-|-|  
|[sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  
  
  Las consultas de PolyBase se dividen en una serie de pasos en sys.dm_exec_distributed_request_steps. La tabla siguiente proporciona una asignación desde el nombre del paso a la DMV asociada.
  
 |Paso de PolyBase|DMV asociada|  
 |-|-| 
 |HadoopJobOperation | sys.dm_exec_external_operations|
 |RandomIdOperation | sys.dm_exec_distributed_request_steps|
 |HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
 |StreamingReturnOperation | sys.dm_exec_dms_workers|
 |OnOperation | sys.dm_exec_distributed_sql_requests |
  
  
## <a name="to-monitor-polybase-queries-using-dmvs"></a>Para supervisar consultas de PolyBase con DMV  
 Supervise y solucione problemas de las consultas de PolyBase con los siguientes DMV.  
  
1.  **Encuentre las consultas que más tardan en ejecutarse**  
  
     Anote el id. de ejecución de la consulta que más tarda en ejecutarse.  
  
    ```tsql  
     -- Find the longest running query  
    SELECT execution_id, st.text, dr.total_elapsed_time  
    FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
2.  **Encuentre el paso de la consulta distribuida que más tarda en ejecutarse**  
  
     Use el id. de ejecución que anotó en el paso anterior. Anote el índice de paso del paso que más tarda en ejecutarse.  
  
     Compruebe el valor location_type del paso que más tarda en ejecutarse:  
  
    -   HEAD o proceso: implica una operación SQL. Vaya al Paso 3a.  
  
    -   DMS: implica una operación del servicio de movimiento de datos de PolyBase. Vaya al Paso 3b.  
  
    ```tsql  
    -- Find the longest running step of the distributed query plan  
    SELECT execution_id, step_index, operation_type, distribution_type,   
    location_type, status, total_elapsed_time, command   
    FROM sys.dm_exec_distributed_request_steps   
    WHERE execution_id = 'QID4547'   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
3.  **Encuentre el progreso de la ejecución del paso que más tarda en ejecutarse**  
  
    1.  **Encuentre el progreso de la ejecución de un paso de SQL**  
  
         Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores. Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores.  
  
        ```tsql  
        -- Find the execution progress of SQL step    
        SELECT execution_id, step_index, distribution_id, status,   
        total_elapsed_time, row_count, command   
        FROM sys.dm_exec_distributed_sql_requests   
        WHERE execution_id = 'QID4547' and step_index = 1;  
  
        ```  
  
    2.  **Encuentre el progreso de la ejecución de un paso de DMS**  
  
         Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores.  
  
        ```tsql  
        -- Find the execution progress of DMS step    
        SELECT execution_id, step_index, dms_step_index, status,   
        type, bytes_processed, total_elapsed_time  
        FROM sys.dm_exec_dms_workers   
        WHERE execution_id = 'QID4547'   
        ORDER BY total_elapsed_time DESC;  
  
        ```  
  
4.  **Encuentre la información sobre las operaciones DMS externas**  
  
     Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores.  
  
    ```tsql  
    SELECT execution_id, step_index, dms_step_index, compute_node_id,   
    type, input_name, length, total_elapsed_time, status   
    FROM sys.dm_exec_external_work   
    WHERE execution_id = 'QID4547' and step_index = 7   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
## <a name="to-view-the--polybase-query-plan"></a>Para ver el plan de consulta de PolyBase  
  
1.  En SSMS, habilite **Incluir plan de ejecución real** (Ctrl+M) y ejecute la consulta.  
  
2.  Haga clic en la pestaña **Plan de ejecución** .  
  
     ![Plan de consulta de PolyBase](../../relational-databases/polybase/media/polybase-query-plan.png "Plan de consulta de PolyBase")  
  
3.  Haga clic con el botón derecho en el **operador de consulta remota** y seleccione **Propiedades**.  
  
4.  Copie y pegue el valor de consulta remota en un editor de texto para ver el plan de consulta remota en formato XML.  A continuación, se muestra un ejemplo.  
  
    ```xml  
  
    <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
           [T1_1].[CustomerKey] AS [CustomerKey],  
           [T1_1].[GeographyKey] AS [GeographyKey],  
           [T1_1].[Speed] AS [Speed],  
           [T1_1].[YearMeasured] AS [YearMeasured]  
    FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                   [T2_1].[CustomerKey] AS [CustomerKey],  
                   [T2_1].[GeographyKey] AS [GeographyKey],  
                   [T2_1].[Speed] AS [Speed],  
                   [T2_1].[YearMeasured] AS [YearMeasured]  
            FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
            WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
    </dsql_query>  
    ```  
  
## <a name="to-monitor-nodes-in-a-polybase-group"></a>Para supervisar los nodos de un grupo de PolyBase  
 Después de configurar un conjunto de máquinas como parte de un grupo de escalado horizontal de PolyBase, puede supervisar el estado de las máquinas. Para obtener detalles sobre cómo crear un grupo de escalado horizontal, vea [Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).  
  
1.  Conéctese a SQL Server en el nodo principal de un grupo.  
  
2.  Ejecute la DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) para ver todos los nodos del grupo de PolyBase.  
  
3.  Ejecute la DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) para ver el estado de todos los nodos del grupo de PolyBase.  
  
 ## <a name="known-limitations"></a>Restricciones conocidas
 
 PolyBase presenta las siguientes limitaciones: 
 - El tamaño máximo posible de fila, incluida la longitud total de las columnas de longitud variable, no puede superar los 1 MB. 
 - PolyBase no admite los tipos de datos de Hive 0.12+ (es decir, Char(), VarChar())   
 - Al exportar datos en un formato de archivo ORC desde SQL Server o Azure SQL Data Warehouse, las columnas pesadas de texto pueden limitarse a tan solo 50 columnas debido a errores de memoria insuficiente de Java. Para solucionar este problema, exporte solo un subconjunto de las columnas.
- [PolyBase no se instala cuando se agrega un nodo a un clúster de conmutación por error de SQL Server 2016](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)
  
## <a name="error-messages-and-possible-solutions"></a>Mensajes de error y posibles soluciones

Para solucionar errores de tabla externa, vea el blog de Murshed Zaman [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "Errores de configuración de PolyBase y posibles soluciones").

