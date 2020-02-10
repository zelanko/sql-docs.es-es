---
title: Activar la característica File Sync del servidor de informes en administración central de SharePoint | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 762cf7e67a9983c345b58d2afd1c47da93306bd0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67413144"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint

La característica Sincronizar archivo del Servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza los controladores de eventos de SharePoint para sincronizar el catálogo del servidor de informes con los elementos de las bibliotecas de documentos. Esta característica es beneficiosa cuando los usuarios cargan con frecuencia los elementos de informe publicados directamente en las bibliotecas de documentos de SharePoint. Si la característica de sincronización de archivos no está activada, el contenido se seguirá sincronizando, pero no con tanta frecuencia.  
  
La característica de sincronización de archivos se puede activar en Administración del sitio de SharePoint después de instalar el Complemento [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] para productos de SharePoint.  
  
Esta característica se puede activar y desactivar manualmente en cada sitio pero no en el nivel de la colección de sitios.  
  
## <a name="prerequisites"></a>Prerequisites  
 Debe estar instalado el Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para SharePoint. Si el complemento no está instalado, la característica de sincronización de archivos no estará visible en la lista de características del sitio.  
  
 Para comprobar la instalación, vea la lista de aplicaciones instaladas en el [!INCLUDE[msCoName](../includes/msconame-md.md)] Panel de control **de**Windows. Si el Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] está instalado, siga las instrucciones de este tema para activar la característica de sincronización del servidor de informes.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Activar o desactivar la característica de sincronización de archivos de Reporting Services en un sitio  
  
1.  En la Página principal del sitio, haga clic en el menú **acciones del sitio** y en **configuración del sitio**.  
  
2.  En **acciones del sitio**, haga clic en **administrar características del sitio**.  
  
3.  Busque **Sincronizar archivo del Servidor de informes** en la lista.  
  
4.  Haga clic en **Activar**.  
  
> [!NOTE]  
>  Para desactivar la característica de sincronización de archivos del servidor de informes, puede usar el mismo procedimiento, pero tiene que hacer clic en **Desactivar**.  
  
## <a name="see-also"></a>Consulte también  
 [Solucionar problemas de elementos de informe &#40;Generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Activar las características de integración del servidor de informes y Power View en SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
