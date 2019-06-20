---
title: Configurar la replicación de SQL Server en Linux | Microsoft Docs
description: En este artículo se describe cómo configurar la replicación de SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 29c8dd4ef4898796722e1c54eeaff94afef1c0c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705340"
---
# <a name="configure-sql-server-replication-on-linux"></a>Configurar la replicación de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] presenta la replicación de SQL Server para las instancias de SQL Server en Linux.

Para obtener información detallada acerca de la replicación, vea [la documentación de SQL Server replication](../relational-databases/replication/sql-server-replication.md).

Configurar la replicación en Linux con SQL Server Management Studio (SSMS) o procedimientos almacenados de Transact-SQL.

* Para usar SSMS, siga las instrucciones de este artículo.

  Usar SSMS en un sistema operativo de Windows para conectarse a instancias de SQL Server. De fondo e instrucciones, consulte [Use SSMS para administrar SQL Server en Linux](./sql-server-linux-manage-ssms.md).
  
* Para obtener un ejemplo con los procedimientos almacenados, siga el [replicación configurar SQL Server en Linux](sql-server-linux-replication-tutorial-tsql.md) tutorial.

## <a name="prerequisites"></a>Requisitos previos

Antes de configurar los publicadores, distribuidores y suscriptores, deberá completar algunos pasos de configuración para la instancia de SQL Server.

1. Habilitar el Agente SQL Server para usar a los agentes de replicación. En todos los servidores de Linux, ejecute los siguientes comandos en el terminal.

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. Configurar la instancia de SQL Server para la replicación. Para configurar la instancia de SQL Server para la replicación, ejecute `sys.sp_MSrepl_createdatatypemappings` en todas las instancias que participan en la replicación.

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. Cree una carpeta de instantáneas. Los agentes de SQL Server requieren a lectura/escritura a una carpeta de instantáneas. Cree la carpeta de instantáneas en el distribuidor.

  Para crear la carpeta de instantáneas y conceder acceso a `mssql` usuario, ejecute el siguiente comando:

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>Configurar y supervisar la replicación con SQL Server Management Studio (SSMS)

### <a name="configure-the-distributor"></a>Configurar el distribuidor
  
Para configurar el distribuidor: 

1. En SSMS, conéctese a la instancia de SQL Server en el Explorador de objetos.

1. Haga clic en **replicación**y haga clic en **Configurar distribución...** .

1. Siga las instrucciones de la **Asistente para configurar la distribución**.

### <a name="create-publication-and-articles"></a>Crear publicaciones y artículos

Para crear una publicación y los artículos:

1. En el Explorador de objetos, haga clic en **replicación** > **publicaciones locales**> **nueva publicación...** .

1. Siga las instrucciones de la **Asistente para nueva publicación** para configurar el tipo de replicación y los artículos que pertenecen a la publicación.

### <a name="configure-the-subscription"></a>Configurar la suscripción

Para configurar la suscripción en el Explorador de objetos, haga clic en **replicación** > **suscripciones locales**> **nuevas suscripciones...** .

### <a name="monitor-replication-jobs"></a>Supervisión de trabajos de replicación

Utilice al Monitor de replicación para supervisar los trabajos de replicación.

En el Explorador de objetos, haga clic en **replicación**y haga clic en **iniciar Monitor de replicación**.

## <a name="next-steps"></a>Pasos siguientes

[Conceptos: Replicación de SQL Server en Linux](sql-server-linux-replication.md)

[Procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).
