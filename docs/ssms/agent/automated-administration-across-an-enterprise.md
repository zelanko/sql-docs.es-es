---
title: Administración automatizada en una empresa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 13403b3941f1d5c14779b0230ede0d1d85a02f11
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "42776662"
---
# <a name="automated-administration-across-an-enterprise"></a>Administración automatizada en una empresa
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Automatizar la administración en varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conoce con el nombre de *administración multiservidor*. Utilice la administración multiservidor para realizar lo siguiente:  
  
-   Administrar dos o más servidores.  
  
-   Programar flujos de información entre servidores corporativos para almacenar datos.  
  
Para aprovechar la administración multiservidor, debe tener un servidor maestro y un servidor de destino, como mínimo. Los servidores maestros distribuyen trabajos a los servidores de destino y reciben eventos de éstos. Asimismo, almacenan la copia central de definiciones de trabajos ejecutados en servidores de destino. Los servidores de destino se conectan periódicamente al servidor maestro para actualizar la programación de los trabajos. Si hay un nuevo trabajo en el servidor maestro, el servidor de destino descarga el trabajo. Cuando el servidor de destino ha realizado el trabajo, se vuelve a conectar al servidor maestro e informa del estado del trabajo. Tenga en cuenta que su definición de trabajo debe ser la misma cuando realiza cualquier actividad relacionada con la base de datos.  
  
En la siguiente ilustración se muestra la relación entre los servidores maestros y de destino:  
  
![Configuración de administración multiservidor](../../ssms/agent/media/multisvr.gif "Configuración de administración multiservidor")  
  
Si administra servidores de departamento en una gran organización, puede definir:  
  
-   Un trabajo de copia de seguridad con pasos del trabajo.  
  
-   Los operadores a los que se notificará en caso de error de copia de seguridad.  
  
-   Un programa de ejecución para el trabajo de copia de seguridad.  
  
Escriba este trabajo de copia de seguridad una vez en el servidor maestro y luego dé de alta el servidor de cada departamento como servidor de destino. Desde la fecha de alta, todos los servidores de departamento ejecutan el mismo trabajo de copia de seguridad, aunque el trabajo se haya definido solo una vez.  
  
> [!NOTE]  
> Las características de la administración multiservidor están destinadas a miembros del rol sysadmin. Sin embargo, los miembros del rol sysadmin del servidor de destino no pueden modificar las operaciones que ha realizado el servidor maestro en el servidor de destino. Esta medida de seguridad evita que se eliminen accidentalmente pasos del trabajo y que se interrumpan operaciones en el servidor de destino.  
  
## <a name="in-this-section"></a>En esta sección  
[Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)  
Contiene información sobre cómo crear y administrar servidores maestros y de destino.  
  
[Elegir la cuenta correcta del servicio del Agente SQL Server para entornos multiservidor](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
Contiene información acerca de cómo usar cuentas de Windows no administrativas o la cuenta Sistema local para que el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda afectar a entornos multiservidor.  
  
[Establecer opciones de cifrado en servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md)  
Contiene información acerca de cómo establecer la subclave del Registro del Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MsxEncryptChannelOptions en los servidores de destino.  
  
[Administrar trabajos en una empresa](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
Contiene información sobre cómo comprobar el estado del trabajo, cómo cambiar servidores de destino de trabajos, cómo sincronizar los relojes de los servidores de destino y cómo sondear el estado del trabajo actual de los servidores maestros.  
  
[Solucionar problemas de trabajos multiservidor que usan servidores proxy](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
Contiene información acerca de cómo solucionar problemas de trabajos multiservidor que usan servidores proxy en los que se producen errores.  
  
[Sondear servidores](../../ssms/agent/poll-servers.md)  
Contiene información sobre cómo conseguir implícita y explícitamente que los servidores de destino sondeen a los servidores maestros para sincronizar la información de los trabajos.  
  
[Administrar eventos](../../ssms/agent/manage-events.md)  
Contiene información sobre el reenvío de eventos desde servidores de destino a servidores maestros.  
  
[Optimizar la administración automatizada en una empresa](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
Contiene información sobre cómo una administración automatizada en un entorno multiservidor se aprovecha de las características de optimización automática de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Ver también  
[Temas de compatibilidad con versiones anteriores para instalar el motor de base de datos de SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
[Registrar servidores](../register-servers/register-servers.md)  
[sp_add_targetservergroup](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)  
[sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)  
[sp_delete_targetservergroup](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)  
[sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)  
[sp_help_jobserver](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)  
[sp_help_targetservergroup](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)  
[sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
[sp_update_targetservergroup](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
[sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
[syslogins](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
[systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
  
