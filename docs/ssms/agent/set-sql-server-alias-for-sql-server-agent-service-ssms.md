---
title: Establecer un alias conexión de SQL Server para el servicio del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ae6b9600ec2fb41439d30ece3a8c2fe8bc08008e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65103228"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo establecer un alias de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de conectarse al [!INCLUDE[ssDE](../../includes/ssde_md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. De manera predeterminada, el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de canalizaciones con nombre, mediante nombres de servidores dinámicos que no requieren ninguna configuración adicional del cliente. Solo es necesario configurar un alias de conexión de servidor si no se utiliza el transporte de red predeterminado o si se va a conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la escucha en una canalización con nombre alternativa.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   [Para establecer un alias de SQL Server para el servicio del Agente SQL Server utilizando SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no funcionará correctamente si no se selecciona un alias que haga referencia a la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Para establecer un alias de SQL Server para servicio del Agente SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] y expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server**_nombre\_servidor_, en **Seleccionar una página**, seleccione **Conexión**, y  
  
4.  En el cuadro de **Servidor de host local del alias** , escriba el alias de servidor al que debe conectarse el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Haga clic en **Aceptar**.  
  
