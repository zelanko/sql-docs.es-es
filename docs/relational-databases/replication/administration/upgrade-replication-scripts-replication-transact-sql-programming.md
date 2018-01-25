---
title: "Actualizar scripts de replicación (programación de la replicación con Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: "41"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09f8ed7bf8cbd407a8bd9dc706d5e9aadf34ce65
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>Actualizar scripts de replicación (programación de la replicación con Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Los archivos de script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] se pueden utilizar para configurar mediante programación una topología de replicación. Para obtener más información, consulte [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md) (Conceptos sobre los procedimientos almacenados del sistema de replicación).  
  
> [!IMPORTANT]  
>  Aunque no necesita actualizar scripts ejecutados por miembros del rol **sysadmin** , se recomienda modificar los ya existentes tal como se describe en este tema. Especifique una cuenta que tenga permisos mínimos para cada agente de replicación tal como se describe en la sección sobre permisos requeridos por el agente del tema [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Estas mejoras de seguridad, que hacen posible un mayor control sobre los permisos permitiéndole especificar de manera explícita las cuentas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows bajo las cuales se ejecutan los trabajos del agente de replicación, afectan a los siguientes procedimientos almacenados de scripts existentes:  
  
-   **sp_addpublication_snapshot**:  
  
     Debería proporcionar ahora las credenciales de Windows como **@job_login** y **@job_password** al ejecutar [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) para crear el trabajo bajo el que el Agente de instantáneas se ejecuta en el distribuidor.  
  
-   **sp_addpushsubscription_agent**:  
  
     Debería ejecutar ahora [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) para agregar explícitamente un trabajo y proporcionar las credenciales de Windows (**@job_login** y **@job_password**) bajo las que se ejecuta el Agente de distribución en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una suscripción de inserción.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     Debería ejecutar ahora [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) para agregar explícitamente un trabajo y proporcionar las credenciales de Windows (**@job_login** y **@job_password**) bajo las que se ejecuta el Agente de mezcla en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una suscripción de inserción.  
  
-   **sp_addpullsubscription_agent**:  
  
     Debería proporcionar ahora las credenciales de Windows como **@job_login** y **@job_password** al ejecutar [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) para crear el trabajo bajo el que el Agente de distribución se ejecuta en el suscriptor.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     Debería proporcionar ahora las credenciales de Windows como **@job_login** y **@job_password** al ejecutar [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) para crear el trabajo bajo el que el Agente de mezcla se ejecuta en el suscriptor.  
  
-   **sp_addlogreader_agent**:  
  
     Debería ejecutar ahora [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) para agregar manualmente el trabajo y proporcionar las credenciales de Windows bajo las que se ejecuta el Agente de registro del LOG en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una publicación transaccional.  
  
-   **sp_addqreader_agent**:  
  
     Debería ejecutar ahora [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) para agregar manualmente el trabajo y proporcionar las credenciales de Windows bajo las que se ejecuta el Agente de lectura de cola en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una publicación transaccional que admitía actualización en cola.  
  
 En el modelo de seguridad introducido en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], los agentes de replicación realizan siempre las conexiones con la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con autenticación de Windows mediante las credenciales proporcionada en **@job_name** y **@job_password**. Para obtener información sobre los requisitos de cuentas de Windows utilizadas al ejecutar los trabajos del Agente de replicación, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si almacena las credenciales en un archivo de script, asegúrese de que dicho archivo está protegido.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>Para actualizar scripts que configuran una instantánea o publicación transaccional  
  
1.  En el script existente, antes de [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ejecute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) en el publicador de la base de datos de publicación. Especifique las credenciales de Windows con las que se ejecuta el Agente de registro del LOG **@job_name** y **@job_password**. Si el agente va a usar autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**. Con ello se crea un trabajo del Agente de registro del LOG para la base de datos de publicación.  
  
    > [!NOTE]  
    >  Este paso es solo para las publicaciones transaccionales y no se requiere para las publicaciones de instantáneas.  
  
