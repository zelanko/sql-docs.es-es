---
title: Configurar una instancia de SQL Server para que se inicie automáticamente (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 300b539e132b9bda9bc6540c0aadcac6ab9f11a1
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640317"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>Configurar una instancia de SQL Server para que se inicie automáticamente (Administrador de configuración de SQL Server)
  En este tema se describe cómo establecer una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se inicie automáticamente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. Durante la instalación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura normalmente para iniciarse automáticamente. Si esto no se ha hecho, puede modificar la configuración en cualquier momento.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>Para configurar que una instancia de SQL Server se inicie automáticamente  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el **página de inicio**, escriba SQLServerManager12.msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 12 por un número inferior. Haga clic en SQLServerManager12.msc abrir el Administrador de configuración. Para anclar el Administrador de configuración a la página de inicio o la barra de tareas, haga clic en SQLServerManager12.msc y, a continuación, haga clic en **Abrir ubicación del archivo**. En el Explorador de archivos de Windows, haga clic en SQLServerManager12.msc y, a continuación, haga clic en **anclar a inicio** o **anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el **búsqueda** acceso a **aplicaciones**, tipo **SQLServerManager\<versión > .msc** como `SQLServerManager12.msc`y, a continuación, presione **ENTRAR**.  
  
2.  En el **Administrador de configuración de SQL Server**, expanda **Servicios**y, a continuación, haga clic en **SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en el nombre de la instancia que quiera iniciar automáticamente y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de \<***nombredeinstancia***> de SQL Server**, establezca **Modo de inicio** en **Automático**.  
  
5.  Haga clic en **Aceptar**y, a continuación, cierre el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Evitar el inicio automático de una instancia de SQL Server &amp;amp;#40;Administrador de configuración de SQL Server&amp;amp;#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Conectarse a otro equipo &#40;Administrador de configuración de SQL Server&#41;](scm-services-connect-to-another-computer.md)   
 [Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
