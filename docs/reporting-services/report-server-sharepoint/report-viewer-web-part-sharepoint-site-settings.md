---
title: "Configuración del sitio de SharePoint para el elemento web Visor de informes | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: jt000
ms.author: jasontre
ms.workload: Inactive
ms.openlocfilehash: 0be12b3f74dd2cf4e6d07d3ccc70208d5bd099b8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part"></a>Configuración del sitio de SharePoint para el elemento web Visor de informes

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
|Recopilar los datos de uso|Habilita el envío de información de errores y uso a Microsoft para ayudar a mejorar nuestros productos. Para obtener información acerca de la directiva de recopilación de datos de informes de error, consulte la [Declaración de privacidad de Microsoft SQL Server](https://go.microsoft.com/fwlink/?linkid=860782&clcid=0x409).|  
|Habilitar los metadatos de accesibilidad para los informes|Define la información del dispositivo [ `AccessibleTablix`](../html-device-information-settings.md) para los informes representados.| 
