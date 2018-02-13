---
title: Crear y configurar un grupo de disponibilidad para SQL Server en Linux | Documentos de Microsoft
description: "Este tutorial muestra cómo crear y configurar grupos de disponibilidad para SQL Server en Linux."
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 4e1190fea92c1e84ce38bd46040a8b5fcdd532d7
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Crear y configurar un grupo de disponibilidad para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial explica cómo crear y configurar un grupo de disponibilidad (AG) para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux. A diferencia de [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] y versiones anteriores en Windows, puede habilitar grupos de disponibilidad con o sin crear primero el clúster marcapasos subyacente. Integración con el clúster, si es necesario, no se realiza hasta más adelante.

El tutorial incluye las siguientes tareas:
 
> [!div class="checklist"]
> * Habilite los grupos de disponibilidad.
> * Crear certificados y extremos del grupo de disponibilidad.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL para crear un grupo de disponibilidad.
> * Crear la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] inicio de sesión y permisos para marcapasos.
> * Crear recursos de grupo de disponibilidad en un clúster de marcapasos (solo para el tipo externo).

## <a name="prerequisite"></a>Requisito previo
- Implementar el clúster de alta disponibilidad marcapasos tal y como se describe en [implementar un clúster marcapasos para SQL Server en Linux](sql-server-linux-deploy-pacemaker-cluster.md).


## <a name="enable-the-availability-groups-feature"></a>Habilitar la característica de grupos de disponibilidad

A diferencia de en Windows, no se puede usar PowerShell o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] característica (AG) de grupos de Configuration Manager para habilitar la disponibilidad. En Linux, se debe usar `mssql-conf` para habilitar la característica. Hay dos maneras de habilitar la característica de grupos de disponibilidad: usar el `mssql-conf` utilidad, o bien editar la `mssql.conf` archivo manualmente.

> [!IMPORTANT]
> La característica de AG debe habilitarse para réplicas de solo configuración, incluso en [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)].

### <a name="use-the-mssql-conf-utility"></a>Use la utilidad mssql-conf

En un símbolo del sistema, ejecute lo siguiente:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Edite el archivo mssql.conf

