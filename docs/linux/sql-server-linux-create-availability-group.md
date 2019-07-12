---
title: Crear y configurar un grupo de disponibilidad para SQL Server en Linux
description: Este tutorial muestra cómo crear y configurar grupos de disponibilidad para SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7bd6f1259989c1cb0286fca546ea9e0410e0837f
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833900"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Crear y configurar un grupo de disponibilidad para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial explica cómo crear y configurar un grupo de disponibilidad (AG) para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux. A diferencia de [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] y anteriormente en Windows, puede habilitar grupos de disponibilidad con o sin crear primero el clúster de Pacemaker subyacente. Integración con el clúster, si es necesario, no se realiza hasta más adelante.

El tutorial incluye las siguientes tareas:
 
> [!div class="checklist"]
> * Habilite los grupos de disponibilidad.
> * Crear certificados y los puntos de conexión del grupo de disponibilidad.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL para crear un grupo de disponibilidad.
> * Crear el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] inicio de sesión y los permisos de Pacemaker.
> * Cree los recursos del grupo de disponibilidad en un clúster de Pacemaker (solo para el tipo externo).

## <a name="prerequisite"></a>Requisito previo
- Implementar el clúster de alta disponibilidad de Pacemaker, como se describe en [implementar un clúster de Pacemaker para SQL Server en Linux](sql-server-linux-deploy-pacemaker-cluster.md).


## <a name="enable-the-availability-groups-feature"></a>Habilitar la característica de grupos de disponibilidad

A diferencia de en Windows, no se puede usar PowerShell o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Configuration Manager para habilitar la disponibilidad de grupos de característica (AG). En Linux, se debe usar `mssql-conf` para habilitar la característica. Hay dos maneras de habilitar la característica de grupos de disponibilidad: usar el `mssql-conf` utilidad, o bien editar la `mssql.conf` archivo manualmente.

> [!IMPORTANT]
> Debe habilitarse la característica de grupo de disponibilidad para las réplicas de solo configuración, incluso en [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)].

### <a name="use-the-mssql-conf-utility"></a>Use la utilidad mssql-conf

En un símbolo del sistema, ejecute lo siguiente:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Edite el archivo mssql.conf

También puede modificar el `mssql.conf` archivo, que se encuentra bajo la `/var/opt/mssql` carpeta, agregue las siguientes líneas:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>Reiniciar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Después de habilitar los grupos de disponibilidad, como en Windows, debe reiniciar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Que se puede realizar mediante lo siguiente:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>Crear los extremos del grupo de disponibilidad y certificados

Un grupo de disponibilidad usa puntos de conexión TCP para la comunicación. En Linux, solo se admiten los puntos de conexión para un grupo de disponibilidad si se usan certificados para la autenticación. Esto significa que debe restaurarse el certificado de una instancia en todas las demás instancias serán las réplicas que participan en el mismo grupo de disponibilidad. El proceso de certificado es necesario incluso para una réplica de solo configuración. 

Creación de puntos de conexión de seguridad y restauración de los certificados solo pueden realizarse a través de Transact-SQL Puede usar que no sean de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-también certificados generados. También necesitará un proceso para administrar y reemplazar los certificados que expiran.

> [!IMPORTANT]
> Si tiene previsto usar el [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] Asistente para crear el grupo de disponibilidad, sigue siendo necesario crear y restaurar los certificados mediante Transact-SQL en Linux.

Para obtener la sintaxis completa de las opciones disponibles para los distintos comandos (por ejemplo, la seguridad adicional), consulte:

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CREAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> Aunque se va a crear un grupo de disponibilidad, el tipo de punto de conexión utiliza *FOR DATABASE_MIRRORING*, porque algunos aspectos subyacentes una vez se hayan compartido con esa característica ahora está en desuso.

En este ejemplo creará certificados para una configuración de tres nodos. Los nombres de instancia son LinAGN1, LinAGN2 y LinAGN3.

