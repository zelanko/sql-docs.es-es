---
title: Impedir el inicio automático de una instancia de SQL Server (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6af4597a4ddf802c80bc98cb38363d59348fa0bb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62810055"
---
# <a name="prevent-automatic-startup-of-an-instance-of-sql-server-sql-server-configuration-manager"></a>Evitar el inicio automático de una instancia de SQL Server (Administrador de configuración de SQL Server)
  En este tema se describe cómo evitar que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicie automáticamente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se suele configurar para iniciarse automáticamente. Puede cambiar esta configuración estableciendo en manual el modo de inicio de la instancia.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>Para evitar el inicio automático de una instancia de SQL Server  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
2.  En Administrador de configuración de SQL Server, expanda **servicios**y, a continuación, haga clic en **SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **MSSQLServer**y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de \<**_nombreDeInstancia_**> de SQL Server**, en el cuadro **Propiedades**, establezca el valor de **Modo de inicio** en **Manual**.  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **SQL Server \< ** _InstanceName_ **> propiedades** y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a continuación, cierre Configuration Manager.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
