---
title: Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 25ce9dc1b4b9b349a2011055cc574e83bcb92254
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42774225"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
En este tema se describe cómo configurar WMI para mostrar el estado del servidor en herramientas de SQL Server en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Al conectarse a los servidores, los componentes Servidores registrados y Explorador de objetos de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], así como el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usan Instrumental de administración de Windows (WMI) para obtener el estado de los servicios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) y el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER). Para mostrar el estado del servicio, el usuario debe tener derechos de acceso remoto al objeto WMI. El servidor debe tener WMI instalado para configurar este permiso.  
  
## <a name="SSMSProcedure"></a>Para configurar el permiso WMI  
  
1.  En el menú **Inicio** del servidor remoto, haga clic en **Ejecutar**.  
  
2.  En el cuadro **Abrir** , escriba **wmimgmt.msc**y, a continuación, haga clic en **Aceptar**.  
  
3.  En el programa **Windows Management Infrastructure** , haga clic con el botón derecho en **Control WMI (Local)** y, luego, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de Control WMI (Local)** , en la pestaña **Seguridad** , expanda **Raíz**y, luego, haga clic en **CIMV2**.  
  
5.  Haga clic en **Seguridad** para abrir el cuadro de diálogo **Seguridad para ROOT\CIMV2** .  
  
6.  Agregue un grupo o un usuario al cuadro **Nombres de grupos o usuarios** y selecciónelo.  
  
7.  En el cuadro **Permisos para***<group or user>*, seleccione la columna **Permitir**, para el permiso **Llamada remota habilitada**, para los usuarios que desee que detecten remotamente el estado del servicio.  
  
## <a name="see-also"></a>Ver también  
[Iniciar, detener o pausar el servicio del Agente SQL Server](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
