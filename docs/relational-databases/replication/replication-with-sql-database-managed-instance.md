---
title: Replicación con Instancia administrada de SQL Database | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d55aea5d50d9ea434aabb392d0c6b53573c0199e
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559575"
---
# <a name="replication-with-sql-database-managed-instance"></a>Replicación con Instancia administrada de SQL Database

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Instancia administrada de Azure SQL Database (versión preliminar) admite la replicación transaccional. Instancia administrada puede hospedad bases de datos del publicador, distribuidor y suscriptor.

## <a name="common-configurations"></a>Configuraciones comunes

En general, tanto el publicador como el distribuidor deben estar en la nube o en el entorno local. Se admiten las siguientes configuraciones:

- **Publicador con distribuidor local en instancia administrada**

   ![Replication-with-azure-sql-db-single-managed-instance-publisher-distributor](./media/replication-with-sql-database-managed-instance/01-single-instance-asdbmi-pubdist.png)

   Las bases de datos del publicador y del distribuidor se configuran en una sola instancia administrada.

- **Publicador con distribuidor remoto en instancia administrada**

   ![Replication-with-azure-sql-db-separate-managed-instances-publisher-distributor](./media/replication-with-sql-database-managed-instance/02-separate-instances-asdbmi-pubdist.png)

   El publicador y el distribuidor se configuran en dos instancias administradas. En esta configuración:

  - Ambas instancias administradas están en la misma red virtual.

  - Ambas instancias administradas están en la misma ubicación.

- **Publicador y distribuidor en el entorno local con suscriptor en instancia administrada**

   ![Replication-from-on-premises-to-azure-sql-db-subscriber](./media/replication-with-sql-database-managed-instance/03-azure-sql-db-subscriber.png)

   En esta configuración, Azure SQL Database es un suscriptor. Esta configuración admite la migración desde el entorno local a Azure. En el rol del suscriptor, la base de datos SQL no requiere una instancia administrada, pero sí se puede usar una Instancia administrada de SQL Database como un paso en la migración desde el entorno local a Azure. Para más información sobre los suscriptores de Azure SQL Database, consulte [Replicación a SQL Database](replication-to-sql-database.md).

## <a name="requirements"></a>Requisitos

El publicador y distribuidor en Azure SQL Database requiere lo siguiente:

- Instancia administrada de Azure SQL Database.

   >[!NOTE]
   >Las instancias de Azure SQL Database que no están configuradas con Instancia administrada solo pueden ser suscriptores.

- Todas las instancias de SQL Server deben estar en la misma red virtual.

- La conectividad usa Autenticación SQL entre los participantes de la replicación.

- Un recurso compartido de cuenta de Azure Storage para el directorio de trabajo de la replicación.

## <a name="features"></a>Características

Es compatible con:

- La combinación de la replicación de instantáneas y transaccional de instancias locales y de Instancia administrada de Azure SQL Database.

- Los suscriptores pueden estar en el entorno local, en Azure SQL Database o puede ser grupos elásticos.

- Replicación unidireccional o bidireccional

## <a name="configure-publishing-and-distribution-example"></a>Configuración de un ejemplo de publicación y distribución

1. [Cree una Instancia administrada de Azure SQL Database](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal) en el portal.

1. [Cree una cuenta de Azure Storage](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#create-a-storage-account) para el directorio de trabajo. Asegúrese de copiar las claves de almacenamiento. Consulte [Visualización y copia de las claves de acceso de almacenamiento](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys).

1. Cree una base de datos para el publicador.

   En los scripts de ejemplo que aparecen a continuación, reemplace `<Publishing_DB>` por el nombre de esta base de datos.

1. Cree un usuario de base de datos con Autenticación SQL para el distribuidor. Consulte [Creación de usuarios de base de datos](http://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial#creating-database-users). Use una contraseña segura.

   En los scripts de ejemplo que aparecen a continuación, use `<SQL_USER>` y `<PASSWORD>` con el usuario y la contraseña de esta base de datos de cuenta de SQL Server.

1. [Conéctese a Instancia administrada de SQL Database](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ssms).

1. Ejecute la consulta siguiente para agregar el distribuidor y la base de datos de distribución.

   ```sql
   USE [master]
   GO
   EXEC sp_adddistributor @distributor = @@ServerName;
   EXEC sp_adddistributiondb @database = N'distribution';
   ```

1. Para configurar un publicador para que use una base de datos de distribución especificada, actualice y ejecute la consulta siguiente.

   Reemplace `<SQL_USER>` y `<PASSWORD>` por la cuenta de SQL Server y su contraseña.

   Reemplace `\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>` por el valor de la cuenta de almacenamiento. 

   Reemplace `<STORAGE_CONNECTION_STRING>` por el valor de las claves de acceso.

   Una vez que actualice la consulta siguiente, ejecútela. 

   ```sql
   USE [master]
   EXEC sp_adddistpublisher @publisher = @@ServerName,
                @distribution_db = N'distribution',
                @security_mode = 0,
                @login = N'<SQL_USER>',
                @password = N'<PASSWORD>',
                @working_directory = N'\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>',
                @storage_connection_string = N'<STORAGE_CONNECTION_STRING>';
   GO
   ```

1. Configure el publicador para replicación. 

    En la consulta siguiente, reemplace `<Publishing_DB>` por el nombre de la base de datos del publicador.

    Reemplace `<Publication_Name>` por el nombre de la publicación.

    Reemplace `<SQL_USER>` y `<PASSWORD>` por la cuenta de SQL Server y su contraseña.

    Una vez que actualice la consulta, ejecútela para crear la publicación.

   ```sql
   USE [<Publishing_DB>]
   EXEC sp_replicationdboption @dbname = N'<Publishing_DB>',
                @optname = N'publish',
                @value = N'true';

   EXEC sp_addpublication @publication = N'<Publication_Name>',
                @status = N'active';

   EXEC sp_changelogreader_agent @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>';

   EXEC sp_addpublication_snapshot @publication = N'<Publication_Name>',
                @frequency_type = 1,
                @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>'
   ```

1. Agregue el artículo, la suscripción y el agente de suscripción de inserción. 

   Para agregar estos objetos, actualice el script siguiente.

   Reemplace `<Object_Name>` por el nombre del objeto de publicación.

   Reemplace `<Object_Schema>` por el nombre del esquema de origen. 

   Reemplace los demás parámetros en corchetes angulares `<>` para que coincidan con los valores de los scripts anteriores. 

   ```sql
   EXEC sp_addarticle @publication = N'<Publication_Name>',
                @type = N'logbased',
                @article = N'<Object_Name>',
                @source_object = N'<Object_Name>',
                @source_owner = N'<Object_Schema>'

   EXEC sp_addsubscription @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @destination_db = N'<Subscribing_DB>',
                @subscription_type = N'Push'

   EXEC sp_addpushsubscription_agent @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @subscriber_db = N'<Subscribing_DB>',
                @subscriber_security_mode = 0,
                @subscriber_login = N'<SQL_USER>',
                @subscriber_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>', 
                @job_password = N'<PASSWORD>'
   GO
   ```

## <a name="limitations"></a>Limitaciones

No se admiten las características siguientes:

- Suscripciones actualizables

- Replicación geográfica activa

## <a name="see-also"></a>Ver también

- [¿Qué es Instancia administrada de SQL Database (versión preliminar)?](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
