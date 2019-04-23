---
title: Iniciar y detener el servicio del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4bd22faaa9d0f3b6ce213c37e20615492b1e95d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968341"
---
# <a name="start-and-stop-the-report-server-service"></a>Iniciar y detener el servicio del servidor de informes
  Un servidor de informes se implementa como un servicio de Windows que contiene el servicio web del servidor de informes, el Administrador de informes y una aplicación de procesamiento en segundo plano. El servicio se debe estar ejecutando si desea usar cualquier funcionalidad del servidor de informes. Al detener el servicio se detienen todas las operaciones del servidor de informes.  
  
 Aunque se detiene el servicio, las solicitudes para el procesamiento de informes y suscripciones programado que deberían haberse producido si se hubiera estado ejecutando el servicio se agregan a la cola. Esto se debe a que los trabajos que se ejecutan con el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crean los eventos. Si desea evitar un trabajo acumulado de operaciones mientras el servicio está apagado, piense también en detener el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Puede usar diversas herramientas para iniciar o detener el servicio del servidor de informes, como son la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la herramienta Servicios que se proporciona en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Si está realizando otras acciones además de iniciar y detener el servicio, como por ejemplo, el cambio de la cuenta de servicio, debe usar la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Si usa otras herramientas para cambiar la cuenta de servicio puede interrumpir la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 No puede pausar ni reanudar el servicio. No existen parámetros de inicio. Aunque no hay dependencias explícitas, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutarse si se admiten suscripciones u operaciones de informe programadas en el servidor de informes.  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>Iniciar o detener el servicio mediante la herramienta de configuración de Reporting Services  
  
1.  Inicie la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese al servidor de informes.  
  
2.  En la página Estado del servidor de informes, haga clic en **Detener** o **Iniciar**.  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>Iniciar o detener el servicio usando Servicios en Herramientas administrativas  
  
-   En Herramientas administrativas, abra Servicios, haga clic con el botón derecho en **SQL Server Reporting Services (MSSQLSERVER)** y haga clic en **Detener** o **Reiniciar**.  
  
 Si se están ejecutando varias instancias o si el servidor de informes se está ejecutando como una instancia con nombre, compruebe que el nombre de instancia que está entre paréntesis corresponde a la instancia del servidor de informes que desea detener o reiniciar.  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>Iniciar o detener el servicio usando el Administrador de configuración de SQL Server  
  
1.  Inicie el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Seleccione Servicios de SQL Server, haga clic con el botón derecho en **SQL Server Reporting Services**y haga clic en **Detener** o en **Reiniciar**.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
