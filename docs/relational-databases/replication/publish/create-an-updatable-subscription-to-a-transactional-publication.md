---
title: Creación de una suscripción actualizable en una publicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 99e605f1ed2a924f504f118dd6d0865fda3229e0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908585"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>Crear una suscripción actualizable en una publicación transaccional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
> [!NOTE]  
>  Esta característica sigue siendo compatible con las versiones de [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] entre 2012 y 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

La replicación transaccional permite que los cambios realizados en un suscriptor puedan volver a propagarse al publicador utilizando suscripciones de actualización inmediatas o en cola. Puede crear las suscripciones de actualización mediante programación usando procedimientos almacenados de replicación. 
 
Configure suscripciones actualizables en la página **Suscripciones actualizables** del **Asistente para nuevas suscripciones**. Esta página solo está disponible si ha habilitado una publicación transaccional para suscripciones actualizables. Para obtener más información sobre cómo habilitar las suscripciones actualizables, vea [Habilitar suscripciones actualizables para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="configure-an-updatable-subscription-from-the-publisher"></a>Configuración de una suscripción actualizable desde el publicador  

1. Conéctese al publicador en Microsoft SQL Server Management Studio y, a continuación, expanda el nodo del servidor.
2. Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .
3. Haga clic con el botón derecho en una publicación transaccional habilitada para actualizar suscripciones y, a continuación, haga clic en **Nuevas suscripciones**.
4. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.
5. En la página **Suscripciones actualizables** del **Asistente para nuevas suscripciones**, asegúrese de que **Replicar está seleccionado**.
6. Seleccione una opción en la lista desplegable **Confirmar en el publicador**:

    * Para utilizar las suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), la propiedad **update_mode** de la suscripción se establece en **failover**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar las suscripciones de actualización en cola, seleccione **Poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), y el suscriptor se está ejecutando en SQL Server 2005 o una versión posterior, la propiedad **update_mode** de la suscripción se establece en queued failover. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener más información sobre cómo cambiar los modos de actualización, consulte [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. La página **Inicio de sesión para suscripciones actualizables** se muestra para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecida en **queued failover**. En la página **Inicio de sesión para suscripciones actualizables**, especifique un servidor vinculado mediante el que se realicen las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante la autenticación de SQL Server**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos que requiere la cuenta del servidor vinculado, vea la sección sobre las **suscripciones de actualización** en [Escriba aquí la descripción del vínculo](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Finalice el asistente.

## <a name="configure-an-updatable-subscription-from-the-subscriber"></a>Configuración de una suscripción actualizable desde el suscriptor


1. Conéctese al suscriptor en SQL Server Management Studio y expanda el nodo de servidor.
2. Expanda la carpeta **Replicación** .
3. Haga clic con el botón secundario en la carpeta **Suscripciones locales** y, a continuación, haga clic en **Nuevas suscripciones**.
4. En la página **Publicación** del **Asistente para nuevas suscripciones**, seleccione **Buscar SQL Server Publisher** de la lista desplegable **Publicador**.
5. Conéctese al publicador en el cuadro de diálogo **Conectar al servidor** .
6. Seleccione una publicación transaccional habilitada para suscripciones de actualización en la página **Publicación**.
7. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.
8. En la página **Suscripciones actualizables** del Asistente para nuevas suscripciones, asegúrese de que **Replicar** está seleccionado.
9. Seleccione una opción en la lista desplegable **Confirmar en el publicador**:

    * Para utilizar las suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), la propiedad **update_mode** de la suscripción se establece en **failover**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar las suscripciones de actualización en cola, seleccione **Poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), y el suscriptor se está ejecutando en SQL Server 2005 o una versión posterior, la propiedad **update_mode** de la suscripción se establece en **queued failover**. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener más información sobre cómo cambiar los modos de actualización, consulte [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. La página **Inicio de sesión para suscripciones actualizables** se muestra para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecida en **queued failover**. En la página **Inicio de sesión para suscripciones actualizables**, especifique un servidor vinculado mediante el que se realicen las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante la autenticación de SQL Server**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos que requiere la cuenta del servidor vinculado, vea la sección sobre las **suscripciones de actualización** en [Escriba aquí la descripción del vínculo](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Finalice el asistente.

## <a name="create-an-immediate-updating-pull-subscription"></a>Creación de una suscripción de extracción de actualización inmediata ##

1. En el publicado, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite las suscripciones de actualización inmediata. 

    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `1`, la publicación admite las suscripciones de actualización inmediata.
    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `0`, la publicación se debe volver a crear con suscripciones de actualización inmediata habilitadas.

2. En el publicador, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite las suscripciones de extracción. 

    * Si el valor de `allow_pull` en el conjunto de resultados es `1`, la publicación admite las suscripciones de extracción.
    * Si el valor de `allow_pull` es `0`, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)y especifique `allow_pull` para `@property` y `true` para `@value`. 

3. En el suscriptor, ejecute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique `@publisher` , `@publication`y uno de los valores siguientes para `@update_mode`:

    * `sync tran` : habilita la suscripción de actualización inmediata.
    * `failover` : habilita la suscripción de actualización inmediata con la actualización en cola como opción de conmutación por error.
    > [!NOTE]  
>  `failover` requiere que la publicación también esté habilitada para las suscripciones de actualización en cola. 
 
4. En el suscriptor, ejecute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique lo siguiente:

    * Los parámetros `@publisher`, `@publisher_db`y `@publication` . 
    * Las credenciales de Microsoft Windows con las que se ejecuta el Agente de distribución en el suscriptor para `@job_login` y `@job_password`. 

    > [!NOTE]  
    > Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el suscriptor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conecta al distribuidor usando la autenticación integrada de Windows. 
 
    * (Opcional) Un valor de `0` para `@distributor_security_mode` y la información de inicio de sesión de Microsoft SQL Server para `@distributor_login` y `@distributor_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al distribuidor. 
    * Una programación para el trabajo del Agente de distribución de esta suscripción. 

5. En el suscriptor de la base de datos de suscripción, ejecute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique `@publisher`, `@publication`, el nombre de la base de datos de publicación para `@publisher_db`y uno de los valores siguientes para `@security_mode`: 

    * `0` - Use Autenticación de SQL Server al realizar las actualizaciones en el publicador. Esta opción le exige que especifique un inicio de sesión válido en el publicador para `@login` y `@password`.
    * `1` - Use el contexto de seguridad del usuario que realiza modificaciones en el suscriptor al conectarse al publicador. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para conocer las restricciones relacionadas con este modo de seguridad.
    * `2` - Use un inicio de sesión vinculado definido por el usuario ya existente y creado con [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).

6. En el publicador, ejecute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) y especifique `@publication`, `@subscriber`, `@destination_db`, un valor de extracción para `@subscription_type`y el mismo valor que especificó en el paso 3 para `@update_mode`. Esto registra la suscripción de extracción en el publicador. 


## <a name="create-an-immediate-updating-push-subscription"></a>Creación de una suscripción de inserción de actualización inmediata ##

1. En el publicado, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite las suscripciones de actualización inmediata. 

    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `1`, la publicación admite las suscripciones de actualización inmediata.
    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `0`, la publicación se debe volver a crear con suscripciones de actualización inmediata habilitadas.

2. En el publicador, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite suscripciones de inserción. 

    * Si el valor de `allow_push` en el conjunto de resultados es `1`, la publicación admite las suscripciones de inserción.
    * Si el valor de `allow_push` es `0`, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)y especifique `allow_push` para `@property` y `true` para `@value`. 

3. En el publicador, ejecute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique `@publication`, `@subscriber`, `@destination_db`y uno de los valores siguientes para `@update_mode`:

    * `sync tran` : habilita la compatibilidad con la actualización inmediata.
    * `failover` : habilita la compatibilidad con la actualización inmediata con actualización en cola como opción de conmutación por error.

    > [!NOTE]  
    >  `failover` requiere que la publicación también esté habilitada para las suscripciones de actualización en cola. 
 
4. En el publicador, ejecute [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique los parámetros siguientes:

    * `@subscriber`, `@subscriber_db`y `@publication`. 

    * Las credenciales de Windows con las que se ejecuta el Agente de distribución en el distribuidor para `@job_login` y `@job_password`. 

    > [!NOTE]  
>  Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el distribuidor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conectará con el suscriptor mediante la autenticación integrada de Windows. 

    * (Opcional) Un valor de `0` para `@subscriber_security_mode` y la información de inicio de sesión de SQL Server para `@subscriber_login` y `@subscriber_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al suscriptor. 
    * Una programación para el trabajo del Agente de distribución de esta suscripción.

5. En el suscriptor de la base de datos de suscripción, ejecute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique `@publisher`, `@publication`, el nombre de la base de datos de publicación para `@publisher_db`y uno de los valores siguientes para `@security_mode`: 

     * `0` - Use Autenticación de SQL Server al realizar las actualizaciones en el publicador. Esta opción le exige que especifique un inicio de sesión válido en el publicador para `@login` y `@password`.
     * `1` - Use el contexto de seguridad del usuario que realiza modificaciones en el suscriptor al conectarse al publicador. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para conocer las restricciones relacionadas con este modo de seguridad.
     * `2` - Use un inicio de sesión vinculado definido por el usuario ya existente y creado con [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).


## <a name="create-a-queued-updating-pull-subscription"></a>Creación de una suscripción de extracción de la actualización en cola

1. En el publicador, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite suscripciones de actualización en cola. 

    * Si el valor de `allow_queued_tran` en el conjunto de resultados es `1`, la publicación admite las suscripciones de actualización inmediata.
    * Si el valor de `allow_queued_tran` en el conjunto de resultados es `0`, la publicación se debe volver a crear con suscripciones de actualización en cola habilitadas.

2. En el publicador, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite las suscripciones de extracción. 

    * Si el valor de `allow_pull` en el conjunto de resultados es `1`, la publicación admite las suscripciones de extracción.
    * Si el valor de `allow_pull` es `0`, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)y especifique `allow_pull` para `@property` y `true` para `@value`. 

