---
title: Servicios SCM - Configurar una instancia para que se inicie automáticamente | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 34430bf70af547a54402c776b05ac6666bee8b71
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40409435"
---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>Servicios SCM - Configurar una instancia para que se inicie automáticamente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo establecer una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se inicie automáticamente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. Durante la instalación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura normalmente para iniciarse automáticamente. Si esto no se ha hecho, puede modificar la configuración en cualquier momento.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>Para configurar que una instancia de SQL Server se inicie automáticamente  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , escriba SQLServerManager13.msc (para **) en la**página de inicio [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 13 por un número inferior. Al hacer clic en SQLServerManager13.msc, se abre el Administrador de configuración. Para anclar el Administrador de configuración a la página de inicio o a la barra de tareas, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Abrir ubicación del archivo**. En el Explorador de archivos de Windows, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Anclar a Inicio** o **Anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba **SQLServerManager\<versión>.msc** (por ejemplo, **SQLServerManager13.msc**) en el acceso a **Buscar** de **Aplicaciones** y, después, pulse **Entrar**.  
  
2.  En el **Administrador de configuración de SQL Server**, expanda **Servicios**y, a continuación, haga clic en **SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en el nombre de la instancia que quiera iniciar automáticamente y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de \<***nombredeinstancia***> de SQL Server**, establezca **Modo de inicio** en **Automático**.  
  
5.  Haga clic en **Aceptar**y, a continuación, cierre el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Ver también  
 
  [Evitar el inicio automático de una instancia de SQL Server &amp;#40;Administrador de configuración de SQL Server&amp;#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Conectarse a otro equipo &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
