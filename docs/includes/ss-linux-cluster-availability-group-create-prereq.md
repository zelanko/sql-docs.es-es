## <a name="prerequisites"></a>Requisitos previos

Antes de crear el grupo de disponibilidad, debe:

- Establecer el entorno para que puedan comunicarse todos los servidores que hospedarán las réplicas de disponibilidad.
- Instale SQL Server.

>[!NOTE]
>En Linux, debe crear un grupo de disponibilidad antes de agregarlo como recurso de clúster para ser administrado por el clúster. En este documento, se proporciona un ejemplo que crea el grupo de disponibilidad. Para que obtener instrucciones de distribución específicos crear el clúster y agregar el grupo de disponibilidad como un recurso de clúster, consulte los vínculos en "Pasos siguientes".

1. Actualice el nombre de equipo para cada host.

   Cada nombre de SQL Server debe cumplir con los siguientes requisitos:
   
   - 15 caracteres o menos.
   - Es único dentro de la red.
   
   Para establecer el nombre del equipo, edite `/etc/hostname`. La siguiente secuencia de comandos le permite editar `/etc/hostname` con `vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. Configurar el archivo de hosts.

    >[!NOTE]
    >Si los nombres de host están registrados con su dirección IP en el servidor DNS, no es necesario realizar los pasos siguientes. Validar que todos los nodos pensadas para formar parte de la configuración del grupo de disponibilidad pueden comunicarse entre sí. (Debe responder a un ping en el nombre de host con la dirección IP correspondiente). Además, asegúrese de que el archivo/etc/hosts no contiene un registro que se asigna la dirección IP de localhost 127.0.0.1 con el nombre de host del nodo.
    >

   El archivo de hosts de cada servidor contiene las direcciones IP y los nombres de todos los servidores que participarán en el grupo de disponibilidad. 

   El comando siguiente devuelve la dirección IP del servidor actual:

   ```bash
   sudo ip addr show
   ```

   Actualice `/etc/hosts`. La siguiente secuencia de comandos le permite editar `/etc/hosts` con `vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   En el ejemplo siguiente, se muestra `/etc/hosts` en **node1** con adiciones para **node1**, **node2** y **node3**. En este documento, **Nodo1** hace referencia al servidor que hospeda la réplica principal. Y **Nodo2** y **Nodo3** hacen referencia a los servidores que hospedan las réplicas secundarias.

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>Instalar SQL Server

Instale SQL Server. Los siguientes vínculos apuntan a las instrucciones de instalación de SQL Server para diversas distribuciones: 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>Habilitar a los grupos de disponibilidad AlwaysOn y reinicie el servidor mssql

Habilitar a los grupos de disponibilidad AlwaysOn en cada nodo que hospeda una instancia de SQL Server. A continuación, reinicie `mssql-server`. Ejecute el script siguiente:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwaysonhealth-event-session"></a>Habilitar una sesión de eventos AlwaysOn_health 

Si lo desea, puede habilitar eventos extendidos grupos de AlwaysOn disponibilidad ayudar a un diagnóstico más detallado y causa para solucionar un grupo de disponibilidad. Ejecute el siguiente comando en cada instancia de SQL Server: 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obtener más información acerca de esta sesión XE, consulte [AlwaysOn eventos extendidos](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-a-database-mirroring-endpoint-user"></a>Crear un usuario de punto de conexión de creación de reflejo de la base de datos

El siguiente script de Transact-SQL crea un inicio de sesión denominado `dbm_login` y un usuario denominado `dbm_user`. Actualice el script con una contraseña segura. Para crear el usuario de extremo de creación de reflejo de la base de datos, ejecute el comando siguiente en todas las instancias de SQL Server:

```SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Crear un certificado

El servicio SQL Server en Linux usa certificados para autenticar la comunicación entre los puntos de conexión de creación de reflejo. 

El siguiente script de Transact-SQL crea una clave maestra y un certificado. A continuación, realiza una copia de seguridad del certificado y protege el archivo con una clave privada. Actualice el script con contraseñas seguras. Conéctese a la instancia principal de SQL Server. Para crear el certificado, ejecute el siguiente script de Transact-SQL:

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

En este punto, la réplica principal de SQL Server tiene un certificado en `/var/opt/mssql/data/dbm_certificate.cer` y una privada at clave `var/opt/mssql/data/dbm_certificate.pvk`. Copie estos dos archivos en la misma ubicación en todos los servidores que hospedarán las réplicas de disponibilidad. Use el usuario mssql o dar permiso al usuario mssql para tener acceso a estos archivos. 

Por ejemplo, en el servidor de origen, el siguiente comando copia los archivos en el equipo de destino. Reemplace el `**<node2>**` valores con los nombres de las instancias de SQL Server que hospedarán las réplicas. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

En cada servidor de destino, dar permiso al usuario mssql para tener acceso al certificado.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Crear el certificado en los servidores secundarios

El siguiente script de Transact-SQL crea una clave maestra y un certificado de copia de seguridad que creó en la réplica principal de SQL Server. El comando también autoriza al usuario para que obtenga acceso al certificado. Actualice el script con contraseñas seguras. La contraseña de descifrado es la misma que ha usado para crear el archivo .pvk en un paso anterior. Para crear el certificado, ejecute el siguiente script en todos los servidores secundarios:

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Crear los puntos de conexión de creación de reflejo de la base de datos en todas las réplicas

Extremos de creación de reflejo de base de datos usa el protocolo de Control de transmisión (TCP) para enviar y recibir mensajes entre las instancias de servidor que participan en la creación de reflejo de la base de datos u hospedan réplicas de disponibilidad. El extremo de creación de reflejo de la base de datos escucha en un número de puerto TCP exclusivo. El agente de escucha TCP requiere una dirección IP de escucha. La dirección IP de escucha debe ser una dirección IPv4. También puede utilizar `0.0.0.0`. 

El script de Transact-SQL siguiente crea un extremo de escucha denominado `Hadr_endpoint` para el grupo de disponibilidad. Inicia el punto de conexión y concede permiso de conexión para el usuario que ha creado. Antes de ejecutar el script, reemplace los valores entre `**< ... >**`.

Actualice el siguiente script de Transact-SQL para su entorno en todas las instancias de SQL Server: 

```SQL
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

>[!NOTE]
>Si usas SQL Server Express Edition en un nodo para hospedar una réplica de solo configuración, el único valor válido para `ROLE` es `WITNESS`. Ejecute el siguiente script en SQL Server Express Edition:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

El puerto TCP en el servidor de seguridad debe estar abierto para el puerto de escucha.



>[!IMPORTANT]
>Para la versión de SQL Server 2017, es el único método de autenticación admitido para el extremo de reflejo de la base de datos `CERTIFICATE`. El `WINDOWS` opción se habilitarán en futuras versiones.

Para obtener más información, consulte [la base de datos (SQL Server) del extremo de reflejo](http://msdn.microsoft.com/library/ms179511.aspx).


