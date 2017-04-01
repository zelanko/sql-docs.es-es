---
title: "Medir la latencia y validar las conexiones de la replicaci&#243;n transaccional | Microsoft Docs"
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
  - "Monitor de replicación, rendimiento"
  - "testigos de seguimiento [replicación de SQL Server]"
  - "latencia [replicación de SQL Server]"
  - "replicación transaccional, testigos de seguimiento"
  - "supervisar rendimiento [replicación de SQL Server], testigos de seguimiento"
ms.assetid: 4addd426-7523-4067-8d7d-ca6bae4c9e34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Medir la latencia y validar las conexiones de la replicaci&#243;n transaccional
  En este tema se describe cómo medir la latencia y validar conexiones para la replicación transaccional en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante el Monitor de replicación, [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). La replicación transaccional proporciona la característica de testigo de seguimiento, que ofrece una forma cómoda de medir la latencia en topologías de replicación transaccional y validar las conexiones entre el publicador, el distribuidor y los suscriptores. Se escribe un token (una pequeña cantidad de datos) en el registro de transacción de la base de datos de publicaciones, marcado como si fuese una transacción replicada, y se envía a través del sistema, de forma que permite calcular:  
  
-   Cuánto tiempo transcurre desde que se confirma una transacción en el publicador hasta que se inserta el comando correspondiente en la base de datos de distribución del distribuidor.  
  
-   Cuánto tiempo transcurre desde que se inserta un comando en la base de datos de distribución hasta que se confirma la transacción correspondiente en el suscriptor.  
  
 A partir de estos cálculos, podrá responder a diversas preguntas, como por ejemplo:  
  
-   ¿Qué suscriptores tardan más en recibir un cambio del publicador?  
  
-   De los suscriptores que esperan recibir el testigo de seguimiento, ¿cuáles, si los hay, no lo han recibido?  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para medir la latencia y validar conexiones con:**  
  
     [Monitor de replicación de SQL Server](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Los testigos de seguimiento también pueden ser útiles al detener el sistema, lo que implica detener todas las actividades y comprobar que todos los nodos han recibido todos los cambios pendientes. Para obtener más información, consulte [Detener una topología de replicación & #40; Programación de Transact-SQL de replicación & #41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
 Para usar testigos de seguimiento, debe utilizar ciertas versiones de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   El distribuidor debe ser [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  
  
-   El publicador debe ser de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior, o un publicador de Oracle.  
  
-   Para las suscripciones de inserción, las estadísticas del token de seguimiento se obtienen del publicador, distribuidor y suscriptores, si el suscriptor es de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 o posterior.  
  
-   Para las suscripciones de extracción, las estadísticas del token de seguimiento se obtienen solo de los suscriptores, si el suscriptor es de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Si el suscriptor es de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], las estadísticas se obtienen solo del publicador y el distribuidor.  
  
 También hay que tener en cuenta otros problemas y restricciones:  
  
-   Para recibir un token de seguimiento, las suscripciones deben estar activas. Una suscripción está activa si se ha inicializado.  
  
-   La reinicialización quita los testigos de seguimiento pendientes en las suscripciones correspondientes.  
  
-   Los suscriptores solo reciben los testigos de seguimiento que se han creado después de la sincronización inicial.  
  
-   Los suscriptores que vuelven a publicar no reenvían los testigos de seguimiento.  
  
-   Después de la conmutación por error a un elemento secundario, el Monitor de replicación no puede ajustar el nombre de la instancia de publicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y seguirá mostrando información de replicación bajo el nombre de la instancia principal original de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Después de la conmutación por error, el Monitor de replicación no puede especificar un token de seguimiento, aunque muestra un token de seguimiento especificado en el nuevo publicador mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
##  <a name="SSMSProcedure"></a> Usar el Monitor de replicación de SQL Server  
 Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para insertar un testigo de seguimiento y ver la información del token  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Testigos de seguimiento** .  
  
3.  Haga clic en **Insertar seguimiento**.  
  
4.  Vea el tiempo transcurrido para el testigo de seguimiento en las siguientes columnas: **Publicador a distribuidor**, **Distribuidor a suscriptor**y **Latencia total**. El valor **Pendiente** indica que el testigo no ha alcanzado un punto específico.  
  
#### Para ver información en el testigo de seguimiento insertado previamente  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Testigos de seguimiento** .  
  
3.  Seleccione una hora en la **vez insertado** lista desplegable.  
  
4.  Vea el tiempo transcurrido para el testigo de seguimiento en las siguientes columnas: **Publicador a distribuidor**, **Distribuidor a suscriptor**y **Latencia total**. El valor **Pendiente** indica que el testigo no ha alcanzado un punto específico.  
  
    > [!NOTE]  
    >  La información del testigo de seguimiento se guarda durante el mismo período que otros datos del historial, que depende del período de retención de historial de la base de datos de distribución. Para obtener información acerca de cómo cambiar las propiedades de la base de datos de distribución, consulte [Propiedades de publicador y distribuidor modificar y vista](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para exponer un token de seguimiento en una publicación transaccional  
  
1.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_helppublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). Compruebe que la publicación existe y que el estado está activo.  
  
2.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_helpsubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Compruebe que la suscripción existe y que el estado está activo.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_posttracertoken & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md), especificando **@publication**. Tenga en cuenta el valor de la **@tracer_token_id** parámetro de salida.  
  
#### Para medir la latencia y validar las conexiones de una replicación transaccional  
  
1.  Exponga un token de seguimiento en la publicación utilizando el procedimiento anterior.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_helptracertokens & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md), especificando **@publication**. Esto devuelve una lista de todos los testigos de seguimiento expuestos en la publicación. Tenga en cuenta el deseado **tracer_id** conjunto de resultados.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_helptracertokenhistory & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md), especificando **@publication** y el identificador del token de seguimiento del paso 2 para **@tracer_id**. Esto devuelve información de latencia del token de seguimiento seleccionado.  
  
