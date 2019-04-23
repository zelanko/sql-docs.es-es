---
title: Informes en modo local frente al Modo conectado en el Visor de informes (Reporting Services en modo de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a230a9bb-6046-401f-b5e5-53ff6edf2264
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0eed8032957a3741d7c1804d21cd08b72ef87657
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59939881"
---
# <a name="local-mode-vs-connected-mode-reports-in-the-report-viewer-reporting-services-in-sharepoint-mode"></a>Informes en modo local frente al modo local en el Visor de informes (Reporting Services en modo de SharePoint)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] pueden configurarse para ejecutarse en *modo local* o en *modo conectado*, lo que permite aprovechar un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] repo ent server. En su lugar, puede utilizar el Visor de informes para representar los informes de SharePoint directamente cuando la extensión de datos admite los informes en modo local. Este enfoque se denomina *modo local*. En versiones anteriores de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], la granja de servidores de SharePoint tenía que estar conectada a un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] configurado en el modo de SharePoint para que el Visor de informes pudiera representar informes. Este enfoque se denomina *modo remoto* o *modo conectado*.  
  
 En *modo local* no hay ningún servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Es necesario que instale el complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para productos de SharePoint, pero no se necesita el servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Con el modo local, los usuarios pueden ver informes pero no tendrán acceso a características del lado servidor como suscripciones y alertas de datos.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] |  
  
 **En este tema:**  
  
-   [Modo local frente al modo conectado y extensiones admitidas](#bkmk_local_vs_connected)  
  
-   [Configurar el modo local y Servicios de Access con SharePoint 2013](#bkmk_local_mode_sharepoint2013)  
  
-   [Configurar informes en modo local con SharePoint 2010](#bkmk_local_mode_sharepoint2010)  
  
##  <a name="bkmk_local_vs_connected"></a> Modo local frente al modo conectado y extensiones admitidas  
 **Modo local:** Cuando tenga una extensión de datos que admite el modo local, el Visor de informes representa de forma directa los informes de SharePoint. En *modo local* no hay ningún servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Es necesario que instale el complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para productos de SharePoint, pero no se necesita el servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Con el modo local, los usuarios pueden ver informes pero **no** tendrán acceso a características del lado servidor como suscripciones y alertas de datos.  
  
 El**modo conectado**, también llamado *modo remoto* , necesita que haya un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] conectado a una granja de servidores de SharePoint para que el Visor de informes pueda representar informes.  
  
 La siguiente es una lista de las extensiones de procesamiento de datos que admite informes en modo local:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 2010. Para obtener más información sobre servicios de Access, consulte [usar servicios de Access con SQL Reporting Services: Instalar SQL Server 2008 R2 Reporting Services Add-In (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686).  
  
-   Extensión de datos de lista de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint Para más información sobre la extensión de datos de lista de SharePoint, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
 También se puede diseñar extensiones de procesamiento de datos personalizadas que admitan el modo local. Para obtener más información, vea [Implementing a Data Processing Extension](extensions/data-processing/implementing-a-data-processing-extension.md).  
  
 El modo local admite la representación de informes que tienen un origen de datos incrustado o un origen de datos compartido de un archivo .rsds. Sin embargo, no puede administrar el informe ni su origen de datos asociado. Si lo intenta, recibirá un error que indica que esto no se admite en modo local. La administración de los orígenes de datos en el sitio de SharePoint solo se admite en el modo conectado.  
  
> [!NOTE]  
>  Como en las versiones anteriores, no puede incrustar nombres de usuario ni contraseñas en el archivo .rsds.  
  
##  <a name="bkmk_local_mode_sharepoint2013"></a> Configurar el modo local y Servicios de Access con SharePoint 2013  
 Puede configurar una granja de SharePoint 2013 para que admita bases de datos web existentes de Access 2010 y el modo local de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Instalación y configuración de Servicios de Access 2010 para bases de datos web en SharePoint Server 2013](https://technet.microsoft.com/library/ee748653\(office.15\).aspx).  
  
 No es posible crear nuevas bases de datos web de Access para SharePoint 2013. Access 2013 emplea un nuevo tipo de base de datos, *aplicación web de Access* , que se crean en Access, y después usa y comparte con otras personas como una aplicación de SharePoint en un explorador web.  
  
 Para obtener más información, vea lo siguiente.  
  
-   [Novedades de Access 2013](http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx) (http://office.microsoft.com/access-help/what-s-new-in-access-2013-HA102809500.aspx).  
  
-   [Tareas básicas para una aplicación de Access](http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500) (http://office.microsoft.com/access-help/basic-tasks-for-an-access-app-HA102840210.aspx?CTT=5&origin=HA102809500).  
  
##  <a name="bkmk_local_mode_sharepoint2010"></a> Configurar informes en modo local con SharePoint 2010  
 El modo local requiere el estado de sesión de ASP.NET. La instalación de los servicios de acceso habilitará el estado de sesión de ASP.NET. También puede habilitarlo con PowerShell.  
  
1.  Abra el Shell de administración de SharePoint 2010.  
  
2.  Escriba el siguiente comando:  
  
    ```  
    - Enable-SPSessionStateService  
    ```  
  
3.  Cuando se le pida, escriba el nombre de la base de datos.  
  
4.  Restablezca IIS.  
  
 Para obtener más información, consulte [usar servicios de Access con SQL Reporting Services: Instalar SQL Server 2008 R2 Reporting Services Add-In (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=192686) y [Enable-SPSessionStateService](https://technet.microsoft.com/library/ff607857\(v=office.15\).aspx).  
  
## <a name="connected-mode"></a>modo conectado  
 Para obtener la información más reciente sobre el uso de la extensión de ADS con el modo conectado de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vea el artículo sobre cómo el [informe de Servicios de Access en el sitio de SharePoint muestra un error en la extensión de datos "ADS"](https://social.technet.microsoft.com/wiki/contents/articles/25298.access-services-report-in-sharepoint-site-shows-error-in-data-extension-ads.aspx).  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
