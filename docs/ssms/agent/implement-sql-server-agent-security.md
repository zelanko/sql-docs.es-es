---
title: Implementar la seguridad del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f7ff348c6e2d01683c59f30b7f89affe833955c
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65096467"
---
# <a name="implement-sql-server-agent-security"></a>Implementar la seguridad del Agente SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente le permite al administrador de la base de datos ejecutar cada paso de trabajo en un contexto seguro que solo tiene los permisos necesarios para realizar ese paso de trabajo, que está determinado por un servidor proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para establecer los permisos para un paso de trabajo concreto, cree un proxy que disponga de los permisos necesarios y, a continuación, asigne ese proxy al paso de trabajo. Se puede especificar un servidor proxy en más de un paso de trabajo. Para los pasos de trabajo que necesitan los mismos permisos se utiliza el mismo proxy.  
  
En las siguientes secciones se explica el rol de base de datos que debe conceder a los usuarios para que puedan crear o ejecutar trabajos mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="granting-access-to-sql-server-agent"></a>Conceder acceso al Agente SQL Server  
Para utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los usuarios deben ser miembros de uno o más de los siguientes roles fijos de base de datos:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Estos roles se almacenan en la base de datos **msdb** . De manera predeterminada, ningún usuario es miembro de estos roles de base de datos. La pertenencia a estos roles se debe conceder explícitamente. Los usuarios que sean miembros del rol fijo de servidor **sysadmin** tienen acceso total al Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , y no necesitan ser miembros de estos roles fijos de base de datos para utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si un usuario no es miembro de uno de estos roles de base de datos ni del rol **sysadmin** , el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no estará disponible para ellos cuando se conecten con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Los miembros de estos roles de base de datos pueden ver y ejecutar trabajos que les pertenecen, así como crear pasos de trabajos que se ejecuten como una cuenta de proxy existente. Para información sobre los permisos específicos asociados a cada uno de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Los miembros del rol fijo de servidor **sysadmin** tienen permiso para crear, modificar o eliminar cuentas de proxy. Los miembros del rol **sysadmin** tienen permiso para crear pasos de trabajo que no especifiquen un proxy, sino que se ejecuten como la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que es la cuenta que se utiliza para iniciar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="guidelines"></a>Instrucciones  
Siga estas instrucciones para mejorar la seguridad de la implementación del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Crear cuentas de usuario dedicadas especialmente para servidores proxy y utilizarlas únicamente para ejecutar pasos de trabajos.  
  
-   Conceder solo los permisos necesarios a las cuentas de usuarios de proxy. Conceder únicamente los permisos realmente necesarios para ejecutar los pasos de trabajo que están asignados a una cuenta de proxy determinada.  
  
-   No ejecutar el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una cuenta de Microsoft Windows que sea miembro del grupo **Administradores** de Windows.  
  
-   Los servidores proxy son tan seguros como el almacén de credenciales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Si las operaciones de escritura de usuario pueden escribir en el registro de eventos de NT, pueden producir alertas mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   No especifique la cuenta de administración de NT como una cuenta de servicio o una cuenta de proxy.  
  
-   Tenga en cuenta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen acceso a activos entre sí. Los dos servicios comparten un único espacio del proceso y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un administrador del sistema en el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Cuando un servidor de destino (TSX) se registra con un servidor principal (MSX), los administradores del sistema del servidor principal obtienen el control total en la instancia del servidor de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   ACE es una extensión y no se puede invocar a sí misma. La invocación de ACE la realiza Chainer ScenarioEngine.exe, también conocido como Microsoft.SqlServer.Chainer.Setup.exe, u otro proceso de host.  
  
-   ACE depende de las DLL de configuración siguientes pertenecientes a SSDP, ya que ACE llama a las siguientes API de DLL:  
  
    -   **SCO**: Microsoft.SqlServer.Configuration.Sco.dll, incluidas las nuevas validaciones de SCO para las cuentas virtuales  
  
    -   **Clúster**: Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC**: Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **Extensión**: Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>Consulte también  
[Usar los roles predefinidos](../../reporting-services/security/role-definitions-predefined-roles.md)  
[sp_addrolemember (Transact-SQL)](https://msdn.microsoft.com/a583c087-bdb3-46d2-b9e5-3921b3e6d10b)  
[sp_droprolemember (Transact-SQL)](https://msdn.microsoft.com/c2f19ab1-e742-4d56-ba8e-8ffd40cf4925)  
[Seguridad y protección (motor de base de datos)](https://msdn.microsoft.com/dfb39d16-722a-4734-94bb-98e61e014ee7)  
  
