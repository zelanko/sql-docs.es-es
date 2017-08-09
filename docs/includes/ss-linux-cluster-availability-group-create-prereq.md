## <a name="prerequisites"></a>Requisitos previos

Antes de crear el grupo de disponibilidad, debe:

- Establecer el entorno de forma que se puedan comunicar todos los servidores que hospedarán las réplicas de disponibilidad
- Instalar SQL Server

>[!NOTE]
>En Linux, debe crear un grupo de disponibilidad antes de agregarlo como un recurso de clúster para que lo administre el clúster. En este documento, se proporciona un ejemplo que crea el grupo de disponibilidad. Para la distribución de instrucciones específicas para crear el clúster y agregar el grupo de disponibilidad como un recurso de clúster, consulte los vínculos en [Pasos siguientes](#next-steps).

1. **Actualizar el nombre de equipo de cada host**

   Cada nombre de SQL Server debe cumplir con los siguientes requisitos:
   
   - Debe tener 15 caracteres o menos.
   - Debe ser único en la red.
   
   Para establecer el nombre del equipo, edite `/etc/hostname`. El siguiente script le permite editar `/etc/hostname` con `vi`.

   ```bash
   sudo vi /etc/hostname
   ```

1. **Configurar el archivo de hosts**

>[!NOTE]
>Si los nombres de host están registrados con su IP en el servidor DNS, no hay que realizar los pasos siguientes. Valide que todos los nodos que van a formar parte de la configuración del grupo de disponibilidad pueden comunicarse entre sí (al hacer ping en el nombre de host se debe responder con la dirección IP correspondiente). Además, asegúrese de que el archivo/etc/hosts no tiene ningún registro que asigne la dirección IP de localhost 127.0.0.1 con el nombre de host del nodo.


   El archivo de hosts de cada servidor contiene las direcciones IP y los nombres de todos los servidores que participarán en el grupo de disponibilidad. 

   El comando siguiente devuelve la dirección IP del servidor actual:

   ```bash
   sudo ip addr show
   ```

   Actualice `/etc/hosts`. El siguiente script le permite editar `/etc/hosts` con `vi`.

   ```bash
   sudo vi /etc/hosts
   ```

   En el ejemplo siguiente, se muestra `/etc/hosts` en **node1** con adiciones para **node1**, **node2** y **node3**. En este documento, **node1** hace referencia al servidor que hospeda la réplica principal. **node2** y **node3** hacen referencia a servidores que hospedan réplicas secundarias.


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.12 node1
   10.128.16.77 node2
   10.128.15.33 node3
   ```

### <a name="install-sql-server"></a>Instalar SQL Server

Instale SQL Server. Los siguientes vínculos apuntan a las instrucciones de instalación de SQL Server para varias distribuciones. 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)

- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)

- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Habilitar los grupos de disponibilidad AlwaysOn y reiniciar sqlserver

Habilite los grupos de disponibilidad AlwaysOn en cada nodo que hospede una instancia de SQL Server y, luego, reinicie `mssql-server`.  Ejecute el script siguiente:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>Habilitar la sesión de eventos AlwaysOn_health 

Opcionalmente, puede habilitar los eventos extendidos de los grupos de disponibilidad AlwaysOn para ayudar con el diagnóstico de la causa raíz cuando solucione los problemas de un grupo de disponibilidad. Ejecute el comando siguiente en cada instancia de SQL Server. 

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obtener más información sobre esta sesión de XE, vea [Eventos extendidos de AlwaysOn](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-db-mirroring-endpoint-user"></a>Crear el usuario de punto de conexión de la creación de reflejo de la base de datos

El siguiente script de Transact-SQL crea un inicio de sesión denominado `dbm_login` y un usuario denominado `dbm_user`. Actualice el script con una contraseña segura. Ejecute el comando siguiente en todas las instancias de SQL Server para crear el usuario de punto de conexión de la creación de reflejo de la base de datos.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Crear un certificado

El servicio SQL Server en Linux usa certificados para autenticar la comunicación entre los puntos de conexión de creación de reflejo. 

El siguiente script de Transact-SQL crea una clave maestra y un certificado. Después, realiza una copia de seguridad del certificado y protege el archivo con una clave privada. Actualice el script con contraseñas seguras. Conéctese a la instancia de SQL Server principal y ejecute el siguiente comando de Transact-SQL para crear el certificado:

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

En este momento, la réplica principal de SQL Server tiene un certificado en `/var/opt/mssql/data/dbm_certificate.cer` y una clave privada en `var/opt/mssql/data/dbm_certificate.pvk`. Copie estos dos archivos en la misma ubicación en todos los servidores que hospedarán las réplicas de disponibilidad. Use el usuario de mssql o conceda permiso al usuario de mssql para tener acceso a estos archivos. 

Por ejemplo, en el servidor de origen, el siguiente comando copia los archivos en el equipo de destino. Reemplace los valores **<node2>** con los nombres de las instancias de SQL Server que hospedarán las réplicas. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

En cada servidor de destino, conceda permiso al usuario de mssql para que acceda al certificado.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Crear el certificado en los servidores secundarios

El siguiente script de Transact-SQL crea una clave maestra y un certificado de la copia de seguridad creada en la réplica principal de SQL Server. El comando también autoriza al usuario para que obtenga acceso al certificado. Actualice el script con contraseñas seguras. La contraseña de descifrado es la misma que ha usado para crear el archivo .pvk en un paso anterior. Ejecute el siguiente script en todos los servidores secundarios para crear el certificado.

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

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Crear los puntos de conexión de creación de reflejo de la base de datos en todas las réplicas

Los extremos de creación de reflejo de la base de datos utilizan el Protocolo de control de transporte (TCP) para enviar y recibir mensajes entre las instancias del servidor que participan en sesiones de creación de reflejo de la base de datos u hospedan réplicas de disponibilidad. El extremo de creación de reflejo de la base de datos escucha en un número de puerto TCP exclusivo. 

El código de Transact-SQL siguiente crea un punto de conexión de escucha denominado `Hadr_endpoint` para el grupo de disponibilidad. Se inicia el punto de conexión y concede permiso de conexión al usuario que ha creado. Antes de ejecutar el script, reemplace los valores entre `**< ... >**`.

>[!NOTE]
>En esta versión, no use una dirección IP diferente para la dirección IP del agente de escucha. Estamos trabajando en una solución a este problema, pero el único valor aceptable por ahora es "0.0.0.0".

Actualice el siguiente código de Transact-SQL para su entorno en todas las instancias de SQL Server: 

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
>El puerto TCP en el firewall debe estar abierto para el puerto de escucha.

>[!IMPORTANT]
>Para la versión de SQL Server 2017, el único método de autenticación que se admite para el punto de conexión de creación de reflejo de la base de datos es `CERTIFICATE`. La opción `WINDOWS` se habilitará en una futura versión.

Para obtener toda la información, vea [El extremo de creación de reflejo de la base de datos (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
