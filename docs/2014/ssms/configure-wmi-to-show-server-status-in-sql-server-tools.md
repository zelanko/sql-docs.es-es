---
title: Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0b0b8236187698917dddd3ca98830add6c3fde9
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129025"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server
  En este tema se describe cómo configurar WMI para mostrar el estado del servidor en herramientas de SQL Server en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Al conectarse a los servidores, los componentes Servidores registrados y Explorador de objetos de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], así como el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usan Instrumental de administración de Windows (WMI) para obtener el estado de los servicios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) y el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER). Para mostrar el estado del servicio, el usuario debe tener derechos de acceso remoto al objeto WMI. El servidor debe tener WMI instalado para configurar este permiso.  
  
##  <a name="SSMSProcedure"></a> Para configurar los permisos de WMI  
  
1.  En el menú **Inicio** del servidor remoto, haga clic en **Ejecutar**.  
  
2.  En el **abierto** cuadro, escriba `wmimgmt.msc`y, a continuación, haga clic en **Aceptar**.  
  
3.  En el programa **Windows Management Infrastructure** , haga clic con el botón derecho en **Control WMI (Local)** y, luego, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de Control WMI (Local)** , en la pestaña **Seguridad** , expanda **Raíz**y, luego, haga clic en **CIMV2**.  
  
5.  Haga clic en **Seguridad** para abrir el cuadro de diálogo **Seguridad para ROOT\CIMV2** .  
  
6.  Agregue un grupo o un usuario al cuadro **Nombres de grupos o usuarios** y selecciónelo.  
  
7.  En el **permisos para**_\<usuario o grupo >_ cuadro, seleccione el **permitir** columna, para el **llamada remota habilitada** permiso , para los usuarios que desee en forma remota detectan el estado del servicio.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar, detener o pausar el servicio del Agente SQL Server](agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
