---
title: "DMV para servicios de aprendizaje de máquina SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 49c9e45e32df10b4b2be5b7d47cfeb569e5bf152
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="dmvs-for-sql-server-machine-learning-services"></a>DMV para servicios de aprendizaje de máquina SQL Server

Este tema enumeran las vistas de catálogo del sistema y DMV que están relacionados con el aprendizaje automático en SQL Server.

Para obtener información sobre los eventos extendidos, vea [eventos extendidos para aprendizaje automático](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md).

> [!TIP]
> El equipo del producto ha proporcionado informes personalizados que puede utilizar para supervisar las sesiones de aprendizaje de máquina y la utilización del paquete. Para obtener más información, consulte [supervisar aprendizaje automático con informes personalizados en Management Studio](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="system-configuration-and-system-resources"></a>Configuración del sistema y los recursos del sistema

Puede supervisar y analizar los recursos que usa scripts externos mediante el uso de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] vistas de catálogo del sistema y DMV.

+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  Devuelve información de conexiones de usuario y sesiones del sistema. Puede identificar las sesiones del sistema examinando la columna *session_id*: los valores mayores o iguales que 51 son las conexiones de usuario y los valores inferiores a 51 son los procesos del sistema.

+ [sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  Devuelve una fila para cada contador de rendimiento del sistema usado por el servidor.  Se puede usar esta información para ver cuántos scripts se ejecutaron, cuáles se ejecutaron mediante un modo de autenticación concreto o cuántas llamadas a R se emitieron en la instancia global.

  Este ejemplo obtiene solo los contadores relacionados con el script de R:

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%External Scripts%'
  ```

  Esta DMV informa de los contadores siguientes de scripts externos por instancia:

  + **Total de ejecuciones**: número de procesos externos iniciados por llamadas locales o remotas
  + **Ejecuciones en paralelo**: número de veces que una secuencia de comandos incluye la  _@parallel_  especificación y que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] fue capaz de generar y utilizar un plan de consulta en paralelo
  + **Ejecuciones de streaming**: número de veces que se ha invocado la característica de transmisión por secuencias
  + **Ejecuciones CC de SQL**: número de externos secuencias de comandos de ejecución donde la llamada se crearon instancias de forma remota y SQL Server se utiliza como el contexto de proceso.
  + **Inicios de sesión de autenticación implícita**: número de veces que se realizó una llamada de bucle invertido ODBC mediante autenticación implícita (es decir, el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ejecutó la llamada en nombre del usuario que envío la solicitud de script)
  + **Total de tiempo de ejecución (ms)**: tiempo transcurrido entre la llamada y la realización de llamadas
  + **Errores de ejecución**: número de veces que los scripts informaron de errores. Este recuento no incluye errores de R.


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  Esta DMV informa sobre una sola fila por cada cuenta de trabajo que está ejecutando actualmente un script externo. Tenga en cuenta que esta cuenta de trabajo es diferente de las credenciales de la persona que envía el script. Si un único usuario de Windows envía varias solicitudes de script, solo se asignaría una cuenta de trabajo para controlar todas las solicitudes de ese usuario. Si otro usuario de Windows inicia sesión para ejecutar un script externo, la solicitud se controlaría desde una cuenta de trabajo independiente.

  Esta DMV no devolverá ningún resultado si no hay scripts actualmente en ejecución. Por tanto, resulta más útil para la supervisión de scripts de ejecución prolongada. Devuelve estos valores:

  + **external_script_request_id**: un GUID, que también se utiliza como el nombre temporal del directorio de trabajo utilizado para almacenar resultados intermedios y secuencias de comandos
  + **idioma**: un valor como `R` que indica el idioma de la secuencia de comandos externo
  + **degree_of_parallelism**: un entero que indica el número de paralelo procesos que se utilizaron
  + **external_user_name**: Launchpad de un trabajo de la cuenta, como **SQLRUser01**

+ [sys.dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  Se proporciona esta DMV para que supervisar interno (telemetría) realizar un seguimiento el número de llamadas de script externo se realiza en una instancia. Inicia el servicio de telemetría cuando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e incrementa un contador basadas en disco cada vez que se llama una función de aprendizaje de máquina específica.

  El contador se incrementa por cada llamada a una función de seguimiento específica. Por ejemplo, si se llama a `rxLinMod` y se ejecuta de manera simultánea, el contador aumenta en 1.
  
  Por lo general, los contadores de rendimiento solo son válidos siempre que el proceso que los genera esté activo. Por lo tanto, una consulta en una DMV no puede mostrar datos detallados para servicios que ya no están en ejecución. Por ejemplo, si el Launchpad crea varios trabajos paralelos de R pero se ejecutan muy rápidamente y, después, el objeto de trabajo de Windows los limpia, es posible que una DMV no muestre ningún dato.
 
  Pero los contadores de los que esta DMV realiza un seguimiento siguen en ejecución y se mantiene el estado del contador dm_external_script _execution mediante escrituras en disco, incluso si la instancia está apagada.
 
 Para más información sobre los contadores de rendimiento del sistema usados por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], vea [Use SQL Server Objects](../../relational-databases/performance-monitor/use-sql-server-objects.md) (Usar objetos de SQL Server).

## <a name="resource-governor-views"></a>Vistas del regulador de recursos

En las ediciones que admiten el regulador de recursos, crear grupos de recursos externos para las cargas de trabajo de R o Python puede ser en efectivo podrán realizar un seguimiento y administrar los recursos.

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  Devuelve información acerca del estado actual del grupo de recursos de servidor, la configuración actual de los grupos de recursos de servidor y estadísticas del grupo de recursos de servidor.

  > [!IMPORTANT]
  > 
  > Se deben modificar los grupos de recursos que se aplican a otros servicios de servidor antes de poder asignar recursos adicionales a R Services.

+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  Una nueva vista de catálogo que muestra los valores de configuración actuales para grupos de recursos externos.
  En Enterprise Edition, se pueden configurar grupos de recursos externos adicionales: por ejemplo, podría decidir controlar los recursos para trabajos de R que se ejecutan en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] por separado de los que proceden de un cliente remoto.

  > [!NOTE]
  > 
  > En Standard Edition, todos los trabajos de script externo se ejecutan en el mismo grupo de recursos externo predeterminado.

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  Devuelve las estadísticas del grupo de cargas de trabajo y la configuración actual del grupo de cargas de trabajo. Esta vista se puede combinar con `sys.dm_resource_governor_resource_pools` para obtener el nombre del grupo de recursos de servidor.
  Para los scripts externos, se ha agregado una nueva columna que muestra el identificador del grupo externo asociado con el grupo de cargas de trabajo.

+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  Una nueva vista de catálogo del sistema que permite ver los procesadores y los recursos afines a un grupo de recursos determinado.

  Devuelve una fila por programador en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] donde cada programador está asignado a un determinado procesador. Use esta vista para supervisar la condición de un programador o identificar tareas descontroladas.

  En la configuración predeterminada, los grupos de cargas de trabajo se asignan automáticamente a los procesadores y, por tanto, no hay ningún valor de afinidad para devolver.

  La programación de afinidad asigna el grupo de recursos a las programaciones de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] indicadas por los identificadores especificados. Estos identificadores se asignan a los valores de la `scheduler_id` columna en `sys.dm_os_schedulers`.


> [!NOTE] 
> 
> Aunque la capacidad de configurar y personalizar los grupos de recursos solo está disponible en las ediciones Enterprise y Developer, los grupos predeterminados, así como las DMV, están disponibles en todas las ediciones. Por lo tanto, puede usar estas DMV en Standard Edition para determinar los límites de recursos para los trabajos de script externo.

Para obtener información general sobre la supervisión de instancias de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], vea [Catalog Views](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) (Vistas de catálogo) y [Resource Governor Related Dynamic Management Views](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md) (Vistas de administración dinámica relacionadas con el regulador de recursos).

## <a name="monitoring-script-execution"></a>Supervisión de la ejecución del script

Scripts de R y Python que se ejecutan en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] iniciados por el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interfaz. Pero Launchpad no es un recurso controlado ni supervisado por separado, dado que se supone que es un servicio seguro proporcionado por Microsoft que administra los recursos adecuadamente.

Secuencias de comandos individuales que se ejecutan en el servicio Launchpad se administran mediante el [objeto de trabajo de Windows](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). Un objeto de trabajo permite administrar grupos de procesos como una unidad. Cada objeto de trabajo es jerárquico y controla los atributos de todos los procesos asociados con él. Las operaciones realizadas en un objeto de trabajo afectan a todos los procesos asociados con el objeto de trabajo.

Por tanto, si es necesario finalizar un trabajo asociado a un objeto, tenga en cuenta que todos los procesos relacionados también se finalizarán. Si se está ejecutando un script de R asignado a un objeto de trabajo de Windows y ese script ejecuta un trabajo de ODBC relacionado que debe finalizarse, también se finalizará el proceso de script de R primario.

Si inicia un script externo que usa el procesamiento en paralelo, un único objeto de trabajo de Windows administra todos los procesos secundarios paralelas.

Para determinar si un proceso se ejecuta en un trabajo, use la función `IsProcessInJob`.

## <a name="next-steps"></a>Pasos siguientes

[Administración y supervisión de soluciones de aprendizaje automático](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
