---
title: "Activar las características de integración del servidor de informes y Power View en SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 462f77f127f9add617ad95e8d5bd21830c87dd6e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Activar las características de integración del servidor de informes y Power View en SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Las características de colección de sitios de Reporting Services se activan de forma predeterminada una vez se ha instalado el complemento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para productos de SharePoint. En algunas situaciones, tendrá que activar las características de forma manual.  

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

 Si instala el complemento de Reporting Services para productos de SharePoint 2010 después de instalar el producto de SharePoint, las características de integración del servidor de informes y de Power View se activarán únicamente para colecciones de sitios raíz. Para las demás colecciones de sitios, debe activar manualmente las características. Por ejemplo, si tiene una colección de sitios de **http://[nombre de mi servidor]/sites/[nombre de la colección de sitios]** debe activar manualmente las características de la colección de sitios de Reporting Services.  
  
 Cuando no hay colecciones de sitios raíz, el complemento de Reporting Services registrará un mensaje similar al siguiente.  
  
 “La aplicación web 80 de Sharepoint no tiene colección de sitios raíz”  
  
 El mensaje se encuentra en el registro de instalación del complemento, "RS_SP_#.log", donde # es un número que se incrementa. El archivo de registro se encuentra en la carpeta Temp de los usuarios actuales, por ejemplo: C:\Usuarios\\[nombre del usuario]\AppData\Local\Temp. Para más información sobre cómo registrar opciones con el complemento, vea [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>Activar las características de colección de sitios de integración del servidor de informes y de Power View
  
1.  Abra el explorador en el sitio donde quiere que estén activas las características de Reporting Services.  
  
2.  Haga clic en **Acciones del sitio**.  
  
3.  Haga clic en **Configuración del sitio**.  
  
4.  Haga clic en **Características de la colección de sitios** en el grupo Administración de la colección de sitios.  
  
5.  Busque **Característica de integración del servidor de informes** o **Característica de integración de Power View** en la lista.  
  
6.  Haga clic en **Activar**.  
  
 Para desactivar las características, puede usar el mismo procedimiento y hacer clic en **Desactivar** en lugar de en **Activar**.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Activar o desactivar la característica de colección de sitios de Administración central de Reporting Services
  
1.  Abra el explorador en Administración central de SharePoint.  
  
2.  Haga clic en **Acciones del sitio**.  
  
3.  Haga clic en **Configuración del sitio**.  
  
4.  Haga clic en **Características de la colección de sitios** en el grupo Administración de la colección de sitios.  
  
5.  Busque la **Característica de administración central del servidor de informes** en la lista.  
  
6.  Haga clic en **Activar**.  
  
 Para desactivar la característica, puede usar el mismo procedimiento y hacer clic en **Desactivar** en lugar de en **Activar**.  
  
## <a name="next-steps"></a>Pasos siguientes

Una vez activada la característica, puede continuar con la integración del servidor.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
