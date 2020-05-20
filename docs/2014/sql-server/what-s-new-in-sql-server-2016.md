---
title: Novedades de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dfee15f0f8b657074bab4104edb4833bd8e2f05f
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001068"
---
# <a name="whats-new-in-sql-server-2014"></a>Novedades de SQL Server 2014 +

En este tema se resumen los vínculos detallados a las nuevas características de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] y se resumen los paquetes de servicios para[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Pruébelo:** ![ ¿La máquina virtual de Azure pequeña ](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) tiene una cuenta de Azure?  Vaya a https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2 para poner en marcha una máquina virtual con SQL Server 2014 Service Pack 1 (SP1) ya instalado.

> [!TIP]
> [Haga clic aquí](../2014-toc/index.yml) para ver la página de documentación principal de SQL Server 2014.

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>Artículos de novedades

-   [Novedades &#40;Motor de base de datos&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novedades de Analysis Services y Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [Novedades de la instalación de SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]no ha presentado nuevas características importantes para las siguientes características:**  
  
-   [Novedades &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Novedades &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="sssql14-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) no introdujo nuevas características importantes.
-  [SQL Server 2014 información de la versión del Service Pack 1](https://support.microsoft.com/kb/3058865).
-  [ ![ Descargue el Service Pack 1 para Microsoft SQL Server 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [Descargue el service pack 1 para Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=46694).


## <a name="sssql14-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server 2014 información de la versión del Service Pack 2](https://support.microsoft.com/kb/3171021).
-  [ ![ Descargue el Service Pack 2 de Microsoft SQL Server 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [descargar el service pack 2 para Microsoft SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [ ![ Descargar SQL Server Feature pack de 2014 SP2](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164) [Descargue el feature Pack de SQL Server 2014 SP2](https://www.microsoft.com/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Incluye las siguientes mejoras:

### <a name="performance-and-scalability-improvements"></a>Mejoras en el rendimiento y la escalabilidad 
-   Creación **automática de particiones de Numa de software:** Con [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, se habilita la Numa automática automática cuando la marca de seguimiento 8079 está activada durante el inicio de la instancia. Cuando la marca de seguimiento 8079 está habilitada durante el inicio, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 interrogará el diseño de hardware y configurará automáticamente Soft Numa en los sistemas que notifican 8 o más CPU por nodo Numa. El comportamiento de NUMA automático y automático es el que reconoce el hiperproceso (procesador HT/lógico). La creación de particiones y la creación de nodos adicionales escala el procesamiento en segundo plano al aumentar el número de agentes de escucha, escalado y capacidades de red y cifrado. Se recomienda probar primero la carga de trabajo de rendimiento con NUMA de software automático antes de ajustarla en producción. [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Escalado de objetos de memoria dinámica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 divide dinámicamente los objetos de memoria en función del número de nodos y núcleos para escalar en el hardware moderno. El objetivo de la promoción dinámica es particionar automáticamente un objeto de memoria seguro para subprocesos (CMEMTHREAD) si se convierte en un cuello de botella. Los objetos de memoria sin particiones se pueden particionar dinámicamente por nodo (el número de particiones es igual al número de nodos NUMA). Los objetos de memoria particionados por nodo se pueden dividir en particiones por CPU (el número de particiones es igual al número de CPU). [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Sugerencia MAXDOP para los \* comandos DBCC check:** esta mejora de direcciones [conecta los comentarios (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Ahora puede ejecutar DBCC CHECKDB con una configuración MAXDOP distinta de la sp_configure valor. Si MAXDOP supera el valor configurado con Resource Governor, el motor de base de datos usa el valor MAXDOP de Resource Governor, descrito en ALTER WORKLOAD GROUP (Transact-SQL). Se pueden aplicar todas las reglas semánticas utilizadas con la opción de configuración max degree of parallelism cuando se utiliza la sugerencia de consulta MAXDOP. Para obtener más información, vea [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilite >8 TB para el grupo de búferes:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 habilita 128 TB de espacio de direcciones virtuales para el uso del grupo de búferes. Esta mejora permite SQL Server grupo de búferes para escalar más allá de 8 TB en hardware moderno.
-   **SOS_RWLock mejora de Spinlock:** El SOS_RWLock es una primitiva de sincronización que se usa en varios lugares de la base de código de SQL Server.  Como implica el nombre, el código puede tener varias propiedad compartida (lectores) o única (escritor). Esta mejora elimina la necesidad de Spinlock por SOS_RWLock y, en su lugar, usa técnicas sin bloqueos similares a OLTP en memoria. Con este cambio, muchos subprocesos pueden leer una estructura de datos protegida por SOS_RWLock en paralelo, sin bloquearse entre sí. Esta paralelización proporciona una mayor escalabilidad. Antes de este cambio, la implementación de Spinlock permitía que solo un subproceso adquirira el SOS_RWLock a la vez, incluso para leer una estructura de datos. [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementación nativa espacial:** La mejora significativa en el rendimiento de las consultas espaciales se introduce en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 a través de la implementación nativa. Para obtener más información, vea el [artículo de Knowledge Base KB3107399](https://support.microsoft.com/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Mejoras de compatibilidad y diagnósticos
-   **Clonación de base de datos:** Clone Database es un nuevo comando DBCC que mejora la solución de problemas de las bases de datos de producción existentes mediante la clonación del esquema y los metadatos sin los datos. El clon se crea con el comando `DBCC clonedatabase('source_database_name', 'clone_database_name')` .  **Nota:** Las bases de datos clonadas no deben usarse en entornos de producción. Use el comando siguiente para determinar si una base de datos se ha generado a partir de una base de datos clonada: `select DATABASEPROPERTYEX('clonedb', 'isClone')` . El valor devuelto de **1** indica que la base de datos se creó a partir de clonedatabase, mientras que **0** indica que no es un clon.
-   **Compatibilidad con tempdb:**  Un nuevo mensaje de registro de errores que indica en el inicio tanto el número de archivos de tempdb como el tamaño y el crecimiento automático de los archivos de datos de tempdb.
-   **Registro de inicialización instantánea de archivos de base de datos:** Un nuevo mensaje de registro de errores que indica en el inicio del servidor, el estado de la inicialización instantánea de archivos de base de datos (habilitada/deshabilitada).
-   **Nombres de módulo en CallStack:** La pila de llamadas de eventos extendidos (XEvent) ahora incluye nombres de módulos más desplazamiento, en lugar de direcciones absolutas.
-   **Nueva DMF para estadísticas incrementales:** Esta mejora resuelve la [conexión de comentarios (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar el seguimiento de las estadísticas incrementales en el nivel de partición. Se introduce una nueva DMF sys. dm_db_incremental_stats_properties para exponer la información por partición para las estadísticas incrementales.
-   **Comportamiento de DMV de uso de índices actualizado:** Esta mejora resuelve la [conexión de comentarios (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de los clientes en los que la regeneración de un índice *no* borrará ninguna entrada de fila existente de sys. dm_db_index_usage_stats para ese índice. El comportamiento será ahora el mismo que en SQL 2008 y SQL Server 2016. [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Correlación mejorada entre los diagnósticos XE y DMV:** Las direcciones de esta mejora [conectan los comentarios (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). `Query_hash`y `query_plan_hash` se usan para identificar una consulta de forma única. DMV los define como varbinary (8), mientras que XEvent los define como UINT64. Dado que SQL Server no tiene "BIGINT sin signo", la conversión no siempre funciona. Esta mejora presenta nuevas columnas de acción y filtro de XEvent. Las columnas son equivalentes a `query_hash` y `query_plan_hash` , salvo que se definen como INT64. La definición INT64 ayuda a correlacionar las consultas entre XE y DMV.
-   **Compatibilidad con UTF-8 en Bulk Insert y BCP:** Las direcciones de esta mejora [conectan los comentarios (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001). BULK INSERT y BCP ahora pueden exportar o importar datos codificados en el juego de caracteres UTF-8.
-   **Generación de perfiles ligera de ejecución de consultas por operador:** SHOWPLAN proporciona información sobre el costo de cada operador en el plan. Sin embargo, las estadísticas de tiempo de ejecución reales están limitadas a elementos como la CPU, las lecturas de e/s y el tiempo transcurrido por subproceso. SQL Server 2014 SP2 presenta estas estadísticas adicionales en tiempo de ejecución por operador en el plan de presentación. R2 también introduce un XEvent denominado `query_thread_profile` para ayudar a solucionar problemas de rendimiento de las consultas. [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Limpieza de Change Tracking:** Se introduce un nuevo procedimiento almacenado `sp_flush_CT_internal_table_on_demand` para limpiar las tablas internas de seguimiento de cambios a petición.
-   **Registro de tiempo de espera de concesión de AlwaysOn** Se ha agregado una nueva capacidad de registro para los mensajes de tiempo de espera de concesión para que se registren la hora actual y los tiempos de renovación esperados. También se ha introducido un nuevo mensaje en el registro de errores de SQL con respecto a los tiempos de espera. [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Nueva DMF para recuperar el búfer de entrada en SQL Server:** Ahora hay disponible una nueva DMF para recuperar el búfer de entrada de una sesión/solicitud (sys. dm_exec_input_buffer). Esta DMF es funcionalmente equivalente a DBCC INPUTBUFFER. [Para obtener más información, consulte el blog](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigación de la concesión de memoria sobreestimada y sobreestimada:** Se han agregado nuevas sugerencias de consulta para Resource Governor a través de MIN_GRANT_PERCENT y MAX_GRANT_PERCENT. Esta nueva consulta permite aprovechar estas sugerencias mientras se ejecutan las consultas, mediante el límite de las concesiones de memoria para evitar la contención de la memoria. Para obtener más información, vea el [artículo de Knowledge Base KB310740](https://support.microsoft.com/kb/3107401).
-   **Mejor concesión de memoria y diagnóstico de uso:** Se ha agregado un nuevo evento extendido denominado `query_memory_grant_usage` a la lista de funcionalidades de seguimiento de SQL Server. Este evento realiza un seguimiento de las concesiones de memoria solicitadas y concedidas. Este evento proporciona mejores capacidades de seguimiento y análisis para solucionar problemas de ejecución de consultas relacionadas con concesiones de memoria. Para obtener más información, vea el [artículo de Knowledge Base KB3107173](https://support.microsoft.com/kb/3107173).
-   **Diagnósticos de ejecución de consultas para el desbordamiento de tempdb:**-las advertencias de hash y de ordenación ahora tienen columnas adicionales para realizar el seguimiento de las estadísticas de e/s física, la memoria usada y las filas afectadas. También se ha incorporado un nuevo hash_spill_details Extended Event. Ahora puede realizar un seguimiento de la información más pormenorizada del hash y de las advertencias de ordenación ([KB3107172](https://support.microsoft.com/kb/3107172)). Esta mejora también se expone ahora a través de los planes de consulta XML en forma de un nuevo atributo para el tipo complejo de SpillToTempDbType ([KB3107400](https://support.microsoft.com/kb/3107400)). Set Statistics `ON` Now muestra ordenar las estadísticas de la tabla de trabajo.
-   **Diagnósticos mejorados para los planes de ejecución de consultas que implican aplicación de predicado residual:** Ahora se muestran las filas reales leídas en los planes de ejecución de consultas para ayudar a mejorar la solución de problemas de rendimiento de las consultas. Estas filas niegan la necesidad de capturar SET STATISTICs IO por separado. Estas filas también permiten ver información relacionada con la desactivación de un predicado residual en un plan de consulta. Para obtener más información, vea el [artículo de Knowledge Base KB3107397](https://support.microsoft.com/kb/3107397).


## <a name="additional-information"></a>Información adicional  
 [Recursos de SQL Server 2014](../2014-toc/index.yml)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro de recursos de SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Sitio web de SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
