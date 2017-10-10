---
title: "Activar las características de integración de Power View en SharePoint y el servidor de informes | Documentos de Microsoft"
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e97378914a59fab938fc3e4c7926847effcffc94
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Activar las características de integración de Power View en SharePoint y el servidor de informes

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Las características de colección de informes de Reporting Services se activan de forma predeterminada después de instalar la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] complemento para productos de SharePoint. En algunas situaciones, debe activar manualmente las características.  

> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

 Si instala el complemento de Reporting Services para productos de SharePoint 2010 después de la instalación del producto de SharePoint, a continuación, la característica de integración del servidor de informes y la característica de integración de Power View solo se activarán para colecciones de sitios raíz. Para otras colecciones de sitios, debe activar manualmente las características. Por ejemplo, si tiene una colección de sitios **http://[my nombre de servidor] / Sites / [nombre de colección de sitios]** tiene que activar manualmente las características de colección de informes de Reporting Services.  
  
 Cuando no hay ninguna colección de sitios raíz, el complemento de Reporting Services registrará un mensaje similar al siguiente.  
  
 “La aplicación web 80 de Sharepoint no tiene colección de sitios raíz”  
  
 El mensaje se encuentra en el registro de instalación del complemento, denominado "RS_SP_ # .log", donde # es un número que se incrementa. El archivo de registro se encuentra en la carpeta actual de Temp de los usuarios, por ejemplo C:\Users\\[nombre de usuario] \AppData\Local\Temp. Para más información sobre cómo registrar opciones con el complemento, vea [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>Activar las características de colección de sitios de integración servidor de informes y Power View
  
1.  Abra el explorador en el sitio donde desea que las características de Reporting Services activa.  
  
2.  Haga clic en **Acciones del sitio**.  
  
3.  Haga clic en **Configuración del sitio**.  
  
4.  Haga clic en **Características de la colección de sitios** en el grupo Administración de la colección de sitios.  
  
5.  Busque **Característica de integración del servidor de informes** o **Característica de integración de Power View** en la lista.  
  
6.  Haga clic en **Activar**.  
  
 Para desactivar las características, puede usar el mismo procedimiento y hacer clic en **Desactivar** en lugar de en **Activar**.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Activar o característica de colección de sitio de administración central de desactivar Reporting Services
  
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
