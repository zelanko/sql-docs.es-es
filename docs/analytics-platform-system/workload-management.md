---
title: Administración de cargas de trabajo de Analytics Platform System | Microsoft Docs
description: Administración de cargas de trabajo de Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2281262c086f4d8dcab27debc8bb735ea5e8e1ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157472"
---
# <a name="workload-management-in-analytics-platform-system"></a>Administración de cargas de trabajo de Analytics Platform System

Capacidades de administración de cargas de trabajo de PDW de SQL Server permiten a los usuarios y administradores para asignar las solicitudes para establecer previamente las configuraciones de memoria y simultaneidad. Use Administración de cargas de trabajo para mejorar el rendimiento de la carga de trabajo coherente o mixto, permitiendo solicitudes para tener los recursos adecuados sin privar así a las solicitudes para siempre.  
  
Por ejemplo, con las técnicas de administración de cargas de trabajo en PDW de SQL Server, puede:  
  
-   Asignar un gran número de recursos para un trabajo de carga.  
  
-   Especifique más recursos para la creación de un índice de almacén de columnas.  
  
-   Solución de problemas de una combinación hash de bajo rendimiento para ver si necesita más memoria y, a continuación, darle más memoria.  
  
## <a name="Basics"></a>Conceptos básicos de administración de cargas de trabajo  
  
### <a name="key-terms"></a>Términos clave  
Administración de cargas de trabajo  
*Administración de cargas de trabajo* es la capacidad de comprender y ajustar el uso de recursos del sistema con el fin de obtener el mejor rendimiento de solicitudes simultáneas.  
  
Clase de recursos  
En SQL Server PDW, un *clase de recurso* es un rol de servidor integrada que tiene asignados previamente los límites de memoria y simultaneidad. PDW de SQL Server asigna recursos a las solicitudes según la pertenencia a roles de recursos clase servidor de inicio de sesión que envía las solicitudes.  
  
En los nodos de proceso, la implementación de las clases de recursos usa la característica regulador de recursos en SQL Server. Para obtener más información sobre el regulador de recursos, consulte [del regulador de recursos](../relational-databases/resource-governor/resource-governor.md) en MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Comprender el uso de recursos actual  
Para entender el uso de recursos del sistema para las solicitudes que se está ejecutando, use las vistas de administración dinámica de PDW de SQL Server. Por ejemplo, puede usar DMV para comprender si una combinación hash grandes de ejecución lenta puede beneficiarse al tener más memoria.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ajustar las asignaciones de recursos  
Para ajustar el uso de recursos, cambiar la pertenencia de la clase de recursos del inicio de sesión que está enviando la solicitud. Los roles de servidor de la clase de recursos se denominan **mediumrc**, **largerc**, y **xlargerc**. Representan las asignaciones de recursos mediana, grande y extragrande respectivamente.  
  
Por ejemplo, para asignar una gran cantidad de recursos del sistema para una solicitud, agregue el inicio de sesión que está enviando la solicitud para el **largerc** rol de servidor. La siguiente instrucción ALTER SERVER ROLE agrega el inicio de sesión Anna al rol de servidor largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descripciones de la clase de recurso  
En la tabla siguiente se describe las clases de recursos y sus asignaciones de recursos del sistema.  
  
|Clase de recursos|Importancia de la solicitud|Uso de memoria máxima *|Espacios de simultaneidad (máxima = 32)|Descripción|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|predeterminados|Media|400 MB|1|De forma predeterminada, cada inicio de sesión se permite una pequeña cantidad de memoria y simultaneidad de recursos para sus solicitudes.<br /><br />Cuando se agrega un inicio de sesión a una clase de recursos, la nueva clase tiene prioridad. Cuando se quita un inicio de sesión de todas las clases de recursos, el inicio de sesión vuelve a la asignación de recursos predeterminado.|  
|MediumRC|Media|1200 MB|3|Ejemplos de solicitudes que pueden necesitar la clase de recursos de tamaño medio:<br /><br />Las operaciones de CTAS que tengan grandes combinaciones hash.<br /><br />Seleccione las operaciones que necesitan más memoria para evitar el almacenamiento en caché en el disco.<br /><br />Cargar datos en los índices de almacén de columnas agrupado.<br /><br />Creación, la regeneración y reorganización de índices de almacén de columnas agrupado para tablas más pequeñas que tienen columnas de 10-15.|  
|Largerc|Alta|2,8 GB|7|Ejemplos de solicitudes que pueden necesitar la clase de recursos grande:<br /><br />Operaciones de CTAS muy grandes que tienen las combinaciones hash enorme o contienen grandes agregaciones, como grandes cláusulas ORDER BY o GROUP BY.<br /><br />Seleccione las operaciones que requieren grandes cantidades de memoria para operaciones como las combinaciones hash o agregaciones, como las cláusulas ORDER BY o GROUP BY<br /><br />Cargar datos en los índices de almacén de columnas agrupado.<br /><br />Creación, la regeneración y reorganización de índices de almacén de columnas agrupado para tablas más pequeñas que tienen columnas de 10-15.|  
|xlargerc|Alta|8.4 GB|22|La clase de recurso extra grande es para las solicitudes que podrían requerir el consumo de recursos extragrande en tiempo de ejecución.|  
  
<sup>*</sup>Uso máximo de memoria es una aproximación.  
  
### <a name="request-importance"></a>Importancia de la solicitud  
La importancia de la solicitud se asigna a la cantidad de tiempo de CPU que ofrecen SQL Server, que se ejecutan en los nodos de proceso a las solicitudes.  Las solicitudes con una prioridad mayor reciben más tiempo de CPU.  
  