#### Para quitar los testigos de seguimiento  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helptracertokens & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md), especificando **@publication**. Esto devuelve una lista de todos los testigos de seguimiento expuestos en la publicación. Tenga en cuenta el **tracer_id** establece el token de seguimiento en el resultado.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_deletetracertokenhistory & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md), especificando **@publication** y el identificador del token para eliminar del paso 2 para **@tracer_id**.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 Este ejemplo expone un registro de token de seguimiento y utiliza el Id. devuelto del token de seguimiento expuesto para ver información de la latencia.  
  
 [!code-sql[HowTo#sp_tracertokens](../../../relational-databases/replication/codesnippet/tsql/measure-latency-and-vali_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
  
#### Para exponer un token de seguimiento en una publicación transaccional  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPublication> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 1.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 3 se definieron incorrectamente, o bien que la publicación no existe.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.TransPublication.PostTracerToken%2A> método. Este método inserta un token de seguimiento en el registro de transacciones de la publicación.  
  
#### Para medir la latencia y validar las conexiones de una replicación transaccional  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.PublicationMonitor> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> Propiedades y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 1.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades del monitor de la publicación del paso 3 se definieron incorrectamente, o bien que la publicación no existe.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> método. Convierte el valor devuelto <xref:System.Collections.ArrayList> objeto a una matriz de <xref:Microsoft.SqlServer.Replication.TracerToken> objetos.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> método. Pase un valor de <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> para un token de seguimiento del paso 5. Devuelve información de latencia para el token de seguimiento seleccionado como un <xref:System.Data.DataSet> objeto. Si se devuelve toda la información del token de seguimiento, la conexión entre el publicador y el distribuidor y la conexión entre el distribuidor y el suscriptor existen, y la topología de replicación está funcionando.  
  
#### Para quitar los testigos de seguimiento  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.PublicationMonitor> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> Propiedades y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 1.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades del monitor de la publicación del paso 3 se definieron incorrectamente, o bien que la publicación no existe.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> método. Convierte el valor devuelto <xref:System.Collections.ArrayList> objeto a una matriz de <xref:Microsoft.SqlServer.Replication.TracerToken> objetos.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.PublicationMonitor.CleanUpTracerTokenHistory%2A> método. Pase uno de los siguientes valores:  
  
    -   El <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> para un token de seguimiento del paso 5. Esto elimina información de un token seleccionado.  
  
    -   Un <xref:System.DateTime> objeto. Esto elimina información de todos los tokens anteriores a la fecha y hora especificada.  
  
  