1.  Ejecute el siguiente LinAGN1 para crear la clave maestra, el certificado y el punto de conexión, así como el certificado de copia de seguridad. En este ejemplo, se usa el puerto TCP 5022 típico para el punto de conexión.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  Lo mismo en LinAGN2:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  Por último, realice la misma secuencia en LinAGN3:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  Uso de `scp` u otra utilidad, copie las copias de seguridad del certificado en cada nodo que va a formar parte del grupo de disponibilidad.
    
    En este ejemplo:
    
    - Copiar LinAGN1_Cert.cer LinAGN2 y LinAGN3
    - Copie LinAGN2_Cert.cer LinAGN1 y LinAGN3.
    - Copie LinAGN3_Cert.cer LinAGN1 y LinAGN2.
    
5.  Cambiar la propiedad y el grupo asociado con los archivos de certificado copiada a `mssql`.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  Cree los inicios de sesión de nivel de instancia y los usuarios asociados con LinAGN2 y LinAGN3 en LinAGN1.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  Restaurar LinAGN2_Cert y LinAGN3_Cert en LinAGN1. Tener los certificados de las otras réplicas es un aspecto importante de la comunicación de grupo de disponibilidad y seguridad.
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  Cree los inicios de sesión de nivel de instancia y los usuarios asociados con LinAGN1 y LinAGN3 en LinAGN2.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. Restaurar LinAGN1_Cert y LinAGN3_Cert en LinAGN2.
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. Conceder a los inicios de sesión asociados con LinAG1 y LinAGN3 permiso para conectarse al punto de conexión en LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. Cree los inicios de sesión de nivel de instancia y los usuarios asociados con LinAGN1 y LinAGN2 en LinAGN3.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. Restaurar LinAGN1_Cert y LinAGN2_Cert en LinAGN3. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. Conceder a los inicios de sesión asociados con LinAG1 y LinAGN2 permiso para conectarse al punto de conexión en LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>Crear el grupo de disponibilidad