2.  (Opcional) Antes de [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ejecute [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md) en el distribuidor de la base de datos de distribución. Especifique las credenciales de Windows con las que se ejecuta el Agente de lectura de cola **@job_name** y **@job_password**. Con ello se crea un trabajo del Agente de lectura de cola para el distribuidor.  
  
    > [!NOTE]  
    >  Este paso solamente se requiere para las publicaciones transaccionales que admiten los suscriptores de actualización en cola.  
  
3.  (Opcional) Actualice la ejecución de [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de replicación.  
  
4.  Después de [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ejecute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) en el publicador de la base de datos de publicación. Especifique **@publication** y las credenciales de Windows con las que se ejecuta el Agente de instantáneas para **@job_name** y **@job_password**. Si el agente va a usar autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
5.  (Opcional) Actualice la ejecución de [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de replicación.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>Para actualizar scripts que agregan suscripciones a una instantánea o publicación transaccional  
  
1.  Después de ejecutar el procedimiento almacenado que crea la suscripción, asegúrese de que ejecuta el procedimiento almacenado que crea un trabajo de Agente de distribución para sincronizar la suscripción. El procedimiento almacenado que utilice dependerá del tipo de suscripción.  
  
    -   Para una suscripción de extracción, actualice la ejecución de [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) para proporcionar las credenciales de Windows bajo las que se ejecuta el Agente de distribución en el suscriptor para **@job_name** y **@job_password**. Esto se hace después de la ejecución de [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md). Para obtener más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Para una suscripción de inserción, ejecute [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md) en el publicador. Especifique **@subscriber**, **@subscriber_db**, **@publication**, credenciales de Windows bajo las que se ejecuta el Agente de distribución en el distribuidor para **@job_name** y **@job_password**, y una programación para este trabajo del agente. Para más información, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Esto se hace después de la ejecución de [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Para más información, consulte [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>Para actualizar scripts que configuran una publicación de combinación  
  
1.  (Opcional) En el script existente, actualice la ejecución de [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de la replicación.  
  
2.  Después de [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ejecute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) en el publicador de la base de datos de publicación. Especifique **@publication** y las credenciales de Windows con las que se ejecuta el Agente de instantáneas para **@job_name** y **@job_password**. Si el agente va a usar autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
3.  (Opcional) Actualice la ejecución de [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de replicación.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>Para actualizar scripts que agregan suscripciones a una publicación de combinación  
  
1.  Después de ejecutar el procedimiento almacenado que crea la suscripción, asegúrese de que ejecuta el procedimiento almacenado que crea un trabajo de Agente de mezcla para sincronizar la suscripción. El procedimiento almacenado que utilice dependerá del tipo de suscripción.  
  
    -   Para una suscripción de extracción, actualice la ejecución de [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) para proporcionar las credenciales de Windows bajo las que se ejecuta el Agente de mezcla en el suscriptor para **@job_name** y **@job_password**. Esto se hace después de la ejecución de [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Para obtener más información, consulte [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md).  
  
    -   Para una suscripción de inserción, ejecute [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md) en el publicador. Especifique **@subscriber**, **@subscriber_db**, **@publication**, las credenciales de Windows bajo las que se ejecuta el Agente de mezcla en el distribuidor para **@job_name** y **@job_password**, y una programación para este trabajo del agente. Para más información, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md). Esto se hace después de la ejecución de [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md). Para más información, consulte [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una publicación transaccional para la tabla Product. Esta publicación admite la actualización inmediata con actualización en cola como conmutación por error. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_1.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de actualización del script anterior, que crea una publicación transaccional, para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Esta publicación admite la actualización inmediata con actualización en cola como conmutación por error. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_2.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una publicación de combinación para la tabla Customers. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_3.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo del script anterior, que crea una publicación de combinación, actualizada para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_4.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de inserción a una publicación transaccional. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_5.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de actualización del script anterior, que crea una suscripción de inserción, para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_6.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de inserción a una publicación de combinación. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo del script anterior, que crea una suscripción de inserción en una publicación de combinación, actualizado para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_8.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de extracción a una publicación transaccional. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_7.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de actualización del script anterior, que crea una suscripción de extracción, actualizado para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_9.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de extracción a una publicación de combinación. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_10.sql)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo del script anterior, que crea una suscripción de extracción en una publicación de combinación, actualizado para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../relational-databases/replication/codesnippet/tsql/upgrade-replication-scri_11.sql)]  
  
## <a name="see-also"></a>Ver también  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)   
 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  (Ver y modificar la configuración de seguridad de la replicación)  
 [MSSQL_ENG021797](../../../relational-databases/replication/mssql-eng021797.md)   
 [MSSQL_ENG021798](../../../relational-databases/replication/mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Actualizar bases de datos replicadas](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
