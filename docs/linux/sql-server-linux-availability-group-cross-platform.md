---
title: Configuración del grupo de disponibilidad de SQL Server Always On en Windows y Linux
description: Configure el grupo de disponibilidad de SQL Server con réplicas en Windows y Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 651467463e0563c9da00e23115ffb7bc4f151d23
ms.sourcegitcommit: cebf41506a28abfa159a5dd871b220630c4c4504
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2020
ms.locfileid: "77479684"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Configuración del grupo de disponibilidad de SQL Server Always On en Windows y Linux (multiplataforma)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

En este artículo se explican los pasos para crear un grupo de disponibilidad (AG) Always On con una réplica en un servidor de Windows y la otra réplica en un servidor Linux. Esta configuración es multiplataforma porque las réplicas están en sistemas operativos diferentes. Use esta configuración para la migración de una plataforma a la otra o para la recuperación ante desastres (DR). Esta configuración no admite la alta disponibilidad porque no hay ninguna solución de clúster para administrar una configuración multiplataforma. 

![Ninguno híbrido](./media/sql-server-linux-availability-group-overview/image1.png)

Antes de continuar, debe estar familiarizado con la instalación y configuración de instancias de SQL Server en Windows y Linux. 

## <a name="scenario"></a>Escenario

En este escenario, hay dos servidores en sistemas operativos diferentes. Una instancia de Windows Server 2016 denominada `WinSQLInstance` hospeda la réplica principal. Un servidor Linux denominado `LinuxSQLInstance` hospeda la réplica secundaria.

## <a name="configure-the-ag"></a>Configuración del AG 

Los pasos para crear el AG son los mismos que los pasos para crear un AG para cargas de trabajo de escalado de lectura. El tipo de clúster de AG es NONE, ya que no hay ningún administrador de clústeres. 

   >[!NOTE]
   >En el caso de los scripts de este artículo, los corchetes angulares `<` y `>` identifican los valores que debe reemplazar para su entorno. Los corchetes angulares en sí no son necesarios para los scripts. 

