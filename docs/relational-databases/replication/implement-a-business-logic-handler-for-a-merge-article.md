---
title: "Implementar un controlador de l&#243;gica de negocios para un art&#237;culo de mezcla | Microsoft Docs"
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
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], controladores de lógica de negocios"
  - "controladores de lógica de negocios de replicación de mezcla [replicación de SQL Server]"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
  - "controladores de lógica de negocios [replicación de SQL Server]"
  - "BusinessLogicModule, clase"
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Implementar un controlador de l&#243;gica de negocios para un art&#237;culo de mezcla
  En este tema se describe cómo implementar un controlador de lógica de negocios para un artículo de mezcla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante programación de la replicación o Replication Management Objects (RMO).  
  
 El <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> espacio de nombres implementa una interfaz que permite escribir lógica de negocios compleja para controlar los eventos que se producen durante el proceso de sincronización de replicación de mezcla. El proceso de la replicación puede invocar los métodos en el controlador de lógica de negocios para cada fila cambiada que se replica durante la sincronización.  
  
 El proceso general para implementar un controlador de lógica de negocios es:  
  
1.  Cree el ensamblado del controlador de lógica de negocios.  
  
2.  Registre el ensamblado en el distribuidor.  
  
3.  Implemente el ensamblado en el servidor en el que se ejecuta el Agente de mezcla. Para una suscripción de extracción, el agente se ejecuta en el suscriptor y, para una suscripción de inserción, se ejecuta en el distribuidor. Al usar la sincronización web, el agente se ejecuta en el servidor web.  
  
