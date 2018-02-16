---
title: "Administración de cargas de trabajo (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69063b1a-a8f3-453a-83ab-afbe7eb4f463
caps.latest.revision: 
ms.openlocfilehash: 738818a49491fbf8f8df491cac2f10ebdeedf3bf
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="workload-management"></a>Administración de cargas de trabajo
Capacidades de administración de cargas de trabajo de SQL Server PDW permiten a los usuarios y administradores asignar solicitudes previamente establecer configuraciones de memoria y simultaneidad. Use Administración de cargas de trabajo para mejorar el rendimiento de la carga de trabajo, ya sea coherente o mixto, lo que permite solicitudes para tener los recursos adecuados sin privar a las solicitudes para siempre.  
  
Por ejemplo, con las técnicas de administración de cargas de trabajo en PDW de SQL Server, puede:  
  
-   Asignar un gran número de recursos a un trabajo de carga.  
  
-   Especificar más recursos para la creación de un índice de almacén de columnas.  
  
-   Solucionar problemas de una combinación hash de bajo rendimiento para ver si necesita más memoria y, a continuación, asígnele más memoria.  
  
## <a name="Basics"></a>Fundamentos de la administración de cargas de trabajo  
  
### <a name="key-terms"></a>Términos clave  
Administración de cargas de trabajo  
*Administración de cargas de trabajo* es la capacidad para comprender y ajustar la utilización de recursos del sistema con el fin de obtener el mejor rendimiento de solicitudes simultáneas.  
  
Clase de recursos  
En SQL Server PDW, un *clase de recursos* es un rol de servidor integrado que tiene asignados previamente límites de memoria y la simultaneidad. PDW de SQL Server asigna recursos a las solicitudes de acuerdo con la pertenencia al rol de recurso clase servidor de inicio de sesión que envía las solicitudes.  
  
