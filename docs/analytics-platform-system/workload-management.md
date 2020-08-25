---
title: Administración de cargas de trabajo
description: Administración de cargas de trabajo en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399445"
---
# <a name="workload-management-in-analytics-platform-system"></a>Administración de cargas de trabajo en Analytics Platform System

Las capacidades de administración de cargas de trabajo de PDW de SQL Server permiten a los usuarios y administradores asignar solicitudes a configuraciones predefinidas de memoria y simultaneidad. Use la administración de cargas de trabajo para mejorar el rendimiento de la carga de trabajo, ya sea coherente o mixta, permitiendo que las solicitudes tengan los recursos adecuados sin privar las solicitudes de manera indefinida.  
  
Por ejemplo, con las técnicas de administración de cargas de trabajo en PDW de SQL Server, puede:  
  
-   Asigne un gran número de recursos a un trabajo de carga.  
  
-   Especifique más recursos para crear un índice de almacén de columnas.  
  
-   Solucionar problemas de una combinación hash de rendimiento lento para ver si necesita más memoria y, a continuación, asignarle más memoria.  
  
## <a name="workload-management-basics"></a><a name="Basics"></a>Aspectos básicos de la administración de cargas de trabajo  
  
### <a name="key-terms"></a>Términos clave  
Administración de cargas de trabajo  
La *Administración de cargas de trabajo* es la capacidad de comprender y ajustar el uso de recursos del sistema para lograr el mejor rendimiento para las solicitudes simultáneas.  
  
Clase de recurso  
En PDW de SQL Server, una *clase de recurso* es un rol de servidor integrado que tiene límites asignados previamente para la memoria y la simultaneidad. PDW de SQL Server asigna recursos a las solicitudes según la pertenencia al rol de servidor de clase de recurso del inicio de sesión que envía las solicitudes.  
  
En los nodos de proceso, la implementación de clases de recursos utiliza la característica Resource Governor en SQL Server. Para obtener más información acerca de Resource Governor, vea [Resource Governor](../relational-databases/resource-governor/resource-governor.md) en MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Comprender el uso de recursos actual  
Para comprender el uso de recursos del sistema para las solicitudes que se están ejecutando actualmente, use el PDW de SQL Server vistas de administración dinámica. Por ejemplo, puede usar DMV para saber si una combinación de hash grande de ejecución lenta podría beneficiarse de una mayor cantidad de memoria.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ajustar asignaciones de recursos  
Para ajustar el uso de recursos, cambie la pertenencia a la clase de recurso del inicio de sesión que envía la solicitud. Los roles de servidor de clase de recurso se denominan **mediumrc**, **largerc**y **xlargerc**. Representan asignaciones de recursos de tamaño medio, grande y extra, respectivamente.  
  
Por ejemplo, para asignar una gran cantidad de recursos del sistema a una solicitud, agregue el inicio de sesión que envía la solicitud al rol de servidor **largerc** . La siguiente instrucción ALTER SERVER ROLE agrega el inicio de sesión Anna al rol de servidor largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="resource-class-descriptions"></a><a name="RC"></a>Descripciones de clases de recursos  
En la tabla siguiente se describen las clases de recursos y sus asignaciones de recursos del sistema.  
  
|Clase de recurso|Importancia de la solicitud|Uso máximo de memoria *|Espacios de simultaneidad (máximo = 32)|Descripción|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|Media|400 MB|1|De forma predeterminada, se permite a cada inicio de sesión una pequeña cantidad de memoria y recursos de simultaneidad para sus solicitudes.<br /><br />Cuando se agrega un inicio de sesión a una clase de recurso, la nueva clase tiene prioridad. Cuando se quita un inicio de sesión de todas las clases de recursos, el inicio de sesión vuelve a la asignación de recursos predeterminada.|  
|MediumRC|Media|1200 MB|3|Ejemplos de solicitudes que podrían necesitar la clase de recursos Medium:<br /><br />Operaciones CTAS que tienen combinaciones hash de gran tamaño.<br /><br />Seleccione operaciones que necesiten más memoria para evitar el almacenamiento en caché en disco.<br /><br />Carga de datos en índices de almacén de columnas en clúster.<br /><br />Compilar, recompilar y reorganizar índices de almacén de columnas en clúster para tablas más pequeñas que tienen 10-15 columnas.|  
|Largerc|Alto|2,8 GB|7|Ejemplos de solicitudes que podrían necesitar la clase de recursos grandes:<br /><br />Operaciones CTAS muy grandes que tienen combinaciones de hash enormes o que contienen agregaciones de gran tamaño, como las cláusulas ORDER BY o GROUP BY de gran tamaño.<br /><br />Seleccione operaciones que requieran grandes cantidades de memoria para operaciones como combinaciones hash o agregaciones como cláusulas ORDER BY o GROUP BY.<br /><br />Carga de datos en índices de almacén de columnas en clúster.<br /><br />Compilar, recompilar y reorganizar índices de almacén de columnas en clúster para tablas más pequeñas que tienen 10-15 columnas.|  
|xlargerc|Alto|8,4 GB|22|La clase de recursos extra grande es para las solicitudes que podrían requerir un mayor consumo de recursos en tiempo de ejecución.|  
  
<sup>*</sup>El uso máximo de memoria es una aproximación.  
  
### <a name="request-importance"></a>Importancia de la solicitud  
La importancia de la solicitud se asigna a la cantidad de tiempo de CPU que SQL Server, que se ejecuta en los nodos de proceso, proporcionará a las solicitudes.  Las solicitudes con mayor prioridad reciben más tiempo de CPU.  
  
