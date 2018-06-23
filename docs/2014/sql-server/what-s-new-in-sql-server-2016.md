---
title: ¿Qué&#39;s nuevos en SQL Server 2014 | Documentos de Microsoft
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- database-engine
- integration-services
- master-data-services
- replication
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 70
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9144eeb653649e36cfed3551e4ec465d403ffdcb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107338"
---
# <a name="what39s-new-in-sql-server-2014"></a>¿Qué&#39;s nuevos en SQL Server 2014
  En este tema se resume detallados vínculos a las nuevas características en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] y se resumen los paquetes de servicios para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**¿Pruébelo:** ![pequeño de máquina Virtual de Azure](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) tiene una cuenta de Azure?  A continuación, vaya **[aquí](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** para acelerar una máquina Virtual con SQL Server 2014 Service Pack 1 (SP1) instalado. 
  
-   [' S New &#40;motor de base de datos&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novedades de Analysis Services y Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [Novedades de la instalación de SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] no se ha presentado nuevas características importantes a lo siguiente:**  
  
-   [' S New &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [' S New &#40;replicación&#41;](../relational-databases/replication/what-s-new-replication.md)  
  
-   [' S New &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) no ha introducido nuevas características importantes.
-  [Información de la versión de SQL Server 2014 Service Pack 1 ](https://support.microsoft.com/en-us/kb/3058865).
-  [![Descargar Service Pack 1 para Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [descargar Service Pack 1 para Microsoft® SQL Server® 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [Información de la versión de SQL Server 2014 Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![Descargar Service Pack 2 para Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](http://go.microsoft.com/fwlink/?LinkID=821558) [descargar Service Pack 2 para Microsoft® SQL Server® 2014](http://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Descargar SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [Descargue el Feature Pack SQL Server 2014 SP2](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2) Incluye las siguientes mejoras:

### <a name="performance-and-scalability-improvements"></a>Mejoras de escalabilidad y rendimiento 
-   **La creación automática de particiones de NUMA de software:** con [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, NUMA de software automática se habilita cuando está activado 8079 de marca de seguimiento durante el inicio de la instancia. Cuando se habilita 8079 de marca de seguimiento durante el inicio, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 se interrogar el diseño de hardware y configurar automáticamente NUMA de software en los sistemas reporting 8 o más unidades de CPU por nodo NUMA. El comportamiento NUMA automática, suave es Threading (procesador HT/lógico) tenga en cuenta. La creación de particiones y la creación de nodos adicionales escala el procesamiento en segundo plano al aumentar el número de agentes de escucha, escalado y capacidades de red y cifrado. Se recomienda para la primera prueba la carga de trabajo de rendimiento con automática Soft NUMA antes de activar en producción. [Consulte el Blog para obtener más información](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Escala de objeto de memoria dinámica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 particiones dinámicamente según el número de nodos y los núcleos se escale en hardware moderno de objetos de memoria. El objetivo de promoción dinámico consiste en Dividir automáticamente un objeto de memoria seguro para la ejecución de subprocesos (CMEMTHREAD) si se convierte en un cuello de botella. Objetos de memoria con particiones no se pueden promocionar dinámicamente a dividirse por nodo (número de particiones es igual a nodos NUMA) y objetos con particiones por nodo pueden por más de memoria se promueve al dividirse por CPU (número de particiones es igual a CPU). [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Sugerencia MAXDOP para DBCC CHECK\* comandos:** direcciones de esta mejora [conectar comentarios (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Ahora puede ejecutar DBCC CHECKDB con la una configuración de MAXDOP distinto del valor de sp_configure. Si MAXDOP supera el valor configurado con Resource Governor, el motor de base de datos usa el valor MAXDOP de Resource Governor, descrito en ALTER WORKLOAD GROUP (Transact-SQL). Se pueden aplicar todas las reglas semánticas utilizadas con la opción de configuración max degree of parallelism cuando se utiliza la sugerencia de consulta MAXDOP. Para obtener más información, consulte [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilitar > 8TB para grupo de búferes:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 permite 128 TB de espacio de direcciones virtuales para el uso del grupo de búferes. Esta mejora permite el grupo de búferes de SQL Server para escalar más allá de 8TB en hardware moderno.
-   **SOS_RWLock spinlock para la mejora:** SOS_RWLock el es una primitiva de sincronización que se utiliza en varios lugares de la base de código de SQL Server.  Como su nombre indica, el código puede tener varios compartidos (lectores) o la propiedad de solo (writer). Esta mejora elimina la necesidad de bloqueo por subproceso para SOS_RWLock y en su lugar utiliza técnicas sin bloqueo similares a OLTP en memoria. Con este cambio, varios subprocesos pueden leer una estructura de datos protegida por SOS_RWLock en paralelo sin bloquear mutuamente y, por tanto, proporcionar una mayor escalabilidad. Antes de realizar este cambio, la implementación de bloqueo por bucle permite solo un subproceso adquirir el SOS_RWLock a la vez, incluso para leer una estructura de datos.  [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementación nativa espacial:** mejora significativa del rendimiento de las consultas espaciales se incorporó en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 a través de la implementación nativa. Para obtener más información, consulte el [el artículo de knowledge base KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Compatibilidad y mejoras de diagnósticos
-   **Clonación de base de datos:** base de datos del clon es un nuevo comando DBCC que mejora la solución de problemas de bases de datos de producción existentes mediante la clonación el esquema y los metadatos sin los datos. El clon se crea con el comando `DBCC clonedatabase(‘source_database_name’, ‘clone_database_name’)`.  **Nota:** bases de datos de clonación no deben usarse en entornos de producción. Utilice el siguiente comando de determinar si se ha generado una base de datos de una base de datos clonado: `select DATABASEPROPERTYEX('clonedb', 'isClone')`. El valor devuelto de **1** indica la base de datos se crea a partir de clonedatabase al **0** indica no es un clon.
-   **Compatibilidad de tempdb:** un nuevo mensaje de registro de errores que indica el número de archivos de tempdb y el tamaño/crecimiento automático de datos de tempdb archivos presente en el inicio del servidor.
-   **Registro de inicialización de archivos instantánea base de datos:** un nuevo mensaje de registro de errores que se indica en el inicio de servidor, el estado de inicialización instantánea de archivos de base de datos (habilitado/deshabilitado).
-   **Nombres de módulo en la pila de llamadas:** Xevent la pila de llamadas ahora incluye nombres de módulos + desplazamiento en lugar de direcciones absolutas.
-   **Nuevo DMF para estadísticas incrementales:** direcciones de esta mejora [conectar comentarios (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar el seguimiento de las estadísticas incrementales en el nivel de partición. Se introdujo un nuevo sys.dm_db_incremental_stats_properties DMF para exponer información por partición para las estadísticas incrementales.
-   **Comportamiento de DMV de uso de índice actualizado:** direcciones de esta mejora [conectar comentarios (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de clientes que volver a generar un índice le *no* borre cualquier entrada de fila existente de sys.dm_db _index_usage_stats para ese índice. Ahora, el comportamiento es el mismo que en SQL 2008 y SQL Server 2016. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Mejorar la correlación entre las DMV y diagnóstico XE:** direcciones de esta mejora [conectar comentarios (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash y query_plan_hash se usan para identificar de forma única una consulta. DMV los define como varbinary (8), mientras que XEvent los define como UINT64. Puesto que SQL server no tiene "unisigned bigint", conversión no siempre funcionará. Esta mejora presenta nuevas columnas de filtro o acción XEvent equivalentes a query_hash y query_plan_hash, salvo que se definen como INT64, lo que puede ayudar a correlacionar consultas entre XE y DMV.
-   **Compatibilidad con UTF-8 en BCP y BULK INSERT:** direcciones de esta mejora [comentarios (370419) connect](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) donde la compatibilidad con exportación e importación de datos codificados en el juego de caracteres UTF-8 está habilitada ahora en BCP y BULK INSERT.
-   **Generación de perfiles de ejecución consulta por cada operador ligera:** durante la solución de problemas de rendimiento de las consultas, aunque showplan proporciona mucha información en el plan de ejecución de consulta y el costo del operador en el plan ha de información limitada sobre real estadísticas de tiempo de ejecución como (CPU, lecturas de E/S, tiempo transcurrido por subproceso). Service Pack 2 de SQL 2014 presenta estas estadísticas adicionales en tiempo de ejecución por cada operador en el plan de presentación, así como un XEvent (query_thread_profile) para ayudar a solucionar problemas de rendimiento de consulta. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Limpieza de seguimiento de cambios:** un nuevo procedimiento almacenado `sp_flush_CT_internal_table_on_demand` se introduce en el seguimiento de las tablas internas a petición de cambios de limpieza.
-   **Registro de tiempo de espera de concesión de AlwaysON** agrega nueva funcionalidad de registro para los mensajes de tiempo de espera de concesión de modo que se registran la hora actual y los tiempos de renovación esperado. También se introdujo un nuevo mensaje en el registro de errores de SQL con respecto a los tiempos de espera. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Búfer en SQL Server de entrada de nuevo DMF para recuperar:** un nuevo DMF para recuperar el búfer de entrada para una sesión/solicitud (sys.dm_exec_input_buffer) ahora está disponible. Es funcionalmente equivalente a DBCC INPUTBUFFER. [Consulte el blog para obtener más información](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigación de concesión de memoria de subestimar y subestimados:** agrega nuevas sugerencias de consulta para el regulador de recursos a través de MIN_GRANT_PERCENT y MAX_GRANT_PERCENT. Esto le permite aprovechar estas sugerencias durante la ejecución de consultas si se restringe sus concesiones de memoria para evitar la contención de la memoria. Para obtener más información, consulte [el artículo de knowledge base KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **Una mejor diagnóstico grant/uso de memoria:** un nuevo evento extendido se agregó a la lista de las capacidades de seguimiento de SQL Server (query_memory_grant_usage) para realizar el seguimiento de concesiones de memoria solicitada y concedido. Esto proporciona mejores capacidades de análisis y seguimiento para solucionar problemas de ejecución de consultas relacionadas con concesiones de memoria. Para obtener más información, consulte [el artículo de knowledge base KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Diagnósticos de la ejecución de volcado de tempdb de consulta:**-Hash Warning y Sort Warnings ahora tienen columnas adicionales para realizar el seguimiento de las estadísticas E/S física, memoria utilizada y filas afectadas. También presentamos un nuevo evento extendido hash_spill_details. Ahora puede realizar un seguimiento de información más detallada para los hash y ordenar las advertencias ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Esta mejora ahora también se expone a través de los planes de consulta de XML en forma de un nuevo atributo al tipo complejo SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Activar las estadísticas ahora muestra ordenar las estadísticas de tabla de trabajo. .
-   **Diagnóstico de los planes de ejecución de consultas que implican la aplicación del predicado residual mejorado:** el número de filas real de lectura ahora se incluirán en los planes de ejecución de consulta para ayudar a mejorar la solución de problemas de rendimiento de consulta. Esto debe invalidar la necesidad para capturar SET STATISTICS IO por separado. Ahora Esto permite ver la información relacionada con una aplicación del predicado residual en un plan de consulta. Para obtener más información, consulte [el artículo de knowledge base KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Información adicional  
 [Recursos de SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](http://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro de recursos SQL Server 2014](http://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Sitio Web de SQLCat](http://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  