En esta sección se explica cómo usar [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL para crear el grupo de disponibilidad para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>Usar [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

En esta sección se muestra cómo crear un grupo de disponibilidad con un tipo de clúster externo mediante SSMS con el Asistente para nuevo grupo de disponibilidad.

1.  En SSMS, expanda **alta disponibilidad de AlwaysOn**, haga clic en **grupos de disponibilidad**y seleccione **el Asistente para nuevo grupo de disponibilidad**.

2.  En el cuadro de diálogo Introducción, haga clic en **siguiente**.

3.  En el cuadro de diálogo Especificar opciones de grupo de disponibilidad, escriba un nombre para el grupo de disponibilidad y seleccione un tipo de clúster EXTERNAL o NONE en la lista desplegable. Externo debe usarse cuando Pacemaker se va a implementar. Ninguno es para escenarios especializados, como el escalado horizontal de lectura. Al seleccionar la opción para la detección de estado del nivel de base de datos es opcional. Para obtener más información sobre esta opción, consulte [opción conmutación por error de detección de estado del nivel de base de datos de disponibilidad grupo](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md). Haga clic en **Next**.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  En el cuadro de diálogo Seleccionar bases de datos, seleccione las bases de datos que participarán en el grupo de disponibilidad. Cada base de datos debe tener una copia de seguridad completa antes de se puede agregar a un grupo de disponibilidad. Haga clic en **Next**.

5.  En el cuadro de diálogo Especificar réplicas, haga clic en **Agregar réplica**.

6.  En conectar en el cuadro de diálogo servidor, escriba el nombre de la instancia de Linux de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que será la réplica secundaria y las credenciales para conectarse. Haga clic en **Conectar**.

7.  Repita los dos pasos anteriores para la instancia que va a contener una réplica de solo configuración u otra réplica secundaria.

8.  Las tres instancias deberían aparecer en el cuadro de diálogo Especificar réplicas. Si usa un tipo de clúster externo, la réplica secundaria que será una base de datos secundaria es true, asegúrese de que coincide con el modo de disponibilidad de la réplica principal y modo de conmutación por error se establece como externa. Para la réplica de solo configuración, seleccione solo un modo de disponibilidad de la configuración.

    El ejemplo siguiente muestra un grupo de disponibilidad con dos réplicas, un tipo de clúster externo y una réplica de solo configuración.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    El ejemplo siguiente muestra un grupo de disponibilidad con dos réplicas, un tipo de clúster None y una réplica de solo configuración.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  Si desea modificar las preferencias de copia de seguridad, haga clic en la ficha Preferencias de copia de seguridad. Para obtener más información sobre las preferencias de copia de seguridad con grupos de disponibilidad, consulte [Configurar copia de seguridad en réplicas de disponibilidad](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).

10. Si usa réplicas secundarias legibles o crear un grupo de disponibilidad con un clúster de tipo None para el escalado de lectura, puede crear un agente de escucha, seleccione la pestaña agente de escucha. Un agente de escucha también se puede agregar más adelante. Para crear un agente de escucha, elija la opción **crear un agente de escucha del grupo de disponibilidad** y escriba un nombre, un puerto TCP/IP y si se debe usar una dirección IP de DHCP estática o asignada automáticamente. Recuerde que para un grupo de disponibilidad con un tipo de clúster ninguno, debe ser la dirección IP estática y establecer a la dirección IP de la principal.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. Si se crea un agente de escucha para los escenarios legibles, SSMS 17.3 o posterior permite la creación del enrutamiento de solo lectura en el asistente. También se agregan posteriormente a través de SSMS o Transact-SQL. Para agregar el enrutamiento de solo lectura ahora:

    a.  Seleccione la pestaña enrutamiento de solo lectura.

    b.  Escriba las direcciones URL para las réplicas de solo lectura. Estas direcciones URL son similares a los extremos, salvo que usan el puerto de la instancia, no el punto de conexión.

    c.  Seleccione cada dirección URL y en la parte inferior, seleccione las réplicas legibles. Realizar una selección múltiple, mantenga presionada la tecla MAYÚS o haga clic y arrastre.

12. Haga clic en **Next**.

13. Elija cómo se inicializará las réplicas secundarias. El valor predeterminado es usar [la propagación automática](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), lo que requiere la misma ruta de acceso en todos los servidores que participan en el grupo de disponibilidad. También puede tener el Asistente para hacer una copia de seguridad, copia y restauración (la segunda opción;) tiene unirse si tiene manualmente una copia de seguridad, copiar y restaurar la base de datos en las réplicas (tercera opción;) o agregar más adelante de la base de datos (la última opción). Al igual que con los certificados, si las copias de seguridad y copiarlos manualmente, los permisos en los archivos de copia debe establecerse en las otras réplicas. Haga clic en **Next**.

14. En el cuadro de diálogo de validación, si todo lo que no envíe como correcto, investigue. Algunas advertencias son aceptables y no grave, por ejemplo, si no crea un agente de escucha. Haga clic en **Next**.

15. En el cuadro de diálogo de resumen, haga clic en **finalizar**. Ahora se iniciará el proceso para crear el grupo de disponibilidad.

16. Una vez completada la creación del grupo de disponibilidad, haga clic en **cerrar** en los resultados. Ahora puede ver el grupo de disponibilidad en las réplicas en las vistas de administración dinámica, así como en la carpeta de alta disponibilidad de AlwaysOn en SSMS.

### <a name="use-transact-sql"></a>Uso de Transact-SQL

En esta sección se muestra ejemplos de creación de un grupo de disponibilidad mediante Transact-SQL. El agente de escucha y el enrutamiento de solo lectura se pueden configurar una vez creado el grupo de disponibilidad. Se puede modificar el grupo de disponibilidad con `ALTER AVAILABILITY GROUP`, pero cambiar el tipo de clúster no puede realizarse [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Si no tenía la intención crear un grupo de disponibilidad con un tipo de clúster externo, debe eliminarlo y volver a crearlo con un tipo de clúster ninguno. Obtener más información y otras opciones se pueden encontrar en los vínculos siguientes:

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [Crear o configurar un agente de escucha del grupo de disponibilidad (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>Réplicas de un segundo ejemplo con una réplica de solo configuración (tipo de clúster externo)

En este ejemplo se muestra cómo crear un grupo de disponibilidad de dos réplicas que usa una réplica de solo configuración.

1.  Ejecutar en el nodo que va a ser la réplica principal que contiene la copia de lectura/escritura completa de las bases de datos. En este ejemplo se emplea la propagación automática.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  En una ventana de consulta conectada a la otra réplica, ejecute el siguiente procedimiento para unir la réplica al grupo de disponibilidad e iniciar el proceso de propagación de la principal a la réplica secundaria.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. En una ventana de consulta conectada a la réplica de solo configuración, debe unirla al grupo de disponibilidad.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>Réplicas de ejemplo dos y tres con enrutamiento de solo lectura (tipo de clúster externo)

En este ejemplo se muestra tres completa las réplicas y el enrutamiento de solo lectura cómo pueden configurarse como parte de la creación inicial del grupo de disponibilidad.

1.  Ejecutar en el nodo que va a ser la réplica principal que contiene la copia de lectura/escritura completa de las bases de datos. En este ejemplo se emplea la propagación automática.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    Algunos aspectos que debe tener en cuenta sobre esta configuración:
    
    - *AGName* es el nombre del grupo de disponibilidad.
    - *DBName* es el nombre de la base de datos que se usará con el grupo de disponibilidad. También puede ser una lista de nombres separados por comas.
    - *ListenerName* es un nombre que es diferente de cualquiera de los servidores y nodos subyacentes. Se registrará en DNS junto con *IPAddress*.
    - *IPAddress* es una dirección IP que está asociada con *ListenerName*. También es único y no es el mismo que cualquiera de los nodos de servidores. Las aplicaciones y los usuarios finales utilizarán cualquiera *ListenerName* o *IPAddress* para conectarse al grupo de disponibilidad.
    - *Máscara de subred* es la máscara de subred *IPAddress*; por ejemplo, 255.255.255.0.

2.  En una ventana de consulta conectada a la otra réplica, ejecute el siguiente procedimiento para unir la réplica al grupo de disponibilidad e iniciar el proceso de propagación de la principal a la réplica secundaria.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Repita el paso 2 para la tercera réplica.

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>Réplicas de ejemplo dos de tres con enrutamiento de solo lectura (tipo de clúster)

En este ejemplo se muestra la creación de una configuración de dos réplicas con un tipo de clúster ninguno. Se usa para el escenario de escalado de lectura donde no se espera ninguna conmutación por error. Esto crea el agente de escucha es realmente la réplica principal, así como el enrutamiento de solo lectura, mediante la funcionalidad de operación por turnos.

1.  Ejecutar en el nodo que va a ser la réplica principal que contiene la copia de lectura/escritura completa de las bases de datos. En este ejemplo se emplea la propagación automática.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    Where
    - *AGName* es el nombre del grupo de disponibilidad.
    - *DBName* es el nombre de la base de datos que se usará con el grupo de disponibilidad. También puede ser una lista de nombres separados por comas.
    - *PortOfEndpoint* es el número de puerto utilizado por el punto de conexión creado.
    - *PortOfInstance* es el número de puerto utilizado por la instancia de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].
    - *ListenerName* es un nombre que es diferente de cualquiera de las réplicas subyacentes pero realmente no se usará.
    - *PrimaryReplicaIPAddress* es la dirección IP de la réplica principal.
    - *Máscara de subred* es la máscara de subred *IPAddress*. Por ejemplo, 255.255.255.0.
    
2.  Combine la réplica secundaria al grupo de disponibilidad e iniciar la propagación automática.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>Crear el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] inicio de sesión y los permisos de Pacemaker

Un clúster de alta disponibilidad de Pacemaker subyacente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, necesita tener acceso a la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instancia, así como los permisos en el mismo grupo de disponibilidad. Estos pasos crea el inicio de sesión y los permisos asociados junto con un archivo que indica el inicio de sesión en Pacemaker [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

1.  En una ventana de consulta conectada a la primera réplica, ejecute lo siguiente:

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  En el nodo 1, escriba el comando 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    Se abrirá el editor Emacs.
    
3.  En el editor, escriba las dos líneas siguientes:

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Mantenga presionada la tecla CTRL y, a continuación, presione X, y después C para salir y guardar el archivo.

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    Para bloquear el archivo.

6.  Repita los pasos del 1 al 5 en los otros servidores que servirá como réplicas.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Creación de la disponibilidad del grupo de recursos del clúster de Pacemaker (sólo externas)

Después de la disponibilidad de un grupo se crea en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], los recursos correspondientes deben crearse en Pacemaker, cuando se especifica un tipo de clúster externo. Hay dos recursos asociados con un grupo de disponibilidad: el grupo de disponibilidad y una dirección IP. Configurar el recurso de dirección IP es opcional si no se utiliza la funcionalidad de agente de escucha, pero se recomienda.

El recurso de grupo de disponibilidad que se crea es un tipo especial de recurso denominado un clon. El recurso de grupo de disponibilidad tiene esencialmente copias en cada nodo y hay un recurso de control que se denomina al patrón. El patrón está asociado con el servidor que hospeda la réplica principal. Las réplicas secundarias (normales o de solo configuración) se consideran subordinadas y se puede promover a maestro en una conmutación por error.

1.  Crear el recurso de grupo de disponibilidad con la sintaxis siguiente:

    **Red Hat Enterprise Linux (RHEL) y Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >En RHEL 7.4, puede encontrar una advertencia con el uso de--master. Para evitarlo, use `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    donde *NameForAGResource* es el nombre único asignado a este recurso de clúster para el grupo de disponibilidad, y *AGName* es el nombre del grupo de disponibilidad que se creó.
 
2.  Crear el recurso de dirección IP para el grupo de disponibilidad que se asociará con la funcionalidad de agente de escucha.

    **Ubuntu y RHEL**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    donde *NameForIPResource* es el nombre único para el recurso IP, y *IPAddress* es la dirección IP estática asignada al recurso. En SLES, también deberá proporcionar la máscara de red. Por ejemplo, 255.255.255.0 tendría un valor de 24 para *máscara de red.*
    
3.  Para asegurarse de que la dirección IP y el recurso de grupo de disponibilidad se ejecutan en el mismo nodo, debe configurarse una restricción de colocación.

    **Ubuntu y RHEL**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    donde *NameForIPResource* es el nombre para el recurso IP, *NameForAGResource* es el nombre para el recurso de grupo de disponibilidad y en SLES, *NameForConstraint* es el nombre de la restricción.

4.  Crear una restricción para asegurarse de que el recurso AG está activo de ordenación y en ejecución antes de la dirección IP. Mientras que la restricción de colocación implica una restricción de ordenación, esto exige.

    **Ubuntu y RHEL**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    donde *NameForIPResource* es el nombre para el recurso IP, *NameForAGResource* es el nombre para el recurso de grupo de disponibilidad y en SLES, *NameForConstraint* es el nombre de la restricción.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido a crear y configurar un grupo de disponibilidad para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux. Ha aprendido a:
> [!div class="checklist"]
> * Habilite los grupos de disponibilidad.
> * Los extremos de crear grupo de disponibilidad y certificados.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL para crear un grupo de disponibilidad.
> * Crear el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] inicio de sesión y los permisos de Pacemaker.
> * Cree los recursos del grupo de disponibilidad en un clúster de Pacemaker.

Muchas tareas de administración de AG, incluidas las actualizaciones y conmuta por error, consulte:

> [!div class="nextstepaction"]
> [Operar el grupo de disponibilidad de alta disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-failover-ha.md)

