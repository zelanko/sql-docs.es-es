---
title: Administración automatizada en una empresa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8df3e34c2c70c81f9710ade0d6855446b930fb50
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011798"
---
# <a name="automated-administration-across-an-enterprise"></a>Administración automatizada en una empresa
   Automatizar la administración en varias instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se conoce como *administración multiservidor*. Utilice la administración multiservidor para realizar lo siguiente:  
  
-   Administrar dos o más servidores.  
  
-   Programar flujos de información entre servidores corporativos para almacenar datos.  
  
> [!NOTE]  
>  Como parte de los esfuerzos continuados de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para reducir el costo total de propiedad, [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introdujo dos características: un método para administrar servidores que se denomina Administración basada en directivas y consultas multiservidor que utilizan servidores de configuración y grupos de servidores. Estas características se pueden utilizar con, o en lugar de, algunas de las características que se describen en este tema. Para obtener más información, vea [administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) y [administrar varios servidores mediante servidores de administración central](../../relational-databases/administer-multiple-servers-using-central-management-servers.md).  
  
 Para aprovechar la administración multiservidor, debe tener un servidor maestro y un servidor de destino, como mínimo. Los servidores maestros distribuyen trabajos a los servidores de destino y reciben eventos de éstos. Asimismo, almacenan la copia central de definiciones de trabajos ejecutados en servidores de destino. Los servidores de destino se conectan periódicamente al servidor maestro para actualizar la programación de los trabajos. Si hay un nuevo trabajo en el servidor maestro, el servidor de destino descarga el trabajo. Cuando el servidor de destino ha realizado el trabajo, se vuelve a conectar al servidor maestro e informa del estado del trabajo.  
  
 En la siguiente ilustración se muestra la relación entre los servidores maestros y de destino:  
  
 ![Configuración de administración multiservidor](../../database-engine/media/multisvr.gif "Configuración de administración multiservidor")  
  
 Si administra servidores de departamento en una gran organización, puede definir:  
  
-   Un trabajo de copia de seguridad con pasos del trabajo.  
  
-   Los operadores a los que se notificará en caso de error de copia de seguridad.  
  
-   Un programa de ejecución para el trabajo de copia de seguridad.  
  
 Escriba este trabajo de copia de seguridad una vez en el servidor maestro y luego dé de alta el servidor de cada departamento como servidor de destino. Desde la fecha de alta, todos los servidores de departamento ejecutan el mismo trabajo de copia de seguridad, aunque el trabajo se haya definido solo una vez.  
  
> [!NOTE]  
>  Las características de la administración multiservidor están destinadas a miembros del rol sysadmin. Sin embargo, los miembros del rol sysadmin del servidor de destino no pueden modificar las operaciones que ha realizado el servidor maestro en el servidor de destino. Esta medida de seguridad evita que se eliminen accidentalmente pasos del trabajo y que se interrumpan operaciones en el servidor de destino.  
  
## <a name="in-this-section"></a>En esta sección  
 [Crear un entorno multiservidor](create-a-multiserver-environment.md)  
 Contiene información sobre cómo crear y administrar servidores maestros y de destino.  
  
 [Elegir la cuenta correcta del servicio del Agente SQL Server para entornos multiservidor](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
 Contiene información acerca de cómo usar cuentas de Windows no administrativas o la cuenta Sistema local para que el servicio del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueda afectar a entornos multiservidor.  
  
 [Establecer opciones de cifrado en servidores de destino](set-encryption-options-on-target-servers.md)  
 Contiene información acerca de cómo establecer la subclave del Registro del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] MsxEncryptChannelOptions en los servidores de destino.  
  
 [Administrar trabajos en una empresa](manage-jobs-across-an-enterprise.md)  
 Contiene información sobre cómo comprobar el estado del trabajo, cómo cambiar servidores de destino de trabajos, cómo sincronizar los relojes de los servidores de destino y cómo sondear el estado del trabajo actual de los servidores maestros.  
  
 [Solucionar problemas de trabajos multiservidor que usan servidores proxy](troubleshoot-multiserver-jobs-that-use-proxies.md)  
 Contiene información acerca de cómo solucionar problemas de trabajos multiservidor que usan servidores proxy en los que se producen errores.  
  
 [Sondear servidores](poll-servers.md)  
 Contiene información sobre cómo conseguir implícita y explícitamente que los servidores de destino sondeen a los servidores maestros para sincronizar la información de los trabajos.  
  
 [Administrar eventos](manage-events.md)  
 Contiene información sobre el reenvío de eventos desde servidores de destino a servidores maestros.  
  
 [Optimizar la administración automatizada en una empresa](tune-automated-administration-across-an-enterprise.md)  
 Contiene información sobre cómo una administración automatizada en un entorno multiservidor se aprovecha de las características de optimización automática de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Registrar servidores](../register-servers/register-servers.md)   
 [sp_add_targetservergroup &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql)   
 [sp_delete_targetserver &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql)   
 [sp_delete_targetservergroup &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql)   
 [sp_help_downloadlist &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql)   
 [sp_help_jobserver &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql)   
 [sp_help_targetservergroup &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)   
 [sp_resync_targetserver &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)   
 [sp_update_targetservergroup &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql)   
 [dbo.sysjobservers &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobservers-transact-sql)   
 [Inicios de sesión desys.sys&#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)   
 [dbo.systargetservers &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-systargetservers-transact-sql)  
  
  
