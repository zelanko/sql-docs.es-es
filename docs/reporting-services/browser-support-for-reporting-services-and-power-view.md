---
title: "Compatibilidad del explorador de Reporting Services y Power View | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "mostrar informes"
  - "scripts [Reporting Services], requisitos"
  - "ver informes"
  - "exploradores [Reporting Services]"
  - "exploradores web [Reporting Services], acerca de la compatibilidad de exploradores"
  - "explorar informes [Reporting Services]"
  - "componentes [Reporting Services], exploradores"
  - "exploradores web [Reporting Services]"
ms.assetid: 48a75bbb-0029-4c43-891d-dc8f4fc0ebe1
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 121
---
# Compatibilidad del explorador de Reporting Services y Power View
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

Obtenga información sobre las versiones del explorador que son compatibles para administrar y ver [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], los controles ReportViewer y Power View.
  
 **Se aplica a:** Modo nativo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] | Modo de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
##  <a name="bkmk_webportal"></a> Requisitos del explorador para el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]

Esta es la lista actual de exploradores admitidos para el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)].

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*
- Microsoft Edge (+)
- Microsoft Internet Explorer 10 u 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple iOS**  
*iPhone y iPad con iOS 9*

- Apple Safari (+)

**Google Android**  
*Teléfonos y tabletas con Android 4.4 (KitKat) o versiones posteriores*

- Google Chrome (+)

 **(+)** Última versión publicada  
  
##  <a name="bkmk_reportviewer"></a> Requisitos del explorador para el control web ReportViewer (2015) 
 Esta es la lista actual de exploradores compatibles con el control web ReportViewer (2015). El visor de informes permite ver informes desde el portal web de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y desde bibliotecas de SharePoint.  
  
**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 u 11
- Google Chrome (+)
- Mozilla Firefox (+)

**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
  
 **(+)** Última versión publicada  
  
 Si usa un producto de SharePoint integrado con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vea [Planear la compatibilidad con exploradores en SharePoint 2016](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx).  
  
###  <a name="bkmk_authentication"></a> Requisitos de autenticación  
 Los exploradores admiten esquemas de autenticación concretos que deben ser administrados por el servidor de informes para que la solicitud del cliente tenga éxito. En la tabla siguiente se identifican los tipos de autenticación predeterminados que admite cada explorador que se ejecuta en un sistema operativo Windows.  
  
|**Tipo de explorador**|**Es compatible con**|**Configuración predeterminada del explorador**|**Configuración predeterminada del servidor**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Microsoft Edge** (+)|Negotiate, Kerberos, NTLM, Basic|Negotiate|Sí. La configuración de autenticación predeterminada funciona con Edge.|  
|**Microsoft Internet Explorer**|Negotiate, Kerberos, NTLM, Basic|Negotiate|Sí. La configuración de autenticación predeterminada funciona con Internet Explorer.|  
|**Google Chrome** (+)|Negotiate, NTLM, Basic|Negotiate|Sí. La configuración de autenticación predeterminada funciona con Chrome.|  
|**Mozilla Firefox** (+)|NTLM, Basic|NTLM|Sí. La configuración de autenticación predeterminada funciona con Firefox.|  
|**Apple Safari** (+)|NTLM, Basic|Básico|Sí. La configuración de autenticación predeterminada funciona con Safari.|  
  
 **(+)** Última versión publicada  
  
### Requisitos de script para ver informes  
 Para usar el Visor de informes, configure el explorador para que ejecute scripts.  
  
 Si el scripting no está habilitado, verá un mensaje de error similar al siguiente al abrir un informe:  
  
-   **Su explorador no admite secuencias de comandos o está configurado para no admitir su ejecución. Haga clic aquí para ver este informe sin scripts**.  
  
 Si decide ver el informe prescindiendo de la compatibilidad con script, se representará en formato HTML y no incorporará funcionalidad del Visor de informes, como la barra de herramientas Informes y el mapa del documento.  
  
> [!NOTE]  
>  La barra de herramientas Informes forma parte del componente Visor HTML. De forma predeterminada la barra de herramientas aparece en la parte superior de todos los informes que se representan en una ventana de explorador. El visor de informes proporciona características entre las que se incluyen la posibilidad de buscar información en el informe, desplazarse a una página específica y ajustar el tamaño de página para la visualización. Para obtener más información acerca de la barra de herramientas Informes o el Visor HTML, vea [HTML Viewer and the Report Toolbar](../reporting-services/html-viewer-and-the-report-toolbar.md).  
  
##  <a name="bkmk_controls"></a> Compatibilidad del explorador con los controles de servidor web ReportViewer en Visual Studio  
 El control de servidor web ReportViewer se emplea para incrustar funcionalidad de informes en una aplicación web ASP.NET. Los controles se incluyen con Visual Studio y admiten otros exploradores y versiones de explorador que de los demás componentes descritos en este tema. El tipo de explorador utilizado para ver la aplicación determina el tipo de funcionalidad de ReportViewer que puede ofrecer en la aplicación. Use la tabla que se facilita en este tema para determinar qué exploradores admitidos están sujetos a las restricciones de la funcionalidad de informes y las plataformas admitidas.  
  
 Use un explorador que tenga habilitada la compatibilidad con scripts. Si el explorador no puede ejecutar scripts, no podrá ver el informe.  
  
**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Edge (+)
- Microsoft Internet Explorer 10 u 11
- Google Chrome (+)
- Mozilla Firefox (+)
  
 **(+)** Última versión publicada  
  
##  <a name="bkmk_powerview"></a> Compatibilidad con exploradores para Power View  

**Microsoft Windows**  
*Windows 7, 8.1, 10; Windows Server 2008 R2, 2012, 2012 R2*

- Microsoft Internet Explorer 10 u 11
- Mozilla Firefox (+)
  
**Apple OS X**  
*OS X 10.9-10.11*

- Apple Safari (+)
  
 **(+)** Última versión publicada  
  
 Para más información sobre la compatibilidad con exploradores de SharePoint 2016, vea [Planear la compatibilidad con exploradores en SharePoint 2013](http://technet.microsoft.com//library/cc263526\(v=office.16\).aspx).  
  
## Vea también  
[Buscar y ver informes en el portal web &#40;generador de informes y SSRS&#41;](http://msdn.microsoft.com/es-es/8556807e-f2e2-4a7b-bb1b-ac5ea1872e51)  
[Herramientas de Reporting Services](../reporting-services/tools/reporting-services-tools.md)  
[Portal web (modo nativo de SSRS)](http://msdn.microsoft.com/es-es/7349e626-6ed5-4d21-b05f-cf042ad9ad70)  
[Visor HTML y la barra de herramientas del informe](../reporting-services/html-viewer-and-the-report-toolbar.md)  
[Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
