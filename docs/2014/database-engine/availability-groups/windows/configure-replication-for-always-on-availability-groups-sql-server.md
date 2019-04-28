---
title: Configurar la replicación para grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 4e001426-5ae0-4876-85ef-088d6e3fb61c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 547ebeb6043345821d2b2a19b407599abfd14008
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814714"
---
# <a name="configure-replication-for-always-on-availability-groups-sql-server"></a>Configurar la replicación para grupos de disponibilidad AlwaysOn (SQL Server)
  La configuración de la replicación y los grupos de disponibilidad AlwaysOn de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere siete pasos. Cada paso se describe con más detalle en las secciones siguientes.  
  

  
##  <a name="step1"></a> 1. Configurar las publicaciones y suscripciones de la base de datos  
 **Configurar el distribuidor**  
  
 El distribuidor no debe ser un host para ninguna de las réplicas actuales (o previstas) del grupo de disponibilidad del que la base de datos de publicación es (o será) un miembro.  
  
1.  Configure la distribución en el distribuidor. Si se utilizan procedimientos almacenados para la configuración, ejecute `sp_adddistributor`. Use el parámetro de *@password* para identificar la contraseña que se utilizará cuando un publicador remoto se conecte al distribuidor. También se necesitará la contraseña de cada publicador remoto cuando el distribuidor remoto está configurado.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistributor  
        @distributor = 'MyDistributor',  
        @password = '**Strong password for distributor**';  
    ```  
  
2.  Cree la base de datos de distribución en el distribuidor. Si se utilizan procedimientos almacenados para la configuración, ejecute `sp_adddistributiondb`.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistributiondb  
        @database = 'distribution',  
        @security_mode = 1;  
    ```  
  
3.  Configure el publicador remoto. Si se utilizan procedimientos almacenados para configurar el distribuidor, ejecute `sp_adddistpublisher`. El parámetro *@security_mode* se usa para determinar cómo se conecta a la réplica principal actual el procedimiento almacenado de validación del publicador que se ejecuta desde los agente de replicación. Si se establece en 1, la autenticación de Windows se usa para conectarse a la réplica principal actual. Si se establece en 0, se usa la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con los valores especificados *@login* y *@password* . El inicio de sesión y la contraseña especificados deben ser válidos en cada réplica secundaria para que el procedimiento almacenado de validación se conecte correctamente a esa réplica.  
  
    > [!NOTE]  
    >  Si algunos agentes de replicación modificados se ejecutan en un equipo distinto del distribuidor, el uso de la autenticación de Windows para la conexión a la principal requerirá que la autenticación Kerberos se configure para la comunicación entre equipos host de réplica. El uso de un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la conexión a la principal actual no necesita la autenticación Kerberos.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_adddistpublisher  
        @publisher = 'AGPrimaryReplicaHost',  
        @distribution_db = 'distribution',  
        @working_directory = '\\MyReplShare\WorkingDir',  
        @login = 'MyPubLogin',  
        @password = '**Strong password for publisher**';  
    ```  
  
 Para obtener más información, vea [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql).  
  
 **Configurar el publicador en el publicador original**  
  
1.  Configure el distribuidor remoto. Si se emplean procedimientos almacenados para configurar el publicador, ejecute `sp_adddistributor`. Especifique el mismo valor para *@password* que utilizó cuando `sp_adddistrbutor` se ejecutó en el distribuidor para configurar la distribución.  
  
    ```  
    exec sys.sp_adddistributor  
        @distributor = 'MyDistributor',  
        @password = 'MyDistPass'  
    ```  
  
2.  Habilite la base de datos para replicación. Si se emplean procedimientos almacenados para configurar el publicador, ejecute `sp_replicationdboption`. Si la replicación transaccional y de mezcla se configuran para la base de datos, cada una debe estar habilitada.  
  
    ```  
    USE master;  
    GO  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'true';  
  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'merge publish',  
        @value = 'true';  
    ```  
  
3.  Cree la publicación de replicación, los artículos y las suscripciones. Para obtener más información acerca de cómo configurar la replicación, vea los objetos Publicar datos y Base de datos.  
  
##  <a name="step2"></a> 2. Configurar el grupo de disponibilidad AlwaysOn  
 En la principal deseada, cree el grupo de disponibilidad con la base de datos publicada (o que va a ser publicada) como una base de datos de miembros. Si usa el Asistente para grupo de disponibilidad, puede permitir que el asistente sincronice inicialmente las bases de datos de réplica secundaria o puede realizar la inicialización manualmente mediante copias de seguridad y restauración.  
  
 Cree un agente de escucha DNS para el grupo de disponibilidad que utilizarán los agentes de replicación para conectarse a la principal actual. El nombre del agente de escucha especificado se utilizará como el destino de la redirección para el par publicador original y base de datos publicada. Por ejemplo, si utiliza DDL para configurar el grupo de disponibilidad, el siguiente ejemplo de código se puede usar para especificar un agente de escucha para un grupo de disponibilidad denominado `MyAG`:  
  
```  
ALTER AVAILABILITY GROUP 'MyAG'   
    ADD LISTENER 'MyAGListenerName' (WITH IP (('10.120.19.155', '255.255.254.0')));  
