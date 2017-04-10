---
title: "Supervisar la replicaci&#243;n mediante programaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
  - "sp_replmonitorhelpmergesessiondetail"
  - "supervisar rendimiento [replicación de SQL Server], estado de publicación"
  - "sp_replmonitorhelpmergesession"
  - "sp_replmonitorhelppublicationthresholds"
  - "supervisar rendimiento [replicación de SQL Server], estado de suscripción"
  - "supervisar rendimiento [replicación de SQL Server], programar con Transact-SQL"
  - "sp_replmonitorsubscriptionpendingcmds"
  - "sp_replmonitorchangepublicationthreshold"
  - "replicación transaccional, supervisar"
  - "sp_replmonitorhelppublication"
  - "sp_replmonitorhelpsubscription"
  - "supervisar rendimiento [replicación de SQL Server], umbrales y advertencias"
  - "supervisar la replicación de mezcla [replicación de SQL Server]"
  - "replicación de instantáneas [SQL Server], supervisar"
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Supervisar la replicaci&#243;n mediante programaci&#243;n
  El Monitor de replicación es una herramienta gráfica que permite supervisar una topología de replicación. Puede tener acceso a los mismos datos de supervisión mediante programación usando los procedimientos de almacenamiento de replicación de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). Estos objetos permiten programar las tareas siguientes:  
  
-   Supervisar el estado de publicadores, publicaciones y suscripciones.  
  
-   Supervisar sesiones del Agente de mezcla en uno o más suscriptores.  
  
-   Supervisar comandos transaccionales que esperan su aplicación en uno o más suscriptores.  
  
-   Definir métricas de umbral que determinan cuándo requiere intervención una publicación.  
  
-   Supervisar el estado de los testigos de seguimiento.  
  
 **En este tema:**  
  
 [Transact-SQL](#Tsql)  
  
 [Replication Management Objects (RMO)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### Para supervisar publicadores, publicaciones y suscripciones desde el distribuidor  
  
1.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md). De esta forma se devuelve la información de supervisión de todos los publicadores que usan este distribuidor. Para limitar el conjunto de resultados a un único publicador, especifique un valor en **@publisher**.  
  
2.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md). De esta forma se devuelve la información de supervisión de todas las publicaciones que usan este distribuidor. Para limitar el conjunto de resultados a un único publicador, publicación o base de datos publicada, especifique **@publisher**, **@publication**, o **@publisher_db**, respectivamente.  
  
3.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md). De esta forma se devuelve la información de supervisión de todas las suscripciones que usan este distribuidor. Para limitar el conjunto de resultados a las suscripciones que pertenecen a un único publicador, publicación o base de datos publicada, especifique **@publisher**, **@publication**, o **@publisher_db**, respectivamente.  
  
#### Para supervisar los comandos transaccionales que esperan su aplicación en el suscriptor  
  
1.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md). De esta forma se devuelve la información de supervisión de todos los comandos pendientes en todas las suscripciones que usan este distribuidor. Para limitar el conjunto de resultados a comandos pendientes para las suscripciones que pertenecen a un único publicador, suscriptor, publicación o base de datos publicada, especifique **@publisher**, **@subscriber**, **@publication**, o **@publisher_db**, respectivamente.  
  
#### Para supervisar los cambios de mezcla que esperan ser cargados o descargados  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). De esta forma se devuelve un conjunto de resultados que muestra información sobre los cambios que esperan su replicación en los suscriptores. Para limitar el conjunto de resultados a los cambios que pertenecen a una publicación o artículo únicos, especifique un valor en **@publication** o **@article**, respectivamente.  
  
2.  En un suscriptor en la base de datos de suscripción, ejecute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). De esta forma se devuelve un conjunto de resultados que muestra información sobre los cambios que esperan su replicación en el publicador. Para limitar el conjunto de resultados a los cambios que pertenecen a una publicación o artículo únicos, especifique un valor en **@publication** o **@article**, respectivamente.  
  
#### Para supervisar las sesiones del Agente de mezcla  
  
1.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Devuelve información de supervisión, incluidos **Session_id**, de todas las sesiones del agente de mezcla para todas las suscripciones que utilicen este distribuidor. También se puede obtener **Session_id** consultando la [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) tabla del sistema.  
  
2.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique un **Session_id** valor del paso 1 para **@session_id**. De esta forma se muestra información detallada de supervisión acerca de la sesión.  
  
3.  Repita el paso 2 para cada sesión que le interese.  
  
#### Para supervisar las sesiones del Agente de mezcla de las suscripciones de extracción del suscriptor  
  
