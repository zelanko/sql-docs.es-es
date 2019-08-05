---
title: Supervisión de la replicación mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_replmonitorhelppublisher
- sp_replmonitorhelpmergesessiondetail
- monitoring performance [SQL Server replication], publication status
- sp_replmonitorhelpmergesession
- sp_replmonitorhelppublicationthresholds
- monitoring performance [SQL Server replication], subscription status
- monitoring performance [SQL Server replication], Transact-SQL programming
- sp_replmonitorsubscriptionpendingcmds
- sp_replmonitorchangepublicationthreshold
- transactional replication, monitoring
- sp_replmonitorhelppublication
- sp_replmonitorhelpsubscription
- monitoring performance [SQL Server replication], thresholds and warnings
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 765eec058514f7a5e0c38a81c66fe214c9f19f00
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68767632"
---
# <a name="programmatically-monitor-replication"></a>Supervisar la replicación mediante programación
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
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
  
#### <a name="to-monitor-publishers-publications-and-subscriptions-from-the-distributor"></a>Para supervisar publicadores, publicaciones y suscripciones desde el distribuidor  
  
1.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md). De esta forma se devuelve la información de supervisión de todos los publicadores que usan este distribuidor. Para limitar el conjunto de resultados a un único publicador, especifique un valor en **@publisher** .  
  
2.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md). De esta forma se devuelve la información de supervisión de todas las publicaciones que usan este distribuidor. Para limitar el conjunto de resultados a un único publicador, publicación o base de datos de publicación, especifique un valor en **@publisher** , **@publication** o **@publisher_db** , respectivamente.  
  
3.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md). De esta forma se devuelve la información de supervisión de todas las suscripciones que usan este distribuidor. Para limitar el conjunto de resultados a las suscripciones que pertenecen a un único publicador, publicación o base de datos de publicación, especifique un valor en **@publisher** , **@publication** o **@publisher_db** , respectivamente.  
  
#### <a name="to-monitor-transactional-commands-waiting-to-be-applied-at-the-subscriber"></a>Para supervisar los comandos transaccionales que esperan su aplicación en el suscriptor  
  
1.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md). De esta forma se devuelve la información de supervisión de todos los comandos pendientes en todas las suscripciones que usan este distribuidor. Para limitar el conjunto de resultados a los comandos pendientes de las suscripciones que pertenecen a un único publicador, suscriptor, publicación o base de datos de publicación, especifique un valor en **@publisher** , **@subscriber** , **@publication** o **@publisher_db** , respectivamente.  
  
#### <a name="to-monitor-merge-changes-waiting-to-be-uploaded-or-downloaded"></a>Para supervisar los cambios de mezcla que esperan ser cargados o descargados  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). De esta forma se devuelve un conjunto de resultados que muestra información sobre los cambios que esperan su replicación en los suscriptores. Para limitar el conjunto de resultados a los cambios que pertenecen a una publicación o artículo únicos, especifique un valor en **@publication** o **@article** , respectivamente.  
  
2.  En el suscriptor de la base de datos de suscripciones, ejecute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). De esta forma se devuelve un conjunto de resultados que muestra información sobre los cambios que esperan su replicación en el publicador. Para limitar el conjunto de resultados a los cambios que pertenecen a una publicación o artículo únicos, especifique un valor en **@publication** o **@article** , respectivamente.  
  
#### <a name="to-monitor-merge-agent-sessions"></a>Para supervisar las sesiones del Agente de mezcla  
  
1.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). De esta forma se devuelve información de supervisión, incluido el valor de **Session_id**, de todas las sesiones del Agente de mezcla de todas las suscripciones que usan este distribuidor. También puede obtener el valor de **Session_id** si consulta la tabla del sistema [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) .  
  
2.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique el valor **Session_id** del paso 1 en **@session_id** . De esta forma se muestra información detallada de supervisión acerca de la sesión.  
  
3.  Repita el paso 2 para cada sesión que le interese.  
  
#### <a name="to-monitor-merge-agent-sessions-for-pull-subscriptions-from-the-subscriber"></a>Para supervisar las sesiones del Agente de mezcla de las suscripciones de extracción del suscriptor  
  
1.  En el suscriptor de la base de datos de suscripciones, ejecute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Para una suscripción determinada, especifique un valor en **@publisher** , **@publication** y el nombre de la base de datos de publicación en **@publisher_db** . De esta forma se devuelve información de supervisión de las últimas cinco sesiones del Agente de mezcla de esta suscripción. Anote el valor de **Session_id** de las sesiones de interés incluidas en el conjunto de resultados.  
  
2.  En el suscriptor de la base de datos de suscripciones, ejecute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique el valor **Session_id** del paso 1 en **@session_id** . De esta forma se muestra información detallada de supervisión acerca de la sesión.  
  
