---
title: Administrar los metadatos cuando una base de datos está disponible en otra instancia de servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- cross-database queries [SQL Server]
- logins [SQL Server], recreating on another server instance
- triggers [SQL Server], DLL
- user-defined error messages [SQL Server]
- permissions [SQL Server], metadata access
- Full-Text Engine [SQL Server]
- metadata [SQL Server], databases available to other instances
- jobs [SQL Server Agent], recreating on another server instance
- failover [SQL Server], managing metadata
- event notifications [SQL Server], metadata
- database mirroring [SQL Server], metadata
- startup options [SQL Server]
- restoring [SQL Server], onto another server instance
- linked servers [SQL Server], metadata
- WMI Provider for Server Events, metadata
- attaching databases [SQL Server]
- log shipping [SQL Server], metadata
- encryption [SQL Server], metadata
- server configuration [SQL Server]
- distributed queries [SQL Server], metadata
- extended stored procedures [SQL Server], metadata
- credentials [SQL Server], metadata
- copying databases
ms.assetid: 5d98cf2a-9fc2-4610-be72-b422b8682681
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5087a925ac163281f4326a5f952c11ce2953c6dd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965975"
---
# <a name="manage-metadata-when-making-a-database-available-on-another-server-instance-sql-server"></a>Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia de servidor (SQL Server)
  Este tema es pertinente en las siguientes situaciones:  
  
-   Configurar las réplicas de disponibilidad en un grupo de disponibilidad de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .  
  
-   Configurar la creación de reflejo de una base de datos.  
  
-   Preparar la conmutación de roles entre los servidores primario y secundario de una configuración de trasvase de registros.  
  
-   Restaurar una base de datos en otra instancia de servidor.  
  
-   Adjuntar una copia de una base de datos en otra instancia de servidor.  
  
 Algunas aplicaciones dependen de información, entidades u objetos que se encuentran fuera del ámbito de una base de datos de usuario único. Normalmente, una aplicación depende de las bases de datos **maestras** y **msdb** , así como de la base de datos del usuario. Cualquier elemento almacenado fuera de la base de datos de usuario que sea necesario para el funcionamiento correcto de dicha base de datos debe estar disponible en la instancia de servidor de destino. Por ejemplo, los inicios de sesión de una aplicación se almacenan como metadatos en la base de datos **maestra** y se deben volver a crear en el servidor de destino. Si una aplicación o un plan de mantenimiento de bases de datos dependen de trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , cuyos metadatos estén almacenados en la base de datos **msdb** , dichos trabajos se deben volver a crear en la instancia del servidor de destino. De forma similar, los metadatos de un desencadenador de servidor se almacenan en la base de datos **maestra**.  
  
 Si mueve la base de datos de una aplicación a otra instancia de servidor, debe volver a crear todos los metadatos de las entidades y los objetos dependientes de las bases de datos **maestra** y **msdb** en la instancia de servidor de destino. Por ejemplo, si una aplicación de la base de datos usa desencadenadores de servidor, no basta con adjuntar o restaurar la base de datos en el nuevo sistema. La base de datos no funcionará según lo previsto a menos que se vuelvan a crear manualmente los metadatos para dichos desencadenadores en la base de datos **maestra** .  
  
##  <a name="information-entities-and-objects-that-are-stored-outside-of-user-databases"></a><a name="information_entities_and_objects"></a> Información, entidades y objetos almacenados fuera de las bases de datos de usuario  
 En lo que queda de este tema se resumen los posibles problemas que podrían afectar a una base de datos que se pone a disposición de otra instancia de servidor. Podría tener que volver a crear uno o varios de los tipos de información, entidades u objetos de la lista siguiente. Para ver un resumen, haga clic en el vínculo del elemento.  
  
