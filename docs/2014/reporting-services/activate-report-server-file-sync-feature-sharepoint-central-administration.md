---
title: Activar la característica de sincronización de archivos del servidor de informes en Administración Central de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8dcdfaf16f4e279ed39c46dab7d486f517854b52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088415"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint
  La característica Sincronizar archivo del Servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza los controladores de eventos de SharePoint para sincronizar el catálogo del servidor de informes con los elementos de las bibliotecas de documentos. Esta característica es beneficiosa cuando los usuarios cargan con frecuencia los elementos de informe publicados directamente en las bibliotecas de documentos de SharePoint. Si la característica de sincronización de archivos no está activada, el contenido se seguirá sincronizando, pero no con tanta frecuencia.  
  
 La característica de File Sync se puede activar en administración del sitio de SharePoint después de instalar el [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] complemento para productos de SharePoint.  
  
 Esta característica se puede activar y desactivar manualmente en cada sitio pero no en el nivel de la colección de sitios.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe estar instalado el Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para SharePoint. Si el complemento no está instalado, la característica de sincronización de archivos no estará visible en la lista de características de sitio.  
  
 Para comprobar la instalación, vea la lista de aplicaciones instaladas en [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows **Panel de Control**. Si el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] complemento está instalado, siga las instrucciones de este tema para activar la característica de sincronización de archivos del servidor de informes.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Activar o desactivar la característica de sincronización de archivos de Reporting Services en un sitio  
  
1.  En la página principal del sitio, haga clic en el menú **Acciones de sitio** y en **Configuración del sitio**.  
  
2.  En **Acciones de sitio** haga clic en **Administrar las características del sitio**.  
  
3.  Busque **Sincronizar archivo del Servidor de informes** en la lista.  
  
4.  Haga clic en **Activar**.  
  
> [!NOTE]  
>  Para desactivar la característica de sincronización de archivos del servidor de informes, puede usar el mismo procedimiento, pero tiene que hacer clic en **Desactivar**.  
  
## <a name="see-also"></a>Vea también  
 [Solucionar problemas de elementos de informe &#40;generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Activar el servidor de informes y Power View Integration Features in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