4.  Cree un artículo que use el controlador de lógica de negocios, o bien modifique un artículo existente para usar dicho controlador.  
  
 El controlador de lógica de negocios especificado se ejecuta para cada fila que se sincroniza. La lógica compleja y las llamadas a otras aplicaciones o servicios de red pueden afectar al rendimiento. Para obtener más información acerca de los controladores de lógica de negocios, consulte [ejecutar lógica de negocios durante la sincronización mezcla](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 **En este tema**  
  
-   **Para implementar un controlador de lógica de negocios para un artículo de mezcla con:**  
  
     [Programación de la replicación](#ReplProg)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="ReplProg"></a> Usar programación de la replicación  
  
#### Para crear e implementar un controlador de lógica de negocios  
  
1.  En Visual Studio [!INCLUDE[msCoName](../../includes/msconame-md.md)] , cree un nuevo proyecto para el ensamblado .NET que contenga el código que implementa el controlador de lógica de negocios.  
  
2.  Agregue referencias al proyecto para los siguientes espacios de nombres.  
  
    |Referencia de ensamblado|Ubicación|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (instalación predeterminada)|  
    |<xref:System.Data>|GAC (componente de .NET Framework)|  
    |<xref:System.Data.Common>|GAC (componente de .NET Framework)|  
  
3.  Agregar una clase que reemplaza el <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> clase.  
  
4.  Implemente el <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> propiedad para indicar los tipos de cambios que se controlan.  
  
5.  Reemplazar uno o varios de los métodos siguientes de la <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> clase:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> -se invoca cuando se confirma un cambio de datos durante la sincronización.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> -se invoca cuando se produce un error cuando una instrucción DELETE es que se ha cargado o descargado.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> -invocada cuando instrucciones DELETE se cargan o descargan.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> -se invoca cuando se produce un error cuando una instrucción INSERT es que se ha cargado o descargado.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> -invocada cuando instrucciones INSERT se cargan o descargan.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> -se invoca cuando se producen las instrucciones UPDATE en el publicador y el suscriptor.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> -se invoca cuando las instrucciones UPDATE entran en conflicto con las instrucciones DELETE en el publicador y el suscriptor.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> -se invoca cuando se produce un error cuando una instrucción UPDATE es que se ha cargado o descargado.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> -invocada cuando instrucciones UPDATE se cargan o descargan.  
  
6.  Genere el proyecto para crear el ensamblado del controlador de lógica de negocios.  
  
7.  Implemente el ensamblado en el directorio que contiene el archivo ejecutable del Agente de mezcla (replmerg.exe), que para una instalación predeterminada es [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM, o bien instálelo en la caché de ensamblados global (GAC) de .NET. Solo debe instalar el ensamblado en la GAC si las aplicaciones distintas del Agente de mezcla requieren acceso al ensamblado. Puede instalar el ensamblado en la GAC mediante la herramienta caché Global de ensamblados (**Gacutil.exe)** proporcionadas en .NET Framework SDK.  
  
    > [!NOTE]  
    >  Un controlador de lógica de negocios se debe implementar en cada servidor en el que se ejecute el Agente de mezcla, que incluye el servidor IIS que hospeda replisapi.dll al usar la sincronización web.  
  
#### Para registrar un controlador de lógica de negocios  
  
1.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) Para comprobar que el ensamblado no ya se registró como un controlador de lógica de negocios.  
  
2.  En el distribuidor, ejecute [sp_registercustomresolver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), especificando un nombre descriptivo para el controlador de lógica de negocios para **@article_resolver**, un valor de **true** para **@is_dotnet_assembly**, el nombre del ensamblado de **@dotnet_assembly_name**, y el nombre completo de la clase que reemplaza <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> de **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Si el ensamblado no está implementado en el mismo directorio que el ejecutable del agente de mezcla, en el mismo directorio que la aplicación que inicia de forma sincrónica el agente de mezcla o en la caché de ensamblados global (GAC), debe especificar la ruta de acceso completa con el nombre de ensamblado para **@dotnet_assembly_name**. Al usar la sincronización web, debe especificar la ubicación de ensamblado en el servidor web.  
  
#### Para usar un controlador de lógica de negocios con un nuevo artículo de tabla  
  
1.  Ejecutar [sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir un artículo, especificando el nombre descriptivo del controlador de lógica de negocios de **@article_resolver**. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para usar un controlador de lógica de negocios con un artículo de tabla existente  
  
1.  Ejecutar [sp_changemergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, un valor de **article_resolver** para **@property**, y el nombre descriptivo del controlador de lógica de negocios de **@value**.  
  
###  <a name="TsqlExample"></a> Ejemplos (programación de la replicación)  
 Este ejemplo muestra un controlador de lógica de negocios que crea un registro de auditoría.  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 El ejemplo siguiente registra un ensamblado de controlador de lógica de negocios en el distribuidor y cambia un artículo de mezcla existente para usar esta lógica empresarial personalizada.  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../relational-databases/replication/codesnippet/tsql/implement-a-business-log_3.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
  
#### Para crear un controlador de lógica de negocios  
  
1.  En Visual Studio [!INCLUDE[msCoName](../../includes/msconame-md.md)] , cree un nuevo proyecto para el ensamblado .NET que contenga el código que implementa el controlador de lógica de negocios.  
  
2.  Agregue referencias al proyecto para los siguientes espacios de nombres.  
  
    |Referencia de ensamblado|Ubicación|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (instalación predeterminada)|  
    |<xref:System.Data>|GAC (componente de .NET Framework)|  
    |<xref:System.Data.Common>|GAC (componente de .NET Framework)|  
  
3.  Agregar una clase que reemplaza el <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> clase.  
  
4.  Implemente el <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> propiedad para indicar los tipos de cambios que se controlan.  
  
5.  Reemplazar uno o varios de los métodos siguientes de la <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> clase:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> -se invoca cuando se confirma un cambio de datos durante la sincronización.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> -invoca si se produce un error mientras una instrucción DELETE se cargan o descargan.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> -invocada cuando instrucciones DELETE se cargan o descargan.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> -invoca si se produce un error cuando una instrucción INSERT es que se ha cargado o descargado.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> -invocada cuando instrucciones INSERT se cargan o descargan.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> -se invoca cuando se producen las instrucciones UPDATE en el publicador y el suscriptor.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> -se invoca cuando las instrucciones UPDATE entran en conflicto con las instrucciones DELETE en el publicador y el suscriptor.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> -invoca si se produce un error cuando una instrucción UPDATE es que se ha cargado o descargado.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> -invocada cuando instrucciones UPDATE se cargan o descargan.  
  
    > [!NOTE]  
    >  El solucionador predeterminado del artículo administra los conflictos de artículo que no controle explícitamente la lógica de negocios personalizada.  
  
6.  Genere el proyecto para crear el ensamblado del controlador de lógica de negocios.  
  
#### Para registrar un controlador de lógica de negocios  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase. Pasar el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
3.  Llame a <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A> y compruebe el valor devuelto <xref:System.Collections.ArrayList> objeto para asegurarse de que el ensamblado no ya se registró como un controlador de lógica de negocios.  
  
4.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler> clase. Especifique las propiedades siguientes:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> -el nombre del ensamblado. NET. Si el ensamblado no está implementado en el mismo directorio que el ejecutable del Agente de mezcla, en el mismo directorio que la aplicación que inicia de forma sincrónica dicho agente o en la GAC, debe incluir la ruta de acceso completa con el nombre del ensamblado. Debe incluir la ruta de acceso completa con el nombre del ensamblado al usar un controlador de lógica de negocios con la sincronización web.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> -el nombre completo de la clase que reemplaza <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> e implementa el controlador de lógica de negocios.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> -un nombre descriptivo que se utiliza cuando se tiene acceso el controlador de lógica de negocios.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> -un valor de **true**.  
  
#### Para implementar un controlador de lógica de negocios  
  
1.  Implemente el ensamblado en el servidor donde se ejecuta el Agente de mezcla, en la ubicación del archivo especificada cuando el controlador de lógica de negocios se registró en el distribuidor. Para una suscripción de extracción, el agente se ejecuta en el suscriptor y, para una suscripción de inserción, se ejecuta en el distribuidor. Al usar la sincronización web, el agente se ejecuta en el servidor web. Si la ruta de acceso completa no estuviera incluida con el nombre del ensamblado cuando se registró el controlador de lógica de negocios, implemente el ensamblado en el mismo directorio como el ejecutable del Agente de mezcla, en el mismo directorio que la aplicación que inicia sincrónicamente dicho agente. Puede instalar el ensamblado en la GAC si hay varias aplicaciones que usen el mismo ensamblado.  
  
#### Para usar un controlador de lógica de negocios con un nuevo artículo de tabla  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeArticle> clase. Establezca las siguientes propiedades:  
  
    -   El nombre del artículo para <xref:Microsoft.SqlServer.Replication.Article.Name%2A>.  
  
    -   El nombre de la publicación para <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>.  
  
    -   El nombre de la base de datos de publicación para <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>.  
  
    -   El nombre descriptivo del controlador de lógica de negocios (<xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>) para <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.Article.Create%2A> método. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para usar un controlador de lógica de negocios con un artículo de tabla existente  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeArticle> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, y <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, se definieron incorrectamente las propiedades de artículo en el paso 3, o bien el artículo no existe. Para más información, consulte [View and Modify Article Properties](../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
6.  Establecer el nombre descriptivo del controlador de lógica de negocios de <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>. Este es el valor de la <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> propiedad especificada al registrar el controlador de lógica de negocios.  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 En este ejemplo se muestra un controlador de lógica de negocios que registra información acerca de inserciones, actualizaciones y eliminaciones en el suscriptor.  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 Este ejemplo registra el controlador de lógica de negocios en el distribuidor.  
  
 [!code-csharp[HowTo#rmo_RegisterBLH_10](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 Este ejemplo cambia un artículo existente para usar el controlador de lógica de negocios.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## Vea también  
 [Implementar un solucionador de conflictos personalizado para un artículo de mezcla](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [Depurar un controlador de lógica de negocios & #40; Programación de la replicación y nº 41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Conceptos de los Replication Management Objects (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  