-   [Valores de configuración del servidor](#server_configuration_settings)  
  
-   [Credenciales](#credentials)  
  
-   [Consultas entre bases de datos](#cross_database_queries)  
  
-   [Propiedad de la base de datos](#database_ownership)  
  
-   [Consultas distribuidas y servidores vinculados](#distributed_queries_and_linked_servers)  
  
-   [Datos cifrados](#encrypted_data)  
  
-   [Mensajes de error definidos por el usuario](#user_defined_error_messages)  
  
-   [Notificaciones de eventos y eventos del Instrumental de administración de Microsoft Windows (WMI) (en el nivel de servidor)](#event_notif_and_wmi_events)  
  
-   [Procedimientos almacenados extendidos](#extended_stored_procedures)  
  
-   [Propiedades del motor de texto completo para SQL Server](#ifts_service_properties)  
  
-   [Trabajos](#jobs)  
  
-   [Inicios de sesión](#logins)  
  
-   [Permisos](#permissions)  
  
-   [Configuración de replicación](#replication_settings)  
  
-   [Aplicaciones de Service Broker](#sb_applications)  
  
-   [Procedimientos de inicio](#startup_procedures)  
  
-   [Desencadenadores (en el nivel de servidor)](#triggers)  
  
##  <a name="server-configuration-settings"></a><a name="server_configuration_settings"></a> Server Configuration Settings  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores instalan e inician servicios y características clave de forma selectiva. Esto ayuda a reducir el área de un sistema susceptible de recibir ataques. Con la configuración predeterminada de nuevas instalaciones, no se habilitan muchas de las características. Si la base de datos se basa en un servicio o característica desactivada de forma predeterminada, este servicio o característica debe habilitarse en la instancia de servidor de destino.  
  
 Para obtener más información sobre estos valores de configuración y su habilitación o deshabilitación, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="credentials"></a><a name="credentials"></a>Sus  
 Una credencial es un registro que contiene la información de autenticación necesaria para conectarse a un recurso fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La mayoría de las credenciales consta de un inicio de sesión de Windows y una contraseña.  
  
 Para obtener más información sobre esta característica, vea [Credenciales &#40;motor de base de datos&#41;](../security/authentication-access/credentials-database-engine.md).  
  
> [!NOTE]  
>  Las cuentas de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usan credenciales. Para conocer el identificador de la credencial de una cuenta proxy, use la tabla del sistema [sysproxies](/sql/relational-databases/system-tables/dbo-sysproxies-transact-sql) .  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="cross-database-queries"></a><a name="cross_database_queries"></a>Consultas entre bases de datos  
 Las opciones de base de datos DB_CHAINING y TRUSTWORTHY se establecen, de forma predeterminada, en OFF. Si alguna de estas opciones se establece en ON para la base de datos original, es posible que deba habilitarlas en la base de datos de la instancia de servidor de destino. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 Las operaciones de adjuntar y separar deshabilitan el encadenamiento de propiedad entre bases de datos. Para obtener más información sobre cómo habilitar el encadenamiento, vea [cross db ownership chaining (opción de configuración del servidor)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
 Para obtener más información, vea también [Configurar una base de datos reflejada para usar la propiedad Trustworthy &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="database-ownership"></a><a name="database_ownership"></a>Propiedad de la base de datos  
 Cuando se restaura una base de datos en otro equipo, el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el usuario de Windows que inicia la operación de restauración se convierte automáticamente en el propietario de la nueva base de datos. Una vez restaurada la base de datos, el administrador del sistema o el nuevo propietario de la base de datos pueden cambiar la propiedad de la base de datos.  
  
##  <a name="distributed-queries-and-linked-servers"></a><a name="distributed_queries_and_linked_servers"></a> Consultas distribuidas y servidores vinculados  
 Las aplicaciones OLE DB admiten las consultas distribuidas y los servidores vinculados. Las consultas distribuidas obtienen acceso a datos desde varios orígenes de datos heterogéneos del mismo equipo o diferentes equipos. Una configuración con servidores vinculados permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutar comandos en orígenes de datos OLE DB situados en servidores remotos. Para obtener más información sobre estas características, vea [Servidores vinculados &#40;motor de base de datos&#41;](../linked-servers/linked-servers-database-engine.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="encrypted-data"></a><a name="encrypted_data"></a>Datos cifrados  
 Si la base de datos que pasa a estar disponible en otra instancia de servidor contiene datos cifrados y la clave maestra de la base de datos está protegida por la clave maestra de servicio del servidor original, es posible que deba volver a crear el cifrado de la clave maestra de servicio. La *clave maestra de la base de datos* es una clave simétrica que se utiliza para proteger las claves privadas de certificados y las claves asimétricas de una base de datos cifrada. Al crearla, la clave maestra de la base de datos se cifra mediante el algoritmo Triple DES y una contraseña proporcionada por el usuario.  
  
 Para habilitar el cifrado automático de la clave maestra de una instancia de servidor, se cifra una copia de esta clave mediante la clave maestra de servicio. Esta copia cifrada se almacena en la base de datos y en **maestra**. Normalmente, la copia almacenada en la **maestra** se actualiza automáticamente cada vez que se cambia la clave maestra. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta primero descifrar la clave maestra de base de datos con la clave maestra de servicio de la instancia. Si ese descifrado produce errores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] buscará en el almacén de credenciales las credenciales de clave maestra con el mismo GUID de familia que la base de datos para la que necesita la clave maestra. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentará después descifrar la clave maestra de la base de datos con cada credencial coincidente hasta que el descifrado se realice correctamente o no queden más credenciales. Para abrir una clave maestra que no se haya cifrado con la clave maestra de servicio, debe utilizarse la instrucción OPEN MASTER KEY y una contraseña.  
  
 Cuando se copia, restaura o adjunta una base de datos a una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], una copia de la clave maestra de la base de datos cifrada por la clave maestra de servicio no se almacena en **maestra** en la instancia de servidor de destino. Se debe abrir la clave maestra de la base de datos en esta instancia. Para abrir la clave maestra, ejecute la siguiente instrucción: abrir el descifrado de la clave maestra por contraseña **= '***contraseña***'**. Se recomienda habilitar el descifrado automático de la clave maestra de la base de datos ejecutando la siguiente instrucción: ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY. La instrucción ALTER MASTER KEY proporciona a la instancia de servidor una copia de la clave maestra de la base de datos que se ha cifrado con la clave maestra de servicio. Para obtener más información, vea [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) y [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
 Para obtener información sobre cómo habilitar el descifrado automático de la clave maestra de base de datos de una base de datos reflejada, vea [Establecer una base de datos reflejada cifrada](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md).  
  
 Para obtener más información, vea también:  
  
-   [Jerarquía de cifrado](../security/encryption/encryption-hierarchy.md)  
  
-   [Establecer una base de datos reflejada cifrada](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [Crear claves simétricas idénticas en dos servidores](../security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="user-defined-error-messages"></a><a name="user_defined_error_messages"></a>Mensajes de error definidos por el usuario  
 Los mensajes de error definidos por el usuario residen en la vista de catálogo [sys.messages](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages) . Esta vista se almacena en la base de datos **maestra**. Si una aplicación de la base de datos depende de los mensajes de error definidos por el usuario y la base de datos pasa a estar disponible en otra instancia del servidor, use [sp_addmessage](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql) para agregar esos mensajes de error en la instancia de servidor de destino.  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="event-notifications-and-windows-management-instrumentation-wmi-events-at-server-level"></a><a name="event_notif_and_wmi_events"></a> Las notificaciones de eventos y eventos de Windows Management Instrumentation (WMI) (en el nivel de servidor)  
  
### <a name="server-level-event-notifications"></a>Notificaciones de eventos del servidor  
 Las notificaciones de eventos del servidor se almacenan en la base de datos **msdb**. Por lo tanto, si una aplicación de la base de datos depende de las notificaciones de eventos del servidor, la notificación de un evento debe volver a crearse en la instancia de servidor de destino. Para ver las notificaciones de eventos de una instancia del servidor, use la vista de catálogo [sys.server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql) . Para más información, consulte [Event Notifications](../service-broker/event-notifications.md).  
  
 Además, las notificaciones de eventos se pueden entregar mediante [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Las rutas de los mensajes entrantes no están incluidas en la base de datos que contiene un servicio. En lugar de ello, las rutas explícitas se almacenan en la base de datos **msdb**. Si el servicio usa una ruta explicita de la base de datos **msdb** para enrutar los mensajes entrantes al servicio, cuando adjunte una base de datos en una instancia diferente debe volver a crear esta ruta.  
  
### <a name="windows-management-instrumentation-wmi-events"></a>Eventos de Instrumental de administración de Windows (WMI)  
 El proveedor WMI para eventos de servidor le permite utilizar el Instrumental de administración de Windows (WMI) para supervisar eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Toda aplicación que dependa de eventos de servidor expuestos a través del proveedor WMI del que depende la base de datos se debe definir en el equipo de la instancia de servidor de destino. El proveedor de eventos WMI crea notificaciones de evento con un servicio de destino definido en **msdb**.  
  
> [!NOTE]  
>  Para obtener más información, vea [Conceptos del proveedor WMI para eventos de servidor](../wmi-provider-server-events/wmi-provider-for-server-events-concepts.md).  
  
 **Para crear una alerta WMI mediante SQL Server Management Studio**  
  
-   [Create a WMI Event Alert](../../ssms/agent/create-a-wmi-event-alert.md)  
  
### <a name="how-event-notifications-work-for-a-mirrored-database"></a>Funcionamiento de las notificaciones de eventos para una base de datos reflejada  
 La entrega entre bases de datos de notificaciones de eventos que implica una base de datos reflejada es remota, por definición, porque la base de datos reflejada puede conmutar por error. [!INCLUDE[ssSB](../../includes/sssb-md.md)]proporciona compatibilidad especial para las bases de datos reflejadas, en forma de *rutas reflejadas*. En una ruta reflejada hay dos direcciones: una para la instancia de servidor principal y otra para la instancia del servidor reflejado.  
  
 Mediante la configuración de rutas reflejadas, se hace que el enrutamiento de [!INCLUDE[ssSB](../../includes/sssb-md.md)] reconozca la creación de reflejo de bases de datos. Las rutas reflejadas permiten que [!INCLUDE[ssSB](../../includes/sssb-md.md)] redireccione conversaciones de manera transparente a la instancia de servidor principal actual. Por ejemplo, considere un servicio, Service_A, que es hospedado por una base de datos reflejada, Database_A. Suponga que necesita que otro servicio, Service_B, que es hospedado por Database_B, tenga un diálogo con Service_A. Para que este diálogo sea posible, Database_B debe contener una ruta reflejada para Service_A. Además, Database_A debe contener una ruta de transporte TCP no reflejada a Service_B que, a diferencia de una ruta local, sigue siendo válida después de una conmutación por error. Estas rutas permiten que los ACK regresen después de la conmutación por error. Puesto que al servicio del remitente siempre se le asigna un nombre de la misma forma, la ruta debe especificar la instancia del agente.  
  
 El requisito de las rutas reflejadas es válido independientemente de que el servicio de la base de datos reflejada sea el servicio iniciador o el de destino:  
  
-   Si el servicio de destino está en la base de datos reflejada, el servicio iniciador debe tener una ruta reflejada de vuelta al destino. No obstante, el destino puede tener una ruta normal de vuelta al iniciador.  
  
-   Si el servicio iniciador está en la base de datos reflejada, el servicio de destino debe tener una ruta reflejada de vuelta al iniciador para entregar reconocimientos y respuestas. No obstante, el iniciador puede tener una ruta normal al destino.  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="extended-stored-procedures"></a><a name="extended_stored_procedures"></a>Procedimientos almacenados extendidos  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, use la [integración con CLR](../clr-integration/common-language-runtime-integration-overview.md) .  
  
 Los procedimientos almacenados extendidos se programan mediante la API Procedimiento almacenado extendido de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un miembro del rol fijo de servidor **sysadmin** puede registrar un procedimiento almacenado extendido con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y conceder permiso a los usuarios para que ejecuten el procedimiento. Los procedimientos almacenados extendidos solo se pueden agregar a la base de datos **maestra** .  
  
 Los procedimientos almacenados extendidos se ejecutan directamente en el espacio de direcciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y pueden producir fugas de memoria y otros problemas que reducen el rendimiento y la confiabilidad del servidor. Debe considerarse la posibilidad de almacenar procedimientos almacenados extendidos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independiente de la instancia que contiene los datos a los que hace referencia. También se debe considerar la posibilidad de utilizar consultas distribuidas para tener acceso a la base de datos.  
  
> [!IMPORTANT]  
>  Antes de agregar procedimientos almacenados extendidos al servidor y otorgar permisos EXECUTE a otros usuarios, el administrador del sistema debe revisar por completo cada procedimiento almacenado extendido para asegurarse de que no contiene código perjudicial o malintencionado.  
  
 Para obtener más información, vea [GRANT &#40;permisos de objeto de Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql), [DENY &#40;permisos de objeto de Transact-SQL&#41;](/sql/t-sql/statements/deny-object-permissions-transact-sql) y [REVOKE &#40;permisos de objeto de Transact-SQL&#41;](/sql/t-sql/statements/revoke-object-permissions-transact-sql).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="full-text-engine-for-sql-server-properties"></a><a name="ifts_service_properties"></a>Propiedades del motor de texto completo para SQL Server  
 Las propiedades se establecen en el motor de texto completo a través de [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql). Asegúrese de que la instancia de servidor de destino tiene la configuración necesaria para estas propiedades. Para obtener más información sobre estas propiedades, vea [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextserviceproperty-transact-sql).  
  
 Además, si el componente de [separadores de palabras y lematizadores](../search/configure-and-manage-word-breakers-and-stemmers-for-search.md) o el componente de [filtros de búsqueda de texto completo](../search/configure-and-manage-filters-for-search.md) tiene versiones diferentes en las instancias del servidor original y de destino, los índices de texto completo y las consultas pueden tener un comportamiento diferente. Además, el [diccionario de sinónimos](../search/full-text-search.md) se almacena en archivos específicos de la instancia. Se debe transferir una copia de esos archivos a una ubicación equivalente de la instancia de servidor de destino o volver a crearlos en la nueva instancia.  
  
> [!NOTE]  
>  Al adjuntar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contiene los archivos de catálogo de texto completo a una instancia del servidor de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , los archivos de catálogo se adjuntan de su ubicación anterior junto con los demás archivos de base de datos, igual que en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información, vea [Actualizar la búsqueda de texto completo](../search/upgrade-full-text-search.md).  
  
 Para obtener más información, vea también:  
  
-   [Realizar copias de seguridad de los catálogos e índices de texto completo y restaurarlos](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   [Creación de reflejo de la base de datos y catálogos de texto completo &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="jobs"></a><a name="jobs"></a>Tareas  
 Si la base de datos depende de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tendrá que volver a crearlos en la instancia de servidor de destino. Los trabajos dependen de sus entornos. Si tiene previsto volver a crear un trabajo existente en la instancia de servidor de destino, es posible que deba modificar esta instancia para que el entorno de ese trabajo coincida con la instancia de servidor original. Los siguientes factores del entorno son importantes:  
  
-   El inicio de sesión que utiliza el trabajo  
  
     Para crear o ejecutar trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , primero debe agregar en la instancia de servidor de destino cualquier inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el trabajo requiera. Para obtener más información, vea [Configurar un usuario para crear y administrar trabajos del Agente SQL Server](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md).  
  
-   Cuenta de inicio del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
     La cuenta de inicio del servicio define la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus permisos de red. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta como una cuenta de usuario especificada. El contexto del servicio del Agente afecta a la configuración del trabajo y a su entorno de ejecución. La cuenta debe tener acceso a los recursos (como por ejemplo, los recursos compartidos de red) que requiere el trabajo. Para obtener información sobre cómo seleccionar y modificar la cuenta de inicio del servicio, vea [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md).  
  
     Para que funcione correctamente, la cuenta de inicio del servicio se debe configurar para que disponga del dominio, el sistema de archivos y los permisos del Registro correctos. Además, es posible que un trabajo requiera un recurso de red compartido que debe configurarse para la cuenta de servicio. Para obtener información, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que está asociado a una instancia específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tiene su propio subárbol del Registro y sus trabajos suelen depender de uno o más parámetros de este subárbol. Un trabajo requiere estos parámetro del Registro para que funcione como se espera. Si utiliza un script para volver a crear un trabajo en otro servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , es posible que su Registro no tenga la configuración correcta para dicho trabajo. Para que los trabajos que se vuelven a crear se comporten correctamente en una instancia de servidor de destino, los servicios originales y de destino del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deberían tener la misma configuración del Registro.  
  
    > [!CAUTION]  
    >  El cambio de valores del Registro en el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino para controlar un trabajo que se ha vuelto a crear puede causar problemas si otros trabajos requieren los parámetros actuales. Además, si el Registro se modifica incorrectamente, pueden provocarse daños graves en el sistema. Antes de efectuar cambios en el Registro, es recomendable realizar una copia de seguridad de los datos importantes del equipo.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Servidores proxy del Agente  
  
     Un proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define el contexto de seguridad de un paso de trabajo especificado. Para ejecutar un trabajo en la instancia de servidor de destino, todos los servidores proxy que requiere se deben volver a crear manualmente en esa instancia. Para obtener más información, vea [Crear un proxy del Agente SQL Server](../../ssms/agent/create-a-sql-server-agent-proxy.md) y [Solucionar problemas de trabajos multiservidor que usan servidores proxy](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md).  
  
 Para obtener más información, vea también:  
  
-   [Implementar trabajos](../../ssms/agent/implement-jobs.md)  
  
-   [Administración de inicios de sesión y trabajos tras la conmutación de roles &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md) (para la creación de reflejo de base de datos)  
  
-   [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (al instalar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
  
-   [Configurar el Agente SQL Server](../../ssms/agent/sql-server-agent.md) (al instalar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
  
-   [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md)  
  
 **Para ver los trabajos existentes y sus propiedades**  
  
-   [Actividad de trabajos de monitor](../../ssms/agent/monitor-job-activity.md)  
  
-   [sp_help_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-job-transact-sql)  
  
-   [View Job Step Information](../../ssms/agent/view-job-step-information.md)  
  
-   [dbo.sysjobs &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobs-transact-sql)  
  
 **Para crear un trabajo**  
  
-   [Crear un trabajo](../../ssms/agent/create-a-job.md)  
  
-   [Crear un trabajo](../../ssms/agent/create-a-job.md)  
  
#### <a name="best-practices-for-using-a-script-to-re-create-a-job"></a>Prácticas recomendadas para usar un script para volver a crear un trabajo  
 Se recomienda empezar por la generación de un script para un trabajo simple; volver a crear el trabajo en el otro servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ejecutarlo para ver si funciona como se espera. Esto permitirá identificar las incompatibilidades e intentar resolverlas. Si el trabajo generado con el script no funciona como se espera en este nuevo entorno, se recomienda crear un trabajo equivalente que funcione de forma correcta en ese entorno.  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="logins"></a><a name="logins"></a>Inicios  
 Para iniciar una sesión en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se requiere un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Este inicio de sesión se utiliza en el proceso de autenticación que comprueba si la entidad de seguridad puede conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un usuario de base de datos cuyo inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente está sin definir o se ha definido de forma incorrecta en una instancia de servidor no podrá iniciar una sesión en la instancia. Es lo que se denomina un *usuario huérfano* de la base de datos en esa instancia de servidor. También puede convertirse en huérfano si se restaura, adjunta o copia una base de datos a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para generar un script de algunos o todos los objetos de la copia original de la base de datos, se puede usar el asistente Generar scripts y, en el cuadro de diálogo **Elegir opciones de script** , configurar la opción **Incluir inicios de sesión en el script** en **True**.  
  
> [!NOTE]  
>  Para obtener información sobre cómo configurar los inicios de sesión de una base de datos reflejada, vea [Configurar cuentas de inicio de sesión para la creación de reflejo de la base de datos o grupos de disponibilidad de AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md) y [Administración de inicios de sesión y trabajos tras la conmutación de roles &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="permissions"></a><a name="permissions"></a> Permisos  
 Los siguientes tipos de permisos se podrían ver afectados cuando una base de datos se pone a disposición de otra instancia de servidor.  
  
-   Permisos GRANT, REVOKE o DENY sobre los objetos del sistema  
  
-   Permisos GRANT, REVOKE o DENY sobre la instancia del servidor (*permisos de servidor*)  
  
### <a name="grant-revoke-and-deny-permissions-on-system-objects"></a>Permisos GRANT, REVOKE o DENY sobre los objetos del sistema  
 Los permisos de los objetos del sistema como procedimientos almacenados, procedimientos almacenados extendidos, funciones y vistas, se almacenan en la base de datos **maestra** y se deben configurar en la instancia de servidor de destino.  
  
 Para generar un script de algunos o todos los objetos de la copia original de la base de datos, se puede usar el asistente Generar scripts y, en el cuadro de diálogo **Elegir opciones de script**, configurar la opción **Incluir permisos de objeto en el script** en **True**.  
  
> [!IMPORTANT]  
>  Si incluye inicios de sesión en el script, no se incluirán las contraseñas. Si tiene inicios de sesión que usan la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , deberá modificar el script en el destino.  
  
 Puede ver los objetos del sistema en la vista de catálogo [sys.system_objects](/sql/relational-databases/system-catalog-views/sys-system-objects-transact-sql) . Los permisos de los objetos del sistema están visibles en la vista de catálogo [Sys. database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) de la base de datos **maestra** . Para obtener información sobre las consultas de estas vistas de catálogo y la concesión de permisos de objetos del sistema, vea [GRANT &#40;permisos de objeto de sistema de Transact-SQL&#41;](/sql/t-sql/statements/grant-system-object-permissions-transact-sql). Para obtener más información, vea [REVOKE &#40;permisos de objeto de sistema de Transact-SQL&#41;](/sql/t-sql/statements/revoke-system-object-permissions-transact-sql) y [DENY &#40;permisos de objeto de sistema de Transact-SQL&#41;](/sql/t-sql/statements/deny-system-object-permissions-transact-sql).  
  
### <a name="grant-revoke-and-deny-permissions-on-a-server-instance"></a>Permisos GRANT, REVOKE o DENY sobre la instancia de servidor  
 Los permisos en el ámbito del servidor se almacenan en la base de datos **maestra** y se deben configurar en la instancia de servidor de destino. Para obtener información sobre los permisos de servidor de una instancia de servidor, consulte la vista de catálogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) ; para obtener información sobre las entidades de seguridad de servidor, consulte la vista de catálogo [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)y, para obtener información sobre la pertenencia a los roles de servidor, consulte la vista de catálogo [sys.server_role_members](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql) .  
  
 Para obtener más información, vea [GRANT &#40;permisos de servidor de Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql), [REVOKE &#40;permisos de objeto de Transact-SQL&#41;](/sql/t-sql/statements/revoke-server-permissions-transact-sql) y [DENY &#40;permisos de objeto de Transact-SQL&#41;](/sql/t-sql/statements/deny-server-permissions-transact-sql).  
  
#### <a name="server-level-permissions-for-a-certificate-or-asymmetric-key"></a>Permisos de nivel de servidor para un certificado o clave asimétrica  
 Los permisos de nivel de servidor para un certificado o clave asimétrica no se pueden conceder directamente. En su lugar, los permisos de nivel de servidor se conceden a un inicio de sesión asignado que se crea exclusivamente para un certificado o clave asimétrica. Por lo tanto, cada certificado o clave asimétrica que requiere permisos de nivel de servidor, necesita su propio *inicio de sesión asignado a un certificado* o *inicio de sesión asignado a una clave asimétrica*. Para conceder permisos de nivel de servidor para un certificado o clave asimétrica, conceda los permisos a su inicio de sesión asignado.  
  
> [!NOTE]  
>  Un inicio de sesión asignado solo se utiliza para la autorización de código firmado con el certificado o clave asimétrica correspondiente. Los inicios de sesión asignados no se pueden utilizar para la autenticación.  
  
 El inicio de sesión asignado y sus permisos residen en la base de datos **maestra**. Si un certificado o clave asimétrica reside en una base de datos que no sea **maestra**, se debe volver a crear en **maestra** y asignarlo a un inicio de sesión. Si la base de datos se mueve, copia o restaura en otra instancia del servidor, se deben volver a crear sus certificados o claves asimétricas en la base de datos **maestra** de la instancia del servidor de destino, asignarlos a un inicio de sesión y conceder a este los permisos necesarios de nivel de servidor.  
  
 **Para crear un certificado o clave asimétrica**  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
 **Para asignar un certificado o clave asimétrica a un inicio de sesión**  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 **Para asignar permisos a un inicio de sesión asignado**  
  
-   [GRANT &#40;permisos de servidor de Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql)  
  
 Para obtener más información acerca de los certificados y las claves asimétricas, vea [Encryption Hierarchy](../security/encryption/encryption-hierarchy.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="replication-settings"></a><a name="replication_settings"></a>Configuración de replicación  
 Si restaura una copia de seguridad de una base de datos replicada en otro servidor o base de datos, no se conservará la configuración de la replicación. En este caso, deberá volver a crear todas las publicaciones y suscripciones después de restaurar las copias de seguridad. Para facilitar este proceso, cree scripts para la configuración actual de la replicación y también para habilitar y deshabilitar la replicación. Para volver a crear los parámetros de la replicación, copie estos scripts y cambie las referencias del nombre de servidor para que funcionen con la instancia de servidor de destino.  
  
 Para obtener más información, vea [Hacer copias de seguridad y restaurar bases de datos replicadas](../replication/administration/back-up-and-restore-replicated-databases.md), [Replicación y creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md) y [Trasvase de registros y replicación &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="service-broker-applications"></a><a name="sb_applications"></a>Aplicaciones Service Broker  
 Muchos aspectos de una aplicación de [!INCLUDE[ssSB](../../includes/sssb-md.md)] se mueven con la base de datos. No obstante, algunos aspectos deben volver a crearse o configurarse en la nueva ubicación.  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="startup-procedures"></a><a name="startup_procedures"></a>Procedimientos de inicio  
 Un procedimiento de inicio es un procedimiento almacenado que se marca para su ejecución automática y se ejecuta cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la base de datos depende de algún procedimiento de inicio, se deben definir en la instancia de servidor de destino y configurarse para su ejecución automática durante el inicio.  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
##  <a name="triggers-at-server-level"></a><a name="triggers"></a>Desencadenadores (en el nivel de servidor)  
 Los desencadenadores DDL activan procedimientos almacenados en respuesta a una variedad de eventos del lenguaje de definición de datos (DDL). Estos eventos corresponden principalmente a instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que comienzan por las palabras clave CREATE, ALTER y DROP. Algunos procedimientos almacenados del sistema que ejecutan operaciones de tipo DDL también pueden activar desencadenadores DDL.  
  
 Para obtener más información acerca de esta característica, vea [DDL Triggers](../triggers/ddl-triggers.md).  
  
 [&#91;Principio&#93;](#information_entities_and_objects)  
  
## <a name="see-also"></a>Consulte también  
 [Bases de datos independientes](contained-databases.md)   
 [Copiar bases de datos en otros servidores](copy-databases-to-other-servers.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [Conmutar por error a una &#40;secundaria de trasvase de registros SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Configurar una base de datos reflejada cifrada](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [Administrador de configuración de SQL Server](../sql-server-configuration-manager.md)   
 [Solucionar problemas de usuarios huérfanos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
