---
title: Crear una suscripción actualizable en una publicación transaccional mediante Transact-SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2014
helpviewer_keywords:
- updatable transactional subscriptions, T-SQL
ms.assetid: 670e1ea0-ffda-4d84-b4cd-f15a331035b9
caps.latest.revision: 3
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e5d773ebed7df043c75accf8f17ed32865097633
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107400"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-using-transact-sql"></a>Crear una suscripción actualizable en una publicación transaccional con Transact-SQL

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
 
La replicación transaccional permite que los cambios realizados en un suscriptor puedan volver a propagarse al publicador utilizando suscripciones de actualización inmediatas o en cola. Puede crear las suscripciones de actualización mediante programación usando procedimientos almacenados de replicación. (Consulte también [Crear una suscripción actualizable a una publicación transaccional [Management Studio]](publish/create-an-updatable-subscription-to-a-transactional-publication.md)). 

## <a name="to-create-an-immediate-updating-pull-subscription"></a>Para crear una suscripción de extracción de actualización inmediata ##

1. En el publicado, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite las suscripciones de actualización inmediata. 

    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `1`, la publicación admite las suscripciones de actualización inmediata.

    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `0`, la publicación se debe volver a crear con suscripciones de actualización inmediata habilitadas.

2. En el publicador, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite las suscripciones de extracción. 

    * Si el valor de `allow_pull` en el conjunto de resultados es `1`, la publicación admite las suscripciones de extracción.

    * Si el valor de `allow_pull` es `0`, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)y especifique `allow_pull` para `@property` y `true` para `@value`. 

3. En el suscriptor, ejecute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique `@publisher` , `@publication`y uno de los valores siguientes para `@update_mode`:

    * `sync tran` : habilita la suscripción de actualización inmediata.

    * `failover` : habilita la suscripción de actualización inmediata con la actualización en cola como opción de conmutación por error.

    > [!NOTE]  
>  `failover` requiere que la publicación también esté habilitada para las suscripciones de actualización en cola. 
 
4. En el suscriptor, ejecute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique lo siguiente:

    * Los parámetros `@publisher`, `@publisher_db`y `@publication` . 

    * Las credenciales de Microsoft Windows con las que se ejecuta el Agente de distribución en el suscriptor para `@job_login` y `@job_password`. 

    > [!NOTE]  
>  Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el suscriptor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conecta al distribuidor usando la autenticación integrada de Windows. 
 
    * (Opcional) Un valor de `0` para `@distributor_security_mode` y la información de inicio de sesión de Microsoft SQL Server para `@distributor_login` y `@distributor_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al distribuidor. 

    * Una programación para el trabajo del Agente de distribución de esta suscripción. 

5. En el suscriptor de la base de datos de suscripción, ejecute [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql). Especifique `@publisher`, `@publication`, el nombre de la base de datos de publicación para `@publisher_db`y uno de los valores siguientes para `@security_mode`: 

    * `0` - Use Autenticación de SQL Server al realizar las actualizaciones en el publicador. Esta opción le exige que especifique un inicio de sesión válido en el publicador para `@login` y `@password`.

    * `1` - Use el contexto de seguridad del usuario que realiza modificaciones en el suscriptor al conectarse al publicador. Consulte [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) para conocer las restricciones relacionadas con este modo de seguridad.

    * `2` - Use un inicio de sesión vinculado definido por el usuario ya existente y creado con [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).

6. En el publicador, ejecute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) y especifique `@publication`, `@subscriber`, `@destination_db`, un valor de extracción para `@subscription_type`y el mismo valor que especificó en el paso 3 para `@update_mode`.

Esto registra la suscripción de extracción en el publicador. 


## <a name="to-create-an-immediate-updating-push-subscription"></a>Para crear una suscripción de inserción de actualización inmediata ##

1. En el publicado, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite las suscripciones de actualización inmediata. 

    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `1`, la publicación admite las suscripciones de actualización inmediata.

    * Si el valor de `allow_sync_tran` en el conjunto de resultados es `0`, la publicación se debe volver a crear con suscripciones de actualización inmediata habilitadas.

2. En el publicador, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite suscripciones de inserción. 

    * Si el valor de `allow_push` en el conjunto de resultados es `1`, la publicación admite las suscripciones de inserción.

    * Si el valor de `allow_push` es `0`, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)y especifique `allow_push` para `@property` y `true` para `@value`. 

3. En el publicador, ejecute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique `@publication`, `@subscriber`, `@destination_db`y uno de los valores siguientes para `@update_mode`:

    * `sync tran` : habilita la compatibilidad con la actualización inmediata.

    * `failover` : habilita la compatibilidad con la actualización inmediata con actualización en cola como opción de conmutación por error.

    > [!NOTE]  
>  `failover` requiere que la publicación también esté habilitada para las suscripciones de actualización en cola. 
 
4. En el publicador, ejecute [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Especifique los parámetros siguientes:

    * `@subscriber`, `@subscriber_db`y `@publication`. 

    * Las credenciales de Windows con las que se ejecuta el Agente de distribución en el distribuidor para `@job_login` y `@job_password`. 

    > [!NOTE]  
>  Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el distribuidor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conectará con el suscriptor mediante la autenticación integrada de Windows. 

    * (Opcional) Un valor de `0` para `@subscriber_security_mode` y la información de inicio de sesión de SQL Server para `@subscriber_login` y `@subscriber_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al suscriptor. 

    * Una programación para el trabajo del Agente de distribución de esta suscripción.

