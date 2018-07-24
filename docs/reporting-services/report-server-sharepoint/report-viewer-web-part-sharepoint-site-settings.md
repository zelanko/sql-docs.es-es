---
title: 'Configuración del sitio de SharePoint para el elemento web Visor de informes: SSRS | Microsoft Docs'
ms.custom: ''
ms.date: 10/31/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: jt000
ms.author: jasontre
ms.openlocfilehash: dc85547d213367d3a754e40764fa4335a45c5ce7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38035153"
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part---reporting-services"></a>Configuración del sitio de SharePoint para el elemento web Visor de informes: Reporting Services | Microsoft Docs

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

El elemento web Visor de informes tiene un par de opciones que se pueden configurar. Un administrador del sitio puede habilitar y deshabilitar estas opciones en la página de configuración del sitio de SharePoint. Tenga en cuenta que cada sitio tiene su propia configuración. Además, esta configuración no se restablecerá después de reinstalar el elemento web Visor de informes.

## <a name="accessing-the-site-settings-page"></a>Acceso a la página de configuración del sitio

Para acceder a la configuración del sitio:

1. Desde el sitio de SharePoint, seleccione el icono de **engranaje** de la parte superior izquierda y, a continuación, **Configuración del sitio**.

    ![Configuración del sitio desde el icono de engranaje.](media/sharepoint-site-settings.png)

2. Haga clic en **Configuración del elemento web del Visor de informes** en el grupo de configuración del sitio de **Reporting Services**.

    > [!NOTE]
    > Para acceder a la configuración del sitio, también puede navegar directamente a `<site>/_layouts/15/ReportViewerWebPart/ReportViewerWebPartSettings.aspx`

## <a name="report-viewer-web-part-settings"></a>Configuración del elemento web Visor de informes

|Configuración|Comentarios|  
|-------------|--------------|  
|Recopilar los datos de uso|Habilita el envío de información de errores y uso a Microsoft para ayudar a mejorar nuestros productos. Para obtener información acerca de la directiva de recopilación de datos de informes de error, consulte la [Declaración de privacidad de Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkID=868444).|  
|Habilitar los metadatos de accesibilidad para los informes|Define la información del dispositivo [ `AccessibleTablix`](../html-device-information-settings.md) para los informes representados.| 