En los nodos de proceso, la implementación de clases de recursos usa la característica de regulador de recursos en SQL Server. Para obtener más información acerca del regulador de recursos, consulte [regulador de recursos](http://msdn.microsoft.com/en-us/library/bb933866(v=sql.11).aspx) en MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Comprender el uso de recursos actual  
Para entender el uso de recursos del sistema para las solicitudes que se están ejecutando, use las vistas de administración dinámica de SQL Server PDW. Por ejemplo, puede utilizar DMV para saber si una combinación hash grandes de ejecución lenta puede beneficiarse de tener más memoria.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ajustar las asignaciones de recursos  
Para ajustar la utilización de recursos, cambie la pertenencia de la clase de recursos de inicio de sesión que está enviando la solicitud. Los roles de servidor de la clase de recurso se denominan **mediumrc**, **largerc**, y **xlargerc**. Representan las asignaciones de recursos de mediano, grande y extragrande respectivamente.  
  
Por ejemplo, para asignar una gran cantidad de recursos del sistema a una solicitud, agregar el inicio de sesión que está enviando la solicitud para la **largerc** rol de servidor. La siguiente instrucción ALTER SERVER ROLE agrega el inicio de sesión Anna al rol de servidor largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descripciones de la clase de recurso  
En la tabla siguiente describe las clases de recursos y sus asignaciones de recursos del sistema.  
  
|Clase de recursos|Importancia de la solicitud|Uso de memoria máxima *|Las ranuras de simultaneidad (máxima = 32)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|predeterminados|Media|400 MB|1|De forma predeterminada, cada inicio de sesión se permite una pequeña cantidad de memoria y recursos de simultaneidad para sus solicitudes.<br /><br />Cuando se agrega un inicio de sesión a una clase de recursos, la nueva clase tiene prioridad. Cuando se quita un inicio de sesión de todas las clases de recursos, el inicio de sesión se vuelve a la asignación de recursos predeterminada.|  
|MediumRC|Media|1200 MB|3|Ejemplos de solicitudes que podrían necesitar la clase de recurso intermedio:<br /><br />Las operaciones de CTAS que tienen grandes combinaciones hash.<br /><br />Seleccione las operaciones que necesitan más memoria para evitar el almacenamiento en caché en el disco.<br /><br />Para cargar datos en índices de almacén de columnas agrupado.<br /><br />Compilar, volver a generar y reorganizar índices de almacén de columnas agrupado para tablas más pequeñas que tienen columnas de 10 a 15.|  
|largerc|Alta|2.8 GB|7|Ejemplos de solicitudes que pueden necesitar la clase de recursos grande:<br /><br />Operaciones CTAS muy grandes que tienen las combinaciones hash muy grandes o contengan agregaciones importantes, como grandes cláusulas ORDER BY o GROUP BY.<br /><br />Seleccione las operaciones que requieren grandes cantidades de memoria para operaciones como las combinaciones hash o agregaciones como cláusulas ORDER BY o GROUP BY<br /><br />Para cargar datos en índices de almacén de columnas agrupado.<br /><br />Compilar, volver a generar y reorganizar índices de almacén de columnas agrupado para tablas más pequeñas que tienen columnas de 10 a 15.|  
|xlargerc|Alta|8.4 GB|22|La clase de recurso extra grande es para las solicitudes que podrían requerir el consumo de recursos de gran tamaño en tiempo de ejecución.|  
  
<sup>*</sup>Uso máximo de memoria es una aproximación.  
  
### <a name="request-importance"></a>Importancia de la solicitud  
La importancia de la solicitud se asigna a la cantidad de tiempo de CPU que SQL Server se ejecute en los nodos de proceso, le dará a las solicitudes.  Las solicitudes con prioridad más alta reciben más tiempo de CPU.  
  
### <a name="maximum-memory-usage"></a>Uso máximo de memoria  
Uso máximo de memoria es la cantidad máxima de memoria disponible, que puede usar una solicitud dentro de cada espacio de procesamiento. Por ejemplo una solicitud de mediumrc puede utilizar hasta 1200 MB para el procesamiento en cada distribución. Es importante para asegurarse de que no se sesga datos con el fin de evitar tener unas distribuciones que se esté realizando la mayoría del trabajo.  
  
### <a name="concurrency-slots"></a>Ranuras de simultaneidad  
El objetivo de asignar 1, 3, 7 y 22 ranuras de simultaneidad es permitir procesos grandes y pequeños se ejecuten al mismo tiempo, sin bloquear el proceso pequeño cuando se está ejecutando un proceso de gran tamaño.  Por ejemplo, SQL Server PDW puede asignar como máximo 32 ranuras de simultaneidad para ejecutar 1 solicitud extra grande (22 ranuras), 1 solicitud de gran tamaño (7 ranuras) y 1 solicitud Media (3 ranuras) al mismo tiempo.  
  
Ejemplos de asignación de hasta 32 ranuras de simultaneidad para solicitudes simultáneas:  
  
-   28 ranuras = 4 grandes  
  
-   30 ranuras = Media 10  
  
-   32 ranuras = 32 predeterminado  
  
-   32 ranuras = 1 extragrande + 1 medio grande + 1  
  
-   32 ranuras = 2 medio grandes + 4 + 6 predeterminado  
  
Suponga que 6 solicitudes grandes se envían a PDW de SQL Server y, a continuación, se envían 10 solicitudes de manera predeterminada. SQL Server PDW procesará las solicitudes en orden de prioridad siguiente:  
  
-   Asignar 28 ranuras de simultaneidad para comenzar a procesar 4 solicitudes de gran tamaño como la memoria disponible y tenga 2 solicitudes grandes en la cola.  
  
-   Asignar 4 ranuras de simultaneidad se inicia el procesamiento 4 solicitudes de manera predeterminada y mantener 6 solicitudes de manera predeterminada en la cola de espera.  
  
Cuando finalicen las solicitudes y las ranuras de simultaneidad estén disponibles, SQL Server PDW asignará las solicitudes restantes según los recursos disponibles y prioridad. Por ejemplo, cuando hay simultaneidad 7 ranuras abrir, espera solicitudes grandes tendrán prioridad más alta de las 7 ranuras que espera las solicitudes de Media.  Si se abre el 6 ranuras, PDW de SQL Server asignará 6 más solicitudes tamaño predeterminado. Sin embargo, las ranuras de memoria y simultaneidad deben estar todas disponibles antes de PDW de SQL Server permite que una solicitud para que se ejecute.  
  
Dentro de cada clase de recursos, las solicitudes se ejecutan en el primero en orden primero en salir (FIFO).  
  
## <a name="GeneralRemarks"></a>Notas generales  
Si un inicio de sesión es miembro de más de una clase de recurso, la clase con el mayor número de recursos tiene prioridad.  
  
Cuando se agrega un inicio de sesión o se quita de una clase de recurso, el cambio surte efecto inmediatamente para todas las solicitudes futuras; no afecta a las solicitudes actuales que se están ejecutando o en espera. El inicio de sesión no es necesario desconectar y volver a conectarse en orden para que se produzca el cambio.  
  
Para cada inicio de sesión, la configuración de la clase de recurso se aplica a las operaciones y las instrucciones individuales y no a la sesión.  
  
Antes de PDW de SQL Server se ejecuta una instrucción, intenta adquirir las ranuras de simultaneidad necesarias para la solicitud. Si no se pueden adquirir suficientes ranuras de simultaneidad, SQL Server PDW mueve la solicitud en un estado de espera de ejecución. Todos los sistema de recursos que ya se han asignado a la solicitud se devuelven al sistema.  
  
La mayoría de las instrucciones SQL siempre son necesarias las asignaciones de recursos de forma predeterminada y, por tanto, no se controla mediante las clases de recursos. Por ejemplo, CREATE LOGIN solo necesita una pequeña cantidad de recursos y se asigna los recursos de manera predeterminada, incluso si el inicio de sesión al llamar a CREATE LOGIN es un miembro de una clase de recursos.  Por ejemplo, si Ana es un miembro de la clase de recurso largerc y envía una instrucción CREATE LOGIN, se ejecutará la instrucción CREATE LOGIN con la cantidad de recursos.  
  
Las instrucciones SQL y las operaciones que se rige por las clases de recursos:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   REGENERACIÓN DE LA TABLA DE ALTER  
  
-   CREAR ÍNDICE AGRUPADO  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREAR TABLA COMO SELECT  
  
-   CREAR TABLA REMOTA COMO, SELECCIONE  
  
-   Carga de datos con **dwloader**.  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   Restaurar base de datos cuando se restaura en un dispositivo con varios nodos de cálculo.  
  
-   Seleccionar, sin incluir las consultas de solo DMV  
  
## <a name="Limits"></a>Limitaciones y restricciones  
Las clases de recursos rigen las asignaciones de memoria y la simultaneidad.  No rigen las operaciones de entrada/salida.  
  
## <a name="Metadata"></a>Metadata  
DMV que contienen información sobre las clases de recursos y los miembros de clase de recurso.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMV que contienen información sobre el estado de las solicitudes y los recursos que necesitan:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Vistas del sistema relacionados expuestas a partir de las DMV de SQL Server en los nodos de proceso. Vea [vistas de administración dinámica de SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para obtener vínculos a estas DMV en MSDN.  
  
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
  
