---
title: "Ver y modificar la configuraci&#243;n de seguridad de la replicaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modificar la configuración de seguridad de la replicación"
  - "replicación [SQL Server], seguridad"
  - "seguridad [replicación de SQL Server], ver configuración"
  - "ver la configuración de seguridad de la replicación"
  - "seguridad [replicación de SQL Server], modificar configuración"
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Ver y modificar la configuraci&#243;n de seguridad de la replicaci&#243;n
  En este tema se describe cómo ver y modificar la configuración de seguridad de la replicación en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). Por ejemplo, puede que desee cambiar la conexión del Agente de registro del LOG al publicador de la autenticación de SQL Server a la autenticación de Windows integrada, o puede que necesite cambiar las credenciales utilizadas para ejecutar un trabajo de agente cuando la contraseña de la cuenta de Windows ha cambiado. Para obtener información acerca de los permisos requeridos por cada agente, consulte [modelo de seguridad del agente de replicación](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para ver y modificar la configuración de seguridad de la replicación con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
-   **Seguimiento:**  [después de modificar la configuración de seguridad de la replicación](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los procedimientos almacenados que se usen dependerán del tipo de agente y del tipo de conexión al servidor.  
  
-   Las propiedades y clases RMO que utilice dependerán dependen del tipo de agente y el tipo de conexión al servidor.  
  
###  <a name="Security"></a> Seguridad  
 Por razones de seguridad, los valores reales de las contraseñas se enmascaran en los conjuntos de resultados devueltos por los procedimientos almacenados de replicación.  
  
####  <a name="Permissions"></a> Permisos  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Vea y modifique la configuración de seguridad en los siguientes cuadros de diálogo:  
  
1.  El cuadro de diálogo **Actualizar contraseñas de replicación** , que está disponible en la carpeta **Replicación** de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Si cambia la contraseña de una cuenta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de Windows en un servidor de una topología de replicación, utilice este cuadro de diálogo después de actualizar la contraseña para cada agente que utilice la cuenta. Si agentes de varios servidores utilizan la misma cuenta, debe conectarse a cada servidor y cambiar la contraseña. La contraseña se actualiza en todos los lugares en los que la replicación utiliza la contraseña. La contraseña no se actualiza en otros lugares, como los servidores vinculados.  
  
2.  El **seguridad del agente** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
3.  El **Propiedades de suscripción - \< suscripción>** cuadro de diálogo. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, vea [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
4.  El **Propiedades del distribuidor: \< distribuidor>** y **Propiedades de la base de datos de distribución: \< base de datos>** cuadros de diálogo. Para obtener más información acerca de cómo obtener acceso a estos cuadros de diálogo, vea [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
5.  El **Propiedades del publicador: \< publicador>** cuadro de diálogo. Para obtener más información acerca de cómo obtener acceso a este cuadro de diálogo, [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
#### Para cambiar la contraseña de una cuenta utilizada por uno o varios agentes  
  
1.  Si se trata de una cuenta de SQL Server, este cuadro de diálogo también cambia la contraseña de dicha cuenta. Si es una cuenta de Windows, cambie primero la contraseña en Windows. Para obtener más información, consulte la documentación de Windows.  
  
    > [!NOTE]  
    >  Después de cambiar una contraseña de replicación, es necesario detener y reiniciar cada agente que utilice la contraseña para que el cambio surta efecto en dicho agente.  
  
2.  Conéctese al servidor en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo de servidor.  
  
3.  Haga clic en el **replicación** carpeta y, a continuación, haga clic en **Actualizar contraseñas de replicación**.  
  
4.  En el cuadro de diálogo **Actualizar contraseñas de replicación** , especifique la cuenta y la contraseña nueva.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la configuración de seguridad del Agente de instantáneas  
  
1.  En la **seguridad del agente** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en el **configuración de seguridad** situado junto a la **agente de instantáneas** cuadro de texto.  
  
2.  En el cuadro de diálogo **Seguridad del Agente de instantáneas** , especifique la cuenta con la que debe ejecutarse el agente:  
  
    -   Indique una nueva cuenta de Windows en el cuadro de texto **Cuenta del agente** .  
  
    -   Escriba una nueva contraseña en los cuadros de texto **Contraseña** y **Confirmar contraseña** .  
  
3.  Especifique el contexto en el que el agente deberá conectarse del distribuidor al publicador. Si selecciona **Mediante el siguiente inicio de sesión de SQL Server**, deberá especificar también el inicio de sesión:  
  
    -   Indique un inicio de sesión en el cuadro de texto **Inicio de sesión** .  
  
    -   Escriba una nueva contraseña en los cuadros de texto **Contraseña** y **Confirmar contraseña** .  
  
    > [!NOTE]  
    >  Si el publicador es un publicador de Oracle, el contexto de conexión se especifica en la **Propiedades del distribuidor: \< distribuidor>**cuadro de diálogo. Vea el procedimiento para cambiar el contexto más adelante en este tema.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la configuración de seguridad del Agente de registro del LOG  
  
1.  En la **seguridad del agente** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en el **configuración de seguridad** situado junto a la **Agente lector del registro** cuadro de texto.  
  
2.  En el cuadro diálogo **Seguridad del Agente de registro del LOG** , especifique la cuenta con la que debe ejecutarse el agente:  
  
    -   Indique una nueva cuenta de Windows en el cuadro de texto **Cuenta del agente** .  
  
    -   Escriba una nueva contraseña en los cuadros de texto **Contraseña** y **Confirmar contraseña** .  
  
3.  Especifique el contexto en el que el agente deberá conectarse del distribuidor al publicador. Si selecciona **Mediante el siguiente inicio de sesión de SQL Server**, deberá especificar también el inicio de sesión:  
  
    -   Indique un inicio de sesión en el cuadro de texto **Inicio de sesión** .  
  
    -   Escriba una nueva contraseña en los cuadros de texto **Contraseña** y **Confirmar contraseña** .  
  
    > [!NOTE]  
    >  Si el publicador es un publicador de Oracle, el contexto de conexión se especifica en la **Propiedades del distribuidor: \< distribuidor>**cuadro de diálogo. Cambie el contexto siguiendo el procedimiento que se indica a continuación.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Existe un Agente de registro del LOG para cada base de datos publicada. El cambio de la configuración de seguridad del agente de una publicación afecta a la configuración de todas las publicaciones de la base de datos.  
  
#### Para cambiar el contexto en el que el Agente de instantáneas y el Agente de registro del LOG para una publicación de Oracle realizan las conexiones con el publicador  
  
1.  En el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** diálogo cuadro, haga clic en el botón de propiedades (**...**) junto a un publicador.  
  
2.  En la sección **Conexión del agente al publicador** , especifique el inicio de sesión y la contraseña utilizados por el esquema de usuario administrativo de replicación que ha configurado. Para obtener más información, consulte [configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la configuración de seguridad del Agente de distribución para una suscripción de inserción  
  
1.  En la **Propiedades de suscripción - \< suscripción>** cuadro de diálogo en el publicador, puede realizar los siguientes cambios:  
  
    -   Para cambiar la cuenta bajo la que el agente de distribución se ejecuta y realiza conexiones al distribuidor, haga clic en la **cuenta de proceso del agente** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique una cuenta y una contraseña en el cuadro de diálogo **Seguridad del Agente de distribución** .  
  
    -   Para cambiar el contexto en el que el agente de distribución se conecta al suscriptor, haga clic en el **conexión de suscriptor** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique el contexto en el cuadro de diálogo **Escribir información de conexión** .  
  
         Si utiliza suscripciones de actualización en cola, el Agente de lectura de cola utiliza también el contexto especificado aquí para las conexiones al suscriptor.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la configuración de seguridad del Agente de distribución para una suscripción de extracción  
  
1.  En la **Propiedades de suscripción - \< suscripción>** cuadro de diálogo en el suscriptor, puede realizar los siguientes cambios:  
  
    -   Para cambiar la cuenta bajo la que el agente de distribución se ejecuta y realiza conexiones al suscriptor, haga clic en la **cuenta de proceso del agente** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique una cuenta y una contraseña en el cuadro de diálogo **Seguridad del Agente de distribución** .  
  
         Si utiliza suscripciones de actualización en cola, el Agente de lectura de cola utiliza también el contexto especificado aquí para las conexiones al suscriptor.  
  
    -   Para cambiar el contexto en el que el agente de distribución se conecta al distribuidor, haga clic en el **conexión del distribuidor** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique el contexto en el cuadro de diálogo **Escribir información de conexión** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la configuración de seguridad del Agente de mezcla para una suscripción de inserción  
  
1.  En la **Propiedades de suscripción - \< suscripción>** cuadro de diálogo en el publicador, puede realizar los siguientes cambios:  
  
    -   Para cambiar la cuenta bajo la que el agente de mezcla se ejecuta y realiza conexiones al publicador y distribuidor, haga clic en la **cuenta de proceso del agente** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique una cuenta y una contraseña en el cuadro de diálogo **Seguridad del Agente de mezcla** .  
  
    -   Para cambiar el contexto en el que el agente de mezcla se conecta al suscriptor, haga clic en el **conexión de suscriptor** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique el contexto en el cuadro de diálogo **Escribir información de conexión** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la configuración de seguridad del Agente de mezcla para una suscripción de extracción  
  
1.  En la **Propiedades de suscripción - \< suscripción>** cuadro de diálogo en el suscriptor, puede realizar los siguientes cambios:  
  
    -   Para cambiar la cuenta bajo la que el agente de mezcla se ejecuta y realiza conexiones al suscriptor, haga clic en la **cuenta de proceso del agente** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique una cuenta y una contraseña en el cuadro de diálogo **Seguridad del Agente de mezcla** .  
  
    -   Para cambiar el contexto en el que el agente de mezcla se conecta al publicador y distribuidor, haga clic en el **conexión de publicador** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila. Especifique el contexto en el cuadro de diálogo **Escribir información de conexión** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para cambiar la cuenta con la que se ejecuta el Agente de lectura de cola  
  
1.  En la **General** página de la **Propiedades del distribuidor: \< distribuidor>** diálogo cuadro, haga clic en las propiedades (**...**) botón situado junto a la base de datos de distribución.  
  
2.  En la **Propiedades de la base de datos de distribución: \< base de datos>** cuadro de diálogo, haga clic en el **configuración de seguridad** situado junto a la **cuenta de proceso del agente** cuadro de texto.  
  
3.  En el cuadro diálogo **Seguridad del Agente de lectura de cola** , especifique la cuenta con la que el agente debe ejecutarse y realizar conexiones al distribuidor:  
  
    -   Indique una nueva cuenta de Windows en el cuadro de texto **Cuenta de proceso** .  
  
    -   Escriba una nueva contraseña en los cuadros de texto **Contraseña** y **Confirmar contraseña** .  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Existe un Agente de lectura de cola para cada base de datos de distribución. El cambio de la configuración de seguridad del agente afecta a la configuración de todas las publicaciones de todos los publicadores que usan esta base de datos de distribución.  
  
#### Para cambiar el contexto en el que el Agente de lectura de cola realiza conexiones al publicador  
  
1.  En el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** diálogo cuadro, haga clic en el botón de propiedades (**...**) situado junto al publicador.  
  
2.  En la sección **Conexión del agente al publicador** , especifique el valor **Suplantar la cuenta de proceso del agente** o **autenticación de SQL Server** para la opción **Modo de conexión del agente** . Si especifica **Autenticación de SQL Server**, indique también valores para **Inicio de sesión** y **Contraseña**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Existe un Agente de lectura de cola para cada base de datos de distribución. El cambio de la configuración de seguridad del agente afecta a la configuración de todas las publicaciones de todos los publicadores que usan esta base de datos de distribución.  
  
#### Para cambiar el contexto en el que el Agente de lectura de cola realiza conexiones al suscriptor  
  
-   El Agente de lectura de cola utiliza el mismo contexto de conexión que el Agente de distribución para la suscripción. Para obtener más información, vea los procedimientos descritos anteriormente para el Agente de distribución.  
  
#### Para cambiar la configuración de seguridad para una suscripción de extracción de actualización inmediata  
  
1.  En la **Propiedades de suscripción - \< suscripción>** cuadro de diálogo en el suscriptor, haga clic en el **conexión de publicador** fila y, a continuación, haga clic en las propiedades (**...**) botón de la fila.  
  
2.  En el cuadro de diálogo **Escribir información de conexión** , seleccione una de las siguientes opciones:  
  
    -   **Utilizar inicio de sesión de un servidor vinculado o remoto**. Seleccione esta opción si ha definido un servidor remoto o vinculado entre el suscriptor y el publicador mediante [sp_addserver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], u otro método.  
  
    -   **Utilizar autenticación de SQL Server con el inicio de sesión y la contraseña siguientes**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación creará un servidor vinculado. La cuenta que especifique debe existir ya en el publicador.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Este procedimiento cambia el método que los desencadenadores de replicación utilizan para conectarse del suscriptor al publicador cuando se realizan cambios en el suscriptor. También puede cambiar la configuración asociada al Agente de distribución para una suscripción de actualización inmediata. Para obtener más información, vea los procedimientos que se describen anteriormente en este tema.  
>   
>  Este procedimiento solamente se aplica a las suscripciones de extracción. Para las suscripciones de inserción, utilice el procedimiento almacenado [sp_link_publication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md).  
  
#### Para cambiar la contraseña de la conexión administrativa del publicador al distribuidor  
  
1.  En el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo, escriba una contraseña segura en el **contraseña** y **Confirmar contraseña** cuadros de texto.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  En la **General** página de la **Propiedades del publicador: \< publicador>** cuadro de diálogo, escriba una contraseña segura en el **contraseña** y **Confirmar contraseña** cuadros de texto.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
> [!IMPORTANT]  
>  En todos los procedimientos siguientes, cuando sea posible, pida a los usuarios que especifiquen las credenciales de seguridad en tiempo de ejecución. Si almacena credenciales en un archivo de script, debe proteger el archivo para evitar el acceso no autorizado.  
  
#### Para cambiar todas las instancias de una contraseña almacenada en un servidor de replicación  
  
1.  En un servidor en una topología de replicación en la base de datos maestra, ejecute [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md). Especifique la cuenta de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows o el inicio de sesión de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuya contraseña se cambia para **@login** y la nueva contraseña de cuenta o inicio de sesión para **@password**. Esto cambia cada instancia de la contraseña que usan todos los agentes del servidor al conectarse a otros servidores de la topología.  
  
    > [!NOTE]  
    >  Para cambiar solamente el inicio de sesión y la contraseña para una conexión a un servidor determinado en la topología (por ejemplo, el distribuidor o suscriptor), especifique el nombre de este servidor para **@server**.  
  
2.  Repita el paso 1 en cada servidor de la topología de replicación en el que se deba actualizar la contraseña.  
  
    > [!NOTE]  
    >  Después de cambiar una contraseña de replicación, es necesario detener y reiniciar cada agente que utilice la contraseña para que el cambio surta efecto en dicho agente.  
  
#### Para cambiar la configuración de seguridad del Agente de instantáneas  
  
1.  En el publicador, ejecute [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), especificando **@publication**. Esto devuelve la configuración de seguridad actual para el Agente de instantáneas.  
  
2.  En el publicador, ejecute [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), especificando **@publication** y uno o más de las siguientes opciones de seguridad para cambiar:  
  
    -   Para cambiar la cuenta de Windows con la que se ejecuta el agente o simplemente la contraseña para esta cuenta, especifique **@job_login** y **@job_password**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al publicador, especifique un valor de **1** o **0** para **@publisher_security_mode**.  
  
    -   Al cambiar el modo de seguridad utilizado al conectarse al publicador de **1** a **0** o cuando se cambia un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Inicio de sesión utilizado para esta conexión, especifique **@publisher_login** y **@publisher_password**.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para cambiar la configuración de seguridad del Agente de registro del LOG  
  
1.  En el publicador, ejecute [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md), especificando **@publisher**. Esto devuelve la configuración de seguridad actual para el Agente de registro del LOG.  
  
2.  En el publicador, ejecute [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md), especificando **@publication** y uno o más de las siguientes opciones de seguridad para cambiar:  
  
    -   Para cambiar la cuenta de Windows con la que se ejecuta el agente o simplemente la contraseña para esta cuenta, especifique **@job_login** y **@job_password**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al publicador, especifique un valor de **1** o **0** para **@publisher_security_mode**.  
  
    -   Al cambiar el modo de seguridad utilizado al conectarse al publicador de **1** a **0** o cuando se cambia un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Inicio de sesión utilizado para esta conexión, especifique **@publisher_login** y **@publisher_password**.  
  
    > [!NOTE]  
    >  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para cambiar la configuración de seguridad del Agente de distribución para una suscripción de inserción  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md), especificando **@publication** y **@subscriber**. Esto devuelve propiedades de suscripción, incluida la configuración de seguridad para el Agente de distribución que se ejecuta en el distribuidor.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md), especificando **@publication**, **@subscriber**, **@subscriber_db**, un valor de **todos los** para **@article**, el nombre de la propiedad de seguridad de **@property**, y el nuevo valor de la propiedad de **@value**.  
  
3.  Repita el paso 2 para cada una de las propiedades de seguridad siguientes que se vayan a cambiar:  
  
    -   Para cambiar la cuenta de Windows con la que se ejecuta el agente o simplemente la contraseña para esta cuenta, especifique un valor de **distrib_job_password** para **@property** y una nueva contraseña para **@value**. Al cambiar la propia cuenta, repita el paso 2 especificando un valor de **distrib_job_login** para **@property** y la nueva cuenta de Windows para **@value**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al suscriptor, especifique un valor de **subscriber_security_mode** para **@property** y un valor de **1** (autenticación integrada de Windows) o **0** (autenticación de SQL Server) para **@value**.  
  
    -   Al cambiar el modo de seguridad del suscriptor para la autenticación de SQL Server, o cambiar la información de inicio de sesión de autenticación de SQL Server, especifique un valor de **subscriber_password** para **@property** y la contraseña nueva para **@value**. Repita el paso 2, especificando un valor de **subscriber_login** para **@property** y el inicio de sesión nuevo **@value**.  
  
    > [!NOTE]  
    >  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo **distrib_job_login** y **distrib_job_password**, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para cambiar la configuración de seguridad del Agente de distribución para una suscripción de extracción  
  
1.  En el suscriptor, ejecute [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md), especificando **@publication**. Esto devuelve propiedades de suscripción, incluida la configuración de seguridad para el Agente de distribución que se ejecuta en el suscriptor.  
  
2.  En el suscriptor en la base de datos de suscripción, ejecute [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), especificando **@publisher**, **@publisher_db**, **@publication**, el nombre de la propiedad de seguridad de **@property**, y el nuevo valor de la propiedad de **@value**.  
  
3.  Repita el paso 2 para cada una de las propiedades de seguridad siguientes que se vayan a cambiar:  
  
    -   Para cambiar la cuenta de Windows con la que se ejecuta el agente o simplemente la contraseña para esta cuenta, especifique un valor de **distrib_job_password** para **@property** y una nueva contraseña para **@value**. Al cambiar la propia cuenta, repita el paso 2 especificando un valor de **distrib_job_login** para **@property** y la nueva cuenta de Windows para **@value**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al distribuidor, especifique un valor de **distributor_security_mode** para **@property** y un valor de **1** (autenticación integrada de Windows) o **0** (autenticación de SQL Server) para **@value**.  
  
    -   Al cambiar el modo de seguridad del distribuidor para la autenticación de SQL Server o cambiar la información de inicio de sesión de autenticación de SQL Server, especifique un valor de **distributor_password** para **@property** y la contraseña nueva para **@value**. Repita el paso 2, especificando un valor de **distributor_login** para **@property** y el inicio de sesión nuevo **@value**.  
  
    > [!NOTE]  
    >  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
#### Para cambiar la configuración de seguridad del Agente de mezcla para una suscripción de inserción  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md), especificando **@publication**, **@subscriber**, y **@subscriber_db**. Esto devuelve propiedades de suscripción, incluida la configuración de seguridad para el Agente de mezcla que se ejecuta en el distribuidor.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md), especificando **@publication**, **@subscriber**, **@subscriber_db**, el nombre de la propiedad de seguridad de **@property**, y el nuevo valor de la propiedad de **@value**.  
  
3.  Repita el paso 2 para cada una de las propiedades de seguridad siguientes que se vayan a cambiar:  
  
    -   Para cambiar la cuenta de Windows en la que se ejecuta el agente, o simplemente la contraseña para esta cuenta, especifique un valor de **merge_job_password** para **@property** y una nueva contraseña para **@value**. Al cambiar la propia cuenta, repita el paso 2 especificando un valor de **merge_job_login** para **@property** y la nueva cuenta de Windows para **@value**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al suscriptor, especifique un valor de **subscriber_security_mode** para **@property** y un valor de **1** (autenticación integrada de Windows) o **0** (autenticación de SQL Server) para **@value**.  
  
    -   Al cambiar el modo de seguridad del suscriptor para la autenticación de SQL Server, o cambiar la información de inicio de sesión de autenticación de SQL Server, especifique un valor de **subscriber_password** para **@property** y la contraseña nueva para **@value**. Repita el paso 2, especificando un valor de **subscriber_login** para **@property** y el inicio de sesión nuevo **@value**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al publicador, especifique un valor de **publisher_security_mode** para **@property** y un valor de **1** (autenticación integrada de Windows) o **0** (autenticación de SQL Server) para **@value**.  
  
    -   Al cambiar el modo de seguridad del publicador para la autenticación de SQL Server, o cambiar la información de inicio de sesión de autenticación de SQL Server, especifique un valor de **publisher_password** para **@property** y la contraseña nueva para **@value**. Repita el paso 2, especificando un valor de **publisher_login** para **@property** y el inicio de sesión nuevo **@value**.  
  
    > [!NOTE]  
    >  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo **merge_job_login** y **merge_job_password**, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para cambiar la configuración de seguridad del Agente de mezcla para una suscripción de extracción  
  
1.  En el suscriptor, ejecute [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md), especificando **@publication**. Esto devuelve propiedades de suscripción, incluida la configuración de seguridad para el Agente de mezcla que se ejecuta en el suscriptor.  
  
2.  En el suscriptor en la base de datos de suscripción, ejecute [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), especificando **@publisher**, **@publisher_db**, **@publication**, el nombre de la propiedad de seguridad de **@property**, y el nuevo valor de la propiedad de **@value**.  
  
3.  Repita el paso 2 para cada una de las propiedades de seguridad siguientes que se vayan a cambiar:  
  
    -   Para cambiar la cuenta de Windows con la que se ejecuta el agente o simplemente la contraseña para esta cuenta, especifique un valor de **merge_job_password** para **@property** y la nueva contraseña para **@value**. Al cambiar la propia cuenta, repita el paso 2 especificando un valor de **merge_job_login** para **@property** y la nueva cuenta de Windows para **@value**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al distribuidor, especifique un valor de **distributor_security_mode** para **@property** y un valor de **1** (autenticación integrada de Windows) o **0** (autenticación de SQL Server) para **@value**.  
  
    -   Al cambiar el modo de seguridad del distribuidor para la autenticación de SQL Server o cambiar la información de inicio de sesión de autenticación de SQL Server, especifique un valor de **distributor_password** para **@property** y la contraseña nueva para **@value**. Repita el paso 2, especificando un valor de **distributor_login** para **@property** y el inicio de sesión nuevo **@value**.  
  
    -   Para cambiar el modo de seguridad utilizado al conectarse al publicador, especifique un valor de **publisher_security_mode** para **@property** y un valor de **1** (autenticación integrada de Windows) o **0** (autenticación de SQL Server) para **@value**.  
  
    -   Al cambiar el modo de seguridad del publicador para la autenticación de SQL Server o cambiar la información de inicio de sesión de autenticación de SQL Server, especifique un valor de **publisher_password** para **@property** y la contraseña nueva para **@value**. Repita el paso 2, especificando un valor de **publisher_login** para **@property** y el inicio de sesión nuevo **@value**.  
  
    > [!NOTE]  
    >  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
#### Para cambiar la configuración de seguridad para que el Agente de instantáneas genere una instantánea filtrada para un suscriptor  
  
1.  En el publicador, ejecute [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md), especificando **@publication**. En el resultado establecido, tenga en cuenta el valor de **job_name** para la partición del suscriptor cambiar.  
  
2.  En el publicador, ejecute [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md), especificando **@publication**, el valor obtenido del paso 1 para **@dynamic_snapshot_jobname**, y una nueva contraseña para **@job_password** o inicio de sesión y la contraseña de la cuenta de Windows bajo la que se ejecuta el agente de **@job_login** y **@job_password**.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para cambiar la configuración de seguridad del Agente de lectura de cola  
  
1.  En el distribuidor, ejecute [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md). Esto devuelve la cuenta de Windows actual con la que se ejecuta el Agente de lectura de cola.  
  
    -   En el distribuidor, ejecute [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md), especificar la configuración de la cuenta de Windows para **@job_login** y **@job_passwsord**.  
  
    > [!NOTE]  
    >  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto. Existe un Agente de lectura de cola para cada base de datos de distribución. El cambio de la configuración de seguridad del agente afecta a la configuración de todas las publicaciones de todos los publicadores que usan esta base de datos de distribución.  
  
2.  El Agente de lectura de cola establece conexiones al suscriptor con el mismo contexto de conexión que el Agente de distribución para la suscripción.  
  
#### Para cambiar el modo de seguridad que usa un suscriptor de actualización inmediata al conectarse al publicador  
  
1.  En el suscriptor en la base de datos de suscripción, ejecute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique **@publisher**, **@publication**, el nombre de la base de datos de publicación para **@publisher_db**, y uno de los siguientes valores para **@security_mode**:  
  
    -   **0** para usar la autenticación de SQL Server al realizar las actualizaciones en el publicador. Esta opción le exige que especifique un inicio de sesión válido en el publicador para **@login** y **@password**.  
  
    -   **1** para usar el contexto de seguridad del usuario que realiza modificaciones en el suscriptor al conectarse al publicador. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para restricciones relacionadas con este modo de seguridad.  
  
    -   **2** para utilizar una existente, definido por el usuario vinculados creado mediante un inicio de sesión de servidor [sp_addlinkedserver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
#### Para cambiar la contraseña de un distribuidor remoto  
  
1.  En el distribuidor en la base de datos de distribución, ejecute [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), especificando la nueva contraseña para este inicio de sesión para **@password**.  
  
    > [!IMPORTANT]  
    >  No cambie la contraseña de **distributor_admin** directamente.  
  
2.  En cada publicador que utiliza este distribuidor remoto, ejecute [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), especificando la contraseña del paso 1 para **@password**.  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### Para cambiar todas las instancias de una contraseña almacenadas en un servidor de replicación  
  
1.  Crear una conexión con el servidor de replicación mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase mediante la conexión del paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> método. Especifique los parámetros siguientes:  
  
    -   *security_mode* - a <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> valor que especifica el tipo de autenticación para el que se cambian todas las instancias de la contraseña.  
  
    -   *inicio de sesión* -el inicio de sesión para el que se cambian todas las instancias de la contraseña.  
  
    -   *contraseña* -el nuevo valor de contraseña.  
  
        > [!IMPORTANT]  
        >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por Windows .NET Framework.  
  
        > [!NOTE]  
        >  Sólo un miembro de la **sysadmin** rol fijo de servidor puede llamar a este método.  
  
4.  Repita los pasos 1-3 repetidos para cada servidor de la topología de replicación en los que se deba actualizar la contraseña.  
  
#### Para cambiar la configuración de seguridad del Agente de distribución para una suscripción de inserción a una publicación transaccional  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, y <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propiedades de la suscripción y establezca la conexión desde el paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 3 se definieron incorrectamente, o bien que la suscripción no existe.  
  
5.  Establezca una o varias de las siguientes propiedades de seguridad en la instancia de <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   Para cambiar las credenciales de la cuenta de Windows bajo la que se ejecuta el agente, establezca la <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar la autenticación integrada de Windows como el tipo de autenticación que utiliza el agente cuando se conecta al suscriptor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propiedad **true**.  
  
    -   Para especificar la autenticación de SQL Server como el tipo de autenticación que utiliza el agente cuando se conecta al suscriptor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propiedad **false**, y especificar las credenciales de inicio de sesión del suscriptor para el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  La conexión del agente al distribuidor siempre se realiza utilizando las credenciales de Windows especificadas por <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Esta cuenta también se utiliza para realizar conexiones remotas mediante la autenticación de Windows.  
  
6.  (Opcional) Si especifica un valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor. Si especifica un valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (valor predeterminado), cambios se envían al servidor inmediatamente.  
  
#### Para cambiar la configuración de seguridad del Agente de distribución para una suscripción de extracción a una publicación transaccional  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPullSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propiedades de la suscripción y establezca la conexión desde el paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 3 se definieron incorrectamente, o bien que la suscripción no existe.  
  
5.  Establezca una o varias de las siguientes propiedades de seguridad en la instancia de <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   Para cambiar las credenciales de la cuenta de Windows bajo la que se ejecuta el agente, establezca la <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar la autenticación integrada de Windows como el tipo de autenticación que utiliza el agente cuando se conecta al distribuidor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propiedad **true**.  
  
    -   Para especificar la autenticación de SQL Server como el tipo de autenticación que utiliza el agente cuando se conecta al distribuidor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propiedad **false**, y especificar las credenciales de inicio de sesión del distribuidor para la <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  La conexión del agente al suscriptor siempre se realiza utilizando las credenciales de Windows especificadas por <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Esta cuenta también se utiliza para realizar conexiones remotas mediante la autenticación de Windows.  
  
6.  (Opcional) Si especifica un valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor. Si especifica un valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (valor predeterminado), cambios se envían al servidor inmediatamente.  
  
#### Para cambiar la configuración de seguridad del Agente de mezcla para una suscripción de extracción a una publicación de combinación  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePullSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propiedades de la suscripción y establezca la conexión desde el paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 3 se definieron incorrectamente, o bien que la suscripción no existe.  
  
5.  Establezca una o varias de las siguientes propiedades de seguridad en la instancia de <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   Para cambiar las credenciales de la cuenta de Windows bajo la que se ejecuta el agente, establezca la <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar la autenticación integrada de Windows como el tipo de autenticación que utiliza el agente cuando se conecta al distribuidor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propiedad **true**.  
  
    -   Para especificar la autenticación de SQL Server como el tipo de autenticación que utiliza el agente cuando se conecta al distribuidor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propiedad **false**, y especificar las credenciales de inicio de sesión del distribuidor para la <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
    -   Para especificar la autenticación integrada de Windows como el tipo de autenticación que utiliza el agente cuando se conecta al publicador, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> propiedad **true**.  
  
    -   Para especificar la autenticación de SQL Server como el tipo de autenticación que utiliza el agente cuando se conecta al publicador, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> propiedad **false**, y especificar las credenciales de inicio de sesión del publicador para la <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  La conexión del agente al suscriptor siempre se realiza utilizando las credenciales de Windows especificadas por <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Esta cuenta también se utiliza para realizar conexiones remotas mediante la autenticación de Windows.  
  
6.  (Opcional) Si especifica un valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor. Si especifica un valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (valor predeterminado), cambios se envían al servidor inmediatamente.  
  
#### Para cambiar la configuración de seguridad del Agente de mezcla para una suscripción de inserción a una publicación de combinación  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, y <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propiedades de la suscripción y establezca la conexión desde el paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 3 se definieron incorrectamente, o bien que la suscripción no existe.  
  
5.  Establezca una o varias de las siguientes propiedades de seguridad en la instancia de <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   Para cambiar las credenciales de la cuenta de Windows bajo la que se ejecuta el agente, establezca la <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar la autenticación integrada de Windows como el tipo de autenticación que utiliza el agente cuando se conecta al suscriptor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propiedad **true**.  
  
    -   Para especificar la autenticación de SQL Server como el tipo de autenticación que utiliza el agente cuando se conecta al suscriptor, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propiedad **false**, y especificar las credenciales de inicio de sesión del suscriptor para el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
    -   Para especificar la autenticación integrada de Windows como el tipo de autenticación que utiliza el agente cuando se conecta al publicador, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> propiedad **true**.  
  
    -   Para especificar la autenticación de SQL Server como el tipo de autenticación que utiliza el agente cuando se conecta al publicador, establezca el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo de la <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> propiedad **false**, y especificar las credenciales de inicio de sesión del publicador para la <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  La conexión del agente al distribuidor siempre se realiza utilizando las credenciales de Windows especificadas por <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Esta cuenta también se utiliza para realizar conexiones remotas mediante la autenticación de Windows.  
  
6.  (Opcional) Si especifica un valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor. Si especifica un valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (valor predeterminado), cambios se envían al servidor inmediatamente.  
  
#### Para cambiar la información de inicio de sesión utilizada por un suscriptor de actualización inmediata cuando se conecta al publicador transaccional  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> clase para la base de datos de suscripción. Especifique <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> y <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 2 se definieron incorrectamente, o bien que la base de datos de suscripciones no existe.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> método, pasando los parámetros siguientes:  
  
    -   *Publisher* -el nombre del publicador.  
  
    -   *PublisherDB* -el nombre de la base de datos de publicación.  
  
    -   *Publicación* : el nombre de la publicación a la que está suscrito el suscriptor de actualización inmediata.  
  
    -   *Distribuidor* -el nombre del distribuidor.  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> objeto que especifica el tipo de modo de seguridad utilizado por el suscriptor de actualización inmediata al conectar con el publicador y el inicio de sesión credenciales para la conexión.  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 Este ejemplo comprueba el valor de inicio de sesión proporcionado y cambia todas las contraseñas para el inicio de sesión de Windows proporcionado o el inicio de sesión de SQL Server almacenado por replicación en el servidor.  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> Seguimiento: después de modificar la configuración de seguridad de la replicación  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## Vea también  
 [Conceptos de los Replication Management Objects (RMO)](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Actualizar Scripts de replicación & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Administrar inicios de sesión y contraseñas en la replicación](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Prácticas recomendadas de seguridad de replicación](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  