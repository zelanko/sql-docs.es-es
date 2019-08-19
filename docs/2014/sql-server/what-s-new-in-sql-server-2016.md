---
title: Novedades&#39;de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f368da503c90595624f476344724719206cdb77c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893705"
---
# <a name="what39s-new-in-sql-server-2014"></a>Novedades&#39;de SQL Server 2014
  En este tema se resumen los vínculos detallados [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] a las nuevas características de y se resumen los paquetes de servicios para[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Pruébelo:** ![¿La máquina virtual](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) de Azure pequeña tiene una cuenta de Azure?  Después, vaya **[aquí](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** para poner en marcha una máquina Virtual con SQL Server 2014 Service Pack 1 (SP1) ya instalado. 
  
-   [Novedades &#40;motor de base de datos&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novedades de Analysis Services y Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [Novedades de la instalación de SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]no ha presentado nuevas características importantes para lo siguiente:**  
  
-   [Novedades &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Novedades &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) no introdujo nuevas características importantes.
-  [SQL Server 2014 información de la versión del Service Pack 1](https://support.microsoft.com/en-us/kb/3058865).
-  [![¿Descargar el Service Pack 1 para Microsoft? ¿SQL Server?? ](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) 2014[descargar el Service Pack 1 para Microsoft? ¿SQL Server?? 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server 2014 información de la versión del Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![¿Descargar Service Pack 2 para Microsoft? ¿SQL Server?? ](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) 2014[descargar Service Pack 2 para Microsoft? ¿SQL Server?? 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Descargar SQL Server Feature Pack de 2014 SP2](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [Descargue el Feature Pack de SQL Server 2014 SP2](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Incluye las siguientes mejoras:

### <a name="performance-and-scalability-improvements"></a>Mejoras en el rendimiento y la escalabilidad 
-   **Creación automática de particiones de NUMA de software:** Con [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, se habilita la Numa automática automática cuando la marca de seguimiento 8079 está activada durante el inicio de la instancia. Cuando la marca de seguimiento 8079 está habilitada [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] durante el inicio, SP2 interrogará el diseño de hardware y configurará automáticamente Soft Numa en los sistemas que notifican 8 o más CPU por nodo Numa. El comportamiento de NUMA automático y automático es el que reconoce el hiperproceso (procesador HT/lógico). La creación de particiones y la creación de nodos adicionales escala el procesamiento en segundo plano al aumentar el número de agentes de escucha, escalado y capacidades de red y cifrado. Se recomienda probar primero la carga de trabajo de rendimiento con NUMA de software automático antes de convertirla en producción. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Escalado de objetos de Memoria dinámica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 divide dinámicamente los objetos de memoria en función del número de nodos y núcleos para escalar en el hardware moderno. El objetivo de la promoción dinámica es particionar automáticamente un objeto de memoria seguro para subprocesos (CMEMTHREAD) si se convierte en un cuello de botella. Los objetos de memoria sin particiones se pueden promocionar dinámicamente para particionarse por nodo (el número de particiones es igual al número de nodos NUMA), y los objetos de memoria particionados por nodo se pueden promoviendo más a través de la CPU (el número de particiones es igual a número de CPU). [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Sugerencia MAXDOP para comandos DBCC\* check:** Las direcciones de esta mejora conectan los [comentarios (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Ahora puede ejecutar DBCC CHECKDB con una configuración MAXDOP distinta del valor sp_configure. Si MAXDOP supera el valor configurado con Resource Governor, el motor de base de datos usa el valor MAXDOP de Resource Governor, descrito en ALTER WORKLOAD GROUP (Transact-SQL). Se pueden aplicar todas las reglas semánticas utilizadas con la opción de configuración max degree of parallelism cuando se utiliza la sugerencia de consulta MAXDOP. Para obtener más información, vea [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilitar > 8 TB para el grupo de búferes:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 habilita 128TB de espacio de direcciones virtuales para el uso del grupo de búferes. Esta mejora permite SQL Server grupo de búferes para escalar más allá de 8 TB en hardware moderno.
-   **Mejora de SOS_RWLock Spinlock:** SOS_RWLock es una primitiva de sincronización que se usa en varios lugares en la SQL Server base de código.  Como implica el nombre, el código puede tener varias propiedad compartida (lectores) o única (escritor). Esta mejora elimina la necesidad de Spinlock para SOS_RWLock y, en su lugar, usa técnicas sin bloqueos similares a OLTP en memoria. Con este cambio, muchos subprocesos pueden leer una estructura de datos protegida por SOS_RWLock en paralelo sin bloquearse entre sí y, por tanto, proporcionar una mayor escalabilidad. Antes de este cambio, la implementación de Spinlock permitía que solo un subproceso adquirira el SOS_RWLock cada vez, incluso para leer una estructura de datos.  [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementación nativa espacial:** La mejora significativa en el rendimiento de las consultas [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] espaciales se introduce en SP2 a través de la implementación nativa. Para obtener más información, vea el [artículo de Knowledge Base KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Mejoras de compatibilidad y diagnósticos
-   **Clonación de base de datos:** Clone Database es un nuevo comando DBCC que mejora la solución de problemas de las bases de datos de producción existentes mediante la clonación del esquema y los metadatos sin los datos. El clon se crea con el comando `DBCC clonedatabase('source_database_name', 'clone_database_name')`.  **Nota:** Las bases de datos clonadas no se deben usar en entornos de producción. Use el comando siguiente para determinar si una base de datos se ha generado a partir de `select DATABASEPROPERTYEX('clonedb', 'isClone')`una base de datos clonada:. El valor devuelto de **1** indica que la base de datos se creó a partir de clonedatabase, mientras que **0** indica que no es un clon.
-   **Compatibilidad con tempdb:**  Un nuevo mensaje de ErrorLog que indica el número de archivos de tempdb y el tamaño y el crecimiento automático de los archivos de datos de tempdb presentes al iniciar el servidor.
-   **Registro de inicialización instantánea de archivos de base de datos:** Un nuevo mensaje de ErrorLog que indica en el servidor statup, el estado de la inicialización instantánea de archivos de la base de datos (habilitada/deshabilitada).
-   **Nombres de módulo en CallStack:** La pila de llamadas de XEvent ahora incluye nombres de módulos + desplazamiento en lugar de direcciones absolutas.
-   **Nueva DMF para estadísticas incrementales:** Esta mejora resuelve la [conexión de comentarios (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar el seguimiento de las estadísticas incrementales en el nivel de partición. Se introduce una nueva DMF sys. DM _ _db_incremental_stats_properties para exponer la información por partición para las estadísticas incrementales.
-   **Comportamiento de DMV de uso de índices actualizado:** En esta mejora, se conectan los [comentarios (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de los clientes en los que la regeneración de un índice *no* borrará ninguna entrada de fila existente de sys. DM _ _db_index_usage_stats para ese índice. El comportamiento será ahora el mismo que en SQL 2008 y SQL Server 2016. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Correlación mejorada entre los diagnósticos XE y DMV:** Las direcciones de esta mejora conectan los [comentarios (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash y query_plan_hash se usan para identificar una consulta de forma única. DMV los define como varbinary (8), mientras que XEvent los define como UINT64. Puesto que SQL Server no tiene "BIGINT no firmado", la conversión no siempre funciona. Esta mejora presenta nuevas columnas de filtro o acción XEvent equivalentes a query_hash y query_plan_hash, salvo que se definen como INT64, lo que puede ayudar a correlacionar consultas entre XE y DMV.
-   **Compatibilidad con UTF-8 en BULK INSERT y BCP:** En esta mejora [, se conectan los comentarios (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) , donde ahora se habilita la compatibilidad con la exportación e importación de datos codificados en el juego de caracteres UTF-8 en Bulk Insert y BCP.
-   **Generación de perfiles de ejecución de consultas por operador ligera:** A la hora de solucionar problemas de rendimiento de las consultas, aunque SHOWPLAN proporciona gran cantidad de información sobre el plan de ejecución de consultas y el costo del operador en el plan, pero tiene información limitada sobre las estadísticas reales en tiempo de ejecución como (CPU, lecturas de e/s, tiempo transcurrido por subproceso). SQL 2014 SP2 presenta estas estadísticas adicionales en tiempo de ejecución por operador en el plan de presentación, así como un XEvent (query_thread_profile) para ayudar a solucionar problemas de rendimiento de las consultas. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Limpieza de Change Tracking:** Se introduce un nuevo `sp_flush_CT_internal_table_on_demand` procedimiento almacenado para limpiar las tablas internas de seguimiento de cambios a petición.
-   **Registro de tiempo de espera de concesión** de AlwaysOn Se ha agregado una nueva capacidad de registro para los mensajes de tiempo de espera de concesión para que se registren la hora actual y los tiempos de renovación esperados. También se ha introducido un nuevo mensaje en el ErrorLog de SQL con respecto a los tiempos de espera. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Nueva DMF para recuperar el búfer de entrada en SQL Server:** Ahora está disponible una nueva DMF para recuperar el búfer de entrada de una sesión o solicitud (sys.dm_exec_input_buffer). Es funcionalmente equivalente a DBCC INPUTBUFFER. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigación de la concesión de memoria sobreestimada y sobreestimada:** Se han agregado nuevas sugerencias de consulta para Resource Governor a través de MIN_GRANT_PERCENT y MAX_GRANT_PERCENT. Esto le permite aprovechar estas sugerencias mientras ejecuta las consultas mediante el límite de las concesiones de memoria para evitar la contención de la memoria. Para obtener más información, vea el [artículo de Knowledge Base KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **Mejor diagnóstico de uso/concesión de memoria:** Se ha agregado un nuevo evento extendido a la lista de funcionalidades de seguimiento de SQL Server (query_memory_grant_usage) para realizar el seguimiento de las concesiones de memoria solicitadas y concedidas. Esto proporciona mejores capacidades de seguimiento y análisis para solucionar problemas de ejecución de consultas relacionadas con concesiones de memoria. Para obtener más información, vea el [artículo de Knowledge Base KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Diagnóstico de ejecución de consultas para el desbordamiento de tempdb:** -las advertencias de hash y de ordenación ahora tienen columnas adicionales para realizar el seguimiento de las estadísticas de e/s físicas, la memoria usada y las filas afectadas. También se ha introducido un nuevo evento extendido hash_spill_details. Ahora puede realizar un seguimiento de la información más pormenorizada del hash y de las advertencias de ordenación ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Esta mejora también se expone ahora a través de los planes de consulta XML en forma de un nuevo atributo para el tipo complejo de SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Set Statistics on Now muestra ordenar las estadísticas de la tabla de trabajo. .
-   **Diagnósticos mejorados para los planes de ejecución de consultas que implican aplicación de predicado residual:** Ahora se mostrarán las filas reales leídas en los planes de ejecución de consultas para ayudar a mejorar la solución de problemas de rendimiento de las consultas. Esto debería negar la necesidad de capturar SET STATISTICs IO por separado. Ahora permite ver información relacionada con un predicado residual aplicación en un plan de consulta. Para obtener más información, vea el [artículo de Knowledge Base KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Información adicional  
 [Recursos de SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro de recursos de SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Sitio web de SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
