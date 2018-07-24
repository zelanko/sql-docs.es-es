---
title: Activar la característica de sincronización de archivos del servidor de informes en SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 0ee22d38c2b15a8b2527d2c83be447133aba82f0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052113"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint"></a>Activar la característica de sincronización de archivos del servidor de informes en SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

La característica Sincronizar archivo del Servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza los controladores de eventos de SharePoint para sincronizar el catálogo del servidor de informes con los elementos de las bibliotecas de documentos. Esta característica es beneficiosa cuando los usuarios cargan con frecuencia los elementos de informe publicados directamente en las bibliotecas de documentos de SharePoint. Si la característica de sincronización de archivos no está activada, el contenido se seguirá sincronizando, pero no con tanta frecuencia.

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.
  
 La característica de sincronización de archivos se puede activar en Administración del sitio de SharePoint después de instalar el Complemento [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para productos de SharePoint.  
  
 Esta característica se puede activar y desactivar manualmente en cada sitio pero no en el nivel de la colección de sitios.  
  
## <a name="prerequisites"></a>Prerequisites

 Debe estar instalado el Complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint. Si el complemento no está instalado, la característica de sincronización de archivos no estará visible en la lista de características de sitio.  
  
 Para comprobar la instalación, vea la lista de aplicaciones instaladas en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] Panel de control **de**Windows. Si el Complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está instalado, siga las instrucciones de este tema para activar la característica de sincronización del servidor de informes.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Para activar o desactivar la característica de sincronización de archivos de Reporting Services en un sitio
  
1.  En la página principal del sitio, haga clic en el menú **Acciones de sitio** y en **Configuración del sitio**.  
  
2.  En **Acciones de sitio** haga clic en **Administrar las características del sitio**.  
  
3.  Busque **Sincronizar archivo del Servidor de informes** en la lista.  
  
4.  Haga clic en **Activar**.  

> [!NOTE]
> Para desactivar la característica de sincronización de archivos del servidor de informes, puede usar el mismo procedimiento, pero tiene que hacer clic en **Desactivar**.

## <a name="see-also"></a>Vea también

 [Solucionar problemas de elementos de informe (Generador de informes y SSRS)](http://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Activar las características de integración del servidor de informes y Power View en SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
