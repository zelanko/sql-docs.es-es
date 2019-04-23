---
title: Activar la característica de sincronización de archivos del servidor de informes en Administración Central de SharePoint | Microsoft Docs
ms.prod: reporting-services-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: b56960b23370de3803f475c02aaee3b98ae491e4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59963967"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint

La característica Sincronizar archivo del Servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza los controladores de eventos de SharePoint para sincronizar el catálogo del servidor de informes con los elementos de las bibliotecas de documentos. Esta característica es beneficiosa cuando los usuarios cargan con frecuencia los elementos de informe publicados directamente en las bibliotecas de documentos de SharePoint. Si no está activada la característica de sincronización de archivos, contenido seguirá sincronizando, pero no con tanta frecuencia.  
  
La característica de sincronización de archivos se puede activar en Administración del sitio de SharePoint después de instalar el Complemento [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] para productos de SharePoint.  
  
Esta característica se puede activar y desactivar manualmente en cada sitio pero no en el nivel de la colección de sitios.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe estar instalado el Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para SharePoint. Si no está instalado el complemento, la característica de sincronización de archivos no será visible en la lista de características del sitio.  
  
 Para comprobar la instalación, vea la lista de aplicaciones instaladas en el [!INCLUDE[msCoName](../includes/msconame-md.md)] Panel de control **de**Windows. Si el Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] está instalado, siga las instrucciones de este tema para activar la característica de sincronización del servidor de informes.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Activar o desactivar la característica de sincronización de archivos de Reporting Services en un sitio  
  
1.  En la página principal del sitio, haga clic en el **acciones del sitio** menú y haga clic en **configuración del sitio**.  
  
2.  En el **acciones del sitio**, haga clic en **administrar las características del sitio**.  
  
3.  Busque **Sincronizar archivo del Servidor de informes** en la lista.  
  
4.  Haga clic en **Activar**.  
  
> [!NOTE]  
>  Para desactivar la característica de sincronización de archivos del servidor de informes, puede usar el mismo procedimiento, pero tiene que hacer clic en **Desactivar**.  
  
## <a name="see-also"></a>Vea también  
 [Solucionar problemas de elementos de informe &#40;generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Activar las características de integración del servidor de informes y Power View en SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