3.  Repita el paso 2 para cada sesión que le interese.  
  
#### <a name="to-view-and-modify-the-monitor-threshold-metrics-for-a-publication"></a>Para ver y modificar las métricas del umbral de supervisión de una publicación  
  
1.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md). De esta forma se devuelve el conjunto de umbrales de supervisión de todas las publicaciones que usan este distribuidor. Para limitar el conjunto de resultados a los umbrales de supervisión de las publicaciones que pertenecen a un único publicador, base de datos de publicación o publicación, especifique un valor en **@publisher** , **@publisher_db** o **@publication** , respectivamente. Anote el valor de **Metric_id** de cualquier umbral que se deba cambiar. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  En el distribuidor de la base de datos de distribución, ejecute [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md). Especifique los valores siguientes, según sea necesario:  
  
    -   El valor de **Metric_id** obtenido en el paso 1 en **@metric_id** .  
  
    -   Un nuevo valor para la métrica del umbral de supervisión en **@value** .  
  
    -   Un valor de **1** en **@shouldalert** para que se registre una alerta cuando se alcance este umbral o un valor de **0** si no se necesita una alerta.  
  
    -   Un valor de **1** en **@mode** para habilitar la métrica del umbral de supervisión o un valor de **2** para deshabilitarla.  
  
##  <a name="RMO"></a> Replication Management Objects (RMO)  
  
#### <a name="to-monitor-a-subscription-to-a-merge-publication-at-the-subscriber"></a>Para supervisar una suscripción a una publicación de combinación en el suscriptor  
  
1.  Cree una conexión al suscriptor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> , y establezca las propiedades <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> de la suscripción y la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creada en el paso 1.  
  
3.  Llame a alguno de los métodos siguientes para devolver información sobre sesiones de Agente de mezcla de esta suscripción:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> : devuelve una matriz de objetos <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> con información de hasta las últimas cinco sesiones del Agente de mezcla. Anote el valor <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> de cualquier sesión que le interese.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> : devuelve una matriz de objetos <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> con información sobre las sesiones de Agente de mezcla que se han producido durante el pasado número de horas pasadas como el parámetro *hours* (hasta las últimas cinco sesiones). Anote el valor <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> de cualquier sesión que le interese.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> : devuelve un objeto <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> con información sobre la última sesión del Agente de mezcla. Anote el valor <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> de esta sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> : devuelve un objeto <xref:System.Data.DataSet> con información sobre hasta las últimas cinco sesiones del Agente de mezcla, una en cada fila. Anote el valor de la columna **Session_id** de las sesiones que le interesen.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> : devuelve un objeto <xref:System.Data.DataRow> con información sobre la última sesión del Agente de mezcla. Anote el valor de la columna **Session_id** de esta sesión.  
  
4.  (Opcional) Llame a <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> para actualizar los datos del objeto <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> pasados como *mss,* o llame a <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> para actualizar los datos del objeto <xref:System.Data.DataRow> pasados como *drRefresh*.  
  
5.  Con el Id. de sesión obtenido en el paso 3, llame a uno de los métodos siguientes para devolver información sobre los detalles de una sesión determinada:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> : devuelve una matriz de objetos <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> para el *SessionId*.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> : devuelve un objeto <xref:System.Data.DataSet> con información del *SessionId*.  
  
#### <a name="to-monitor-replication-properties-for-all-publications-at-a-distributor"></a>Para supervisar las propiedades de replicación de todas las publicaciones en un distribuidor  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> .  
  
3.  Establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creada en el paso 1.  
  
4.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto.  
  
5.  Ejecute uno o más de los métodos siguientes para devolver información de replicación para todos los publicadores que utilizan este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los agentes de distribución en este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre los errores almacenados en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los agentes de registro del LOG en este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los agentes de mezcla en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todo los agentes de replicación en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los publicadores en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> : devuelve un objeto <xref:System.Data.DataSet> que devuelve los publicadores que utilizan este distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los agentes de registro del LOG en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene los detalles sobre el Agente de lectura de cola especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de sesión sobre el Agente de lectura de cola especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los agentes de instantáneas en el distribuidor.  
  
#### <a name="to-monitor-publication-properties-for-a-specific-publisher-at-the-distributor"></a>Para supervisar las propiedades de publicación de un publicador concreto en el distribuidor  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Obtenga un objeto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> de alguna de estas maneras.  
  
    -   Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.PublisherMonitor> . Establezca las propiedades <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> del publicador, y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creada en el paso 1. Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve **false**, significa que el nombre del publicador se definió incorrectamente o que la publicación no existe.  
  
    -   De <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> al que obtuvo acceso por medio de la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> de un objeto <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> existente.  
  
