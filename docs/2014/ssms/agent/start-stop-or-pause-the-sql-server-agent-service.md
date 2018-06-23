---
title: Iniciar, detener o pausar el servicio del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 79b32b0cd24073bd08fe9b93fcb5ce79cb22b442
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109406"
---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>Start, Stop, or Pause the SQL Server Agent Service
  En este tema se describe cómo iniciar, detener o reiniciar el servicio del Agente SQL Server en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Puede configurar el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se inicie automáticamente cuando se inicie el sistema operativo o puede iniciarlo manualmente cuando necesite completar trabajos. El servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede detener o pausar con el fin de suspender trabajos, notificaciones para los operadores y alertas.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para iniciar, detener o reiniciar el servicio del Agente SQL Server mediante SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar ejecutándose como un servicio. Para obtener más información, consulte [Configure SQL Server Agent](configure-sql-server-agent.md).  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
 Para obtener más información acerca de los permisos de Windows necesarios para la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente, consulte [seleccionar una cuenta para el servicio del Agente SQL Server](select-an-account-for-the-sql-server-agent-service.md) y [configurar cuentas de servicio de Windows y Permisos](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>Para iniciar, detener o reiniciar el servicio del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea administrar el servicio del Agente SQL Server.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, seleccione **Iniciar**, **Detener**o **Reiniciar**.  
  
3.  En el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Sí**.  
  
4.  Cuando se le pregunte si desea realizar la acción, haga clic en **Sí**.  
  
 Para obtener más información, vea:  
  
-   [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
-   [Iniciar automáticamente el Agente SQL Server &#40;SQL Server Management Studio&#41;](autostart-sql-server-agent-sql-server-management-studio.md)  
  
  