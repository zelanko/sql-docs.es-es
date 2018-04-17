---
title: Supervisar el rendimiento de los grupos de disponibilidad Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dfd2b639-8fd4-4cb9-b134-768a3898f9e6
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 0d41627a8c08e2fd06a9d5fdb391f5e626599233
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="monitor-performance-for-always-on-availability-groups"></a>Supervisar el rendimiento de los grupos de disponibilidad Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El rendimiento de los grupos de disponibilidad Always On es vital para mantener el contrato de nivel de servicio (SLA) de las bases de datos de críticas. La comprensión de cómo envían los registros los grupos de disponibilidad a las réplicas secundarias puede ayudar a estimar el objetivo de tiempo de recuperación (RTO) y el objetivo de punto de recuperación (RPO) de la implementación de disponibilidad y a identificar cuellos de botella en grupos de disponibilidad o réplicas con un mal rendimiento. En este artículo se explica el proceso de sincronización, se muestra cómo calcular algunas de las métricas clave y se proporcionan vínculos a algunos de los escenarios de solución de problemas de rendimiento comunes.  
  
 Se tratan los siguientes temas:  
  
-   [Proceso de sincronización de datos](#BKMK_DATA_SYNC_PROCESS)  
  
-   [Puertas de control de flujo](#BKMK_FLOW_CONTROL_GATES)  
  
-   [Estimación del tiempo de conmutación por error (RTO)](#BKMK_RTO)  
  
-   [Estimación de la posible pérdida de datos (RPO)](#BKMK_RPO)  
  
-   [Supervisión de RTO y RPO](#BKMK_Monitoring_for_RTO_and_RPO)  
  
-   [Escenarios de solución de problemas de rendimiento](#BKMK_SCENARIOS)  
  
-   [Eventos extendidos de utilidad](#BKMK_XEVENTS)  
  
##  <a name="BKMK_DATA_SYNC_PROCESS"></a> Proceso de sincronización de datos  
 Para estimar el tiempo necesario para una sincronización completa e identificar el cuello de botella, debe comprender el proceso de sincronización. Un cuello de botella de rendimiento puede estar en cualquier fase del proceso; su detección puede ayudar a profundizar en los problemas subyacentes. En la ilustración y la tabla siguientes se muestra el proceso de sincronización de datos:  
  
 ![Sincronización de datos de grupo de disponibilidad](media/always-onag-datasynchronization.gif "Sincronización de datos de grupo de disponibilidad")  
  
|||||  
|-|-|-|-|  
|**Secuencia**|**Descripción del paso**|**Comentarios**|**Métricas de utilidad**|  
|1|Generación de registro|Los datos del registro se vacían en el disco. Este registro se debe replicar en las réplicas secundarias. Las entradas del registro entran en la cola de envío.|[SQL Server: Base de datos > Bytes de registro vaciados/s](~/relational-databases/performance-monitor/sql-server-databases-object.md)|  
|2|Capturar|Los registros de cada base de datos se capturan y se envían a la cola de asociado correspondiente (uno por par de réplica de base de datos). Este proceso de captura se ejecuta de forma continua siempre que la réplica de disponibilidad esté conectada y no se suspenda el movimiento de datos por algún motivo; el par de réplica de base de datos se muestra como Sincronizando o Sincronizado. Si el proceso de captura no es capaz de examinar y poner en cola los mensajes con la suficiente rapidez, la cola de envío de registros se acumula.|[SQL Server: Réplica de disponibilidad > Bytes enviados a la réplica\s](~/relational-databases/performance-monitor/sql-server-availability-replica.md), que es una agregación de la suma de todos los mensajes de la base de datos en cola para esa réplica de disponibilidad.<br /><br /> [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) y [log_bytes_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB/s) en la réplica principal.|  
|3|Send|Los mensajes de cada cola de réplica de base de datos se quitan de la cola y se envían a través de la conexión a la réplica secundaria correspondiente.|[SQL Server: Réplica de disponibilidad > Bytes enviados al transporte\s](~/relational-databases/performance-monitor/sql-server-availability-replica.md) y [SQL Server: Réplica de disponibilidad > Tiempo de confirmación del mensaje](~/relational-databases/performance-monitor/sql-server-availability-replica.md) (ms)|  
|4|Recepción y almacenamiento en caché|Cada réplica secundaria recibe y almacena en caché el mensaje.|Contador de rendimiento [SQL Server: Réplica de disponibilidad > Bytes de registro recibidos/s](~/relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|5|Protección|El registro se vacía en la réplica secundaria para su protección. Tras el vaciado del registro, se envía una confirmación a la réplica principal.<br /><br /> Una vez protegido el registro, se evita la pérdida de datos.|Contador de rendimiento [SQL Server: Base de datos > Bytes de registro vaciados/s](~/relational-databases/performance-monitor/sql-server-databases-object.md)<br /><br /> Tipo de espera [HADR_LOGCAPTURE_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|6|Rehacer|Las páginas vaciadas se ponen al día en la réplica secundaria. Las páginas se mantienen en la cola de puesta al día mientras esperan.|[SQL Server: Réplica de base de datos > Bytes puestos al día/s](~/relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) y [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).<br /><br /> Tipo de espera [REDO_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
  
##  <a name="BKMK_FLOW_CONTROL_GATES"></a> Puertas de control de flujo  
 Los grupos de disponibilidad se diseñan con puertas de control de flujo en la réplica principal para evitar un uso excesivo de recursos, por ejemplo de red y memoria, en todas las réplicas de disponibilidad. Estas puertas de control de flujo no afectan al estado de sincronización de las réplicas de disponibilidad, pero sí pueden hacerlo al rendimiento general de las bases de datos de disponibilidad, incluido el RPO.  
  
 Una vez capturados los registros en la réplica principal, están sujetos a dos niveles de control de flujo, como se muestra en la tabla siguiente.  
  
|||||  
|-|-|-|-|  
|**Level**|**Número de puertas**|**Número de mensajes**|**Métricas de utilidad**|  
|Transporte|1 por réplica de disponibilidad|8192|Evento extendido **database_transport_flow_control_action**|  
|Base de datos|1 por base de datos de disponibilidad|11200 (x64)<br /><br /> 1600 (x86)|[DBMIRROR_SEND](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)<br /><br /> Evento extendido **hadron_database_flow_control_action**|  
  
 Una vez que se alcanza el umbral de mensajes de cualquier puerta, los mensajes de registro ya no se envían a una réplica determinada ni para una base de datos concreta. Los mensajes pueden enviarse una vez que se reciben los mensajes de confirmación de los mensajes enviados a fin de reducir el número de mensajes enviados por debajo del umbral.  
  
 Además de las puertas de control de flujo, hay otro factor que puede evitar que los mensajes de registro se envíen. La sincronización de réplicas garantiza que los mensajes se envíen y se apliquen en el orden de los números de secuencia de registro (LSN). Antes de enviar un mensaje de registro, también se compara su LSN con el LSN confirmado más bajo para asegurarse de que es menor que uno de los umbrales (según el tipo de mensaje). Si la diferencia entre los dos LSN es mayor que el umbral, los mensajes no se envían. Una vez que la diferencia vuelve a estar por debajo del umbral, se envían los mensajes.  
  
 Dos útiles contadores de rendimiento, [SQL Server: Réplica de disponibilidad > Control de flujo/s](~/relational-databases/performance-monitor/sql-server-availability-replica.md) y [SQL Server: Réplica de disponibilidad > Tiempo de control de flujo (ms/s)](~/relational-databases/performance-monitor/sql-server-availability-replica.md), muestran, durante el último segundo, cuántas veces se ha activado el control de flujo y cuánto tiempo se ha esperado en el control de flujo. Un mayor tiempo de espera en el control de flujo se traduce en un RPO superior. Para obtener más información sobre los tipos de problemas que pueden dar lugar a un tiempo de espera elevado en el control de flujo, vea [Solución de problemas: el grupo de disponibilidad superó el RPO](troubleshoot-availability-group-exceeded-rpo.md).  
  
##  <a name="BKMK_RTO"></a> Estimación del tiempo de conmutación por error (RTO)  
 El RTO del SLA depende del tiempo de conmutación por error de la implementación de Always On en un momento dado, que se puede expresar en la siguiente fórmula:  
  
 ![Cálculo de RTO de grupos de disponibilidad](media/always-on-rto.gif "Cálculo de RTO de grupos de disponibilidad")  
  
> [!IMPORTANT]  
>  Si un grupo de disponibilidad contiene más de una base de datos de disponibilidad, aquella con el valor Tfailover más alto se convierte en el valor límite para el cumplimiento del RTO.  
  
 El tiempo de detección de errores, Tdetection, es el tiempo que tarda el sistema en detectar el error. Este tiempo depende de la configuración del clúster y no de las réplicas de disponibilidad individuales. Según la condición de conmutación automática por error configurada, una conmutación por error se puede desencadenar como una respuesta inmediata a un error interno de SQL Server crítico, como un bloqueo por subproceso huérfano. En este caso, la detección puede ser tan rápida como tarda en enviarse el informe de error [sp_server_diagnostics &#40;Transact-SQL&#41; ](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) al clúster WSFC (el intervalo predeterminado es 1/3 del tiempo de espera de comprobación de estado). Una conmutación por error también se puede desencadenar debido a un tiempo de espera, por ejemplo, cuando el tiempo de espera de comprobación de estado del clúster ha expirado (30 segundos de forma predeterminada) o la concesión entre la DLL del recurso y la instancia de SQL Server ha expirado (20 segundos de forma predeterminada). En este caso, el tiempo de detección es tan largo como el intervalo de tiempo de espera. Para obtener más información, vea [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](https://msdn.microsoft.com/library/hh710061(SQL.120).aspx).  
  
 Lo único que la réplica secundaria tiene que hacer para prepararse para una conmutación por error es que la fase de puesta al día alcance el final del registro. El tiempo de fase de puesta al día, Tredo, se calcula mediante la siguiente fórmula:  
  
 ![Cálculo de tiempo de fase de puesta al día de grupos de disponibilidad](media/always-on-redo.gif "Cálculo de tiempo de fase de puesta al día de grupos de disponibilidad")  
  
 donde *redo_queue* es el valor de [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) y *redo_rate* es el valor de [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).  
  
 El tiempo de sobrecarga de conmutación por error, Toverhead, incluye el tiempo necesario para conmutar por error el clúster WSFC y poner en línea las bases de datos. Este tiempo suele ser breve y constante.  
  
##  <a name="BKMK_RPO"></a> Estimación de la posible pérdida de datos (RPO)  
 El RPO del SLA depende de la posible pérdida de datos de la implementación de Always On en un momento dado. Esta posible pérdida de datos se puede expresar en la siguiente fórmula:  
  
 ![Cálculo de RPO de grupos de disponibilidad](media/always-on-rpo.gif "Cálculo de RPO de grupos de disponibilidad")  
  
 donde *log_send_queue* es el valor de [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) y *log generation rate* es el valor de [SQL Server: Base de datos > Bytes de registro vaciados/s](~/relational-databases/performance-monitor/sql-server-databases-object.md).  
  
> [!WARNING]  
>  Si un grupo de disponibilidad contiene más de una base de datos de disponibilidad, aquella con el valor Tdata_loss más alto se convierte en el valor límite para el cumplimiento del RPO.  
  
 La cola de envío de registro representa todos los datos que se pueden perder a causa de un error irrecuperable. A primera vista, es curioso que se use la velocidad de generación de registro en lugar de la velocidad de envío de registro (vea [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)). Pero recuerde que el uso de la velocidad de envío de registro solo proporciona el tiempo de sincronización, mientras que el RPO mide la pérdida de datos en función de la velocidad de generación, no la rapidez con que se sincroniza.  
  
 Una manera más sencilla de estimar Tdata_loss es usar [last_commit_time](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md). La DMV de la réplica principal notifica este valor para todas las réplicas. Puede calcular la diferencia entre el valor de la réplica principal y el de la réplica secundaria para estimar la velocidad con que el registro de la réplica secundaria alcanza a la réplica principal. Como se ha mencionado anteriormente, este cálculo no indica la posible pérdida de datos en función de la velocidad con que se genera el registro, aunque debería ser una buena aproximación.  
  
##  <a name="BKMK_Monitoring_for_RTO_and_RPO"></a> Supervisión de RTO y RPO  
 En esta sección se muestra cómo supervisar las métricas RTO y RPO de los grupos de disponibilidad. Esta demostración es similar al tutorial de GUI de [The Always On health model, part 2: Extending the health model](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx) (Parte 2 del modelo de estado de Always On: extensión del modelo de estado).  
  
 Se proporcionan elementos de los cálculos de tiempo de conmutación por error y de posible pérdida de datos de [Estimación del tiempo de conmutación por error (RTO)](#BKMK_RTO) y [Estimación de la posible pérdida de datos (RPO)](#BKMK_RPO) como métricas de rendimiento de la faceta de administración de directivas **Estado de réplica de base de datos** (vea [Ver las facetas de administración basada en directivas en un objeto de SQL Server](~/relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)). Puede supervisar estas dos métricas según una programación y recibir alertas cuando superen el RTO y el RPO, respectivamente.  
  
 Los scripts que se muestran crean dos directivas del sistema que se ejecutan según sus respectivas programaciones, con las siguientes características:  
  
-   Una directiva de RTO que da error cuando el tiempo estimado de conmutación por error supera los 10 minutos, evaluado cada 5 minutos  
  
-   Una directiva de RPO que da error cuando la pérdida de datos estimada supera 1 hora, evaluada cada 30 minutos  
  
-   Las dos directivas tienen una configuración idéntica en todas las réplicas de disponibilidad  
  
-   Las directivas se evalúan en todos los servidores, pero solo en los grupos de disponibilidad cuya réplica de disponibilidad local es la réplica principal. Si la réplica de disponibilidad local no es la réplica principal, las directivas no se evalúan.  
  
-   Los errores de las directivas se muestran en el panel Always On cuando se abre en la réplica principal.  

Para crear las directivas, siga las instrucciones siguientes en todas las instancias de servidor que participen en el grupo de disponibilidad:  

1.  [Inicie el servicio Agente SQL Server](~/ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md) si aún no se ha iniciado.  
  
2.  En SQL Server Management Studio, en el menú **Herramientas**, haga clic en **Opciones**.  
  
3.  En la pestaña **SQL Server Always On**, seleccione **Habilitar directiva Always On definida por el usuario** y haga clic en **Aceptar**.  
  
     Esta configuración permite mostrar las directivas personalizadas configuradas correctamente en el panel Always On.  
  
4.  Cree una [condición de administración basada en directivas](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) con las especificaciones siguientes:  
  
    -   **Nombre**: `RTO`  
  
    -   **Faceta**: **Estado de la réplica de base de datos**  
  
    -   **Campo**: `Add(@EstimatedRecoveryTime, 60)`  
  
    -   **Operador**: **<=**  
  
    -   **Valor**: `600`  
  
     Se produce un error en esta condición cuando el tiempo de conmutación por error posible supera los 10 minutos, incluida una sobrecarga de 60 segundos para la detección de errores y la conmutación por error.  
  
5.  Cree una segunda [condición de administración basada en directivas](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) con las especificaciones siguientes:  
  
    -   **Nombre**: `RPO`  
  
    -   **Faceta**: **Estado de la réplica de base de datos**  
  
    -   **Campo**: `@EstimatedDataLoss`  
  
    -   **Operador**: **<=**  
  
    -   **Valor**: `3600`  
  
     Se produce un error en esta condición cuando la posible pérdida de datos supera 1 hora.  
  
6.  Cree una tercera [condición de administración basada en directivas](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) con las especificaciones siguientes:  
  
    -   **Nombre**: `IsPrimaryReplica`  
  
    -   **Faceta**: **Grupo de disponibilidad**  
  
    -   **Campo**: `@LocalReplicaRole`  
  
    -   **Operador**: **=**  
  
    -   **Valor**: `Primary`  
  
     Esta condición comprueba si la réplica de disponibilidad local de un grupo de disponibilidad determinado es la réplica principal.  
  
7.  Cree una [directiva de administración basada en directivas](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md) con las especificaciones siguientes:  
  
    -   Página **General**:  
  
        -   **Nombre**: `CustomSecondaryDatabaseRTO`  
  
        -   **Condición de comprobación**: `RTO`  
  
        -   **Para destinos**: **Cada DatabaseReplicaState** en **IsPrimaryReplica AvailabilityGroup**  
  
             Esta configuración garantiza que la directiva se evalúe solo en los grupos de disponibilidad cuya réplica de disponibilidad local es la réplica principal.  
  
        -   **Modo de evaluación**: **Según programación**  
  
        -   **Programación**: **CollectorSchedule_Every_5min**  
  
        -   **Habilitado**: **seleccionado**  
  
    -   Página **Descripción**:  
  
        -   **Categoría**: **Advertencias de base de datos de disponibilidad**  
  
             Esta configuración permite que los resultados de evaluación de directivas se muestren en el panel Always On.  
  
        -   **Descripción**: **La réplica actual tiene un RTO que supera los 10 minutos, asumiendo una sobrecarga de 1 minuto para la detección y la conmutación por error. Debe investigar los problemas de rendimiento en la instancia de servidor respectiva inmediatamente.**  
  
        -   **Texto para mostrar**: **RTO superado.**  
  
8.  Cree una segunda [directiva de administración basada en directivas](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md) con las especificaciones siguientes:  
  
    -   Página **General**:  
  
        -   **Nombre**: `CustomAvailabilityDatabaseRPO`  
  
        -   **Condición de comprobación**: `RPO`  
  
        -   **Para destinos**: **Cada DatabaseReplicaState** en **IsPrimaryReplica AvailabilityGroup**  
  
        -   **Modo de evaluación**: **Según programación**  
  
        -   **Programación**: **CollectorSchedule_Every_30min**  
  
        -   **Habilitado**: **seleccionado**  
  
    -   Página **Descripción**:  
  
        -   **Categoría**: **Advertencias de base de datos de disponibilidad**  
  
        -   **Descripción**: **La base de datos de disponibilidad ha superado el RPO de 1 hora. Debe investigar los problemas de rendimiento en las réplicas de disponibilidad inmediatamente.**  
  
        -   **Texto para mostrar**: **RPO superado.**  
  
 Al terminar se crean dos nuevos trabajos del Agente SQL Server, uno por programación de evaluación de directivas. Estos trabajos deben tener nombres que comiencen por **syspolicy_check_schedule**.  
  
 Puede ver el historial de trabajos para inspeccionar los resultados de la evaluación. Los errores de evaluación también se registran en el registro de aplicaciones de Windows (en el Visor de eventos) con el Id. de evento 34052. También puede configurar el Agente SQL Server para enviar alertas sobre los errores de directiva. Para obtener más información, vea [Configurar alertas para notificar los errores de directiva a los administradores de directivas](~/relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md).  
  
##  <a name="BKMK_SCENARIOS"></a> Escenarios de solución de problemas de rendimiento  
 En la tabla siguiente se enumeran los escenarios de solución de problemas relacionados con el rendimiento comunes.  
  
|Escenario|Description|  
|--------------|-----------------|  
|[Solución de problemas: el grupo de disponibilidad superó el RTO](troubleshoot-availability-group-exceeded-rto.md)|Después de una conmutación por error automática o una manual planeada sin pérdida de datos, el tiempo de conmutación por error supera el RTO. O bien, al estimar el tiempo de conmutación por error de una réplica secundaria de confirmación sincrónica (por ejemplo, un asociado de conmutación automática por error), descubre que supera el RTO.|  
|[Solución de problemas: el grupo de disponibilidad superó el RPO](troubleshoot-availability-group-exceeded-rpo.md)|Después de realizar una conmutación por error manual forzada, la pérdida de datos supera el RPO. O bien, al calcular la posible pérdida de datos de una réplica secundaria de confirmación asincrónica, descubre que supera el RPO.|  
|[Solución de problemas: cambios en la réplica principal que no se reflejan en la réplica secundaria](troubleshoot-primary-changes-not-reflected-on-secondary.md)|La aplicación cliente finaliza una actualización en la réplica principal correctamente, pero una consulta a la réplica secundaria muestra que el cambio no se ha reflejado.|  
  
##  <a name="BKMK_XEVENTS"></a> Eventos extendidos de utilidad  
 Los siguientes eventos extendidos son útiles al solucionar problemas de réplicas en estado **Sincronizando**.  
  
|Nombre del evento|Categoría|Canal|réplica de disponibilidad|  
|----------------|--------------|-------------|--------------------------|  
|redo_caught_up|transacciones|Depuración|Secundario|  
|redo_worker_entry|transacciones|Depuración|Secundario|  
|hadr_transport_dump_message|`alwayson`|Depuración|Principal|  
|hadr_worker_pool_task|`alwayson`|Depuración|Principal|  
|hadr_dump_primary_progress|`alwayson`|Depuración|Principal|  
|hadr_dump_log_progress|`alwayson`|Depuración|Principal|  
|hadr_undo_of_redo_log_scan|`alwayson`|Analíticos|Secundario|  
  
  