### <a name="maximum-memory-usage"></a>Uso de memoria máximo  
Uso máximo de memoria es la cantidad máxima de memoria disponible, que puede usar una solicitud dentro de cada espacio de procesamiento. Por ejemplo puede usar una solicitud mediumrc hasta 1200 MB para el procesamiento dentro de cada distribución. Es importante para asegurarse de que no están sesgados datos con el fin de evitar tener algunas distribuciones que se esté realizando la mayoría del trabajo.  
  
### <a name="concurrency-slots"></a>Espacios de simultaneidad  
El objetivo de asignar 1, 3, 7 y 22 espacios de simultaneidad es permitir que los procesos grandes y pequeños se ejecuten al mismo tiempo, sin bloquear el proceso pequeño cuando se está ejecutando un proceso de gran tamaño.  Por ejemplo, PDW de SQL Server puede asignar como máximo 32 ranuras de simultaneidad para ejecutar 1 solicitud extra grande (22 ranuras), 1 solicitud de gran tamaño (7 ranuras) y 1 solicitud medio (3 ranuras) al mismo tiempo.  
  
Ejemplos de asignación de hasta 32 ranuras de simultaneidad a las solicitudes simultáneas:  
  
-   28 ranuras = 4 grandes  
  
-   30 ranuras = Media 10  
  
-   32 ranuras = 32 predeterminado  
  
-   32 ranuras = extragrande 1 + 1 medio grande + 1  
  
-   32 ranuras = 2 medio grandes + 4 + 6 predeterminado  
  
Supongamos que 6 solicitudes de gran tamaño se envían a PDW de SQL Server y, a continuación, se envían 10 solicitudes de forma predeterminada. PDW de SQL Server procesará las solicitudes en orden de prioridad como sigue:  
  
-   Asignar 28 ranuras de simultaneidad para comenzar a procesar 4 solicitudes de gran tamaño como la memoria disponible y tenga 2 solicitudes de gran tamaño en la cola.  
  
-   Asignar 4 espacios de simultaneidad para comenzar el proceso de 4 solicitudes de forma predeterminada y mantener 6 solicitudes de forma predeterminada en la cola de espera.  
  
Cuando finalicen las solicitudes y las ranuras de simultaneidad estén disponibles, PDW de SQL Server asignará las solicitudes restantes según prioridad y los recursos disponibles. Por ejemplo, cuando se abra ranuras de simultaneidad 7, espera solicitudes de gran tamaño tendrá prioridad más alta de las 7 ranuras que esperar a que las solicitudes de medio.  Si abre 6 ranuras, PDW de SQL Server asignará 6 más solicitudes tamaño predeterminado. Sin embargo, las ranuras de memoria y simultaneidad deben disponibles antes de PDW de SQL Server permite que una solicitud ejecutar.  
  
Dentro de cada clase de recursos, las solicitudes se ejecutan en el primero en orden, primero en salir (FIFO).  
  
## <a name="GeneralRemarks"></a>Notas generales  
Si un inicio de sesión es miembro de más de una clase de recursos, la clase con la mayoría de los recursos tiene prioridad.  
  
Cuando se agrega un inicio de sesión o se quita de una clase de recurso, el cambio surte efecto inmediatamente para todas las solicitudes futuras; no se ven afectadas las solicitudes actuales que están ejecutando o en espera. El inicio de sesión no es necesario desconectar y volver a conectar en orden para que se produzca el cambio.  
  
Para cada inicio de sesión, la configuración de la clase de recursos se aplica a las operaciones y las instrucciones individuales y no a la sesión.  
  
Antes de PDW de SQL Server se ejecuta una instrucción, intenta adquirir las ranuras de simultaneidad necesarias para la solicitud. Si no puede adquirir suficientes espacios de simultaneidad, PDW de SQL Server mueve la solicitud en un estado de espera de ejecutarse. Sistema de todos los recursos que ya se han asignado a la solicitud se devuelven al sistema.  
  
La mayoría de las instrucciones SQL siempre son necesarias las asignaciones de recursos predeterminado y, por tanto, no se controla mediante las clases de recursos. Por ejemplo, CREATE LOGIN solo necesita una pequeña cantidad de recursos y se asigna a los recursos predeterminados incluso si el inicio de sesión llamar a CREATE LOGIN es miembro de una clase de recursos.  Por ejemplo, si Ana es un miembro de la clase de recurso largerc y envía una instrucción CREATE LOGIN, se ejecutará la instrucción CREATE LOGIN con el número predeterminado de los recursos.  
  
Las instrucciones SQL y operaciones regidas por clases de recursos:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   CREAR ÍNDICE AGRUPADO  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   INSTRUCCIÓN CREATE TABLE AS SELECT  
  
-   INSTRUCCIÓN CREATE REMOTE TABLE AS SELECT  
  
-   Carga de datos con **dwloader**.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   SUPRIMIR  
  
-   Restaurar base de datos al restaurar en un dispositivo con más nodos de proceso.  
  
-   Seleccionar, sin incluir las consultas de solo DMV  
  
## <a name="Limits"></a>Limitaciones y restricciones  
Las clases de recursos controlan las asignaciones de memoria y simultaneidad.  No controlan las operaciones de entrada/salida.  
  
## <a name="Metadata"></a>Metadata  
DMV que contienen información sobre las clases de recursos y los miembros de clase de recurso.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMV que contienen información sobre el estado de las solicitudes y los recursos que necesitan:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Vistas del sistema relacionados procedentes de las DMV de SQL Server en los nodos de proceso. Consulte [vistas de administración dinámica de SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para obtener vínculos a estas DMV en MSDN.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>Tareas relacionadas  
[Tareas de administración de cargas de trabajo](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