```  
  
 Para obtener más información, vea [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md).  
  
##  <a name="step3"></a> 3. Asegurarse de que todos los hosts de la réplica secundaria están configurados para la replicación  
 Compruebe que se ha configurado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cada host de réplica secundaria para admitir la replicación. La siguiente consulta se puede ejecutar en cada host de réplica secundaria para determinar si está instalada la replicación:  
  
```  
USE master;  
GO  
DECLARE @installed int;  
EXEC @installed = sys.sp_MS_replication_installed;  
SELECT @installed;  
```  
  
 Si *@installed* es 0, se debe agregar la replicación a la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="step4"></a> 4. Configurar los hosts de la réplica secundaria como publicadores de replicación  
 Una réplica secundaria no puede actuar como un publicador o republicador de la replicación, pero la replicación debe configurarse de modo que la secundaria pueda asumir el control después de una conmutación por error. En el distribuidor, configure la distribución para cada host de réplica secundaria. Especifique la misma base de datos de distribución y directorio de trabajo que se especificó cuando se agregó el publicador original en el distribuidor. Si usa procedimientos almacenados para configurar la distribución, utilice `sp_adddistpublisher` para asociar los publicadores remotos al distribuidor. Si *@login* y *@password* , especifique los mismos valores al agregar los hosts de la réplica secundaria como publicadores.  
  
```  
EXEC sys.sp_adddistpublisher  
    @publisher = 'AGSecondaryReplicaHost',  
    @distribution_db = 'distribution',  
    @working_directory = '\\MyReplShare\WorkingDir',  
    @login = 'MyPubLogin',  
    @password = '**Strong password for publisher**';  
```  
  
 En cada host de réplica secundaria, configure la distribución. Identifique el distribuidor del publicador original como distribuidor remoto. Use la misma contraseña que se utiliza al ejecutar `sp_adddistributor` originalmente en el distribuidor. Si se utilizan procedimientos almacenados para configurar la distribución, el *@password* parámetro de `sp_adddistributor` se usa para especificar la contraseña.  
  
```  
EXEC sp_adddistributor   
    @distributor = 'MyDistributor',  
    @password = '**Strong password for distributor**';  
```  
  
 En cada host de réplica secundaria, asegúrese de que los suscriptores de inserción de publicaciones de la base de datos aparezcan como servidores vinculados. Si se emplean procedimientos almacenados para configurar los publicadores remotos, use `sp_addlinkedserver` para agregar los suscriptores (si todavía no están presentes) como servidores vinculados para los publicadores.  
  
```  
EXEC sys.sp_addlinkedserver   
    @server = 'MySubscriber';  
