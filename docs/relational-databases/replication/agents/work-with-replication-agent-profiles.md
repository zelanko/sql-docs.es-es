---
title: "Trabajar con perfiles del Agente de replicaci&#243;n | Microsoft Docs"
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
  - "replicación [SQL Server], agentes y perfiles"
  - "perfiles de agente de replicación [SQL Server]"
  - "agentes [replicación de SQL Server], perfiles"
  - "perfiles [SQL Server], agentes de replicación"
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 49
---
# Trabajar con perfiles del Agente de replicaci&#243;n
  En este tema, se describe cómo trabajar con perfiles de agente de replicación en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). El comportamiento de cada agente de replicación está controlado por un conjunto de parámetros que se pueden establecer a través de perfiles de agente. Cada agente tiene un perfil predeterminado y algunos tienen perfiles adicionales predefinidos; solo hay un perfil activo para un agente en cada momento.  
  
 **En este tema**  
  
-   **Para trabajar con perfiles de agente de replicación con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   Obtener acceso al cuadro de diálogo Perfiles de agente  
  
    -   Especificar un perfil para un agente  
  
    -   Crear un perfil  
  
    -   Modificar un perfil  
  
    -   Eliminar un perfil  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   Crear un perfil  
  
    -   Modificar un perfil  
  
    -   Eliminar un perfil  
  
    -   Usar perfiles de agente durante la sincronización  
  
    -   Ejemplo de Transact-SQL  
  
     [Replication Management Objects](#RMOProcedure)  
  
    -   Crear un perfil  
  
    -   Modificar un perfil  
  
    -   Eliminar un perfil  
  
-   **Seguimiento:**  [después de cambiar los parámetros de agente](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> Para obtener acceso al cuadro de diálogo Perfiles de agente en SQL Server Management Studio  
  
1.  En la **General** página de la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo, haga clic en **valores predeterminados de perfil**.  
  
#### Para obtener acceso al cuadro de diálogo Perfiles de agente en el Monitor de replicación  
  
-   Para abrir el cuadro de diálogo para todos los agentes, haga clic en un publicador y, a continuación, haga clic en **perfiles de agente**.  
  
-   Para abrir el cuadro de diálogo para un solo agente:  
  
    1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
    2.  Para los perfiles de agente de distribución y agente de mezcla, haga clic en una suscripción en el **todas las suscripciones** y, a continuación, haga clic en **perfil del agente**. Para otros agentes, haga clic en el agente en el **agentes** y, a continuación, haga clic en **perfil del agente**.  
  
###  <a name="Specify_SSMS"></a> Para especificar un perfil para un agente  
  
1.  Si el cuadro de diálogo **Perfiles de agente** muestra perfiles para varios agentes, seleccione un agente.  
  
2.  Seleccione un perfil en la columna **Predeterminado para nuevos** de la cuadrícula **Perfiles de agente** . De forma predeterminada, el perfil solamente se aplica a los agentes para las publicaciones y suscripciones nuevas.  
  
3.  Para especificar que utilicen el perfil todos los agentes del tipo seleccionado para las publicaciones o suscripciones existentes, haga clic en **Cambiar agentes existentes**.  
  
###  <a name="Modify_SSMS"></a> Para ver y modificar los parámetros asociados con un perfil  
  
1.  Si el cuadro de diálogo **Perfiles de agente** muestra perfiles para varios agentes, seleccione un agente.  
  
2.  Haga clic en el botón de propiedades (**...**) junto a un perfil.  
  
3.  Ver los parámetros y valores en el **\< nombreDePerfil> Propiedades de perfil** cuadro de diálogo.  
  
    -   Los parámetros de los perfiles definidos por el usuario se pueden modificar, a diferencia de los parámetros de los perfiles predefinidos del sistema, que no se pueden modificar.  
  
    -   Para ver todos los parámetros de un agente, desactive la casilla **Mostrar solamente los parámetros utilizados en este perfil** . Para obtener información acerca de los parámetros de agentes, vea los vínculos que aparecen al final de este tema.  
  
4.  Haga clic en **Cerrar**.  
  
###  <a name="Create_SSMS"></a> Para crear un perfil definido por el usuario  
  
1.  Si el cuadro de diálogo **Perfiles de agente** muestra perfiles para varios agentes, seleccione un agente.  
  
2.  Haga clic en **Nueva**.  
  
3.  En el cuadro de diálogo de inicialización **Nuevo perfil de agente** , seleccione el perfil existente en el que desea basar el nuevo perfil.  
  
4.  En el cuadro de diálogo **Nuevo perfil de agente** , escriba valores en los cuadros de texto **Nombre** y **Descripción** .  
  
5.  Modifique los parámetros para personalizar el perfil. Para ver todos los parámetros de un agente, desactive la casilla **Mostrar solamente los parámetros utilizados en este perfil** . Para obtener información acerca de los parámetros de agentes, vea los vínculos que aparecen al final de este tema.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> Para eliminar un perfil definido por el usuario  
  
1.  Si el cuadro de diálogo **Perfiles de agente** muestra perfiles para varios agentes, seleccione un agente.  
  
2.  Si un perfil está asociado con uno o más agentes, cambie el perfil para esos agentes:  
  
    1.  Seleccione un perfil distinto en la cuadrícula **Perfiles de agente** .  
  
    2.  Haga clic en **Cambiar agentes existentes**.  
  
        > [!NOTE]  
        >  Al hacer esto, cambiará el perfil de todos los agentes del tipo seleccionado para las publicaciones y suscripciones existentes, y no solo de los que usen el perfil que desea eliminar.  
  
3.  Seleccione el perfil que desea eliminar y haga clic en **Eliminar**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
###  <a name="Create_tsql"></a> Para crear un nuevo perfil de agente  
  
1.  En el distribuidor, ejecute [sp_add_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md). Especifique **@name**, un valor de **1** para **@profile_type**, y uno de los siguientes valores para **@agent_type**:  
  
    -   **1** - [agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [el agente de lector del registro de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de replicación de mezcla](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [agente de lector de cola de duplicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     Si este perfil se va a convertir en el nuevo perfil predeterminado para su tipo de agente de replicación, especifique el valor **1** en **@default**. Se devuelve el identificador del nuevo perfil utilizando la **@profile_id** parámetro de salida. De esta forma crea un nuevo perfil con un conjunto de parámetros de perfil basados en el perfil predeterminado del tipo de agente indicado.  
  
2.  Una vez creado el nuevo perfil, agregue, quite o modifique los parámetros predeterminados para personalizarlo.  
  
###  <a name="Modify_tsql"></a> Para modificar un perfil de agente existente  
  
1.  En el distribuidor, ejecute [sp_help_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique uno de los siguientes valores para **@agent_type**:  
  
    -   **1** - [agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [el agente de lector del registro de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de replicación de mezcla](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [agente de lector de cola de duplicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     De esta forma se devuelven todos los perfiles del tipo de agente especificado. Tenga en cuenta el valor de **profile_id** el conjunto de resultados cambiar el perfil.  
  
2.  En el distribuidor, ejecute [sp_help_agent_parameter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md). Especifique el identificador de perfil del paso 1 para **@profile_id**. De esta forma se devuelven todos los parámetros del perfil. Anote el nombre de cualquier parámetro que desee modificar o quitar del perfil.  
  
3.  Para cambiar el valor de un parámetro en un perfil, ejecute [sp_change_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md). Especifique el identificador de perfil del paso 1 para **@profile_id**, el nombre del parámetro que se va a cambiar para **@property**, y un nuevo valor para el parámetro **@value**.  
  
    > [!NOTE]  
    >  No puede cambiar un perfil de agente existente para convertirlo en el perfil predeterminado de un agente. Debe crear un nuevo perfil como perfil predeterminado, como se muestra en el procedimiento anterior.  
  
4.  Para quitar un parámetro de un perfil, ejecute [sp_drop_agent_parameter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md). Especifique el identificador de perfil del paso 1 para **@profile_id** y el nombre del parámetro que se va a quitar de **@parameter_name**.  
  
5.  Para agregar un nuevo parámetro a un perfil, debe hacer lo siguiente:  
  
    -   Consulta el [MSagentparameterlist & #40; Transact-SQL & #41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) tabla en el distribuidor para determinar qué parámetros de perfil se pueden establecer para cada tipo de agente.  
  
    -   En el distribuidor, ejecute [sp_add_agent_parameter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md). Especifique el identificador de perfil del paso 1 para **@profile_id**, el nombre de un parámetro válido para agregar para **@parameter_name**, y el valor del parámetro **@parameter_value**.  
  
###  <a name="Delete_tsql"></a> Para eliminar un perfil de agente  
  
1.  En el distribuidor, ejecute [sp_help_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique uno de los siguientes valores para **@agent_type**:  
  
    -   **1** - [agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [el agente de lector del registro de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de replicación de mezcla](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [agente de lector de cola de duplicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     De esta forma se devuelven todos los perfiles del tipo de agente especificado. Tenga en cuenta el valor de **profile_id** el conjunto de resultados quitar el perfil.  
  
2.  En el distribuidor, ejecute [sp_drop_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md). Especifique el identificador de perfil del paso 1 para **@profile_id**.  
  
###  <a name="Synch_tsql"></a> Para usar perfiles de agente durante la sincronización  
  
1.  En el distribuidor, ejecute [sp_help_agent_profile & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md). Especifique uno de los siguientes valores para **@agent_type**:  
  
    -   **1** - [agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [el agente de lector del registro de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [agente de replicación de mezcla](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [agente de lector de cola de duplicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     De esta forma se devuelven todos los perfiles del tipo de agente especificado. Tenga en cuenta el valor de **nombre_perfil** el conjunto de resultados utilizar el perfil.  
  
2.  Si el agente se inicia desde un trabajo del agente, modifique el paso de trabajo que inicia el agente para especificar el valor de **nombre_perfil** obtenido en el paso 1 después de la **- ProfileName** parámetro de línea de comandos. Para obtener más información, consulte [Ver y modificar parámetros de línea de comandos del agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md).  
  
3.  Al iniciar el agente desde el símbolo del sistema, especifique el valor de **nombre_perfil** obtenido en el paso 1 después de la **- ProfileName** parámetro de línea de comandos.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 Este ejemplo crea un perfil personalizado para el agente de mezcla denominado **custom_merge**, cambia el valor de la **- UploadReadChangesPerBatch** agrega un nuevo parámetro, **- ExchangeType** parámetro y devuelve información sobre el perfil que se crea.  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> Usar RMO  
  
###  <a name="Create_RMO"></a> Para crear un nuevo perfil de agente  
  
1.  Crear una conexión al distribuidor mediante una instancia de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.AgentProfile> clase.  
  
3.  Establezca las siguientes propiedades en el objeto:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -el nombre del perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> : una <xref:Microsoft.SqlServer.Replication.AgentType> valor que especifica el tipo de agente de replicación para el que se crea el perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
    -   (Opcional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> -una descripción del perfil.  
  
    -   (Opcional) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> -Establezca esta propiedad en **true** si todos los nuevos trabajos de agente para este <xref:Microsoft.SqlServer.Replication.AgentType> usará este perfil de forma predeterminada.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> método para crear el perfil en el servidor.  
  
5.  Una vez que el perfil existe en el servidor, puede personalizarlo agregando, quitando o cambiando los valores de parámetros de agente de replicación.  
  
6.  Para asignar el perfil a un trabajo del agente de replicación existente, llame a la <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> método. Pase el nombre de la base de datos de distribución para *distributionDBName* y el Id. del trabajo para *agentID*.  
  
###  <a name="Modify_RMO"></a> Para modificar un perfil de agente existente  
  
1.  Crear una conexión al distribuidor mediante una instancia de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase. Pasar el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto creado en el paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Si este método devuelve **false**, compruebe que el distribuidor existe.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> método. Pasar un <xref:Microsoft.SqlServer.Replication.AgentType> valor para reducir los perfiles devueltos a un tipo específico de agente de replicación.  
  
5.  Obtener el deseado <xref:Microsoft.SqlServer.Replication.AgentProfile> objeto devuelto <xref:System.Collections.ArrayList>, donde el <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> propiedad del objeto coincide con el nombre del perfil.  
  
6.  Llame a uno de los siguientes métodos de <xref:Microsoft.SqlServer.Replication.AgentProfile> para cambiar el perfil:  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> -agrega un parámetro compatible al perfil, donde *nombre* es el nombre del parámetro del agente de replicación y *valor* es el valor especificado. Para enumerar todos los parámetros de agentes admitidos para un tipo de agente determinado, llame el <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> método. Este método devuelve un <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> objetos que representan todos los parámetros compatibles.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> -quita un parámetro existente del perfil, donde *nombre* es el nombre del parámetro del agente de replicación. Para enumerar todos los parámetros de agente actuales definidos para el perfil, llame el <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> método. Este método devuelve un <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> objetos que representan el parámetro existente para este perfil.  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> -cambia el valor de un parámetro existente en el perfil, donde *nombre* es el nombre del parámetro del agente y *newValue* es el valor al que se está cambiando el parámetro. Para enumerar todos los parámetros de agente actuales definidos para el perfil, llame el <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> método. Este método devuelve un <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> objetos que representan el parámetro existente para este perfil. Para enumerar todos admite la configuración de parámetros de agente, llame a la <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> método. Este método devuelve un <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> objetos que representan los valores admitidos para todos los parámetros.  
  
###  <a name="Delete_RMO"></a> Para eliminar un perfil de agente  
  
1.  Crear una conexión al distribuidor mediante una instancia de la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.AgentProfile> clase. Establecer el nombre del perfil para <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> y <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Si este método devuelve **false**, significa que el nombre especificado era incorrecto o el perfil no existe en el servidor.  
  
4.  Compruebe que la <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> propiedad está establecida en <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, lo que indica un perfil de cliente. No debería quitar un perfil que tiene un valor de <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> para <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> método para quitar el perfil definido por el usuario representado por este objeto desde el servidor.  
  
##  <a name="FollowUp"></a> Seguimiento: después de cambiar los parámetros de agente  
 Los cambios en los parámetros del agente tendrán efecto la próxima vez que se inicie el agente. Si el agente se ejecuta sin interrupción, debe detenerlo y reiniciarlo.  
  
## Vea también  
 [Perfiles del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Agente de registro del LOG de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de mezcla de replicación](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  