---
title: "Establecer la conexión de SQL Server del servicio del Agente SQL Server | Microsoft Docs"
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
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4129f5324f4b93efb98e9bd437571daa0bc404a1
ms.lasthandoff: 04/11/2017

---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>Establecer la conexión de SQL Server para el servicio del Agente SQL Server (SQL Server Management Studio)
En este tema se describe cómo establecer la conexión entre el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y el [!INCLUDE[ssDE](../../includes/ssde_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. El servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] puede conectarse a una instancia local de SQL Server mediante Autenticación de Windows.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para establecer la conexión de SQL Server para el Agente SQL Server, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si se tiene permiso para usarlo.  
  
-   A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no admite la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Esta opción solo está disponible al administrar una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>Para establecer la conexión a SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que desea configurar con una conexión con el servicio del Agente SQL Server.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server***nombre_servidor* , en **Seleccionar una página**, haga clic en **Conexión**.  
  
4.  En **Conexión de SQL Server**, seleccione **Usar autenticación de Windows** para que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conecte a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssDE](../../includes/ssde_md.md)] mediante la autenticación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows. Las conexiones a las bases de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] y versiones posteriores requieren la autenticación de Windows.  
  

