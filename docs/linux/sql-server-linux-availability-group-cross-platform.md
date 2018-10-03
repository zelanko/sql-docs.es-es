---
title: Configuración de SQL Server AlwaysOn en el grupo de disponibilidad en Windows y Linux | Microsoft Docs
description: Configurar el grupo de disponibilidad de SQL Server con réplicas en Windows y Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 8ab0b1bc65009a7439c9de8b8728a483413d09a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676573"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Configurar SQL Server grupo de disponibilidad AlwaysOn en Windows y Linux (multiplataforma)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

En este artículo se explica los pasos para crear un siempre en grupo de disponibilidad (AG) con una réplica en un servidor de Windows y la otra réplica en un servidor Linux. Esta configuración es multiplataforma, dado que las réplicas están en distintos sistemas operativos. Use esta configuración para la migración desde una plataforma a otra o para recuperación ante desastres (DR). Esta configuración no es compatible con alta disponibilidad porque no hay ninguna solución de clúster para administrar una configuración de desarrollo multiplataforma. 

![Híbrido ninguno](./media/sql-server-linux-availability-group-overview/image1.png)

Antes de continuar, debe estar familiarizado con la instalación y configuración para las instancias de SQL Server en Windows y Linux. 

## <a name="scenario"></a>Escenario

En este escenario, dos servidores están en distintos sistemas operativos. Windows Server 2016 denominado `WinSQLInstance` hospeda la réplica principal. Un servidor de Linux denominado `LinuxSQLInstance` hospedar la réplica secundaria.

## <a name="configure-the-ag"></a>Configurar el grupo de disponibilidad 

Los pasos para crear el grupo de disponibilidad son el mismo que los pasos para crear un grupo de disponibilidad para cargas de trabajo de escalado de lectura. El tipo de clúster del grupo de disponibilidad es NONE, porque no hay ningún administrador de clústeres. 

   >[!NOTE]
   >Para las secuencias de comandos en este artículo, los corchetes angulares `<` y `>` identificar valores que necesita para reemplazar su entorno. Los corchetes angulares a sí mismos no son necesarios para las secuencias de comandos. 

