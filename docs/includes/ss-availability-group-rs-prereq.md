## <a name="prerequisites"></a>Prerequisites

Antes de crear el grupo de disponibilidad, debe:

- Establecer el entorno de forma que todos los servidores que hospedarán las réplicas de disponibilidad se puedan comunicar.
- Instale SQL Server. Vea [Instalar SQL Server](../database-engine/install-windows/install-sql-server.md) para obtener más información.

## <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>Habilitar los grupos de disponibilidad AlwaysOn y reiniciar mssql-server

>[!NOTE]
>En el comando siguiente se usan los cmdlets del módulo sqlserver que se publica en la Galería de PowerShell. Puede instalar este módulo mediante el comando Install-Module.

Habilite los grupos de disponibilidad AlwaysOn en todas las réplicas en las que se hospede una instancia de SQL Server. Después, reinicie el servicio SQL Server. Ejecute el comando siguiente para habilitar y reiniciar los servicios de SQL Server:

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwayson_health-event-session"></a>Habilitar una sesión de eventos AlwaysOn_health

 Para ayudar con el diagnóstico de la causa raíz cuando solucione los problemas de un grupo de disponibilidad, opcionalmente puede habilitar una sesión de eventos extendidos (XEvents) de los grupos de disponibilidad AlwaysOn. Para hacerlo, ejecute el comando siguiente en todas las instancias de SQL Server:

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obtener más información sobre esta sesión de XEvents, vea [Eventos extendidos de grupos de disponibilidad AlwaysOn](../database-engine/availability-groups/windows/always-on-extended-events.md).

## <a name="database-mirroring-endpoint-authentication"></a>Autenticación de puntos de conexión de creación de reflejo de la base de datos

Para que la sincronización funcione correctamente, las réplicas que participan en el grupo de disponibilidad de escalado de lectura se deben autenticar a través del punto de conexión. En las secciones siguientes se describen los dos escenarios principales que se pueden usar para este tipo de autenticación.

### <a name="service-account"></a>Cuenta de servicio

En un entorno de Active Directory donde todas las réplicas secundarias están unidas al mismo dominio, SQL Server se puede autenticar mediante la cuenta de servicio. Tendrá que crear de forma explícita un inicio de sesión para la cuenta de servicio en todas las instancias de SQL Server:

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>Autenticación del inicio de sesión SQL

En los entornos donde es posible que las réplicas secundarias no estén unidas a un dominio de Active Directory, tendrá que usar la autenticación de SQL. El script de Transact-SQL siguiente crea un inicio de sesión denominado `dbm_login` y un usuario denominado `dbm_user`. Actualice el script con una contraseña segura. Para crear el usuario de punto de conexión de creación de reflejo de la base de datos, ejecute el comando siguiente en todas las instancias de SQL Server:

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>Autenticación de certificado

Si se usa una réplica secundaria que requiere la autenticación con Autenticación de SQL, use un certificado para la autenticación entre los puntos de conexión de creación de reflejo.

El script de Transact-SQL siguiente crea una clave maestra y un certificado. Después, realiza una copia de seguridad del certificado y protege el archivo con una clave privada. Actualice el script con contraseñas seguras. Ejecute el script en la instancia principal de SQL Server para crear el certificado:

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

En este momento, la réplica principal de SQL Server tiene un certificado en `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer` y una clave privada en `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk`. Copie estos dos archivos en la misma ubicación en todos los servidores que hospedarán las réplicas de disponibilidad.

En cada réplica secundaria, asegúrese de que la cuenta de servicio para la instancia de SQL Server tenga permisos para acceder al certificado.

#### <a name="create-the-certificate-on-secondary-servers"></a>Crear el certificado en los servidores secundarios

El script de Transact-SQL siguiente crea una clave maestra y un certificado a partir de la copia de seguridad creada en la réplica principal de SQL Server. El comando también autoriza al usuario a acceder al certificado. Actualice el script con contraseñas seguras. La contraseña de descifrado es la misma que se usó para crear el archivo *.pvk* en un paso anterior. Para crear el certificado, ejecute el script siguiente en todas las réplicas secundarias:

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-database-mirroring-endpoints-on-all-replicas"></a>Crear puntos de conexión de creación de reflejo de la base de datos en todas las réplicas

Los puntos de conexión de creación de reflejo de la base de datos usan el Protocolo de control de transmisión (TCP) para enviar y recibir mensajes entre las instancias del servidor que participan en las sesiones de creación de reflejo de la base de datos o que hospedan las réplicas de disponibilidad. El punto de conexión de creación de reflejo de la base de datos escucha en un número de puerto TCP exclusivo.

El script de Transact-SQL siguiente crea un punto de conexión de escucha denominado `Hadr_endpoint` para el grupo de disponibilidad. Inicia el punto de conexión y concede permiso de conexión a la cuenta de servicio o al inicio de sesión de SQL que se creó en el paso anterior. Antes de ejecutar el script, reemplace los valores entre `**< ... >**`. Opcionalmente puede incluir una dirección IP, `LISTENER_IP = (0.0.0.0)`. La dirección IP de escucha debe ser una dirección IPv4. También se puede usar `0.0.0.0`.

Actualice el script de Transact-SQL siguiente para el entorno en todas las instancias de SQL Server:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

El puerto TCP en el firewall debe estar abierto para el puerto de escucha.

Para obtener más información, vea [El punto de conexión de creación de reflejo de la base de datos (SQL Server)](https://docs.microsoft.com/sql/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server?view=sql-server-2017).