1. Instale SQL Server 2017 en Windows Server 2016, habilite los grupos de disponibilidad Always On desde el administrador de configuración de SQL Server y establezca la autenticación de modo mixto. 

   >[!TIP]
   >Si va a validar esta solución en Azure, coloque ambos servidores en el mismo conjunto de disponibilidad para asegurarse de que se separan en el centro de datos. 

   **Habilitación de grupos de disponibilidad**

   Para obtener instrucciones, consulte [Habilitación o deshabilitación de la característica de grupo de disponibilidad Always On](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).

   ![Habilitación de grupos de disponibilidad](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   El administrador de configuración de SQL Server nota que el equipo no es un nodo en un clúster de conmutación por error. 

   Después de habilitar los grupos de disponibilidad, reinicie SQL Server.

   **Configuración de la autenticación de modo mixto**

   Para obtener instrucciones, consulte [Cambiar el modo de autenticación del servidor](../database-engine/configure-windows/change-server-authentication-mode.md#change-authentication-mode-with-ssms).

1. Instale SQL Server 2017 en Linux. Para obtener instrucciones, consulte [Instalación de SQL Server](sql-server-linux-setup.md). Habilite `hadr` mediante mssql-conf.

   Para habilitar `hadr` mediante mssql-conf desde una solicitud de shell, emita el siguiente comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   Después de habilitar `hadr`, reinicie la instancia de SQL Server.  

   En la siguiente imagen se muestra este paso al completo.

   ![Habilitación de grupos de disponibilidad Linux](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. Configure el archivo de hosts en ambos servidores o registre los nombres de servidor con DNS.

1. Abra los puertos de firewall para TPC 1433 y 5022 en Windows y Linux.

1. En la réplica principal, cree un inicio de sesión y una contraseña de base de datos.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. En la réplica principal, cree una clave y un certificado maestros y, después, haga una copia de seguridad del certificado con una clave privada.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. Copie el certificado y la clave privada en el servidor Linux (réplica secundaria) en `/var/opt/mssql/data`. Puede usar `pscp` para copiar los archivos en el servidor Linux. 

1. Establezca el grupo y la propiedad de la clave privada y el certificado en `mssql:mssql`.

   El siguiente script establece el grupo y la propiedad de los archivos. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   En el diagrama siguiente, la propiedad y el grupo están configurados correctamente para el certificado y la clave.

   ![Habilitación de grupos de disponibilidad Linux](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. En la réplica secundaria, cree un inicio de sesión y una contraseña de base de datos y cree una clave maestra.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. En la réplica secundaria, restaure el certificado que copió en `/var/opt/mssql/data`. 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. En la réplica principal, cree un punto de conexión.

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >El firewall debe estar abierto para el puerto TCP de escucha. En el script anterior, el puerto es 5022. Use cualquier puerto TCP disponible. 

1. En la réplica secundaria, cree el punto de conexión. Repita el script anterior en la réplica secundaria para crear el punto de conexión. 

1. En la réplica principal, cree el AG con `CLUSTER_TYPE = NONE`. El script de ejemplo usa `SEEDING_MODE = AUTOMATIC` para crear el AG. 

   >[!NOTE]
   >Cuando la instancia de Windows de SQL Server usa diferentes rutas de acceso para los archivos de datos y de registro, la propagación automática no se realiza correctamente en la instancia de Linux de SQL Server porque estas rutas de acceso no existen en la réplica secundaria. Para usar el siguiente script para un AG multiplataforma, la base de datos requiere la misma ruta de acceso para los archivos de datos y de registro en el servidor de Windows. También puede actualizar el script para establecer `SEEDING_MODE = MANUAL` y, después, realizar una copia de seguridad y restaurar la base de datos con `NORECOVERY` para inicializar la base de datos. 
   >
   >Este comportamiento se aplica a las imágenes de Azure Marketplace. 
   >
   >Para obtener más información sobre la propagación automática, vea [Propagación automática - Diseño de disco](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout). 

   Antes de ejecutar el script, actualice los valores de los AG.

      * Reemplace `<WinSQLInstance>` por el nombre del servidor de la instancia de SQL Server de la réplica principal.

      * Reemplace `<LinuxSQLInstance>` por el nombre del servidor de la instancia de SQL Server de la réplica secundaria. 

   Para crear el AG, actualice los valores y ejecute el script en la réplica principal.  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   Para obtener más información, vea [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md).

1. En la réplica secundaria, conecte el AG.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. Cree una base de datos para el AG. En los pasos de ejemplo se utiliza una base de datos denominada `<TestDB>`. Si utiliza la propagación automática, establezca la misma ruta de acceso para los archivos de datos y de registro. 

   Antes de ejecutar el script, actualice los valores de la base de datos.

      * Reemplace `<TestDB>` por el nombre de la base de datos.

      * Reemplace `<F:\Path>` por la ruta de acceso de los archivos de base de datos y de registro. Use la misma ruta de acceso para los archivos de base de datos y de registro. 

      También se puede utilizar las rutas de acceso predeterminadas. 

    Para crear la base de datos, ejecute el script. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. Realice una copia de seguridad completa de la base de datos. 

1. Si no utiliza la propagación automática, restaure la base de datos en el servidor de réplica secundaria (Linux). [Migración de una base de datos SQL Server de Windows a Linux mediante Copia de seguridad y restauración](sql-server-linux-migrate-restore-database.md). Restaure la base de datos `WITH NORECOVERY` en la réplica secundaria. 

1. Agregue la base de datos al AG. Actualice el script de ejemplo. Reemplace `<TestDB>` por el nombre de la base de datos. En la réplica principal, ejecute la consulta SQL para agregar la base de datos al AG.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. Compruebe que la base de datos se está rellenando en la réplica secundaria. 

## <a name="fail-over-the-primary-replica"></a>Conmutación por error de la réplica principal

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

En este artículo se revisan los pasos para crear un AG multiplataforma para admitir las cargas de trabajo de migración o de escalado de lectura. Se puede utilizar para la recuperación ante desastres manual. También se explica cómo conmutar por error el AG. Un AG multiplataforma usa el tipo de clúster `NONE` y no admite la alta disponibilidad porque no hay ninguna herramienta de clúster multiplataforma. 

## <a name="next-steps"></a>Pasos siguientes

[Información general de los grupos de disponibilidad AlwaysOn](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Conceptos básicos sobre disponibilidad de SQL Server para implementaciones de Linux](sql-server-linux-ha-basics.md)