1. Instalar SQL Server 2017 en Windows Server 2016, habilitar a grupos de disponibilidad AlwaysOn de SQL Server Configuration Manager y establecer la autenticación de modo mixto. 

   >[!TIP]
   >Si va a validar esta solución en Azure, coloque ambos servidores en el mismo conjunto de disponibilidad para asegurarse de que se separan del centro de datos. 

   **Habilitar a grupos de disponibilidad**

   Para obtener instrucciones, consulte [habilitar y deshabilitar grupos de disponibilidad AlwaysOn (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).

   ![Habilitar a grupos de disponibilidad](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   Administrador de configuración de SQL Server, se observa que el equipo no es un nodo en un clúster de conmutación por error. 

   Después de habilitar a los grupos de disponibilidad, reinicie SQL Server.

   **Configurar la autenticación de modo mixto**

   Para obtener instrucciones, consulte [cambiar el modo de autenticación de servidor](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure).

1. Instalar a SQL Server 2017 en Linux. Para obtener instrucciones, consulte [instalar SQL Server](sql-server-linux-setup.md). Habilitar `hadr` mediante mssql-conf.

   Para habilitar `hadr` mediante mssql-conf desde un símbolo del sistema del shell, emita el siguiente comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   Después de habilitar `hadr`, reinicie la instancia de SQL Server.  

   La imagen siguiente muestra este paso completa.

   ![Habilitar Linux de grupos de disponibilidad](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. Configurar el archivo de hosts en ambos servidores o registrar los nombres de servidor DNS.

1. Abra los puertos de firewall para TCP 1433 y 5022 en Windows y Linux.

1. En la réplica principal, cree un inicio de sesión de base de datos y una contraseña.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. En la réplica principal, cree una clave maestra y un certificado y luego realizar una copia de seguridad del certificado con una clave privada.

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

1. Copie el certificado y clave privada en el servidor de Linux (réplica) en `/var/opt/mssql/data`. Puede usar `pscp` para copiar los archivos en el servidor Linux. 

1. Establecer el grupo y la propiedad de la clave privada y el certificado que `mssql:mssql`.

   El siguiente script establece el grupo y la propiedad de los archivos. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   En el diagrama siguiente, la propiedad y el grupo están establecidas correctamente para el certificado y la clave.

   ![Habilitar Linux de grupos de disponibilidad](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. En la réplica secundaria, cree un inicio de sesión de base de datos y una contraseña y cree una clave maestra.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. En la réplica secundaria, restaure el certificado que ha copiado en `/var/opt/mssql/data`. 

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
   >El firewall debe estar abierto para el agente de escucha el puerto TCP. En el script anterior, el puerto es 5022. Utilice cualquier puerto TCP disponible. 

1. En la réplica secundaria, cree el punto de conexión. Repita el script anterior en la réplica secundaria para crear el punto de conexión. 

1. En la réplica principal, cree el grupo de disponibilidad con `CLUSTER_TYPE = NONE`. El script de ejemplo usa `SEEDING_MODE = AUTOMATIC` para crear el grupo de disponibilidad. 

   >[!NOTE]
   >Cuando la instancia de Windows de SQL Server utiliza diferentes rutas de acceso para archivos de datos y registro, la propagación se produce un error en la instancia de Linux de SQL Server, dado que estas rutas de acceso no existe en la réplica secundaria automática. Para usar el siguiente script para un grupo de disponibilidad multiplataforma, la base de datos requiere la misma ruta de acceso para los archivos de datos y de registro en el servidor de Windows. También puede actualizar la secuencia de comandos para establecer `SEEDING_MODE = MANUAL` y, a continuación, realizar copias de seguridad y restaurar la base de datos con `NORECOVERY` para inicializar la base de datos. 
   >
   >Este comportamiento se aplica a imágenes de Azure Marketplace. 
   >
   >Para obtener más información acerca de la propagación automática, consulte [la propagación automática: diseño de disco](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout). 

   Antes de ejecutar el script, actualice los valores de los grupos de disponibilidad.

      * Reemplace `<WinSQLInstance>` con el nombre del servidor de la instancia de SQL Server de la réplica principal.

      * Reemplace `<LinuxSQLInstance>` con el nombre del servidor de la instancia de SQL Server de réplica secundaria. 

   Para crear el grupo de disponibilidad, actualice los valores y ejecute el script en la réplica principal.  

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
   
   Para obtener más información, consulte [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md).

1. En la réplica secundaria, combine el grupo de disponibilidad.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. Crear una base de datos para el grupo de disponibilidad. Los pasos de ejemplo usa una base de datos denominada `<TestDB>`. Si usa la propagación automática, establezca la misma ruta de acceso para los datos y los archivos de registro. 

   Antes de ejecutar el script, actualice los valores de la base de datos.

      * Reemplace `<TestDB>` con el nombre de la base de datos.

      * Reemplace `<F:\Path>` con la ruta de acceso para los archivos de registro y base de datos. Utilice la misma ruta de acceso para los archivos de registro y base de datos. 

      También puede usar las rutas de acceso de forma predeterminada. 

    Para crear la base de datos, ejecute el script. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. Realizar copia de seguridad de la base de datos completa. 

1. Si no usa la propagación automática, restaure la base de datos en el servidor de réplica secundaria (Linux). [Migrar una base de datos de SQL Server de Windows para Linux mediante la copia de seguridad y restauración](sql-server-linux-migrate-restore-database.md). Restaurar la base de datos `WITH NORECOVERY` en la réplica secundaria. 

1. Agregue la base de datos al grupo de disponibilidad. Actualice el script de ejemplo. Reemplace `<TestDB>` con el nombre de la base de datos. En la réplica principal, ejecute la consulta SQL para agregar la base de datos al grupo de disponibilidad.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. Compruebe que se están rellenando la base de datos en la réplica secundaria. 

## <a name="fail-over-the-primary-replica"></a>Conmutar por error la réplica principal

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

En este artículo se revisa los pasos para crear un grupo de disponibilidad multiplataforma para admitir cargas de trabajo de migración o escalado de lectura. Se puede usar para la recuperación ante desastres manual. También se explica cómo conmutar por error el grupo de disponibilidad. Tipo de clúster utiliza un grupo de disponibilidad multiplataforma `NONE` y no admite la alta disponibilidad porque no hay ninguna herramienta clúster entre plataformas. 

## <a name="next-steps"></a>Pasos siguientes

[Información general de grupos de disponibilidad de AlwaysOn](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Conceptos básicos de la disponibilidad de SQL Server para las implementaciones de Linux](sql-server-linux-ha-basics.md)
