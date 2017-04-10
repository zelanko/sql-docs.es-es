---
title: "DMV para los servicios SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# DMV para los servicios SQL Server R

Este tema enumeran las vistas de catálogo del sistema y DMV que están relacionados con [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. 


Para obtener información sobre los eventos extendidos, vea [eventos extendidos para SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md).

> [!TIP]
> El equipo del producto ha proporcionado informes personalizados que puede utilizar para supervisar paquetes y las sesiones de R Services. Para obtener más información consulte [Monitor R Services con informes personalizados en Management Studio](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md).
> 

## <a name="system-configuration-and-system-resources"></a>Configuración del sistema y los recursos del sistema

Puede supervisar y analizar los recursos que usa scripts de R mediante el uso de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] vistas de catálogo del sistema y DMV.


**General**
+ [ Sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  Devuelve información de las conexiones de usuario y las sesiones del sistema. Puede identificar las sesiones de sistema examinando el *session_id* columna; los valores mayores que o igual a 51 son las conexiones de usuario y valores inferiores a 51 son procesos del sistema. 



+ [Sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  Devuelve una fila para cada contador de rendimiento del sistema que se va a utilizar el servidor.  Puede usar esta información para ver el número de secuencias de comandos se ejecutaron, se ejecutaron las secuencias de comandos con el modo de autenticación o el número de llamadas de R se genera en la instancia global.

  Este ejemplo obtiene solo los contadores relacionados con el script de R:

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  Esta DMV para scripts externos por instancia notifican los siguientes contadores:

  + **Total de ejecuciones**: número de procesos de R iniciadas por llamadas locales o remotas
  + **Ejecuciones en paralelo**: número de veces que una secuencia de comandos incluye el @parallel especificación y que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] fue capaz de generar y utilizar un plan de consulta en paralelo
  + **Ejecuciones de streaming**: número de veces que se ha invocado la característica de transmisión por secuencias. 
  + **Ejecuciones CC de SQL**: número de R scripts que ejecutan en la llamada se crearon instancias de forma remota y SQL Server se usa como el contexto de proceso. 
  + **Autenticación implícita. Los inicios de sesión**: número de veces que se realizó una llamada de bucle invertido ODBC mediante implícito autenticación; es decir, el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ejecuta la llamada en nombre del usuario que envía la solicitud de secuencia de comandos
  + **Total de tiempo de ejecución (ms)**: tiempo transcurrido entre la llamada y la finalización de la llamada.
  + **Errores de ejecución**: número de veces que informaron de errores de secuencias de comandos. Este número no incluye los errores de R.


+ [Sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  Esta DMV informa sobre una única fila para cada cuenta de trabajo que se está ejecutando un script externo. Tenga en cuenta que esta cuenta de trabajo es diferente de las credenciales de la persona que envía la secuencia de comandos. Si un usuario de Windows solo envía varias solicitudes de secuencia de comandos, se asignarían cuenta solo un trabajo para controlar todas las solicitudes de dicho usuario. Si otro usuario de Windows inicia sesión para ejecutar un script externo, la solicitud se administrará mediante una cuenta de trabajo independientes. 
  Esta DMV no devolvió ningún resultado si no hay secuencias de comandos se están ejecutando actualmente; por lo tanto, es más útil para supervisar las secuencias de comandos de ejecución prolongada. Devuelve estos valores:
  + **external_script_request_id**: un GUID, que también se utiliza como el nombre temporal del directorio de trabajo utilizado para almacenar las secuencias de comandos y los resultados intermedios.  
  + **idioma**: un valor como `R` que indica el lenguaje de script externo.
  + **degree_of_parallelism**: un entero que indica el número de paralelo procesos que se usaron. 
  + **external_user_name**: una cuenta de trabajo Launchpad, como SQLRUser01. 
  

+ [Sys.dm_external_script_execution_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  Se proporciona esta DMV para que supervisar interno (telemetría) realizar un seguimiento el número de llamadas de R se realiza en una instancia. Inicia el servicio de telemetría cuando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e incrementa un contador basadas en disco cada vez que se invoque una función de R específica.

  El contador se incrementa por cada llamada a una función. Por ejemplo, si se llama a `rxLinMod` y se ejecuta de manera simultánea, el contador aumenta en 1.
  
  Por lo general, los contadores de rendimiento solo son válidos siempre que el proceso que los genera esté activo. Por lo tanto, una consulta en una DMV no puede mostrar datos detallados para servicios que ya no están en ejecución. Por ejemplo, si se Launchpad crea varios trabajos paralelos de R y aún se ejecuta muy rápidamente y, a continuación, limpia el objeto de trabajo de Windows, es posible que una DMV no muestre ningún dato.
 
  Sin embargo, se mantienen los contadores que se realiza el seguimiento de esta DMV se está ejecutando y estado para dm_external_script _execution contador se conserva mediante el uso de escrituras en el disco, incluso si se cierra la instancia.
 
 Para obtener más información sobre los contadores de rendimiento del sistema utilizados por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).

**Vistas del regulador de recursos**

+ [Sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  Devuelve información acerca del estado actual del grupo de recursos de servidor, la configuración actual de los grupos de recursos de servidor y estadísticas del grupo de recursos de servidor.

  > [!IMPORTANT]
  > 
  > Debe modificar los grupos de recursos que se aplican a otros servicios de servidor antes de poder asignar recursos adicionales para R Services.


+ [Sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  Una nueva vista de catálogo que muestra los valores actuales de configuración de grupos de recursos externos.
  En las ediciones Enterprise, puede configurar grupos de recursos externos adicionales: por ejemplo, podría decidir controlar los recursos para trabajos de R que se ejecutan [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] por separado de los que se originan desde un cliente remoto. 

  > [!NOTE]
  > 
  > En Standard Edition, todos los trabajos de R se ejecutan en el mismo grupo de recursos externo predeterminado.

+ [Sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  Devuelve estadísticas de grupo de cargas de trabajo y la configuración actual del grupo de cargas de trabajo. Puede unirse esta vista con sys.dm_resource_governor_resource_pools para obtener el nombre del grupo de recursos de servidor.
  Para los scripts externos, se ha agregado una nueva columna que muestra el identificador del grupo externo asociado al grupo de cargas de trabajo. 


+ [Sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  Una nueva vista de catálogo del sistema que le permite ver los procesadores y los recursos que se ha establecido la afinidad para un grupo de recursos determinado.

  Devuelve una fila por programador en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] donde cada programador está asignado a un determinado procesador. Use esta vista para supervisar la condición de un programador o identificar tareas descontroladas.

  En la configuración predeterminada, los grupos de carga de trabajo se asignan automáticamente a los procesadores y por lo tanto, no hay ningún valor de afinidad para devolver.

  La programación de afinidad asigna el grupo de recursos para el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] programaciones identificadas por los identificadores especificados. Estos identificadores se asignan a los valores de la columna scheduler_id de sys.dm_os_schedulers (Transact-SQL).


> [!NOTE] 
> 
> Aunque la capacidad de configurar y personalizar los grupos de recursos solo está disponible en Enterprise y Developer ediciones, los grupos predeterminados, así como las DMV están disponibles en todas las ediciones. Por lo tanto, puede usar estas DMV en Standard Edition para determinar los límites de recursos para los trabajos de R. 

Para obtener información general acerca de la supervisión [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancias, vea [vistas de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) y [relacionados Dynamic Management Views de regulador de recursos](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).

## <a name="r-script-execution-and-monitoring"></a>Ejecución de scripts de R y supervisión

Scripts de R que se ejecutan en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] iniciados por el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interfaz. Sin embargo, Launchpad no es recurso rige o supervisado por separado, ya que se supone que un servicio seguro proporcionado por Microsoft que administra los recursos apropiadamente.

Los scripts de R individuales que se ejecutan en el servicio Launchpad se administran mediante el [objeto de trabajo de Windows](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). Un objeto de trabajo permite a los grupos de procesos que se van a administrarse como una unidad. Cada objeto de trabajo tiene una estructura jerárquica y controla los atributos de todos los procesos asociados con él. Las operaciones realizadas en un objeto de trabajo afecta a todos los procesos asociados con el objeto de trabajo. 

Por lo tanto, si es necesario finalizar un trabajo asociado a un objeto, tenga en cuenta que también puede finalizar todos los procesos relacionados. Si está ejecutando un script de R que se asigna a un objeto de trabajo de Windows y ese script ejecuta un trabajo relacionado de ODBC que debe terminar, también puede finalizar el proceso de script de R de elemento primario. 

Si inicia un script de R que utiliza el procesamiento en paralelo, un único objeto de trabajo de Windows administra todos los procesos secundarios paralelas.

Para determinar si un proceso se ejecuta en un trabajo, use la `IsProcessInJob` función.

## <a name="see-also"></a>Vea también
[Administración y supervisión](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

