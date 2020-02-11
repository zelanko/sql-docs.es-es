---
title: Actualizar scripts de replicación (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd3f6498cbfb4ef8cf38e27879d619472a6693ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68210760"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>Actualizar scripts de replicación (programación de la replicación con Transact-SQL)
  [!INCLUDE[tsql](../../../includes/tsql-md.md)]los archivos de script se pueden utilizar para configurar mediante programación una topología de replicación. Para obtener más información, consulte [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md) (Conceptos sobre los procedimientos almacenados del sistema de replicación).  
  
> [!IMPORTANT]  
>  Aunque no necesita actualizar scripts ejecutados por miembros del rol `sysadmin`, se recomienda modificar los ya existentes tal como se describe en este tema. Especifique una cuenta que tenga permisos mínimos para cada agente de replicación tal como se describe en la sección sobre permisos requeridos por el agente del tema [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
 Estas mejoras de seguridad, que hacen posible un mayor control sobre los permisos permitiéndole especificar de manera explícita las cuentas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows bajo las cuales se ejecutan los trabajos del agente de replicación, afectan a los siguientes procedimientos almacenados de scripts existentes:  
  
-   **sp_addpublication_snapshot**:  
  
     Ahora debe proporcionar las credenciales de Windows **@job_login** como **@job_password** y al ejecutar [sp_addpublication_snapshot &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) para crear el trabajo en el que se ejecuta la agente de instantáneas en el distribuidor.  
  
-   **sp_addpushsubscription_agent**:  
  
     Ahora debería ejecutar [sp_addpushsubscription_agent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql) para agregar explícitamente un trabajo y proporcionar las credenciales**@job_login** de **@job_password**Windows (y) bajo las que se ejecuta el trabajo de agente de distribución en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una suscripción de inserción.  
  
-   **sp_addmergepushsubscription_agent**:  
  
     Ahora debería ejecutar [sp_addmergepushsubscription_agent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql) para agregar explícitamente un trabajo y proporcionar las credenciales**@job_login** de **@job_password**Windows (y) bajo las que se ejecuta el trabajo de agente de mezcla en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una suscripción de inserción.  
  
-   **sp_addpullsubscription_agent**:  
  
     Ahora debe proporcionar las credenciales de Windows **@job_login** como **@job_password** y al ejecutar [sp_addpullsubscription_agent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) para crear el trabajo en el que se ejecuta la agente de distribución en el suscriptor.  
  
-   **sp_addmergepullsubscription_agent**:  
  
     Ahora debe proporcionar las credenciales de Windows **@job_login** como **@job_password** y al ejecutar [sp_addmergepullsubscription_agent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) para crear el trabajo en el que se ejecuta la agente de mezcla en el suscriptor.  
  
-   **sp_addlogreader_agent**:  
  
     Debería ejecutar ahora [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) para agregar manualmente el trabajo y proporcionar las credenciales de Windows bajo las que se ejecuta el Agente de registro del LOG en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una publicación transaccional.  
  
-   **sp_addqreader_agent**:  
  
     Debería ejecutar ahora [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) para agregar manualmente el trabajo y proporcionar las credenciales de Windows bajo las que se ejecuta el Agente de lectura de cola en el distribuidor. En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], esto se hacía automáticamente cuando se creaba una publicación transaccional que admitía actualización en cola.  
  
 En el modelo de seguridad introducido [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]en, los agentes de replicación realizan siempre las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la instancia local de con autenticación de Windows **@job_name** mediante **@job_password**las credenciales proporcionadas en y. Para obtener información sobre los requisitos de cuentas de Windows utilizadas al ejecutar los trabajos del Agente de replicación, vea [Replication Agent Security Model](../security/replication-agent-security-model.md).  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si almacena las credenciales en un archivo de script, asegúrese de que dicho archivo está protegido.  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>Para actualizar scripts que configuran una instantánea o publicación transaccional  
  
1.  En el script existente, antes de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), ejecute [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) en el publicador de la base de datos de publicación. Especifique las credenciales de Windows con las que se **@job_name** ejecuta **@job_password**el agente de registro del log para y. Si el agente va a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar la autenticación de al conectarse al publicador, también debe especificar un valor de **@publisher_security_mode** 0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la información **@publisher_login** de **@publisher_password**inicio de sesión de para y. **** Con ello se crea un trabajo del Agente de registro del LOG para la base de datos de publicación.  
  
    > [!NOTE]  
    >  Este paso es solo para las publicaciones transaccionales y no se requiere para las publicaciones de instantáneas.  
  
2.  (Opcional) Antes de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), ejecute [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) en el distribuidor de la base de datos de distribución. Especifique las credenciales de Windows con las que se **@job_name** ejecuta **@job_password**el agente de lectura de cola para y. Con ello se crea un trabajo del Agente de lectura de cola para el distribuidor.  
  
    > [!NOTE]  
    >  Este paso solamente se requiere para las publicaciones transaccionales que admiten los suscriptores de actualización en cola.  
  
3.  (Opcional) Actualice la ejecución de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de replicación.  
  