5. En el suscriptor de la base de datos de suscripción, ejecute [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql). Especifique `@publisher`, `@publication`, el nombre de la base de datos de publicación para `@publisher_db`y uno de los valores siguientes para `@security_mode`: 

     * `0` - Use Autenticación de SQL Server al realizar las actualizaciones en el publicador. Esta opción le exige que especifique un inicio de sesión válido en el publicador para `@login` y `@password`.

     * `1` - Use el contexto de seguridad del usuario que realiza modificaciones en el suscriptor al conectarse al publicador. Consulte [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) para conocer las restricciones relacionadas con este modo de seguridad.

     * `2` - Use un inicio de sesión vinculado definido por el usuario ya existente y creado con [sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).


## <a name="to-create-a-queued-updating-pull-subscription"></a>Para crear una suscripción de extracción de la actualización en cola ##

1. En el publicador, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite suscripciones de actualización en cola. 

    * Si el valor de `allow_queued_tran` en el conjunto de resultados es `1`, la publicación admite las suscripciones de actualización inmediata.

    * Si el valor de `allow_queued_tran` en el conjunto de resultados es `0`, la publicación se debe volver a crear con suscripciones de actualización en cola habilitadas.

2. En el publicador, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite las suscripciones de extracción. 

    * Si el valor de `allow_pull` en el conjunto de resultados es `1`, la publicación admite las suscripciones de extracción.

    * Si el valor de `allow_pull` es `0`, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)y especifique `allow_pull` para `@property` y `true` para `@value`. 