```  
  
##  <a name="step5"></a> 5. Redirigir el publicador original al nombre del agente de escucha  
 En el distribuidor, en la base de datos de distribución, ejecute el procedimiento almacenado `sp_redirect_publisher` para asociar el publicador original y la base de datos publicada al nombre del agente de escucha del grupo de disponibilidad.  
  
```  
USE distribution;  
GO  
EXEC sys.sp_redirect_publisher   
@original_publisher = 'MyPublisher',  
    @publisher_db = 'MyPublishedDB',  
    @redirected_publisher = 'MyAGListenerName';  
```  
  
##  <a name="step6"></a> 6. Ejecutar el procedimiento almacenado de validación de la replicación para comprobar la configuración  
 En el distribuidor, en la base de datos de distribución, ejecute el procedimiento almacenado `sp_validate_replica_hosts_as_publishers` para comprobar que ahora todos los hosts de la réplica se configuran para servir como publicadores de la base de datos publicada.  
  
```  
USE distribution;  
GO  
DECLARE @redirected_publisher sysname;  
EXEC sys.sp_validate_replica_hosts_as_publishers  
    @original_publisher = 'MyPublisher',  
    @publisher_db = 'MyPublishedDB',  
    @redirected_publisher = @redirected_publisher output;  
```  
  
 El procedimiento almacenado `sp_validate_replica_hosts_as_publishers` se debe ejecutar desde un inicio de sesión con autorización suficiente en cada host de réplica del grupo de disponibilidad para consultar información acerca del grupo de disponibilidad. A diferencia de `sp_validate_redirected_publisher`, usa las credenciales del llamador y no utiliza el inicio de sesión que se conservan en msdb.dbo.MSdistpublishers para conectarse a las réplicas del grupo de disponibilidad.  
  
> [!NOTE]  
>  `sp_validate_replica_hosts_as_publishers` producirá el error siguiente al validar los hosts de réplica secundaria que no permiten el acceso de lectura o requieren especificar la intención de lectura.  
>   
>  Mensaje 21899, nivel 11, estado 1, procedimiento `sp_hadr_verify_subscribers_at_publisher`, línea 109  
>   
>  La consulta en el publicador redireccionado "MyReplicaHostName" para determinar si hay entradas de sysserver para los suscriptores del publicador original "MyOriginalPublisher" no se ha podido realizar por el error "976", mensaje de error "Error 976, Level 14, State 1, Message: La base de datos de destino "MyPublishedDB" participa en un grupo de disponibilidad y actualmente no es accesible para las consultas. El movimiento de datos se ha suspendido o la réplica de disponibilidad no está habilitada para el acceso de lectura. Para permitir el acceso de solo lectura a esta y a otras bases de datos del grupo de disponibilidad, habilite el acceso de lectura en una o varias réplicas de disponibilidad secundarias del grupo.  Para obtener más información, vea la instrucción `ALTER AVAILABILITY GROUP` en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]'.  
>   
>  Se encontraron uno o varios errores de validación del publicador para el host de réplica 'MyReplicaHostName'.  
  
 Este es el comportamiento normal. Debe comprobar la presencia de las entradas del servidor del suscriptor en estos host de réplica secundaria consultando las entradas de sysserver directamente en el host.  
  
##  <a name="step7"></a> 7. Agregar el publicador original al Monitor de replicación  
 En cada réplica del grupo de disponibilidad, agregue el publicador original al Monitor de replicación.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Replicación**  
  
-   [Mantener una base de datos de publicación AlwaysOn &#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [Replicación, seguimiento de cambios, captura de datos modificados y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)  
  
-   [Preguntas más frecuentes para administradores de replicación](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
 **Para crear y configurar un grupo de disponibilidad**  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Crear un grupo de disponibilidad &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Crear una base de datos de extremo de reflejo para grupos de disponibilidad AlwaysOn &#40;PowerShell de SQL Server&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn: Interoperabilidad (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [Replicación de SQL Server](../../../relational-databases/replication/sql-server-replication.md)  
  
  
