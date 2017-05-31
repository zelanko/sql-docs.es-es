---
title: "Administración automatizada en una empresa | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 618e199812a39ec29e032f8371419ec6184c713f
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="automated-administration-across-an-enterprise"></a>Administración automatizada en una empresa
Automatizar la administración en varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conoce con el nombre de *administración multiservidor*. Utilice la administración multiservidor para realizar lo siguiente:  
  
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
Contiene información acerca de cómo usar cuentas de Windows no administrativas o la cuenta Sistema local para que el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] pueda afectar a entornos multiservidor.  
  
[Establecer opciones de cifrado en servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md)  
Contiene información acerca de cómo establecer la subclave del Registro del Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] MsxEncryptChannelOptions en los servidores de destino.  
  
[Administrar trabajos en una empresa](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
Contiene información sobre cómo comprobar el estado del trabajo, cómo cambiar servidores de destino de trabajos, cómo sincronizar los relojes de los servidores de destino y cómo sondear el estado del trabajo actual de los servidores maestros.  
  
[Solucionar problemas de trabajos multiservidor que usan servidores proxy](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
Contiene información acerca de cómo solucionar problemas de trabajos multiservidor que usan servidores proxy en los que se producen errores.  
  
[Sondear servidores](../../ssms/agent/poll-servers.md)  
Contiene información sobre cómo conseguir implícita y explícitamente que los servidores de destino sondeen a los servidores maestros para sincronizar la información de los trabajos.  
  
[Administrar eventos](../../ssms/agent/manage-events.md)  
Contiene información sobre el reenvío de eventos desde servidores de destino a servidores maestros.  
  
[Optimizar la administración automatizada en una empresa](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
Contiene información sobre cómo una administración automatizada en un entorno multiservidor se aprovecha de las características de optimización automática de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Vea también  
[Temas de compatibilidad con versiones anteriores para instalar el motor de base de datos de SQL Server](http://msdn.microsoft.com/en-us/10de5ec6-d3cf-42ef-aa62-1bdf3fbde841)  
[Registrar servidores](http://msdn.microsoft.com/en-us/c2a2513e-fa09-419c-99e7-a12d57c5a0db)  
[sp_add_targetservergroup](http://msdn.microsoft.com/en-us/acb69343-d766-46ff-b771-0c7655c5231a)  
[sp_delete_targetserver](http://msdn.microsoft.com/en-us/cc438701-ad91-419d-9f23-ebc4c548c700)  
[sp_delete_targetservergroup](http://msdn.microsoft.com/en-us/d8dd838e-64aa-419f-9ccb-ff04908cf3e4)  
[sp_help_downloadlist](http://msdn.microsoft.com/en-us/745b265b-86e8-4399-b928-c6969ca1a2c8)  
[sp_help_jobserver](http://msdn.microsoft.com/en-us/57971787-f9f5-4199-9f64-c2b61a308906)  
[sp_help_targetservergroup](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)  
[sp_resync_targetserver](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)  
[sp_update_targetservergroup](http://msdn.microsoft.com/en-us/4ac65ed6-e07e-40e4-a282-13bfd92dfa41)  
[sysjobservers](http://msdn.microsoft.com/en-us/9abcc20f-a421-4591-affb-62674d04575e)  
[syslogins](http://msdn.microsoft.com/en-us/4cb34f17-a4bb-469f-a218-71f074e6308f)  
[systargetservers](http://msdn.microsoft.com/en-us/479d1314-be37-4d19-ac9c-419fc9110e53)  
  