3. En el suscriptor, ejecute [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique `@publisher` , `@publication`y uno de los valores siguientes para `@update_mode`:

    * `queued tran` : habilita la suscripción para actualización en cola.

    * `queued failover` : habilita la compatibilidad con la actualización en cola con actualización inmediata como opción de conmutación por error.

    > [!NOTE]  
>  `queued failover` requiere que la publicación también esté habilitada para la suscripción de actualización inmediata. Para conmutar por error a la actualización inmediata, debe usar [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) para definir las credenciales bajo las que se replican en el publicador los cambios realizados en el suscriptor.
 
4. En el suscriptor, ejecute [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique los parámetros siguientes:

    * @publisher, `@publisher_db`y `@publication`. 

    * Las credenciales de Windows con las que se ejecuta el Agente de distribución en el suscriptor para `@job_login` y `@job_password`. 

    > [!NOTE]  
>  Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el suscriptor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conecta al distribuidor usando la autenticación integrada de Windows. 
 
    * (Opcional) Un valor de `0` para `@distributor_security_mode` y la información de inicio de sesión de SQL Server para `@distributor_login` y `@distributor_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al distribuidor. 

    * Una programación para el trabajo del Agente de distribución de esta suscripción.

5. En el publicador, ejecute [sp_addsubscriber](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql) para registrar el suscriptor en el publicador y especifique `@publication`, `@subscriber`, `@destination_db`, un valor de extracción para `@subscription_type`y el mismo valor que especificó en el paso 3 para `@update_mode`.

Esto registra la suscripción de extracción en el publicador. 


## <a name="to-create-a-queued-updating-push-subscription"></a>Para crear una suscripción de inserción de la actualización en cola ##

1. En el publicador, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite suscripciones de actualización en cola. 

    * Si el valor de allow_queued_tran en el conjunto de resultados es 1, la publicación admite suscripciones de actualización inmediata.

    * Si el valor de allow_queued_tran en el conjunto de resultados es 0, la publicación se debe volver a crear con suscripciones de actualización en cola habilitadas. Para más información, consulte Habilitar suscripciones actualizables para publicaciones transaccionales (programación de la replicación con Transact-SQL).

2. En el publicador, ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)para comprobar que la publicación admite suscripciones de inserción. 

    * Si el valor de `allow_push` en el conjunto de resultados es `1`, la publicación admite las suscripciones de inserción.

    * Si el valor de `allow_push` es `0`, ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)y especifiqueallow_push para `@property` y `true` para `@value`. 

3. En el publicador, ejecute [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique `@publication`, `@subscriber`, `@destination_db`y uno de los valores siguientes para `@update_mode`:

    * `queued tran` : habilita la suscripción para actualización en cola.

    * `queued failover` : habilita la compatibilidad con la actualización en cola con actualización inmediata como opción de conmutación por error.

    > [!NOTE]  
>  La opción queued failover option requiere que la publicación también esté habilitada para las suscripciones de actualización inmediatas. Para conmutar por error a la actualización inmediata, debe usar [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) para definir las credenciales bajo las que se replican en el publicador los cambios realizados en el suscriptor.

4. En el publicador, ejecute [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Especifique los parámetros siguientes:

    * `@subscriber`, `@subscriber_db`y `@publication`. 

    * Las credenciales de Windows con las que se ejecuta el Agente de distribución en el distribuidor para `@job_login` y `@job_password`. 

    > [!NOTE]  
>  Las conexiones que se realicen con la autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por `@job_login` y `@job_password`. El Agente de distribución siempre realiza la conexión local con el distribuidor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conecta al suscriptor usando la autenticación integrada de Windows. 
 
    * (Opcional) Un valor de `0` para `@subscriber_security_mode` y la información de inicio de sesión de SQL Server para `@subscriber_login` y `@subscriber_password`, en caso de que necesite usar Autenticación de SQL Server cuando se conecte al suscriptor. 

    * Una programación para el trabajo del Agente de distribución de esta suscripción.


## <a name="example"></a>Ejemplo ##

Este ejemplo crea una suscripción de extracción de actualización inmediata a una publicación que admite suscripciones de actualización inmediatas. Los valores de inicio de sesión y contraseña se proporcionan en tiempo de ejecución mediante variables de scripting de sqlcmd.

> [!NOTE]  
>  Este script usa variables de scripting de sqlcmd. Estas variables tienen el formato `$(MyVariable)`. Para información sobre cómo usar las variables de scripting en la línea de comandos y en SQL Server Management Studio, consulte la sección **Ejecutar scripts de replicación** en el tema [Conceptos sobre los procedimientos almacenados del sistema de replicación](concepts/replication-system-stored-procedures-concepts.md).

```
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

## <a name="see-also"></a>Vea también ##

[Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)

[Usar sqlcmd con variables de script](../scripting/sqlcmd-use-with-scripting-variables.md)

[Crear una suscripción actualizable a una publicación transaccional [Management Studio]](publish/create-an-updatable-subscription-to-a-transactional-publication.md)