### <a name="maximum-memory-usage"></a>Uso máximo de memoria  
El uso de memoria máximo es la cantidad máxima de memoria disponible que puede usar una solicitud dentro de cada espacio de procesamiento. Por ejemplo, una solicitud mediumrc puede usar hasta 1200 MB para el procesamiento dentro de cada distribución. Todavía es importante asegurarse de que los datos no se sesgan con el fin de evitar que algunas distribuciones realicen la mayor parte del trabajo.  
  
### <a name="concurrency-slots"></a>Espacios de simultaneidad  
El objetivo de asignar 1, 3, 7 y 22 espacios de simultaneidad es permitir que los procesos grandes y pequeños se ejecuten al mismo tiempo, sin bloquear el proceso pequeño cuando se está ejecutando un proceso grande.  Por ejemplo, PDW de SQL Server puede asignar un máximo de 32 ranuras de simultaneidad para ejecutar una solicitud extra grande (22 ranuras), una solicitud de gran tamaño (7 ranuras) y una solicitud de 1 medio (3 ranuras) al mismo tiempo.  
  
Ejemplos de asignación de hasta 32 ranuras de simultaneidad a solicitudes simultáneas:  
  
-   28 ranuras = 4 grandes  
  
-   30 ranuras = 10 medianas  
  
-   32 ranuras = 32 valor predeterminado  
  
-   32 ranuras = 1 extra grande + 1 grande + 1 medio  
  
-   32 ranuras = 2 grandes + 4 medio + 6 predeterminado  
  
Supongamos que se envían 6 solicitudes grandes a PDW de SQL Server y, a continuación, se envían 10 solicitudes predeterminadas. PDW de SQL Server procesará las solicitudes en orden de prioridad como se indica a continuación:  
  
-   Asigne 28 ranuras de simultaneidad para iniciar el procesamiento de 4 solicitudes grandes a medida que la memoria esté disponible y mantenga 2 solicitudes grandes en la cola.  
  
-   Asigne 4 espacios de simultaneidad para iniciar el procesamiento de 4 solicitudes predeterminadas y mantener 6 solicitudes predeterminadas en la cola de espera.  
  
A medida que finalicen las solicitudes y estén disponibles los espacios de simultaneidad, PDW de SQL Server asignará las solicitudes restantes en función de los recursos disponibles y la prioridad. Por ejemplo, cuando hay 7 ranuras de simultaneidad abiertas, la espera de solicitudes grandes tendrá mayor prioridad para las 7 ranuras que las solicitudes medianas en espera.  Si hay 6 ranuras abiertas, PDW de SQL Server asignará 6 solicitudes más de tamaño predeterminado. Sin embargo, todos los espacios de memoria y simultaneidad deben estar disponibles antes de que PDW de SQL Server permita la ejecución de una solicitud.  
  
Dentro de cada clase de recurso, las solicitudes se ejecutan en el orden FIFO (primero en salir).  
  
## <a name="general-remarks"></a><a name="GeneralRemarks"></a>Notas generales  
Si un inicio de sesión es miembro de más de una clase de recurso, la clase con la mayoría de los recursos tiene prioridad.  
  
Cuando se agrega o se quita un inicio de sesión en una clase de recurso, el cambio surte efecto inmediatamente en todas las solicitudes futuras; las solicitudes actuales que se están ejecutando o en espera no se ven afectadas. El inicio de sesión no necesita desconectarse y volver a conectarse para que se produzca el cambio.  
  
En cada inicio de sesión, los valores de la clase de recursos se aplican a instrucciones y operaciones individuales, y no a la sesión.  
  
Antes de que PDW de SQL Server ejecute una instrucción, intenta adquirir los espacios de simultaneidad necesarios para la solicitud. Si no puede adquirir suficientes espacios de simultaneidad, PDW de SQL Server mueve la solicitud a un estado en espera de ejecución. Todo el sistema de recursos que ya se asignó a la solicitud se devuelve al sistema.  
  
La mayoría de las instrucciones SQL siempre necesitan las asignaciones predeterminadas de recursos y, por tanto, las clases de recursos no las controlan. Por ejemplo, crear inicio de sesión solo necesita una pequeña cantidad de recursos y se le asignan los recursos predeterminados incluso si el inicio de sesión que llama a CREATE LOGIN es miembro de una clase de recurso.  Por ejemplo, si Anna es miembro de la clase de recursos largerc y envía una instrucción CREATE LOGIN, la instrucción CREATE LOGIN se ejecutará con el número predeterminado de recursos.  
  
Instrucciones y operaciones SQL regidas por clases de recursos:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER TABLE REBUILD  
  
-   CREAR ÍNDICE CLÚSTER  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREAR TABLA REMOTA COMO SELECT  
  
-   Carga de datos con **dwloader**.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   Delete  
  
-   RESTAURe la base de datos al restaurar en un dispositivo con más nodos de proceso.  
  
-   SELECT, excluidas las consultas solo de DMV  
  
## <a name="limitations-and-restrictions"></a><a name="Limits"></a>Limitaciones y restricciones  
Las clases de recursos rigen las asignaciones de memoria y simultaneidad.  No controlan las operaciones de entrada/salida.  
  
## <a name="metadata"></a><a name="Metadata"></a>Metadatos  
DMV que contienen información sobre las clases de recursos y los miembros de clase de recurso.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMV que contienen información sobre el estado de las solicitudes y los recursos que necesitan:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Vistas del sistema relacionadas que se exponen desde el SQL Server DMV en los nodos de proceso. Vea [SQL Server vistas de administración dinámica](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para obtener vínculos a estas DMV en MSDN.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   Sys. dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a>Tareas relacionadas  
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
  
