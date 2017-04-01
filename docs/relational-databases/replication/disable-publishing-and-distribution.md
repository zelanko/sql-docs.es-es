---
title: "Deshabilitar la publicaci&#243;n y la distribuci&#243;n | Microsoft Docs"
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
  - "deshabilitar la publicación"
  - "publicar [replicación de SQL Server], deshabilitar"
  - "distribución, deshabilitar [replicación de SQL Server]"
  - "quitar la replicación"
  - "replicación [SQL Server], eliminar"
  - "deshabilitar la replicación"
  - "deshabilitar la distribución"
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Deshabilitar la publicaci&#243;n y la distribuci&#243;n
  En este tema se describe cómo deshabilitar la publicación y la distribución en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 Puede hacer lo siguiente:  
  
-   Eliminar todas las bases de datos del distribuidor.  
  
-   Deshabilitar todos los publicadores que utilizan el distribuidor y eliminar todas las publicaciones en esos publicadores.  
  
-   Eliminar todas las suscripciones a las publicaciones. Los datos de las bases de datos de publicaciones y de suscripciones no se eliminarán; sin embargo, pierden su relación de sincronización con todas las bases de datos de publicaciones. Si desea eliminar los datos del suscriptor, debe hacerlo de forma manual.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
-   **Para deshabilitar la publicación y la distribución con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para deshabilitar la publicación y la distribución, todas las bases de datos de distribución y de publicaciones deben estar en línea. Si existe alguna *instantánea de base de datos* para las bases de datos de distribución o de publicaciones, deben quitarse antes de deshabilitar la publicación y distribución. Una instantánea de base de datos es una copia de solo lectura sin conexión de una base de datos y no está relacionada con una instantánea de replicación. Para obtener más información, consulte [instantáneas de base de datos & #40; SQL Server & #41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Deshabilite la publicación y la distribución con el Asistente para deshabilitar la publicación y distribución.  
  
#### Para deshabilitar la publicación y la distribución  
  
1.  Conéctese al publicador o el distribuidor que desea deshabilitar en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo de servidor.  
  
2.  Haga clic en el **replicación** carpeta y, a continuación, haga clic en **Deshabilitar la publicación y distribución**.  
  
3.  Siga todos los pasos del Asistente para deshabilitar la publicación y distribución.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede deshabilitarse la publicación y la distribución mediante programación con los procedimientos almacenados de la replicación.  
  
#### Para deshabilitar la publicación y la distribución  
  
1.  Detenga todos los trabajos relacionados con replicación. Para obtener una lista de nombres de tarea, vea la sección "Seguridad de agentes con el Agente SQL Server" de [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
2.  En cada suscriptor en la base de datos de suscripción, ejecute [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para quitar objetos de replicación de la base de datos. Este procedimiento almacenado no quitará los trabajos de replicación del distribuidor.  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para quitar objetos de replicación de la base de datos.  
  
4.  Si el publicador utiliza un distribuidor remoto, ejecute [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md).  
  
5.  En el distribuidor, ejecute [sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md). Este procedimiento almacenado se debería ejecutar una vez para cada publicador registrado en el distribuidor.  
  
6.  En el distribuidor, ejecute [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) para eliminar la base de datos de distribución. Este procedimiento almacenado se debería ejecutar una vez para cada base de datos de distribución en el distribuidor. Esto también quita cualquier trabajo del Agente de lectura de cola asociado a la base de datos de distribución.  
  
7.  En el distribuidor, ejecute [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) para quitar la designación del distribuidor del servidor.  
  
    > [!NOTE]  
    >  Si no se quitan todos los objetos de publicación y distribución de replicación antes de ejecutar [sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md) y [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md), estos procedimientos, se devolverá un error. Para quitar todos los relacionados con la replicación de objetos cuando se quita un publicador o distribuidor, el **@no_checks** parámetro debe establecerse en **1**. Si un publicador o distribuidor está sin conexión o no está disponible, el **@ignore_distributor** establecido en **1** para que puedan quitarse; sin embargo, cualquier publicación y distribución de objetos que se quedan atrás deben quitarse manualmente.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este script de ejemplo quita los objetos de replicación de la base de datos de suscripciones.  
  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_1.sql)]  
  
 Este script de ejemplo deshabilita la publicación y la distribución en un servidor que sea publicador y distribuidor, y quita la base de datos de distribución.  
  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
  
#### Para deshabilitar la publicación y la distribución  
  
1.  Quite todas las suscripciones a las publicaciones que usan el Distribuidor. Para obtener más información, consulte [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md) y [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md).  
  
2.  Quite todas las publicaciones que usan el Distribuidor y deshabilite la publicación para todas las bases de datos si el Publicador y el Distribuidor están en el mismo servidor. Para más información, consulte [Delete a Publication](../../relational-databases/replication/publish/delete-a-publication.md).  
  
3.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
4.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.DistributionPublisher> clase. Especifique el <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> propiedad y pase el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto del paso 3.  
  
5.  (Opcional) Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto y compruebe que existe el publicador. Si este método devuelve **false**, el nombre del Publicador establecido en el paso 4 era incorrecto o este Distribuidor no usa el Publicador.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> método. Pase un valor de **true** para *force* si el Publicador y el Distribuidor están en servidores diferentes, y cuando el Publicador se debería desinstalar en el Distribuidor sin comprobar primero que las publicaciones ya no existen en el Publicador.  
  
7.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase. Pasar el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto del paso 3.  
  
8.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> método. Pase un valor de **true** para que *force* quite todos los objetos de replicación en el Distribuidor sin comprobar primero que todas las bases de datos de publicación locales se han deshabilitado y se han desinstalado las bases de datos de distribución.  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 Este ejemplo quita el registro del Publicador en el Distribuidor, coloca la base de datos de distribución y desinstala el Distribuidor.  
  
 [!code-csharp[HowTo#rmo_DropDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 Este ejemplo desinstala el Distribuidor sin deshabilitar primero las bases de datos de publicación locales o quitar la base de datos de distribución.  
  
 [!code-csharp[HowTo#rmo_DropDistPubForce](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## Vea también  
 [Conceptos de los Replication Management Objects (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  