3. En el suscriptor, ejecute [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Especifique `@publisher` , `@publication`y uno de los valores siguientes para `@update_mode`:

    * `queued tran` : habilita la suscripción para actualización en cola.
    * `queued failover` : habilita la compatibilidad con la actualización en cola con actualización inmediata como opción de conmutación por error.

    > [!NOTE]  
>  `queued failover` requiere que la publicación también esté habilitada para la suscripción de actualización inmediata. Para conmutar por error a la actualización inmediata, debe usar [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para definir las credenciales bajo las que se replican en el publicador los cambios realizados en el suscriptor.
 
4. En el suscriptor, ejecute [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Especifique los parámetros siguientes:

    * @publisher, `@publisher_db`y `@publication`. 
    * Las credenciales de Windows con las que se ejecuta el Agente de distribución en el suscriptor para `@job_login` y `@job_password`. 

    > [!NOTE]  
    > Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el suscriptor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conecta al distribuidor usando la autenticación integrada de Windows. 
 
    * (Opcional) Un valor de `0` para `@distributor_security_mode` y la información de inicio de sesión de SQL Server para `@distributor_login` y `@distributor_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al distribuidor. 
    * Una programación para el trabajo del Agente de distribución de esta suscripción.

5. En el publicador, ejecute [sp_addsubscriber](../../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md) para registrar el suscriptor en el publicador y especifique `@publication`, `@subscriber`, `@destination_db`, un valor de extracción para `@subscription_type`y el mismo valor que especificó en el paso 3 para `@update_mode`. Esto registra la suscripción de extracción en el publicador. 


## <a name="create-a-queued-updating-push-subscription"></a>Creación de una suscripción de inserción de la actualización en cola 

1. En el publicador, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite suscripciones de actualización en cola. 

    * Si el valor de allow_queued_tran en el conjunto de resultados es 1, la publicación admite suscripciones de actualización inmediata.
    * Si el valor de allow_queued_tran en el conjunto de resultados es 0, la publicación se debe volver a crear con suscripciones de actualización en cola habilitadas. Para más información, vea Cómo: Habilitar suscripciones actualizables para publicaciones transaccionales (programación de la replicación con Transact-SQL).

2. En el publicador, ejecute [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)para comprobar que la publicación admite suscripciones de inserción. 

    * Si el valor de `allow_push` en el conjunto de resultados es `1`, la publicación admite las suscripciones de inserción.
    * Si el valor de `allow_push` es `0`, ejecute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)y especifiqueallow_push para `@property` y `true` para `@value`. 

3. En el publicador, ejecute [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique `@publication`, `@subscriber`, `@destination_db`y uno de los valores siguientes para `@update_mode`:

    * `queued tran` : habilita la suscripción para actualización en cola.
    * `queued failover` : habilita la compatibilidad con la actualización en cola con actualización inmediata como opción de conmutación por error.

    > [!NOTE]  
    > La opción queued failover option requiere que la publicación también esté habilitada para las suscripciones de actualización inmediatas. Para conmutar por error a la actualización inmediata, debe usar [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para definir las credenciales bajo las que se replican en el publicador los cambios realizados en el suscriptor.

4. En el publicador, ejecute [sp_addpushsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique los parámetros siguientes:

    * `@subscriber`, `@subscriber_db`y `@publication`. 
    * Las credenciales de Windows con las que se ejecuta el Agente de distribución en el distribuidor para `@job_login` y `@job_password`. 

    > [!NOTE]  
    > Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el distribuidor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conecta al suscriptor usando la autenticación integrada de Windows. 
 
    * (Opcional) Un valor de `0` para `@subscriber_security_mode` y la información de inicio de sesión de SQL Server para `@subscriber_login` y `@subscriber_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al suscriptor. 
    * Una programación para el trabajo del Agente de distribución de esta suscripción.

## <a name="set-queued-updating-conflict-resolution-options"></a>Establecimiento de opciones de resolución de conflictos de actualización en cola 
Establezca las opciones de resolución de conflictos para las publicaciones que admiten suscripciones de actualización en cola en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación - \<Publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
  
1.  En la página **Opciones de suscripción**, del cuadro de diálogo **Propiedades de la publicación - \<Publicación>** , seleccione uno de los siguientes valores para la opción **Directiva de resolución de conflictos**:  
  
    -   **Mantener el cambio del publicador**    
    -   **Mantener el cambio del suscriptor**    
    -   **Reinicializar la suscripción**  


## <a name="example"></a>Ejemplo

Este ejemplo crea una suscripción de extracción de actualización inmediata a una publicación que admite suscripciones de actualización inmediatas. Los valores de inicio de sesión y contraseña se proporcionan en tiempo de ejecución mediante variables de scripting de sqlcmd.

> [!NOTE]  
>  Este script usa variables de scripting de sqlcmd. Estas variables tienen el formato `$(MyVariable)`. Para información sobre cómo usar las variables de scripting en la línea de comandos y en SQL Server Management Studio, consulte la sección **Ejecutar scripts de replicación** en el tema [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md).

```sql
-- Execute this batch at the Subscriber.
DECLARE @publication AS sysname;
DECLARE @publicationDB AS sysname;
DECLARE @publisher AS sysname;
DECLARE @login AS sysname;
DECLARE @password AS nvarchar(512);
SET @publication = N'AdvWorksProductTran';
SET @publicationDB = N'AdventureWorks2008R2';
SET @publisher = $(PubServer);
SET @login = $(Login);
SET @password = $(Password);

-- At the subscription database, create a pull subscription to a transactional 
-- publication using immediate updating with queued updating as a failover.
EXEC sp_addpullsubscription 
    @publisher = @publisher, 
    @publication = @publication, 
    @publisher_db = @publicationDB, 
    @update_mode = N'failover', 
    @subscription_type = N'pull';

-- Add an agent job to synchronize the pull subscription, 
-- which uses Windows Authentication when connecting to the Distributor.
EXEC sp_addpullsubscription_agent 
    @publisher = @publisher, 
    @publisher_db = @publicationDB, 
    @publication = @publication,
    @job_login = @login,
    @job_password = @password; 

-- Add a Windows Authentication-based linked server that enables the 
-- Subscriber-side triggers to make updates at the Publisher. 
EXEC sp_link_publication 
    @publisher = @publisher, 
    @publication = @publication,
    @publisher_db = @publicationDB, 
    @security_mode = 0,
    @login = @login,
    @password = @password;
GO

USE AdventureWorks2008R2;
GO

-- Execute this batch at the Publisher.
DECLARE @publication AS sysname;
DECLARE @subscriptionDB AS sysname;
DECLARE @subscriber AS sysname;
SET @publication = N'AdvWorksProductTran'; 
SET @subscriptionDB = N'AdventureWorks2008R2Replica'; 
SET @subscriber = $(SubServer);

-- At the Publisher, register the subscription, using the defaults.
USE [AdventureWorks2008R2]
EXEC sp_addsubscription 
    @publication = @publication, 
    @subscriber = @subscriber, 
    @destination_db = @subscriptionDB, 
    @subscription_type = N'pull', 
    @update_mode = N'failover';
GO
``` 


## <a name="see-also"></a>Consulte también

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
[Usar sqlcmd con variables de script](../../../ssms/scripting/sqlcmd-use-with-scripting-variables.md)   


