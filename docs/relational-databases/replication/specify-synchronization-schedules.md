---
title: "Especificar programaciones de sincronizaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "suscripciones [replicación de SQL Server], sincronizar"
  - "programar sincronización [replicación de SQL Server]"
  - "sincronización [replicación de SQL Server], programar"
  - "replicación [SQL Server], sincronizar"
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Especificar programaciones de sincronizaci&#243;n
  En este tema se describe cómo especificar programaciones de sincronización en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO). Al crear una suscripción, puede definir una programación de sincronización que controla cuándo se ejecutará el agente de replicación para la suscripción. Si no especifica parámetros de programación, la suscripción usará la programación predeterminada.  
  
 El Agente de distribución (para las instantáneas y la replicación transaccional) o el Agente de mezcla (para la replicación de mezcla) sincronizan las suscripciones. Los agentes pueden ejecutarse continuamente, a petición o según una programación.  
  
 **En este tema**  
  
-   **Para especificar programaciones de sincronización con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especifique programaciones de sincronización en la página **Programación de sincronización** del Asistente para nuevas suscripciones. Para obtener más información sobre cómo utilizar este asistente, vea [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md) y [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
 Modifique las programaciones de sincronización en el cuadro de diálogo **Propiedades de programación del trabajo** , al que se obtiene acceso desde la carpeta **Trabajos** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y desde las ventanas de detalles del agente en el Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
 Si especifica programaciones desde la carpeta **Trabajos** , use la tabla siguiente para determinar el nombre del trabajo del agente.  
  
|Agente|Nombre del trabajo|  
|-----------|--------------|  
|Agente de mezcla para suscripciones de extracción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< Basededatosdesuscripciones>-\< entero>**|  
|Agente de mezcla para suscripciones de inserción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>**|  
|Agente de distribución para suscripciones de inserción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>** <sup>1</sup>|  
|Agente de distribución para suscripciones de extracción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< Basededatosdesuscripciones>-\< GUID>** <sup>2</sup>|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>**|  
  
 <sup>1</sup> para suscripciones de inserción a publicaciones de Oracle, es **\< publicador>-\< publicador**> en lugar de **\< publicador>-\< Basededatosdepublicaciones>**  
  
 <sup>2</sup> para suscripciones de extracción a publicaciones de Oracle, es **\< publicador>-\< DistributionDatabase**> en lugar de **\< publicador>-\< Basededatosdepublicaciones>**  
  
#### Para especificar programaciones de sincronización  
  
1.  En el **SynchronizationSchedule** página del Asistente de suscripción nueva, seleccione uno de los siguientes valores en el **programación del agente** la lista desplegable para cada suscripción que está creando:  
  
    -   **Ejecutar continuamente**  
  
    -   **Ejecutar solamente a petición**  
  
    -   **\<Definir programación...>**  
  
2.  Si selecciona **\< Definir programación … >**, especifique una programación en la **Propiedades de programación de trabajo** cuadro de diálogo y, a continuación, haga clic en **Aceptar**.  
  
3.  Finalice el asistente.  
  
#### Para modificar una programación de sincronización para una suscripción de inserción en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic en una suscripción y, a continuación, haga clic en **Ver detalles**.  
  
4.  En el **suscripción \< Nombredesuscripción >** ventana, haga clic en **acción**, y, a continuación, haga clic en **\< Nombreagente> Propiedades del trabajo**.  
  
5.  En el **programaciones** página de la **Propiedades del trabajo - \< JobName>** cuadro de diálogo, haga clic en **Editar.**  
  
6.  En la **Propiedades de programación de trabajo** cuadro de diálogo, seleccione un valor en el **tipo de programación** lista desplegable:  
  
    -   Para especificar que el agente debe ejecutarse continuamente, seleccione **Iniciar automáticamente al iniciar el Agente SQL Server**.  
  
    -   Para especificar que el agente debe ejecutarse de acuerdo con una programación, seleccione **Periódica**.  
  
    -   Para especificar que el agente debe ejecutarse a petición, seleccione **Una vez**.  
  
7.  Si selecciona **Periódica**, especifique una programación para el agente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Para modificar una programación de sincronización para una suscripción de inserción en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic en el trabajo para el agente de distribución o el agente de mezcla asociado con la suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  En el **programaciones** página de la **Propiedades del trabajo - \< JobName>** cuadro de diálogo, haga clic en **Editar.**  
  
5.  En la **Propiedades de programación de trabajo** cuadro de diálogo, seleccione un valor en el **tipo de programación** lista desplegable:  
  
    -   Para especificar que el agente debe ejecutarse continuamente, seleccione **Iniciar automáticamente al iniciar el Agente SQL Server**.  
  
    -   Para especificar que el agente debe ejecutarse de acuerdo con una programación, seleccione **Periódica**.  
  
    -   Para especificar que el agente debe ejecutarse a petición, seleccione **Una vez**.  
  
6.  Si selecciona **Periódica**, especifique una programación para el agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Para modificar una programación de sincronización para una suscripción de extracción en Management Studio  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic en el trabajo para el agente de distribución o el agente de mezcla asociado con la suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  En el **programaciones** página de la **Propiedades del trabajo - \< JobName>** cuadro de diálogo, haga clic en **Editar.**  
  
5.  En la **Propiedades de programación de trabajo** cuadro de diálogo, seleccione un valor en el **tipo de programación** lista desplegable:  
  
    -   Para especificar que el agente debe ejecutarse continuamente, seleccione **Iniciar automáticamente al iniciar el Agente SQL Server**.  
  
    -   Para especificar que el agente debe ejecutarse de acuerdo con una programación, seleccione **Periódica**.  
  
    -   Para especificar que el agente debe ejecutarse a petición, seleccione **Una vez**.  
  
6.  Si selecciona **Periódica**, especifique una programación para el agente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede definir programaciones de sincronización mediante programación usando los procedimientos almacenados de replicación. Los procedimientos almacenados que usa dependen del tipo de replicación y del tipo de suscripción (extracción o inserción).  
  
 Una programación se define mediante los siguientes parámetros de programación, los comportamientos de las cuales se heredan de [sp_add_schedule & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md):  
  
-   **@frequency_type** -el tipo de frecuencia usado al programar el agente.  
  
-   **@frequency_interval** : el día de la semana cuando se ejecuta un agente.  
  
-   **@frequency_relative_interval** : la semana de un mes determinado cuando el agente está programado para que se ejecute mensualmente.  
  
-   **@frequency_recurrence_factor** -el número de unidades del tipo de frecuencia que se producen entre sincronizaciones.  
  
-   **@frequency_subday** -la unidad de frecuencia cuando el agente se ejecuta más de una vez al día.  
  
-   **@frequency_subday_interval** -el número de unidades de frecuencia entre ejecuciones cuando el agente se ejecuta más de una vez al día.  
  
-   **@active_start_time_of_day** : la hora más temprana de un día determinado cuando se inicia la ejecución de un agente.  
  
-   **@active_end_time_of_day** : la hora más reciente de un día determinado cuando se inicia la ejecución de un agente.  
  
-   **@active_start_date** : el primer día que surta efecto la programación del agente.  
  
-   **@active_end_date** : el último día que surta efecto la programación del agente.  
  
#### Para definir la programación de sincronización para una suscripción de extracción a una publicación transaccional  
  
1.  Cree una nueva suscripción de extracción para una publicación transaccional. Para más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  En el suscriptor, ejecute [sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, y [!INCLUDE[msCoName](../../includes/msconame-md.md)] las credenciales de Windows en la que se ejecuta el agente de distribución en el suscriptor para **@job_name** y **@password**. Especifique los parámetros de sincronización, detallados anteriormente, que definen la programación para el trabajo del Agente de distribución que sincroniza la suscripción.  
  
#### Para definir la programación de sincronización para una suscripción de inserción a una publicación transaccional  
  
1.  Cree una nueva suscripción de inserción para una publicación transaccional. Para obtener más información, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  En el suscriptor, ejecute [sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique **@subscriber**, **@subscriber_db**, **@publication**, y las credenciales de Windows en la que se ejecuta el agente de distribución en el suscriptor para **@job_name** y **@password**. Especifique los parámetros de sincronización, detallados anteriormente, que definen la programación para el trabajo del Agente de distribución que sincroniza la suscripción.  
  
#### Para definir la programación de sincronización para una suscripción de extracción a una publicación de combinación  
  
1.  Cree una nueva suscripción de extracción para una publicación de combinación. Para más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  En el suscriptor, ejecute [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, y las credenciales de Windows en la que se ejecuta el agente de mezcla en el suscriptor para **@job_name** y **@password**. Especifique los parámetros de sincronización, detallados anteriormente, que definen la programación para el trabajo del Agente de distribución que sincroniza la suscripción.  
  
#### Para definir la programación de sincronización para una suscripción de inserción a una publicación de combinación  
  
1.  Cree una nueva suscripción de inserción a una publicación de combinación. Para obtener más información, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  En el suscriptor, ejecute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Especifique **@subscriber**, **@subscriber_db**, **@publication**, y las credenciales de Windows en la que se ejecuta el agente de mezcla en el suscriptor para **@job_name** y **@password**. Especifique los parámetros de sincronización, detallados anteriormente, que definen la programación para el trabajo del Agente de distribución que sincroniza la suscripción.  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 La replicación usa el Agente SQL Server para programar los trabajos de las actividades que se producen periódicamente, como la generación de instantáneas y la sincronización de suscripción. Puede usar Replication Management Objects (RMO) mediante programación para especificar las programaciones de los trabajos de agente de replicación.  
  
> [!NOTE]  
>  Al crear una suscripción y especifique un valor **false** para **CreateSyncAgentByDefault** (el comportamiento predeterminado para las suscripciones de extracción) no se crea el trabajo del agente y se omiten las propiedades de programación. En este caso, la aplicación debe determinar la programación de sincronización. Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) y [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
#### Para definir una programación del agente de replicación al crear una suscripción de inserción a una publicación transaccional  
  
1.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransSubscription> clase para la suscripción que se va a crear. Para obtener más información, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Antes de llamar a <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, establezca uno o más de los siguientes campos de la <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> propiedad:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -el tipo de frecuencia (como diaria o semanal) que se usa cuando se programa el agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : el día de la semana en los que se ejecuta un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : la semana de un mes determinado cuando el agente está programado para que se ejecute mensualmente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -el número de unidades del tipo de frecuencia que se producen entre sincronizaciones.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -la unidad de frecuencia cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -el número de unidades de frecuencia entre ejecuciones cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora de un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : última hora en un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primer día en que la programación del agente está en vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : último día en que la programación del agente está en vigor.  
  
    > [!NOTE]  
    >  Si no especifica una de estas propiedades, se establece un valor predeterminado.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método para crear la suscripción.  
  
#### Para definir una programación del agente de replicación al crear una suscripción de extracción a una publicación transaccional  
  
1.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPullSubscription> clase para la suscripción que se va a crear. Para más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Antes de llamar a <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, establezca uno o más de los siguientes campos de la <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> propiedad:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -el tipo de frecuencia (como diaria o semanal) que se usa al programar el agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : el día de la semana en los que se ejecuta un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : la semana de un mes determinado que el agente está programado para ejecutarse cada mes.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -el número de unidades del tipo de frecuencia que se producen entre sincronizaciones.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -la unidad de frecuencia cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -el número de unidades de frecuencia entre ejecuciones cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora de un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : última hora en un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primer día en que la programación del agente está en vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : último día en que la programación del agente está en vigor.  
  
    > [!NOTE]  
    >  Si no especifica una de estas propiedades, se establece un valor predeterminado.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> método para crear la suscripción.  
  
#### Para definir una programación del agente de replicación al crear una suscripción de extracción a una publicación de combinación  
  
1.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePullSubscription> clase para la suscripción que se va a crear. Para más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md).  
  
2.  Antes de llamar a <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>, establezca uno o más de los siguientes campos de la <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> propiedad:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -el tipo de frecuencia (como diaria o semanal) que se usa al programar el agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : el día de la semana en los que se ejecuta un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : la semana de un mes determinado que el agente está programado para ejecutarse cada mes.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -el número de unidades del tipo de frecuencia que se producen entre sincronizaciones.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -la unidad de frecuencia cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -el número de unidades de frecuencia entre ejecuciones cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora de un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : última hora en un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primer día en que la programación del agente está en vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : último día en que la programación del agente está en vigor.  
  
    > [!NOTE]  
    >  Si no especifica una de estas propiedades, se establece un valor predeterminado.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> método para crear la suscripción.  
  
#### Para definir una programación del agente de replicación al crear una suscripción de inserción a una publicación de combinación  
  
1.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeSubscription> clase para la suscripción que se va a crear. Para obtener más información, consulte [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
2.  Antes de llamar a <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>, establezca uno o más de los siguientes campos de la <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> propiedad:  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> -el tipo de frecuencia (como diaria o semanal) que se usa al programar el agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> : el día de la semana en los que se ejecuta un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> : la semana de un mes determinado que el agente está programado para ejecutarse cada mes.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> -el número de unidades del tipo de frecuencia que se producen entre sincronizaciones.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> -la unidad de frecuencia cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> -el número de unidades de frecuencia entre ejecuciones cuando el agente se ejecuta más de una vez al día.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - hora de un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> : última hora en un día determinado en el que se inicia la ejecución de un agente.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> : primer día en que la programación del agente está en vigor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> : último día en que la programación del agente está en vigor.  
  
    > [!NOTE]  
    >  Si no especifica una de estas propiedades, se establece un valor predeterminado.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método para crear la suscripción.  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 Este ejemplo crea una suscripción de inserción a una publicación de combinación y especifica la programación en la que se sincroniza la suscripción.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## Vea también  
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sincronizar una suscripción de inserción](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Sincronizar una suscripción de extracción](../../relational-databases/replication/synchronize-a-pull-subscription.md)   
 [Sincronizar datos](../../relational-databases/replication/synchronize-data.md)  
  
  