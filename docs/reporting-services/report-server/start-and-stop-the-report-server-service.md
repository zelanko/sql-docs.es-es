---
title: Iniciar y detener el servicio del servidor de informes | Microsoft Docs
ms.date: 05/21/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6463dc7e4b17992138a61e6a37277149fccfda68
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "66270200"
---
# <a name="start-and-stop-the-report-server-service"></a>Inicio y detención del servicio del servidor de informes

  Un servidor de informes se implementa como un servicio de Windows que contiene el servicio web del servidor de informes, el portal web y una aplicación de procesamiento en segundo plano. El servicio se debe estar ejecutando si desea usar cualquier funcionalidad del servidor de informes. Al detener el servicio se detienen todas las operaciones del servidor de informes.  
  
 Aunque se detiene el servicio, las solicitudes para el procesamiento de informes y suscripciones programado que deberían haberse producido si se hubiera estado ejecutando el servicio se agregan a la cola. Esto se debe a que los trabajos que se ejecutan con el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crean los eventos. Si desea evitar un trabajo acumulado de operaciones mientras el servicio está apagado, piense también en detener el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Puede usar diversas herramientas para iniciar o detener el servicio del servidor de informes, como son la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la herramienta Servicios que se proporciona en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Si está realizando otras acciones además de iniciar y detener el servicio, como por ejemplo, el cambio de la cuenta de servicio, debe usar la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si usa otras herramientas para cambiar la cuenta de servicio puede interrumpir la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 No puede pausar ni reanudar el servicio. No existen parámetros de inicio. Aunque no hay dependencias explícitas, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutarse si se admiten suscripciones u operaciones de informe programadas en el servidor de informes.  
  
## <a name="use-the-reporting-services-configuration-tool"></a>Uso de la herramienta de configuración de Reporting Services  
  
1. Inicie la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese al servidor de informes.  
  
2. En la página Estado del servidor de informes, seleccione **Detener** o **Iniciar**.  
  
## <a name="use-administrative-tools"></a>Uso de Herramientas administrativas  

- En Herramientas administrativas, abra Servicios, haga clic con el botón derecho en **SQL Server Reporting Services (MSSQLSERVER)** y haga clic en **Detener** o **Reiniciar**.  
  
- Si se están ejecutando varias instancias o si el servidor de informes se está ejecutando como una instancia con nombre, compruebe que el nombre de instancia que está entre paréntesis corresponde a la instancia del servidor de informes que desea detener o reiniciar.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Iniciar, detener o pausar el servicio del Agente SQL Server](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  