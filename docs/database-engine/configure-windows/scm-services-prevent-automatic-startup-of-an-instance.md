---
title: Servicios SCM - Impedir el inicio automático de una instancia | Microsoft Docs
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
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d2abc9a96023941ad76c2181d0bbba07ddde9d3f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32865200"
---
# <a name="scm-services---prevent-automatic-startup-of-an-instance"></a>Servicios SCM - Impedir el inicio automático de una instancia
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo evitar que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicie automáticamente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se suele configurar para iniciarse automáticamente. Puede cambiar esta configuración estableciendo en manual el modo de inicio de la instancia.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>Para evitar el inicio automático de una instancia de SQL Server  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , escriba SQLServerManager13.msc (para **) en la**página de inicio [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 13 por un número inferior. Al hacer clic en SQLServerManager13.msc, se abre el Administrador de configuración. Para anclar el Administrador de configuración a la página de inicio o a la barra de tareas, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Abrir ubicación del archivo**. En el Explorador de archivos de Windows, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Anclar a Inicio** o **Anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba **SQLServerManager\<versión>.msc** (por ejemplo, **SQLServerManager13.msc**) en el acceso a **Buscar** de **Aplicaciones** y, después, pulse **Entrar**.  
  
2.  En el Administrador de configuración de SQL Server, expanda **Servicios**y haga clic en **SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **MSSQLServer**y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **SQL Server \<Propiedades de ***nombredeinstancia***>**, en la pestaña **Servicio**, en el cuadro **General**, establezca el valor de **Modo de inicio** en **Manual**.  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de \<***nombredeinstancia***> de SQL Server** y, luego, cierre el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
