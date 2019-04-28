---
title: Crear un grupo de disponibilidad (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: 8b0a6301-8b79-4415-b608-b40876f30066
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 13d14fafd18fb9e0cdb156617798c8d2f15ff661
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815368"
---
# <a name="create-an-availability-group-transact-sql"></a>Crear un grupo de disponibilidad (Transact-SQL)
  En este tema se describe cómo usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] para crear y configurar un grupo de disponibilidad en las instancias de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] en que se habilita la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Un *grupo de disponibilidad* define un conjunto de bases de datos de usuario que realizarán la conmutación por error como una sola unidad y un conjunto de asociados de conmutación por error, conocido como *réplicas de disponibilidad*, que admiten la conmutación por error.  
  
> [!NOTE]  
>  Para obtener una introducción a los grupos de disponibilidad, vea [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  

  
> [!NOTE]  
>  Como alternativa al uso de [!INCLUDE[tsql](../../../includes/tsql-md.md)], puede usar el Asistente para crear grupo de disponibilidad o cmdlets de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obtener más información, vea [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md), [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)o [Crear un grupo de disponibilidad &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
 Se recomienda encarecidamente leer esta sección antes de intentar crear el primer grupo de disponibilidad.  
  
###  <a name="PrerequisitesRestrictions"></a> Requisitos previos, restricciones y recomendaciones  
  
-   Antes de crear un grupo de disponibilidad, compruebe que las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedan réplicas de disponibilidad residen en otro nodo (WSFC) de clúster de conmutación por error de Windows Server en el mismo clúster de conmutación por error de WSFC. Además, compruebe que cada una de las instancias del servidor cumple los requisitos previos de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para más información, recomendamos encarecidamente que lea [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
###  <a name="SummaryTsqlStatements"></a> Resumen de las tareas e instrucciones Transact-SQL correspondientes  
 En la tabla siguiente se enumeran las tareas básicas relacionadas con la creación y configuración de un grupo de disponibilidad y se indican las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] que han de utilizarse para estas tareas. Las tareas de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se deben realizar en la secuencia en que se muestran en la tabla.  
  
|Tarea|Instrucciones Transact-SQL|Dónde realizar la tarea**<sup>*</sup>**|  
|----------|----------------------------------|-------------------------------------------|  
|Crear extremo de creación de reflejo de la base de datos (una vez por instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )|[CREATE ENDPOINT](/sql/t-sql/statements/create-endpoint-transact-sql) *nombre_del_punto_de_conexión* ... FOR DATABASE_MIRRORING|Se ejecuta en cada instancia del servidor que carece de extremo de creación de reflejo de la base de datos.|  
|Crear grupo de disponibilidad|[CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)|Se ejecuta en la instancia del servidor que va a hospedar la réplica principal inicial.|  
|Unir la réplica secundaria al grupo de disponibilidad|[ALTER AVAILABILITY GROUP](join-a-secondary-replica-to-an-availability-group-sql-server.md) *group_name* JOIN|Se ejecuta en cada una de las instancias del servidor que hospedan una réplica secundaria.|  
|Preparar la base de datos secundaria|[BACKUP](/sql/t-sql/statements/backup-transact-sql) y [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql).|Se crean las copias de seguridad de la instancia del servidor que hospeda la réplica principal.<br /><br /> Se restauran las copias de seguridad en cada una de las instancias del servidor que hospedan una réplica secundaria utilizando RESTORE WITH NORECOVERY.|  
|Iniciar la sincronización de datos uniendo cada base de datos secundaria al grupo de disponibilidad|[ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) *database_name* SET HADR AVAILABILITY GROUP = *group_name*|Se ejecuta en cada una de las instancias del servidor que hospedan una réplica secundaria.|  
  
 **<sup>*</sup>**  Para llevar a cabo una tarea determinada, conéctese a la instancia del servidor indicado o instancias.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL para crear y configurar un grupo de disponibilidad  
  
> [!NOTE]  
>  Para obtener un procedimiento de configuración de ejemplo que contiene ejemplos de código de cada una de estas instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)], vea [Ejemplo: Configuración de un grupo de disponibilidad que usa la Autenticación de Windows](#ExampleConfigAGWinAuth).  
  
1.  Conéctese a la instancia del servidor que va a hospedar la réplica principal.  
  
2.  Cree el grupo de disponibilidad mediante la instrucción [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
3.  Una la nueva réplica secundaria al grupo de disponibilidad. Para obtener más información, vea [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
4.  Para cada base de datos del grupo de disponibilidad, cree una base de datos secundaria restaurando las copias de seguridad recientes de la base de datos principal, utilizando RESTORE WITH NORECOVERY. Para más información, vea [Ejemplo: Configuración de un grupo de disponibilidad mediante la Autenticación de Windows (Transact-SQL)](create-an-availability-group-transact-sql.md), comenzando por el paso que restaura la copia de seguridad de la base de datos.  
  
5.  Una cada nueva base de datos secundaria al grupo de disponibilidad. Para obtener más información, vea [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
##  <a name="ExampleConfigAGWinAuth"></a> Ejemplo: Configurar un grupo de disponibilidad que utiliza la autenticación de Windows  
 En este ejemplo se crea un procedimiento de configuración de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] de ejemplo que utiliza [!INCLUDE[tsql](../../../includes/tsql-md.md)] para configurar los extremos de creación de reflejo de la base de datos que utilizan la Autenticación de Windows y para crear y configurar un grupo de disponibilidad y sus bases de datos secundarias.  
  
 Este ejemplo contiene las siguientes secciones:  
  
-   [Requisitos previos para utilizar el procedimiento de configuración de ejemplo](#PrerequisitesForExample)  
  
-   [Procedimiento de configuración de ejemplo](#SampleProcedure)  
  
-   [Ejemplo completo de código del procedimiento de configuración de ejemplo](#CompleteCodeExample)  
  
###  <a name="PrerequisitesForExample"></a> Requisitos previos para utilizar el procedimiento de configuración de ejemplo  
 Este procedimiento de ejemplo tiene los requisitos siguientes:  
  
-   Las instancias del servidor deben admitir [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para más información, vea [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Debe haber dos bases de datos, *MyDb1* y *MyDb2*, en la instancia del servidor que va a hospedar la réplica principal. En los siguientes ejemplos de código se crean y configuran estas dos bases de datos y se crea una copia de seguridad completa de cada una. Ejecute estos ejemplos de código en la instancia del servidor en que desea crear el grupo de disponibilidad de ejemplo. Esta instancia del servidor hospedará la réplica principal inicial del grupo de disponibilidad de ejemplo.  
  
    1.  En el siguiente ejemplo de [!INCLUDE[tsql](../../../includes/tsql-md.md)] se crean estas bases de datos y se modifican para utilizar el modelo de recuperación completa:  
  
        ```  
        -- Create sample databases:  
        CREATE DATABASE MyDb1;  
        GO  
        ALTER DATABASE MyDb1 SET RECOVERY FULL;  
        GO  
  
        CREATE DATABASE MyDb2;  
        GO  
        ALTER DATABASE MyDb2 SET RECOVERY FULL;  
        GO  
        ```  
  
    2.  En el ejemplo de código siguiente se crea una copia de seguridad completa de las bases de datos *MyDb1* y *MyDb2*. En este ejemplo de código se usa un recurso compartido de copia de seguridad ficticio, \ \\\\*FILESERVER*\\*SQLbackups*.  
  
        ```  
        -- Backup sample databases:  
        BACKUP DATABASE MyDb1   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
            WITH FORMAT  
        GO  
  
        BACKUP DATABASE MyDb2   
        TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
            WITH FORMAT  
        GO  
  
        ```  
  
###  <a name="SampleProcedure"></a> Procedimiento de configuración de ejemplo  
 En esta configuración de ejemplo, la réplica de disponibilidad se creará en dos instancias del servidor independientes cuyas cuentas de servicio se ejecutan en diferentes dominios de confianza (`DOMAIN1` y `DOMAIN2`).  
  
 En la siguiente tabla se resumen los valores utilizados en esta configuración de ejemplo.  
  
|Rol inicial|Sistema|Hospeda la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|------------------|------------|---------------------------------------------|  
|Principal|`COMPUTER01`|`AgHostInstance`|  
|Secundario|`COMPUTER02`|instancia predeterminada.|  
  
1.  Cree un punto de conexión de creación de reflejo de la base de datos denominado *dbm_endpoint* en la instancia del servidor en la que planea crear el grupo de disponibilidad (se trata de una instancia llamada `AgHostInstance` en `COMPUTER01`). Este punto de conexión usa el puerto 7022. Tenga en cuenta que la instancia del servidor en que se crea el grupo de disponibilidad hospedará la réplica principal.  
  
    ```  
    -- Create endpoint on server instance that hosts the primary replica:  
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
  
    ```  
  
2.  Cree un punto de conexión *dbm_endpoint* en la instancia del servidor que hospedará la réplica secundaria (se trata de la instancia del servidor predeterminada en `COMPUTER02`). Este extremo usa el puerto 5022.  
  
    ```  
    -- Create endpoint on server instance that hosts the secondary replica:   
    CREATE ENDPOINT dbm_endpoint  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=5022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
  
    ```  
  
3.  > [!NOTE]  
    >  Si las cuentas de servicio de las instancias del servidor que van a hospedar las réplicas de disponibilidad se ejecutan en la misma cuenta de dominio, este paso no es necesario. Omítalo y vaya directamente al paso siguiente.  
  
     Si las cuentas de servicio de las instancias del servidor se ejecutan en usuarios de dominio diferentes, en cada instancia del servidor, cree un inicio de sesión para la otra instancia del servidor y conceda este permiso de inicio de sesión para tener acceso al extremo de creación de reflejo de la base de datos local.  
  
     En el ejemplo de código siguiente se muestran las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] para crear un inicio de sesión y concederle permiso en un extremo. La cuenta de dominio de la instancia del servidor remoto se representa aquí como *domain_name*\\*user_name*.  
  
    ```  
    -- If necessary, create a login for the service account, domain_name\user_name  
    -- of the server instance that will host the other replica:  
    USE master;  
    GO  
    CREATE LOGIN [domain_name\user_name] FROM WINDOWS;  
    GO  
    -- And Grant this login connect permissions on the endpoint:  
    GRANT CONNECT ON ENDPOINT::dbm_endpoint   
       TO [domain_name\user_name];  
    GO  
    ```  
  
4.  En la instancia del servidor donde residen las bases de datos de usuario, cree el grupo de disponibilidad.  
  
     En el ejemplo de código siguiente se crea un grupo de disponibilidad denominado *MyAG* en la instancia del servidor en la que se crearon las bases de datos de ejemplo, *MyDb1* y *MyDb2*. La instancia del servidor local, `AgHostInstance`, en *COMPUTER01* se especifica primero. Esta instancia hospedará la réplica principal inicial. Una instancia del servidor remoto, la instancia del servidor predeterminada en *COMPUTER02*, se especifica para hospedar una réplica secundaria. Ambas réplicas de disponibilidad están configuradas para usar el modo de confirmación asincrónica con conmutación por error manual (para las réplicas de confirmación asincrónica, la conmutación por error manual significa una conmutación por error forzada con posible pérdida de datos).  
  
    ```  
  
              -- Create the availability group, MyAG:   
    CREATE AVAILABILITY GROUP MyAG   
       FOR   
          DATABASE MyDB1, MyDB2   
       REPLICA ON   
          'COMPUTER01\AgHostInstance' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',   
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             ),  
          'COMPUTER02' WITH   
             (  
             ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );   
    GO  
    ```  
  
     Para obtener ejemplos adicionales de código [!INCLUDE[tsql](../../../includes/tsql-md.md)] para la creación de un grupo de disponibilidad, vea [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql).  
  
5.  En la instancia del servidor que hospeda la réplica secundaria, combine la réplica secundaria con el grupo de disponibilidad.  
  
     En el ejemplo de código siguiente se une la réplica secundaria de `COMPUTER02` al grupo de disponibilidad `MyAG` .  
  
    ```  
    -- On the server instance that hosts the secondary replica,   
    -- join the secondary replica to the availability group:  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    GO  
    ```  
  
6.  En la instancia del servidor que hospeda la réplica secundaria, cree las bases de datos secundarias.  
  
     En el ejemplo de código siguiente se crean las bases de datos secundarias *MyDb1* y *MyDb2* mediante la restauración de las copias de seguridad de base de datos con RESTORE WITH NORECOVERY.  
  
    ```  
    -- On the server instance that hosts the secondary replica,   
    -- Restore database backups using the WITH NORECOVERY option:  
    RESTORE DATABASE MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NORECOVERY  
    GO  
  
    RESTORE DATABASE MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH NORECOVERY  
    GO  
  
    ```  
  
7.  En la instancia del servidor que hospeda la réplica principal, realice una copia de seguridad del registro de transacciones en cada una de las bases de datos principales.  
  
    > [!IMPORTANT]  
    >  Cuando configure un grupo de disponibilidad real, conviene que, antes de realizar la copia de seguridad de registros, suspenda las tareas de copia de seguridad de registros para las bases de datos principales hasta haber combinado las bases de datos secundarias con el grupo de disponibilidad.  
  
     En el ejemplo de código siguiente se crea una copia de seguridad del registro de transacciones en MyDb1 y en MyDb2.  
  
    ```  
    -- On the server instance that hosts the primary replica,   
    -- Backup the transaction log on each primary database:  
    BACKUP LOG MyDb1   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH NOFORMAT  
    GO  
  
    BACKUP LOG MyDb2   
    TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITHNOFORMAT  
    GO  
  
    ```  
  
    > [!TIP]  
    >  Normalmente, debe realizarse una copia de seguridad de registros en cada base de datos principal y, después, restaurarse en la base de datos secundaria correspondiente (utilizando WITH NORECOVERY). Sin embargo, puede que no se necesite esta copia de seguridad de registros si la base de datos se ha creado recientemente y no se ha realizado todavía ninguna copia de seguridad de registros, o si el modelo de recuperación ha cambiado recientemente de SIMPLE a FULL.  
  
8.  En la instancia del servidor que hospeda la réplica secundaria, aplique las copias de seguridad de registros a las bases de datos secundarias.  
  
     En el ejemplo de código siguiente se aplican copias de seguridad a las bases de datos secundarias *MyDb1* y *MyDb2* mediante la restauración de las copias de seguridad de base de datos con RESTORE WITH NORECOVERY.  
  
    > [!IMPORTANT]  
    >  Cuando se prepara una base de datos secundaria real, es necesario aplicar cada copia de seguridad de registros desde la copia de seguridad de base de datos a partir de la cual se creó la base de datos secundaria, empezando por la más temprana y utilizando siempre RESTORE WITH NORECOVERY. Por supuesto, si restaura tanto la copia de seguridad diferencial como la copia de seguridad completa de bases de datos, solo tendría que aplicar las copias de seguridad de registros realizadas después de la copia de seguridad diferencial.  
  
    ```  
    -- Restore the transaction log on each secondary database,  
    -- using the WITH NORECOVERY option:  
    RESTORE LOG MyDb1   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    RESTORE LOG MyDb2   
        FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
9. En la instancia del servidor que hospeda la réplica secundaria, combine las nuevas bases de datos secundarias al grupo de disponibilidad.  
  
     En el ejemplo de código siguiente se une la base de datos secundaria *MyDb1* y luego la base de datos secundaria *MyDb2* al grupo de disponibilidad *MyAG* .  
  
    ```  
    -- On the server instance that hosts the secondary replica,   
    -- join each secondary database to the availability group:  
    ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
    GO  
  
    ```  
  
###  <a name="CompleteCodeExample"></a> Ejemplo completo de código del procedimiento de configuración de ejemplo  
 En el ejemplo siguiente se unen los ejemplos de código de todos los pasos del procedimiento de configuración de ejemplo. En la tabla siguiente se resumen los valores de marcador de posición utilizados en este ejemplo de código. Para obtener más información acerca de los pasos de este ejemplo de código, vea [Requisitos previos para usar el procedimiento de configuración de ejemplo](#PrerequisitesForExample) y [Procedimiento de configuración de ejemplo](#SampleProcedure), anteriormente en este tema.  
  
|Marcador de posición|Descripción|  
|-----------------|-----------------|  
|\\\\*FILESERVER*\\*SQLbackups*|Recurso compartido de copia de seguridad ficticio.|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb1.bak*|Archivo de copia de seguridad de MyDb1.|  
|\\\\*FILESERVER*\\*SQLbackups\MyDb2.bak*|Archivo de copia de seguridad de MyDb2.|  
|*7022*|Número de puerto asignado a cada extremo de creación de reflejo de la base de datos.|  
|*COMPUTER01\AgHostInstance*|Instancia del servidor que hospeda la réplica principal inicial.|  
|*COMPUTER02*|Instancia del servidor que hospeda la réplica secundaria inicial. Esta es la instancia del servidor predeterminada en `COMPUTER02`.|  
|*dbm_endpoint*|Nombre especificado para cada extremo de creación de reflejo de la base de datos.|  
|*MyAG*|Nombre del grupo de disponibilidad de ejemplo.|  
|*MyDb1*|Nombre de la primera base de datos de ejemplo.|  
|*MyDb2*|Nombre de la segunda base de datos de ejemplo.|  
|*DOMAIN1\user1*|Cuenta de servicio de la instancia del servidor que va a hospedar la réplica principal inicial.|  
|*DOMAIN2\user2*|Cuenta de servicio de la instancia del servidor que va a hospedar la réplica secundaria inicial.|  
|TCP://*COMPUTER01.Adventure-Works.com*:*7022*|Dirección URL de la instancia AgHostInstance de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en COMPUTER01.|  
|TCP://*COMPUTER02.Adventure-Works.com*:*5022*|Dirección URL del extremo de la instancia predeterminada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en COMPUTER02.|  
  
> [!NOTE]  
>  Para obtener ejemplos adicionales de código [!INCLUDE[tsql](../../../includes/tsql-md.md)] para la creación de un grupo de disponibilidad, vea [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql).  
  
```  
-- on the server instance that will host the primary replica,   
-- create sample databases:  
CREATE DATABASE MyDb1;  
GO  
ALTER DATABASE MyDb1 SET RECOVERY FULL;  
GO  
  
CREATE DATABASE MyDb2;  
GO  
ALTER DATABASE MyDb2 SET RECOVERY FULL;  
GO  
  
-- Backup sample databases:  
BACKUP DATABASE MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FORMAT  
GO  
  
BACKUP DATABASE MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FORMAT  
GO  
  
-- Create the endpoint on the server instance that will host the primary replica:  
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- Create the endpoint on the server instance that will host the secondary replica:   
CREATE ENDPOINT dbm_endpoint  
    STATE=STARTED   
    AS TCP (LISTENER_PORT=7022)   
    FOR DATABASE_MIRRORING (ROLE=ALL)  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the primary replica,   
-- create a login for the service account   
-- of the server instance that will host the secondary replica, DOMAIN2\user2,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
CREATE LOGIN [DOMAIN2\user2] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN2\user2];  
GO  
  
-- If both service accounts run under the same domain account, skip this step. Otherwise,   
-- On the server instance that will host the secondary replica,  
-- create a login for the service account   
-- of the server instance that will host the primary replica, DOMAIN1\user1,   
-- and grant this login connect permissions on the endpoint:  
USE master;  
GO  
  
CREATE LOGIN [DOMAIN1\user1] FROM WINDOWS;  
GO  
GRANT CONNECT ON ENDPOINT::dbm_endpoint   
   TO [DOMAIN1\user1];  
GO  
  
-- On the server instance that will host the primary replica,   
-- create the availability group, MyAG:  
CREATE AVAILABILITY GROUP MyAG   
   FOR   
      DATABASE MyDB1, MyDB2   
   REPLICA ON   
      'COMPUTER01\AgHostInstance' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         ),  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.Adventure-Works.com:7022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         );   
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join the secondary replica to the availability group:  
ALTER AVAILABILITY GROUP MyAG JOIN;  
GO  
  
-- Restore database backups onto this server instance, using RESTORE WITH NORECOVERY:  
RESTORE DATABASE MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NORECOVERY  
GO  
  
RESTORE DATABASE MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH NORECOVERY  
GO  
  
-- Back up the transaction log on each primary database:  
BACKUP LOG MyDb1   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH NOFORMAT  
GO  
  
BACKUP LOG MyDb2   
TO DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITHNOFORMAT  
GO  
  
-- Restore the transaction log on each secondary database,  
-- using the WITH NORECOVERY option:  
RESTORE LOG MyDb1   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb1.bak'   
    WITH FILE=1, NORECOVERY  
GO  
RESTORE LOG MyDb2   
    FROM DISK = N'\\FILESERVER\SQLbackups\MyDb2.bak'   
    WITH FILE=1, NORECOVERY  
GO  
  
-- On the server instance that hosts the secondary replica,   
-- join each secondary database to the availability group:  
ALTER DATABASE MyDb1 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
ALTER DATABASE MyDb2 SET HADR AVAILABILITY GROUP = MyAG;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar el grupo de disponibilidad y las propiedades de réplica**  
  
-   [Cambiar el modo de disponibilidad de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Cambiar el modo de conmutación por error de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar la directiva de conmutación por error Flexible para controlar las condiciones para la conmutación por error automática (grupos de disponibilidad AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Cambiar el tiempo de espera de la sesión en una réplica de disponibilidad &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para completar la configuración del grupo de disponibilidad**  
  
-   [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneras alternativas de crear un grupo de disponibilidad**  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Crear un grupo de disponibilidad &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
 **Para habilitar a grupos de disponibilidad AlwaysOn**  
  
-   [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Para configurar un extremo de creación del reflejo de la base de datos**  
  
-   [Crear una base de datos de extremo de reflejo para grupos de disponibilidad AlwaysOn &#40;PowerShell de SQL Server&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para solucionar problemas de configuración de grupos de disponibilidad AlwaysOn**  
  
-   [Solución de problemas de grupos de configuración de disponibilidad AlwaysOn (SQL Server) eliminado](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solución de problemas de una operación de agregar archivos con error &#40;grupos de disponibilidad AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [AlwaysON - HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (Series de aprendizaje de Always ON - HADRON: uso del grupo de trabajo para las bases de datos compatibles con HADRON)  
  
     [Blogs del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](https://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server Code-Named "Denali", serie AlwaysOn, parte 1: Introducción a la solución de alta disponibilidad de próxima generación](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali", serie AlwaysOn, parte 2: Creación de una solución esencial de alta disponibilidad utilizando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Notas del producto:**  
  
     [Guía de soluciones de Microsoft SQL Server AlwaysOn para alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Notas del producto de Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vea también  
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
