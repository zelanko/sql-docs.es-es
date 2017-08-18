---
title: Iniciar, detener o pausar el servicio del Agente SQL Server | Microsoft Docs
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
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af137c019a7f96769b801d01f882e1d98b0da2ea
ms.contentlocale: es-es
ms.lasthandoff: 08/18/2017

---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>Iniciar, detener o pausar el servicio del Agente SQL Server
En este tema se describe cómo iniciar, detener o reiniciar el servicio del Agente SQL Server en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
Puede configurar el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para que se inicie automáticamente cuando se inicie el sistema operativo o puede iniciarlo manualmente cuando necesite completar trabajos. El servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se puede detener o pausar con el fin de suspender trabajos, notificaciones para los operadores y alertas.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   [Para iniciar, detener o reiniciar el servicio del Agente SQL Server mediante SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe estar ejecutándose como un servicio. Para obtener más información, consulte [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md).  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si se tiene permiso para usarlo.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>Para iniciar, detener o reiniciar el servicio del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea administrar el servicio del Agente SQL Server.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, seleccione **Iniciar**, **Detener**o **Reiniciar**.  
  
3.  En el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Sí**.  
  
4.  Cuando se le pregunte si desea realizar la acción, haga clic en **Sí**.  
  
Para obtener más información, vea:  
  
-   [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](http://msdn.microsoft.com/en-us/32660a02-e5a1-411a-9e57-7066ca459df6)  
  
-   [Iniciar automáticamente el Agente SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/agent/autostart-sql-server-agent-sql-server-management-studio.md)  
  

