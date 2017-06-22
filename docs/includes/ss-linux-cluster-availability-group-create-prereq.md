## <a name="prerequisites"></a>Requisitos previos

Antes de crear el grupo de disponibilidad, debe:

- Establecer el entorno de forma que pueden comunicarse todos los servidores que hospedarán las réplicas de disponibilidad
- Instalar SQL Server

>[!NOTE]
>En Linux, debe crear un grupo de disponibilidad antes de agregarlo como recurso de clúster para ser administrado por el clúster. Este documento proporciona un ejemplo que crea el grupo de disponibilidad. Para la distribución de instrucciones específicas para crear el clúster y agregar el grupo de disponibilidad como un recurso de clúster, consulte los vínculos en [pasos siguientes](#next-steps).

1. **Actualice el nombre de equipo para cada host**

   Cada nombre de SQL Server debe ser:
   
   - 15 caracteres o menos
   - Único dentro de la red
   
   Para establecer el nombre del equipo, edite `/etc/hostname`. La siguiente secuencia de comandos le permite editar `/etc/hostname` con `vi`.

   ```bash
   sudo vi /etc/hostname
   ```

1. **Configurar el archivo de hosts**

>[!NOTE]
>Si los nombres de host están registrados con su dirección IP en el servidor DNS, no hay ninguna necesidad de realizar los pasos siguientes. Validar que todos los nodos que se van a formar parte de la configuración del grupo de disponibilidad pueden comunicarse entre sí (hacer ping en el nombre de host debe responder con la dirección IP correspondiente). Además, asegúrese de que el archivo/etc/hosts no tiene un registro que se asigna la dirección IP de localhost, 127.0.0.1 con el nombre de host del nodo.


   El archivo de hosts en cada servidor contiene las direcciones IP y nombres de todos los servidores que vaya a participar en el grupo de disponibilidad. 

   El comando siguiente devuelve la dirección IP del servidor actual:

   ```bash
   sudo ip addr show
   ```

   Actualización `/etc/hosts`. La siguiente secuencia de comandos le permite editar `/etc/hosts` con `vi`.

   ```bash
   sudo vi /etc/hosts
   ```

   El ejemplo siguiente muestra `/etc/hosts` en **Nodo1** adiciones para **Nodo1** y **Nodo2**. En este documento **Nodo1** hace referencia a la réplica principal de SQL Server. **Nodo2** hace referencia a la secundaria de SQL Server.;


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 node1
   10.128.16.77 node2
   ```

### <a name="install-sql-server"></a>Instalar SQL Server

Instalar a SQL Server. Los siguientes vínculos apuntan a las instrucciones de instalación de SQL Server para varias distribuciones. 

- [Red Hat Enterprise Linux](..\linux\sql-server-linux-setup-red-hat.md)

- [SUSE Linux Enterprise Server](..\linux\sql-server-linux-setup-suse-linux-enterprise-server.md)

- [Ubuntu](..\linux\sql-server-linux-setup-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Habilitar a grupos de disponibilidad AlwaysOn y reinicie SQL Server

Habilitar grupos de disponibilidad AlwaysOn en cada nodo que hospeda el servicio SQL Server, a continuación, reinicie `mssql-server`.  Ejecute el script siguiente:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>Habilitar la sesión de eventos AlwaysOn_health 

Puede habilitar optionaly grupos de disponibilidad AlwaysOn específico eventos extendidos para ayudar a un diagnóstico más detallado y causa para solucionar un grupo de disponibilidad.

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obtener más información acerca de esta sesión XE, consulte [siempre en Extended Events](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-db-mirroring-endpoint-user"></a>Crear usuario del extremo de creación de reflejo de la base de datos

El siguiente script de Transact-SQL crea un inicio de sesión denominado `dbm_login`y un usuario denominado `dbm_user`. Actualizar la secuencia de comandos con una contraseña segura. Ejecute el siguiente comando en todos los servidores de SQL Server para crear la base de datos de usuario del extremo de creación de reflejo.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Crear un certificado

Servicio de SQL Server en Linux utiliza certificados para autenticar las comunicaciones entre los extremos de creación de reflejo. 

El siguiente script de Transact-SQL crea una clave maestra y el certificado. A continuación, se realiza una copia del certificado y se protege el archivo con una clave privada. Actualizar la secuencia de comandos con contraseñas seguras. Conectarse a SQL Server principal y ejecute el siguiente Transact-SQL para crear el certificado:

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

En este momento la réplica principal de SQL Server tiene un certificado en `/var/opt/mssql/data/dbm_certificate.cer` y una privada at clave `var/opt/mssql/data/dbm_certificate.pvk`. Copie estos dos archivos en la misma ubicación en todos los servidores que hospedarán las réplicas de disponibilidad. Use el usuario mssql o dar permiso al usuario de mssql para tener acceso a estos archivos. 

Por ejemplo en el servidor de origen, el siguiente comando copia los archivos en el equipo de destino. Reemplace el  **<node2>**  valores con los nombres de las instancias de SQL Server que hospedarán las réplicas. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

En el servidor de destino, conceda permisos a mssql usuario tiene acceso al certificado.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Crear el certificado en los servidores secundarios

El siguiente script de Transact-SQL crea una clave maestra y el certificado de copia de seguridad que creó en la réplica principal de SQL Server. El comando también autoriza al usuario obtener acceso al certificado. Actualizar la secuencia de comandos con contraseñas seguras. La contraseña de descifrado es la misma contraseña que usó para crear el archivo .pvk en un paso anterior. Ejecute el siguiente script en todos los servidores secundarios para crear el certificado.

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Crear lo extremos en todas las réplicas de creación de reflejo de la base de datos

Los extremos de creación de reflejo de la base de datos utilizan el Protocolo de control de transporte (TCP) para enviar y recibir mensajes entre las instancias del servidor que participan en sesiones de creación de reflejo de la base de datos u hospedan réplicas de disponibilidad. El extremo de creación de reflejo de la base de datos escucha en un número de puerto TCP exclusivo. 

El código Transact-SQL siguiente crea un extremo de escucha denominado `Hadr_endpoint` para el grupo de disponibilidad. Se inicia el punto de conexión, y concede permiso de conexión para el usuario que ha creado. Antes de ejecutar la secuencia de comandos, reemplace los valores entre `**< ... >**`.


>[!NOTE]
>En esta versión, no utilice una dirección IP diferente para la dirección IP del agente de escucha. Estamos trabajando en una solución para este problema, pero el valor aceptable sólo por ahora es '0.0.0.0'.

Actualice el siguiente Transact-SQL para su entorno en todas las instancias de SQL Server: 

```Transact-SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!IMPORTANT]
>El puerto TCP en el servidor de seguridad debe estar abierto para el puerto de escucha.

Para obtener más información, consulte [el extremo de creación de reflejo de base de datos (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