1.  En el suscriptor en la base de datos de suscripción, ejecute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Para una suscripción determinada, especifique **@publisher**, **@publication**, y el nombre de la base de datos de publicación para **@publisher_db**. De esta forma se devuelve información de supervisión de las últimas cinco sesiones del Agente de mezcla de esta suscripción. Tenga en cuenta el valor de **Session_id** para las sesiones de interés en el resultado establecido.  
  
2.  En el suscriptor en la base de datos de suscripción, ejecute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique un **Session_id** valor del paso 1 para **@session_id**. De esta forma se muestra información detallada de supervisión acerca de la sesión.  
  
3.  Repita el paso 2 para cada sesión que le interese.  
  
#### Para ver y modificar las métricas del umbral de supervisión de una publicación  
  
1.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md). De esta forma se devuelve el conjunto de umbrales de supervisión de todas las publicaciones que usan este distribuidor. Para limitar el conjunto de resultados al supervisar los umbrales para publicaciones que pertenecen a un publicador único o la base de datos publicada o a una publicación, especifique **@publisher**, **@publisher_db**, o **@publication**, respectivamente. Tenga en cuenta el valor de **Metric_id** para los umbrales que se deben cambiar. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  En el distribuidor en la base de datos de distribución, ejecute [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md). Especifique los valores siguientes, según sea necesario:  
  
    -   El **Metric_id** valor obtenido en el paso 1 para **@metric_id**.  
  
    -   Un nuevo valor para la métrica del umbral de supervisión en **@value**.  
  
    -   Un valor de **1** en **@shouldalert** para que se registre una alerta cuando se alcance este umbral o un valor de **0** si no se necesita una alerta.  
  
    -   Un valor de **1** en **@mode** para habilitar la métrica del umbral de supervisión o un valor de **2** para deshabilitarla.  
  
##  <a name="RMO"></a> Replication Management Objects (RMO)  
  
#### Para supervisar una suscripción a una publicación de combinación en el suscriptor  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> clase y establezca la <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> Propiedades para la suscripción y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
3.  Llame a alguno de los métodos siguientes para devolver información sobre sesiones de Agente de mezcla de esta suscripción:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -Devuelve una matriz de <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> los objetos con información de hasta las últimas cinco sesiones del agente de mezcla. Tenga en cuenta el <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> valor para las sesiones de interés.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -Devuelve una matriz de <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objetos con información sobre las sesiones del agente de mezcla que se han producido durante el pasado número de horas que se pasa como el *horas* parámetro (hasta las últimas cinco sesiones). Tenga en cuenta el <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> valor para las sesiones de interés.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> -devuelve un <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objeto con información sobre la última sesión de agente de mezcla. Tenga en cuenta el <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> valor para esta sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> -devuelve un <xref:System.Data.DataSet> objeto con información de hasta las últimas cinco sesiones del agente de mezcla, uno en cada fila. Tenga en cuenta el valor de la **Session_id** columna para las sesiones de interés.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> -devuelve un <xref:System.Data.DataRow> objeto con información sobre la última sesión de agente de mezcla. Tenga en cuenta el valor de la **Session_id** columna para esta sesión.  
  
4.  (Opcional) Llame a <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> Para actualizar los datos de la <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objeto pasado como *mss,* o llame al <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> para actualizar los datos en el <xref:System.Data.DataRow> objeto pasado como *drRefresh*.  
  
5.  Con el Id. de sesión obtenido en el paso 3, llame a uno de los métodos siguientes para devolver información sobre los detalles de una sesión determinada:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> -devuelve una matriz de <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> objetos para proporcionado *SessionId*.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> -devuelve un <xref:System.Data.DataSet> objeto con información especificado *SessionId*.  
  
#### Para supervisar las propiedades de replicación de todas las publicaciones en un distribuidor  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto.  
  
5.  Ejecute uno o más de los métodos siguientes para devolver información de replicación para todos los publicadores que utilizan este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los agentes de distribución en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre los errores que se almacena en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los agentes de lector del registro en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los agentes de mezcla en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre el resto de los agentes de replicación en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los publicadores en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> -devuelve un <xref:System.Data.DataSet> objeto que devuelve los publicadores que utilizan este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los agentes de lector de cola en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene detalles sobre el agente de lector de cola y la sesión especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre el agente de lector de cola especificado de la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los agentes de instantáneas en el distribuidor.  
  
#### Para supervisar las propiedades de publicación de un publicador concreto en el distribuidor  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Obtener un <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto en uno de estos procedimientos.  
  
    -   Cree una instancia de la <xref:Microsoft.SqlServer.Replication.PublisherMonitor> clase. Establecer el <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> propiedad para el publicador y el conjunto de la <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1. Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que el nombre del publicador se definió incorrectamente o que la publicación no existe.  
  
    -   Desde el <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> tiene acceso por medio de la <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> propiedad de un miembro de <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> objeto.  
  