4.  Después de [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), ejecute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) en el publicador de la base de datos de publicación. Especifique **@publication** y las credenciales de Windows con las que se **@job_name** ejecuta **@job_password**el agente de instantáneas para y. Si el agente va a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar la autenticación de al conectarse al publicador, también debe especificar un valor de **@publisher_security_mode** 0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la información **@publisher_login** de **@publisher_password**inicio de sesión de para y. **** Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
5.  (Opcional) Actualice la ejecución de [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de replicación.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>Para actualizar scripts que agregan suscripciones a una instantánea o publicación transaccional  
  
1.  Después de ejecutar el procedimiento almacenado que crea la suscripción, asegúrese de que ejecuta el procedimiento almacenado que crea un trabajo de Agente de distribución para sincronizar la suscripción. El procedimiento almacenado que utilice dependerá del tipo de suscripción.  
  
    -   Para una suscripción de extracción, actualice la ejecución de [sp_addpullsubscription_agent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) para proporcionar las credenciales de Windows con las que se ejecuta la **@job_name** agente de distribución **@job_password**en el suscriptor para y. Esto se hace después de la ejecución de [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Para obtener más información, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
    -   Para una suscripción de inserción, ejecute [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql) en el publicador. **@publication** **@job_name** Especifique las credenciales de Windows con las que se ejecuta el agente de distribución en el distribuidor **@job_password**para y, y una programación para este trabajo del agente. **@subscriber** **@subscriber_db** Para obtener más información, vea [especificar programaciones de sincronización](../specify-synchronization-schedules.md). Esto se hace después de la ejecución de [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Para obtener más información, consulte [Create a Push Subscription](../create-a-push-subscription.md).  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>Para actualizar scripts que configuran una publicación de combinación  
  
1.  (Opcional) En el script existente, actualice la ejecución de [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de la replicación.  
  
2.  Después de [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), ejecute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) en el publicador de la base de datos de publicación. Especifique **@publication** y las credenciales de Windows con las que se **@job_name** ejecuta **@job_password**el agente de instantáneas para y. Si el agente va a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar la autenticación de al conectarse al publicador, también debe especificar un valor de **@publisher_security_mode** 0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la información **@publisher_login** de **@publisher_password**inicio de sesión de para y. **** Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
3.  (Opcional) Actualice la ejecución de [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para establecer cualquier valor no predeterminado para los parámetros que implementan nuevas funcionalidades de replicación.  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>Para actualizar scripts que agregan suscripciones a una publicación de combinación  
  
1.  Después de ejecutar el procedimiento almacenado que crea la suscripción, asegúrese de que ejecuta el procedimiento almacenado que crea un trabajo de Agente de mezcla para sincronizar la suscripción. El procedimiento almacenado que utilice dependerá del tipo de suscripción.  
  
    -   Para una suscripción de extracción, actualice la ejecución de [sp_addmergepullsubscription_agent &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) para proporcionar las credenciales de Windows con las que se ejecuta la **@job_name** agente de mezcla **@job_password**en el suscriptor para y. Esto se hace después de la ejecución de [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Para obtener más información, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).  
  
    -   Para una suscripción de inserción, ejecute [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql) en el publicador. Especifique **@subscriber**, **@subscriber_db**, **@publication**, las credenciales de Windows con las que se ejecuta el agente de mezcla **@job_name** en **@job_password**el distribuidor para y, y una programación para este trabajo del agente. Para obtener más información, vea [especificar programaciones de sincronización](../specify-synchronization-schedules.md). Esto se hace después de la ejecución de [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Para obtener más información, consulte [Create a Push Subscription](../create-a-push-subscription.md).  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una publicación transaccional para la tabla Product. Esta publicación admite la actualización inmediata con actualización en cola como conmutación por error. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpub80.sql#sp_createtranpub_nwpreupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de actualización del script anterior, que crea una publicación transaccional, para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Esta publicación admite la actualización inmediata con actualización en cola como conmutación por error. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpublication.sql#sp_createtranpub_nwpostupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una publicación de combinación para la tabla Customers. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepub80.sql#sp_createmergepub_nwpreupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo del script anterior, que crea una publicación de combinación, actualizada para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepublication.sql#sp_createmergepub_nwpostupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de inserción a una publicación transaccional. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpushsub80.sql#sp_createtranpushsub_nwpreupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de actualización del script anterior, que crea una suscripción de inserción, para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createtranpushsub_nwpostupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de inserción a una publicación de combinación. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo del script anterior, que crea una suscripción de inserción en una publicación de combinación, actualizado para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createmergepushsub_nwpostupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de extracción a una publicación transaccional. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de actualización del script anterior, que crea una suscripción de extracción, actualizado para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createtranpullsub_nwpostupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de un script [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] que crea una suscripción de extracción a una publicación de combinación. Los parámetros predeterminados se han quitado para mayor legibilidad.  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepullsub80.sql#sp_createmergepullsub_nwpreupgrade)]  
  
## <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo del script anterior, que crea una suscripción de extracción en una publicación de combinación, actualizado para ejecutarse correctamente para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y las versiones posteriores. Los valores predeterminados de los nuevos parámetros se ha declarado explícitamente.  
  
> [!NOTE]  
>  Las credenciales de Windows se proporcionan en el tiempo de ejecución mediante las variables de scripting **sqlcmd** .  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createmergepullsub_nwpostupgrade)]  
  
## <a name="see-also"></a>Consulte también  
 [Create a Publication](../publish/create-a-publication.md)   
 [Create a Push Subscription](../create-a-push-subscription.md)   
 [Create a Pull Subscription](../create-a-pull-subscription.md)   
 [Ver y modificar la configuración de seguridad de la replicación](../security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../mssql-eng021797.md)   
 [MSSQL_ENG021798](../mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Actualizar bases de datos replicadas](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