También puede modificar el `mssql.conf` archivo, situado bajo el `/var/opt/mssql` carpeta, agregue las siguientes líneas:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>Reinicio [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Después de habilitar los grupos de disponibilidad, como en Windows, debe reiniciar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Esto puede realizarse por el texto siguiente:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>Crear los extremos del grupo de disponibilidad y certificados

Un grupo de disponibilidad usa puntos de conexión TCP para la comunicación. En Linux, solo se admiten extremos para un grupo de disponibilidad si se usan certificados para la autenticación. Esto significa que debe restaurarse el certificado de una instancia en todas las demás instancias serán réplicas que participan en la mismo AG. El proceso de certificado es necesario incluso para una réplica de solo configuración. 

Creación de puntos de conexión y restaurar certificados sólo se pueden realizar a través de Transact-SQL. Puede usar no -[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-genera certificados también. También necesitará un proceso para administrar y reemplazar los certificados que expiran.

> [!IMPORTANT]
> Si tiene previsto usar el [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] Asistente para crear el AG, sigue siendo necesario crear y restaurar los certificados mediante Transact-SQL en Linux.

Para obtener la sintaxis completa de las opciones disponibles para los distintos comandos (por ejemplo, la seguridad adicional), consulte:

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CREAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> Aunque va a crear un grupo de disponibilidad, el tipo de punto de conexión utiliza *FOR DATABASE_MIRRORING*, porque algunos aspectos subyacentes una vez se han compartido con esa característica ahora desusado.

En este ejemplo creará certificados para una configuración de tres nodos. Los nombres de instancia son LinAGN1, LinAGN2 y LinAGN3.

1.  Ejecute el siguiente LinAGN1 para crear la clave maestra, el certificado y el punto de conexión, así como realizar copias de seguridad del certificado. En este ejemplo, se utiliza el puerto TCP 5022 típico para el extremo.
    
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
    
2.  Haga lo mismo en LinAGN2:
    
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
    
4.  Con `scp` u otra utilidad, copie las copias de seguridad del certificado en cada nodo que va a formar parte de disponibilidad.
    
    En este ejemplo:
    
    - Copie LinAGN1_Cert.cer en LinAGN2 y LinAGN3
    - Copie LinAGN2_Cert.cer en LinAGN1 y LinAGN3.
    - Copie LinAGN3_Cert.cer en LinAGN1 y LinAGN2.
    
5.  Cambiar la propiedad y el grupo asociado con los archivos de certificado copiado a `mssql`.
    
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
    
7.  Restaurar LinAGN2_Cert y LinAGN3_Cert en LinAGN1. Tener los certificados de las otras réplicas es un aspecto importante de la comunicación AG y seguridad.
    
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
    
10.  Restaurar LinAGN1_Cert y LinAGN3_Cert en LinAGN2. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
11.  Grant the logins associated with LinAG1 and LinAGN3 permission to connect to the endpoint on LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12.  Cree los inicios de sesión de nivel de instancia y los usuarios asociados con LinAGN1 y LinAGN2 en LinAGN3.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13.  Restaurar LinAGN1_Cert y LinAGN2_Cert en LinAGN3. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
14.  Grant the logins associated with LinAG1 and LinAGN2 permission to connect to the endpoint on LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>Crear el grupo de disponibilidad

Esta sección explica cómo usar [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL para crear el grupo de disponibilidad para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>Uso [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

Esta sección muestra cómo crear un grupo de disponibilidad con un tipo de clúster de externo con SSMS con el Asistente para nuevo grupo de disponibilidad.

1.  En SSMS, expanda **alta disponibilidad de AlwaysOn**, haga clic en **grupos de disponibilidad**y seleccione **el Asistente para nuevo grupo de disponibilidad**.

2.  En el cuadro de diálogo Introducción, haga clic en **siguiente**.

3.  En el cuadro de diálogo Especificar opciones de grupo de disponibilidad, escriba un nombre para el grupo de disponibilidad y seleccione un tipo de clúster de externo o ninguno en la lista desplegable. Externo debe utilizarse cuando se implementarán marcapasos. Ninguno es para escenarios especializados, como lectura escalado horizontal. Al seleccionar la opción de detección de estado de nivel de base de datos es opcional. Para obtener más información sobre esta opción, vea [opción conmutación por error de detección de estado de nivel de base de datos de disponibilidad grupo](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md). Haga clic en **Siguiente**.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  En el cuadro de diálogo Seleccionar bases de datos, seleccione las bases de datos que vaya a participar en el AG. Cada base de datos debe tener una copia de seguridad completa antes de que se puede agregar a un AG. Haga clic en **Siguiente**.

5.  En el cuadro de diálogo Especificar réplicas, haga clic en **agregar una réplica**.

6.  En conectar al cuadro de diálogo de servidor, escriba el nombre de la instancia de Linux de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que será la réplica secundaria y las credenciales para conectarse. Haga clic en **Conectar**.

7.  Repita los dos pasos anteriores para la instancia que va a contener una réplica de solo configuración o de otra réplica secundaria.

8.  Las tres instancias deben aparecer ahora en el cuadro de diálogo Especificar réplicas. Si usa un tipo de clúster de externo, para la réplica secundaria que será un elemento secundario es true, asegúrese de que coincide con el modo de disponibilidad de la réplica principal y el modo de conmutación por error se establece en externa. Para la réplica solo configuración, seleccione un modo de disponibilidad de configuración solo.

    En el ejemplo siguiente se muestra un AG con dos réplicas, un tipo de clúster de externo y una réplica de solo configuración.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    En el ejemplo siguiente se muestra un AG con dos réplicas, un tipo de clúster de None y una réplica de solo configuración.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  Si desea modificar las preferencias de copia de seguridad, haga clic en la ficha Preferencias de copia de seguridad. Para obtener más información sobre las preferencias de copia de seguridad con grupos de disponibilidad, consulte [Configurar copia de seguridad en réplicas de disponibilidad](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).

10. Si usa réplicas secundarias legibles o crear un grupo de disponibilidad con un clúster de tipo None para la escala de lectura, puede crear un agente de escucha, seleccione la pestaña de agente de escucha. Un agente de escucha también puede agregarse más adelante. Para crear un agente de escucha, elija la opción **crear un agente de escucha del grupo de disponibilidad** y escriba un nombre, un puerto TCP/IP y si se debe usar una dirección de IP de DHCP estática o asignada automáticamente. Recuerde que, para un grupo de disponibilidad con un tipo de clúster de ninguno, la dirección IP debe ser estático y establezca como dirección IP del primario.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. Si se crea un agente de escucha para escenarios legibles, SSMS 17,3 o una versión posterior permite la creación de enrutamiento de solo lectura en el asistente. También puede agregar más adelante a través de SSMS o Transact-SQL. Para agregar el enrutamiento de solo lectura ahora:

    A.  Seleccione la ficha enrutamiento de solo lectura.

    B.  Escriba las direcciones URL para las réplicas de solo lectura. Estas direcciones URL son similares a los puntos de conexión, excepto en usan el puerto de la instancia, no el punto de conexión.

    c.  Seleccione cada dirección URL y en la parte inferior, seleccione las réplicas legibles. Para seleccionar varios, mantenga presionada la tecla MAYÚS o haga clic y arrastre.

12. Haga clic en **Siguiente**.

13. Elija cómo se inicializará la secundaria. El valor predeterminado es usar [la propagación automática](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), lo que requiere la misma ruta de acceso en todos los servidores que participan en el AG. También puede hacer que el Asistente para hacer una copia de seguridad y restaurar (la segunda opción;) tiene combinar si tienen manualmente copia de seguridad, copiar y restaurar la base de datos en las réplicas (tercera opción;) o agregar la base de datos más adelante (la última opción). Al igual que con los certificados, si va a realizar copias de seguridad y copiarlos manualmente, los permisos de los archivos de copia de seguridad debe establecerse en las otras réplicas. Haga clic en **Siguiente**.

14. En el cuadro de diálogo de validación, si todo lo que no vuelven a estar como correcto, investigue. Algunas advertencias son aceptables y no grave, como si no crea un agente de escucha. Haga clic en **Siguiente**.

15. En el cuadro de diálogo de resumen, haga clic en **finalizar**. Ahora se iniciará el proceso de creación de disponibilidad.

16. Una vez completada la creación de AG, haga clic en **cerrar** en los resultados. Ahora puede ver el AG en las réplicas en las vistas de administración dinámica, así como en la carpeta de alta disponibilidad de AlwaysOn en SSMS.

### <a name="use-transact-sql"></a>Usar Transact-SQL

En esta sección se muestra ejemplos de creación de un AG mediante Transact-SQL. El agente de escucha y el enrutamiento de solo lectura se pueden configurar una vez creado el AG. Disponibilidad sí se puede modificar con `ALTER AVAILABILITY GROUP`, pero si cambia el tipo de clúster no se puede realizar [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Si no tenía la intención crear un grupo de disponibilidad con un tipo de clúster de externo, debe eliminarlo y volver a crearla con un tipo de clúster de None. Obtener más información y otras opciones pueden encontrarse en los siguientes vínculos:

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [Crear o configurar un agente de escucha del grupo de disponibilidad (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one--two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>Réplicas de ejemplo dos: uno con una réplica de solo configuración (tipo de clúster externo)

En este ejemplo se muestra cómo crear un AG de dos réplicas que usa una réplica de configuración.

1.  Se ejecuta en el nodo que será la réplica principal que contiene la copia de lectura/escritura completa de las bases de datos. Este ejemplo utiliza la propagación automática.

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
    
2.  En una ventana de consulta conectada a la otra réplica, ejecute el siguiente procedimiento para combinar la réplica con lo AG e iniciar el proceso de propagación del servidor principal a la réplica secundaria.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  En una ventana de consulta conectada a la única réplica de configuración, unirlo a disponibilidad.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    ```

#### <a name="example-two--three-replicas-with-read-only-routing-external-cluster-type"></a>Réplicas de ejemplo dos, tres con enrutamiento de solo lectura (tipo de clúster externo)

En este ejemplo se muestra tres completa réplicas y enrutamiento de solo lectura cómo pueden configurarse como parte de la creación de AG inicial.

1.  Se ejecuta en el nodo que será la réplica principal que contiene la copia de lectura/escritura completa de las bases de datos. Este ejemplo utiliza la propagación automática.

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
    
    Aspectos a tener en cuenta acerca de esta configuración:
    
    - *AGName* es el nombre del grupo de disponibilidad.
    - *DBName* es el nombre de la base de datos que se usará con el grupo de disponibilidad. También puede ser una lista de nombres separados por comas.
    - *ListenerName* es un nombre que es distinto de cualquiera de los servidores/nodos subyacentes. Se registrará en DNS junto con *IPAddress*.
    - *IPAddress* es una dirección IP que está asociada a *ListenerName*. También es único y no es el mismo que cualquiera de los nodos de servidores. Las aplicaciones y los usuarios finales utilizará *ListenerName* o *IPAddress* para conectarse a la disponibilidad.
    - *Máscara de subred* es la máscara de subred *IPAddress*; por ejemplo, 255.255.255.0.

2.  En una ventana de consulta conectada a la otra réplica, ejecute el siguiente procedimiento para combinar la réplica con lo AG e iniciar el proceso de propagación del servidor principal a la réplica secundaria.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Repita el paso 2 para la tercera réplica.

#### <a name="example-three--two-replicas-with-read-only-routing-none-cluster-type"></a>Réplicas de tres: el segundo ejemplo con enrutamiento de solo lectura (ninguno clúster tipo)

En este ejemplo se muestra la creación de una configuración de dos réplicas utilizando un tipo de clúster de None. Se usa para el escenario de lectura escala donde no se espera ninguna conmutación por error. Esto crea el agente de escucha que está realmente la réplica principal, así como el enrutamiento de solo lectura, utilizando la funcionalidad de operación por turnos.

1.  Se ejecuta en el nodo que será la réplica principal que contiene la copia de lectura/escritura completa de las bases de datos. Este ejemplo utiliza la propagación automática.

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
    - *ListenerName* es un nombre que es distinto de cualquiera de las réplicas subyacentes pero realmente no se usará.
    - *PrimaryReplicaIPAddress* es la dirección IP de la réplica principal.
    - *Máscara de subred* es la máscara de subred *IPAddress*. Por ejemplo, 255.255.255.0.
    
2.  Combine la réplica secundaria para disponibilidad e iniciar la propagación automática.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>Crear la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] inicio de sesión y permisos para marcapasos

Un clúster de alta disponibilidad marcapasos subyacente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, necesita tener acceso a la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instancia, así como permisos en el grupo de disponibilidad. Estos pasos para crear el inicio de sesión y los permisos asociados junto con un archivo que indica marcapasos cómo iniciar sesión en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

1.  En una ventana de consulta conectada a la primera réplica, ejecute lo siguiente:

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD '<StrongPassword>';
    
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
    
    Se abrirá el editor de Emacs.
    
3.  Escriba las dos líneas siguientes en el editor:

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Mantenga presionada la tecla CTRL y, a continuación, presione X, a continuación, C para salir y guardar el archivo.

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    Para bloquear el archivo.

6.  Repita los pasos 1-5 en los otros servidores que servirá como réplicas.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Crear recursos de grupo de la disponibilidad del clúster marcapasos (sólo externas)

Después de la disponibilidad de un grupo se crea en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], los recursos correspondientes deben crearse en marcapasos, cuando se especifica un tipo de clúster de externo. Hay dos recursos asociados con un AG: el AG. y una dirección IP. Configurar el recurso de dirección IP es opcional si no se utiliza la funcionalidad de agente de escucha, pero se recomienda.

El recurso de AG que se crea es un tipo especial de recurso denominado un clon. El recurso de AG básicamente tiene copias en cada nodo y no hay un recurso de control que se denomina al patrón. El patrón está asociado con el servidor que hospeda la réplica principal. Las réplicas secundarias (normales o solo configuración) se consideran subordinadas y se puede promover a maestro en una conmutación por error.

1.  Crear el recurso de grupo de disponibilidad con la sintaxis siguiente:

    **Red Hat Enterprise Linux (RHEL) y Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> --master meta notify=true
    ```

    >[!NOTE]
    >En RHEL 7.4, puede producirse una advertencia con el uso de--master. Para evitar esto, utilice `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
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
    
    donde *NameForAGResource* es el nombre único asignado a este recurso de clúster para el AG, y *AGName* es el nombre de disponibilidad que se creó.
 
2.  Crear el recurso de dirección IP para el AG que se asociará con la funcionalidad de agente de escucha.

    **RHEL y Ubuntu**
    
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
    
    donde *NameForIPResource* es el nombre único para el recurso IP, y *IPAddress* es la dirección IP estática asignada al recurso. En SLES, también debe proporcionar la máscara de red. Por ejemplo, 255.255.255.0 tendría un valor de 24 para *máscara de red.*
    
3.  Para asegurarse de que la dirección IP y el recurso de AG se ejecutan en el mismo nodo, debe configurarse una restricción de colocación.

    **RHEL y Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    donde *NameForIPResource* es el nombre para el recurso IP, *NameForAGResource* es el nombre del recurso de AG y en SLES, *NameForConstraint* es el nombre de la restricción.

4.  Crear una ordenación restricción para asegurarse de que el recurso de AG está activo y en ejecución antes de la dirección IP. Mientras que la restricción de colocación implica una restricción de ordenación, esto lo aplica.

    **RHEL y Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    donde *NameForIPResource* es el nombre para el recurso IP, *NameForAGResource* es el nombre del recurso de AG y en SLES, *NameForConstraint* es el nombre de la restricción.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a crear y configurar un grupo de disponibilidad para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux. También habrá aprendido cómo para:
> [!div class="checklist"]
> * Habilite los grupos de disponibilidad.
> * Los extremos de creación AG y certificados.
> * Use [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) o Transact-SQL para crear un AG.
> * Crear la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] inicio de sesión y permisos para marcapasos.
> * Crear recursos de AG en un clúster marcapasos.

De muchas tareas de administración de AG, incluidas las actualizaciones y conmuta por error, vea:

> [!div class="nextstepaction"]
> [Funcionar el grupo de disponibilidad de alta disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-failover-ha.md)