3.  Ejecute uno o más de los métodos siguientes para devolver información de replicación de todos los publicadores que pertenecen este publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene detalles sobre el agente de distribución y la sesión especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre el agente de distribución especificado de la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información de registro de error sobre el error especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene los detalles para el agente de lector del registro y la sesión especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información de sesión para el agente de lector de registro especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene detalles sobre el agente de mezcla y la sesión especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene detalles adicionales sobre el agente de mezcla y la sesión especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información de sesión para el agente de mezcla especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información de sesión adicional para el agente de mezcla especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todas las publicaciones en este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información adicional acerca de todas las publicaciones en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene detalles sobre el agente de instantáneas y la sesión especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información de sesión para el agente de instantáneas especificada.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todas las suscripciones a publicaciones en el distribuidor.  
  
#### Para supervisar las propiedades de una publicación concreta en el distribuidor  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Obtener un <xref:Microsoft.SqlServer.Replication.PublicationMonitor> objeto en uno de estos procedimientos.  
  
    -   Cree una instancia de la <xref:Microsoft.SqlServer.Replication.PublicationMonitor> clase. Establecer el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1. Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de la publicación de definieron incorrectamente o que la publicación no existe.  
  
    -   Desde el <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> tiene acceso por medio de la <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> propiedad de un miembro de <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto.  
  
3.  Ejecute uno o más de los métodos siguientes para devolver información sobre esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene los registros de error sobre el error especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre el agente de lector del registro para esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> -devuelve un <xref:System.Data.DataSet> establece el objeto que contiene información acerca de los umbrales de advertencia de monitor para esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre el agente de lector de cola utilizado por esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre el agente de instantáneas para esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información acerca de las suscripciones a esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información adicional acerca de las suscripciones a esta publicación según proporcionado <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información de latencia para el token de seguimiento especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> -devuelve un <xref:System.Data.DataSet> objeto que contiene información sobre todos los testigos de seguimiento insertados en esta publicación.  
  
#### Para supervisar comandos transaccionales a la espera de ser aplicados en el suscriptor.  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Obtener un <xref:Microsoft.SqlServer.Replication.PublicationMonitor> objeto en uno de estos procedimientos.  
  
    -   Cree una instancia de la <xref:Microsoft.SqlServer.Replication.PublicationMonitor> clase. Establecer el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1. Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de la publicación de definieron incorrectamente o que la publicación no existe.  
  
    -   Desde el <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> tiene acceso por medio de la <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> propiedad de un miembro de <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto.  
  
3.  Ejecute el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> método, que devuelve un <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> objeto.  
  
4.  Utilice las propiedades de este <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> objeto para determinar el número estimado de comandos pendientes y la longitud de tiempo que tardará en completarse la entrega de estos comandos.  
  
#### Para establecer los umbrales de advertencias del monitor de una  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Obtener un <xref:Microsoft.SqlServer.Replication.PublicationMonitor> objeto en uno de estos procedimientos.  
  
    -   Cree una instancia de la <xref:Microsoft.SqlServer.Replication.PublicationMonitor> clase. Establecer el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1. Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de la publicación de definieron incorrectamente o que la publicación no existe.  
  
    -   Desde el <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> tiene acceso por medio de la <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> propiedad de un miembro de <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto.  
  
3.  Ejecute el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> método. Tenga en cuenta la configuración de umbral actual en el valor devuelto <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.MonitorThreshold> objetos.  
  
4.  Ejecute el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> método. Pase los siguientes parámetros:  
  
    -   *metricID* : una <xref:System.Int32> valor que representa la métrica de umbral de supervisión de la tabla siguiente:  
  
        |Valor|Descripción|  
        |-----------|-----------------|  
        |1|**expiración** -supervisa la expiración inminente de suscripciones a publicaciones transaccionales.|  
        |2|**latencia** -supervisa el rendimiento de las suscripciones a publicaciones transaccionales.|  
        |4|**mergeexpiration** -supervisa la expiración inminente de suscripciones a publicaciones de mezcla.|  
        |5|**mergeslowrunduration** -supervisa la duración de sincronizaciones de mezcla en conexiones de ancho de banda bajo (acceso telefónico).|  
        |6|**mergefastrunduration** -supervisa la duración de sincronizaciones de mezcla en conexiones de ancho de banda alto (LAN).|  
        |7|**mergefastrunspeed** -supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de ancho de banda alto (LAN).|  
        |8|**mergeslowrunspeed** -supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de ancho de banda bajo (acceso telefónico).|  
  
    -   *habilitar* - <xref:System.Boolean> valor que indica si la métrica está habilitada para la publicación.  
  
    -   *thresholdValue* -valor entero que establece el umbral.  
  
    -   *shouldAlert* -entero que indica si este umbral debería generar una alerta.  
  
  