3.  Ejecute uno o más de los métodos siguientes para devolver información de replicación de todos los publicadores que pertenecen este publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene los detalles sobre el Agente de distribución especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de sesión sobre el Agente de distribución especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de registro de error sobre un error especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene los detalles sobre el Agente de registro del LOG especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de sesión de un Agente de registro del LOG especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene los detalles sobre el Agente de mezcla especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene los detalles adicionales sobre el Agente de mezcla especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información del Agente de mezcla especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de sesión adicional sobre el Agente de mezcla especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todas las publicaciones en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información adicional sobre todas las publicaciones en el distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene los detalles sobre el Agente de instantánea especificado y la sesión.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de sesión de un Agente de instantánea especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todas las suscripciones a publicaciones en el distribuidor.  
  
#### <a name="to-monitor-properties-for-a-specific-publication-at-the-distributor"></a>Para supervisar las propiedades de una publicación concreta en el distribuidor  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Obtenga un objeto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> de alguna de estas maneras.  
  
    -   Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.PublicationMonitor> . Establezca las propiedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> de la publicación, y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creada en el paso 1. Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de la publicación de definieron incorrectamente o que la publicación no existe.  
  
    -   De <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> al que obtuvo acceso por medio de la propiedad <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> de un objeto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> existente.  
  
3.  Ejecute uno o más de los métodos siguientes para devolver información sobre esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene registros de error sobre un error especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre el Agente de registro del LOG de esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre el conjunto de umbrales de advertencia del monitor para esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre el Agente de lectura de cola utilizado por esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre el Agente de instantáneas de esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre las suscripciones a esta publicación.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información adicional sobre suscripciones a esta publicación basándose en el <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>proporcionado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información de latencia del token de seguimiento especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> : devuelve un objeto <xref:System.Data.DataSet> que contiene información sobre todos los testigos de seguimiento insertados en esta publicación.  
  
#### <a name="to-monitor-transactional-commands-that-are-waiting-to-be-applied-at-the-subscriber"></a>Para supervisar comandos transaccionales a la espera de ser aplicados en el suscriptor.  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Obtenga un objeto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> de alguna de estas maneras.  
  
    -   Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.PublicationMonitor> . Establezca las propiedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> de la publicación, y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creada en el paso 1. Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de la publicación de definieron incorrectamente o que la publicación no existe.  
  
    -   De <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> al que obtuvo acceso por medio de la propiedad <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> de un objeto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> existente.  
  
3.  Ejecute el método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> , que devuelve un objeto <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> .  
  
4.  Utilice las propiedades de este objeto <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> para determinar el número estimado de comandos pendientes y el tiempo que tardará en completarse la entrega de estos comandos.  
  
#### <a name="to-set-the-monitor-warning-thresholds-for-a-publication"></a>Para establecer los umbrales de advertencias del monitor de una  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Obtenga un objeto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> de alguna de estas maneras.  
  
    -   Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.PublicationMonitor> . Establezca las propiedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> de la publicación, y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creada en el paso 1. Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de la publicación de definieron incorrectamente o que la publicación no existe.  
  
    -   De <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> al que obtuvo acceso por medio de la propiedad <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> de un objeto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> existente.  
  
3.  Ejecute el método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> . Anote los valores de umbral actuales del <xref:System.Collections.ArrayList> devuelto de los objetos <xref:Microsoft.SqlServer.Replication.MonitorThreshold> .  
  
4.  Ejecute el método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> . Pase los siguientes parámetros:  
  
    -   *metricID* : un valor <xref:System.Int32> que representa la métrica de umbral de supervisión en la tabla siguiente:  
  
        |Valor|Descripción|  
        |-----------|-----------------|  
        |1|**expiration** : supervisa la expiración inminente de suscripciones a publicaciones transaccionales.|  
        |2|**latency** : supervisa el rendimiento de suscripciones a publicaciones transaccionales.|  
        |4|**mergeexpiration** : supervisa la expiración inminente de suscripciones a publicaciones de combinación.|  
        |5|**mergeslowrunduration** : supervisa la duración de sincronizaciones de mezcla en conexiones de poco ancho de banda (acceso telefónico).|  
        |6|**mergefastrunduration** : supervisa la duración de sincronizaciones de mezcla en conexiones de gran ancho de banda (LAN).|  
        |7|**mergefastrunspeed** : supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de red de área local (LAN) de gran ancho de banda.|  
        |8|**mergeslowrunspeed** : supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de poco ancho de banda (acceso telefónico).|  
  
    -   *enable* - <xref:System.Boolean> que indica si la métrica está habilitada para la publicación.  
  
    -   *thresholdValue* : el valor entero que establece el umbral.  
  
    -   *shouldAlert* : el entero que indica si este umbral debería generar una alerta.  
  
  
