---
ms.openlocfilehash: 7d392ee6791c120243b304ab24b2f8268499617d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215576"
---
## <a name="prerequisites"></a>Prerequisites

Antes de crear el grupo de disponibilidad, debe:

- Establecer el entorno de forma que todos los servidores que hospedarán las réplicas de disponibilidad se puedan comunicar.
- Instale SQL Server.

>[!NOTE]
>En Linux, debe crear un grupo de disponibilidad antes de agregarlo como un recurso de clúster para que lo administre el clúster. En este documento, se proporciona un ejemplo que crea el grupo de disponibilidad. Para obtener instrucciones específicas de la distribución sobre cómo crear el clúster y agregar el grupo de disponibilidad como recurso del clúster, consulte los vínculos en "Pasos siguientes".

1. Actualice el nombre de equipo de cada host.

   Cada nombre de SQL Server debe cumplir con los siguientes requisitos:
   
   - 15 caracteres o menos.
   - Debe ser único en la red.
   
   Para establecer el nombre del equipo, edite `/etc/hostname`. El siguiente script le permite editar `/etc/hostname` con `vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. Configure el archivo de hosts.

    >[!NOTE]
    >Si los nombres de host están registrados con su IP en el servidor DNS, no hay que realizar los pasos siguientes. Compruebe que todos los nodos destinados a formar parte de la configuración del grupo de disponibilidad pueden comunicarse entre sí. (Un ping al nombre de host debe responder con la dirección IP correspondiente). Además, asegúrese de que el archivo /etc/hosts no contiene ningún registro que asigne la dirección IP de localhost 127.0.0.1 con el nombre de host del nodo.
    >

   El archivo de hosts de cada servidor contiene las direcciones IP y los nombres de todos los servidores que participarán en el grupo de disponibilidad. 

   El comando siguiente devuelve la dirección IP del servidor actual:

   ```bash
   sudo ip addr show
   ```

   Actualice `/etc/hosts`. El siguiente script le permite editar `/etc/hosts` con `vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   En el ejemplo siguiente, se muestra `/etc/hosts` en **node1** con adiciones para **node1**, **node2** y **node3**. En este documento, **node1** hace referencia al servidor que hospeda la réplica principal. Y **node2** y **node3** hacen referencia a servidores que hospedan las réplicas secundarias.

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>Instalar SQL Server

Instale SQL Server. Los siguientes vínculos apuntan a las instrucciones de instalación de SQL Server para varias distribuciones: 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>Habilitar los grupos de disponibilidad AlwaysOn y reiniciar mssql-server

Habilite los grupos de disponibilidad AlwaysOn en cada nodo en el que se hospede una instancia de SQL Server. A continuación, reinicie `mssql-server`. Ejecute el script siguiente:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwayson_health-event-session"></a>Habilitar una sesión de eventos AlwaysOn_health 

Opcionalmente, puede habilitar los eventos extendidos de los grupos de disponibilidad AlwaysOn para ayudar con el diagnóstico de la causa raíz cuando solucione los problemas de un grupo de disponibilidad. Ejecute el comando siguiente en todas las instancias de SQL Server: 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Para obtener más información sobre esta sesión de XE, vea [Eventos extendidos de AlwaysOn](https://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-a-certificate"></a>Crear un certificado

El servicio SQL Server en Linux usa certificados para autenticar la comunicación entre los puntos de conexión de creación de reflejo. 

El script de Transact-SQL siguiente crea una clave maestra y un certificado. Después, realiza una copia de seguridad del certificado y protege el archivo con una clave privada. Actualice el script con contraseñas seguras. Conecte con la instancia de SQL Server principal. Para crear el certificado, ejecute el script siguiente de Transact-SQL:

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

En este momento, la réplica principal de SQL Server tiene un certificado en `/var/opt/mssql/data/dbm_certificate.cer` y una clave privada en `var/opt/mssql/data/dbm_certificate.pvk`. Copie estos dos archivos en la misma ubicación en todos los servidores que hospedarán las réplicas de disponibilidad. Utilice el usuario de mssql o conceda permiso al usuario de mssql para tener acceso a estos archivos. 

Por ejemplo, en el servidor de origen, el siguiente comando copia los archivos en el equipo de destino. Reemplace los valores `**<node2>**` por los nombres de las instancias de SQL Server que hospedarán las réplicas. 

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

El script de Transact-SQL siguiente crea una clave maestra y un certificado a partir de la copia de seguridad creada en la réplica principal de SQL Server. Actualice el script con contraseñas seguras. La contraseña de descifrado es la misma que ha usado para crear el archivo .pvk en un paso anterior. Ejecute el siguiente script en todos los servidores secundarios para crear el certificado:

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Crear los puntos de conexión de creación de reflejo de la base de datos en todas las réplicas

Los extremos de creación de reflejo de la base de datos usan el Protocolo de control de transmisión (TCP) para enviar y recibir mensajes entre las instancias del servidor que participan en las sesiones de creación de reflejo de la base de datos o que hospedan las réplicas de disponibilidad. El extremo de creación de reflejo de la base de datos escucha en un número de puerto TCP exclusivo. 

El script de Transact-SQL siguiente crea un punto de conexión de escucha denominado `Hadr_endpoint` para el grupo de disponibilidad. Se inicia el punto de conexión y se concede permiso de conexión al certificado que ha creado. Antes de ejecutar el script, reemplace los valores entre `**< ... >**`. Opcionalmente puede incluir una dirección IP `LISTENER_IP = (0.0.0.0)`. La dirección IP de escucha debe ser una dirección IPv4. También se puede usar `0.0.0.0`. 

Actualice el script de Transact-SQL siguiente para el entorno en todas las instancias de SQL Server: 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

>[!NOTE]
>Si usa SQL Server Express Edition en un nodo para hospedar una réplica de solo configuración, el único valor válido para `ROLE` es `WITNESS`. Ejecute el siguiente script en SQL Server Express Edition:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

El puerto TCP en el firewall debe estar abierto para el puerto de escucha.



>[!IMPORTANT]
>Para la versión de SQL Server 2017, el único método de autenticación que se admite para el punto de conexión de creación de reflejo de la base de datos es `CERTIFICATE`. La opción `WINDOWS` se habilitará en una futura versión.

Para obtener más información, vea [El punto de conexión de creación de reflejo de la base de datos (SQL Server)](https://msdn.microsoft.com/library/ms179511.aspx).


