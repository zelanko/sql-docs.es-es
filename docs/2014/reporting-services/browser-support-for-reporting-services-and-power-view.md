---
title: Planear la compatibilidad del explorador de Reporting Services y Power View (Reporting Services 2014)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: f82cf64ef78280b3c9562ae28afc71d06a03b1da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "76925786"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>Planear la compatibilidad del explorador de Reporting Services y Power View (Reporting Services 2014)
  En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], se puede usar un explorador web para ver informes y ejecutar el Administrador de informes. No todos los exploradores admiten toda la funcionalidad de informes. En este tema se describe la compatibilidad y los requisitos de las características de administración del Administrador de informes, cómo ver informes y los controles del visor de informes en Visual Studio. En el tema también se resume la disponibilidad de características para los exploradores compatibles, los requisitos de autenticación y los requisitos de script.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Modo de SharePoint | [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Modo nativo  
  
 **En este tema:**  
  
- [Escenarios del explorador para Power View](#bkmk_powerview)  
  
- [Requisitos del explorador para el Administrador de informes (modo nativo)](#bkmk_reportmanager)  
  
- [Requisitos del explorador para ver informes](#bkmk_reportviewer)  
  
- [Requisitos de autenticación](#bkmk_authentication)  
  
- [Compatibilidad del explorador con los controles de servidor Web ReportViewer en Visual Studio](#bkmk_controls)  
  
##  <a name="bkmk_powerview"></a>Escenarios del explorador Power View

 La lista de exploradores y versiones de explorador que [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] admite depende del tipo de documento abierto. Los libros de Excel 2013 y los archivos "**. rdlx**" usan distintos componentes.  
  
|Tipo de documento|Entorno|Compatibilidad con exploradores|  
|-------------------|-----------------|---------------------|  
|Informe de Power View (.RDLX)|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] el modo integrado de SharePoint y la aplicación Web de Power View.|Vea [Power View en SharePoint Server y el modo integrado de SharePoint de Reporting Services](#bkmk_powerview_on_SSRS).|  
|Libro de Excel 2013 con hojas de Power View|**SharePoint Server:** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] en Excel Services.<br /><br /> **SharePoint Online (Office 365):** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] en la aplicación Web de Excel.|Vea [Power View en Excel Services o Excel Web App en SharePoint Online](#bkmk_powerview_on_ExcelServices).|  
  
###  <a name="bkmk_powerview_on_SSRS"></a>Power View en el servidor de SharePoint y Reporting Services el modo integrado de SharePoint  
 En la tabla siguiente se resumen las versiones admitidas del explorador para [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] cuando un usuario abre un informe de Power View (.RDLX) en una granja de servidores de SharePoint que tiene una aplicación de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y el complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para SharePoint instalado y configurado.  
  
- La tabla se aplica a SharePoint 2010 y SharePoint 2013.  
  
- Para obtener más información acerca de la compatibilidad con exploradores de SharePoint 2013, consulte planear lahttps://technet.microsoft.com/library/cc263526(office.15).aspx) [compatibilidad con exploradores en SharePoint 2013](https://technet.microsoft.com//library/cc263526\(office.15\).aspx) (.  
  
- Para obtener más información acerca de la compatibilidad con exploradores de SharePoint 2010, vea [planear la compatibilidad con exploradores (SharePoint Server 2010)](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) (https://technet.microsoft.com/library/cc263526(office.14).aspx).  
  
|**Browser**|**Windows 8 y 8.1**|**Windows 7**|**Windows Server 2012 y 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10,6-10,9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (para el escritorio)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|  
|**Internet Explorer 10 (para el escritorio)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|  
|**Internet Explorer 9**|No compatible|32 bits, 64 bits|No compatible|32 bits, 64 bits|32 bits, 64 bits|No compatible|  
|**Internet Explorer 8**|No compatible|32 bits, 64 bits|No compatible|32 bits, 64 bits|32 bits, 64 bits|No compatible|  
|**Mozilla Firefox (la última versión publicada)**|32 bits|32 bits|32 bits|32 bits|32 bits|No compatible|  
|**Apple Safari (versión más reciente publicada)**|No compatible|No compatible|No compatible|No compatible|No compatible|32 bits, 64 bits|  
  
> [!NOTE]  
> '32 bits' hace referencia al explorador, no al sistema operativo. Puede utilizar Internet Explorer 9 de 32 bits en Windows 7 de 64 bits, por ejemplo.  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Característica de exploración de InPrivate en Internet Explorer

 
  [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] no admite la característica de exploración de InPrivate en [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 e Internet Explorer 9. Para obtener más información acerca de la exploración de InPrivate, vea [¿Qué es la exploración de InPrivate?](https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="bkmk_powerview_on_ExcelServices"></a>Power View en Excel Services o Excel Web App en SharePoint Online

 En la tabla siguiente se resumen las versiones de explorador admitidas para [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] cuando un usuario abre un libro de Excel 2013 con hojas de Power View en un servidor de SharePoint Server que ejecuta Excel Services:  
  
-   Para obtener más información acerca de la compatibilidad con exploradores de SharePoint 2013, consulte planear lahttps://technet.microsoft.com/library/cc263526(office.15).aspx) [compatibilidad con exploradores en SharePoint 2013](https://technet.microsoft.com/library/cc263526\(office.15\).aspx) (.  
  
|**Browser**|**Windows 8 y 8.1**|**Windows 7**|**Windows Server 2012 y 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10,6-10,9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11 (para el escritorio)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|  
|**Internet Explorer 10 (para el escritorio)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|  
|**Internet Explorer 9**|No compatible|32 bits, 64 bits|No compatible|32 bits, 64 bits|32 bits, 64 bits|No compatible|  
|**Internet Explorer 8**|No compatible|32 bits, 64 bits|No compatible|32 bits, 64 bits|32 bits, 64 bits|No compatible|  
|**Mozilla Firefox (la última versión publicada)**|32 bits|32 bits|32 bits|32 bits|32 bits|32 bits, 64 bits|  
|**Apple Safari (versión más reciente publicada)**|No compatible|No compatible|No compatible|No compatible|No compatible|32 bits, 64 bits|  
|**Google Chrome (la última versión publicada)**|32 bits **(\*)** para tiempo limitado|32 bits **(\*)** para tiempo limitado|32 bits **(\*)** para tiempo limitado|32 bits **(\*)** para tiempo limitado|32 bits **(\*)** para tiempo limitado|No compatible|  
  
 **(\*)** Chrome dejará de admitir la API del complemento de Netscape (NPAPI), que se usa en Silverlight. Power View es dependiente de Silverlight.  Para obtener más información, consulte [The Final Countdown for NPAPI](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html).  
  
##  <a name="bkmk_reportmanager"></a>Requisitos del explorador Administrador de informes (modo nativo)

 A continuación se muestra la lista actualizada de exploradores admitidos que puede usar para ejecutar el Administrador de informes en modo nativo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar informes y el servidor de informes.  
  
|Browser|  
|-------------|  
|Internet Explorer 7 o más reciente con scripting habilitado.|  
|Mozilla FireFox (la última versión publicada)|  
|Apple Safari (versión más reciente publicada)|  
|Google Chrome (la última versión publicada)|  
  
##  <a name="bkmk_reportviewer"></a>Requisitos del explorador para ver informes

 A continuación se ofrece la lista actual de exploradores y características compatibles con el visor de informes. El visor de informes admite ver informes desde el administrador de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y bibliotecas de SharePoint.  
  
|**Browser**|**Windows 8 y 8.1**|**Windows 7**|**Windows Server 2012 y 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10,6-10,9**|**iOS 6 -7 para iPad**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11 (para el escritorio)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|No compatible|No compatible|  
|**Internet Explorer 10 (para el escritorio)**|32 bits, 64 bits|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|No compatible|No compatible|  
|**Internet Explorer 9**|No compatible|32 bits, 64 bits|No compatible|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|  
|**Internet Explorer 8**|No compatible|32 bits, 64 bits|No compatible|32 bits, 64 bits|32 bits, 64 bits|No compatible|No compatible|  
|**Internet Explorer 7**|No compatible|No compatible|No compatible|No compatible|32 bits, 64 bits|No compatible|No compatible|  
|**Mozilla Firefox (la última versión publicada)**|32 bits|32 bits|32 bits|32 bits|32 bits|No compatible|No compatible|  
|**Apple Safari (versión más reciente publicada)**|No compatible|No compatible|No compatible|No compatible|No compatible|32 bits, 64 bits|Compatible con características limitadas <sup>(1)</sup>|  
|**Google Chrome (la última versión publicada)**|32 bits|32 bits|32 bits|32 bits|32 bits|No compatible|No compatible|  
  
 **<sup>(1)</sup>** se admiten las siguientes características:  
  
- Exportar a los formatos PDF y TIFF.  
  
- Ver informes de forma interactiva en Apple Safari en dispositivos iOS. Entre la compatibilidad de características se incluye expandir o contraer, el panel de parámetros y ordenación interactiva.  
  
- Para obtener más información, vea [ver informes de Reporting Services en dispositivos de Microsoft Surface y dispositivos iOS de Apple](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md).  
  
 **Nota:** Si tiene acceso a un servidor de informes desde un equipo Macintosh, recomendamos usar Safari. Si está usando un producto de SharePoint integrado con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vea [Planear la compatibilidad con exploradores (Windows SharePoint Services)](https://go.microsoft.com/fwlink/?LinkId=183583).  
  
### <a name="url-access-for-viewing-reports"></a>Acceso URL para ver informes

 Para ver informes directamente, en lugar de verlos a través del Administrador de informes, puede usar el acceso URL para vincular con el informe y el visor de informes. El acceso URL admite diversos exploradores.  
  
 Para obtener más información acerca del acceso URL, vea el siguiente tema:  
  
- [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
###  <a name="bkmk_authentication"></a>Requisitos de autenticación

 Los exploradores admiten esquemas de autenticación concretos que deben ser administrados por el servidor de informes para que la solicitud del cliente tenga éxito. En la tabla siguiente se identifican los tipos de autenticación predeterminados que admite cada explorador que se ejecuta en un sistema operativo Windows.  
  
|**Tipo de explorador**|**Es compatible con**|**Configuración predeterminada del explorador**|**Configuración predeterminada del servidor**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|Negotiated, Kerberos, NTLM, Basic|Negotiate|Sí. La configuración de autenticación predeterminada funciona con Internet Explorer.|  
|**Firefox**|NTLM, Basic|NTLM|Sí. La configuración de autenticación predeterminada funciona con Firefox.|  
|**Safari**|Básica|Básica|Sí. La configuración de autenticación predeterminada funciona con Safari.|  
|**Fondo**|Negotiated, NTLM, Basic|Negotiated|Sí. La configuración de autenticación predeterminada funciona con Chrome.|  
  
### <a name="script-requirements"></a>Requisitos de script

 Para usar el Visor de informes, configure el explorador para que ejecute scripts.  
  
 Si el scripting no está habilitado, verá un mensaje de error similar al siguiente al abrir un informe:  
  
- **Su explorador no admite secuencias de comandos o está configurado para no admitir su ejecución. Haga clic aquí para ver este informe sin scripts**.  
  
 Si decide ver el informe prescindiendo de la compatibilidad con script, se representará en formato HTML y no incorporará funcionalidad del Visor de informes, como la barra de herramientas Informes y el mapa del documento.  
  
> [!NOTE]  
> La barra de herramientas Informes forma parte del componente Visor HTML. De forma predeterminada la barra de herramientas aparece en la parte superior de todos los informes que se representan en una ventana de explorador. El visor de informes proporciona características entre las que se incluyen la posibilidad de buscar información en el informe, desplazarse a una página específica y ajustar el tamaño de página para la visualización. Para obtener más información acerca de la barra de herramientas Informes o el Visor HTML, vea [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md).  
  
##  <a name="bkmk_controls"></a>Compatibilidad del explorador con los controles de servidor Web ReportViewer en Visual Studio

 El control de servidor web ReportViewer se emplea para incrustar funcionalidad de informes en una aplicación web ASP.NET. Los controles se incluyen con Visual Studio y admiten otros exploradores y versiones de explorador que de los demás componentes descritos en este tema. El tipo de explorador utilizado para ver la aplicación determina el tipo de funcionalidad de ReportViewer que puede ofrecer en la aplicación. Use la tabla que se facilita en este tema para determinar qué exploradores admitidos están sujetos a las restricciones de la funcionalidad de informes y las plataformas admitidas.  
  
 Debido a las diferencias en los motores de representación de los exploradores admitidos, algunas características de informes avanzadas pueden mostrarse de manera diferente en exploradores diferentes.  Por ejemplo, la rotación de texto.  
  
### <a name="scripting-requirements"></a>Requisitos de script

 Use un explorador que tenga habilitada la compatibilidad con scripts. Si el explorador no puede ejecutar scripts, no podrá ver el informe.  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>Requisitos del explorador para ver informes con controles de servidor web ReportViewer

 La compatibilidad con las características de informe interactivas varía según el tipo de explorador. La matriz de compatibilidad siguiente muestra los tipos de explorador que son compatibles en cada plataforma, de acuerdo con las restricciones apuntadas en la columna de las notas.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**Browser**|**Windows 8** y **Windows 8.1**|**Windows 7**|**Windows Server 2012** y **2012 R2**|**Windows Server 2008** y **2008 R2**|**Windows Server 2003**|**Mac OS X 10,6-10,9**|**Notas**|  
|**Internet Explorer 11 (para el escritorio**|Sí|Sí|Sí|No compatible|No compatible|No compatible|Internet Explorer admite el conjunto completo de características de ReportViewer.|  
|**Internet Explorer 10 (para el escritorio)**|Sí|Sí|Sí|No compatible|No compatible|No compatible|Internet Explorer admite el conjunto completo de características de ReportViewer.|  
|**Internet Explorer 9**|No compatible|Sí|No compatible|Sí|Sí|Sí|Internet Explorer admite el conjunto completo de características de ReportViewer.|  
|**Internet Explorer 8.0**|No compatible|Sí|No compatible|Sí|Sí<sup>1</sup>|No compatible|Internet Explorer admite el conjunto completo de características de ReportViewer. <sup>1</sup>|  
|**Internet Explorer 7.0**|No compatible|Sí|No compatible|Sí|Sí<sup>1</sup>|No compatible|Internet Explorer admite el conjunto completo de características de ReportViewer. <sup>1</sup>|  
|**Firefox (la última versión publicada)**|Sí|Sí|Sí|Sí|Sí|No compatible|Imprimir y ampliar y reducir no se admiten.|  
|**Safari (última versión publicada)**|No compatible|No compatible|No compatible|No compatible|No compatible|Sí|Imprimir y ampliar y reducir no se admiten.<br /><br /> El control de calendario que se usa para seleccionar fechas en un informe con parámetros está deshabilitado en este explorador. Los usuarios deben escribir las fechas que quieran usar manualmente en el área de mensajes de parámetros.|  
|**Chrome (última versión publicada)**|Sí|Sí|Sí|Sí|Sí|No compatible|Imprimir y ampliar y reducir no se admiten.|  
  
 <sup>1</sup> En el modo estándar, Internet Explorer 7,0 y 8,0 no muestran líneas inclinadas en los informes. Si usa líneas inclinadas en los informes, establezca la página ASP.NET para que se ejecute en modo Quirks en Internet Explorer. Para ello, busque el \<. DOCTYPE> etiqueta en la página de ASP.NET. O bien, si usa una página maestra, puede encontrar la etiqueta en el archivo .master. Esta etiqueta tiene la siguiente apariencia:  
  
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```
  
 Reemplace el \<. DOCTYPE> etiqueta con la siguiente etiqueta:  
  
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```
  
 Para obtener más información sobre los modos de compatibilidad en Internet Explorer, vea definirhttps://go.microsoft.com/fwlink/?LinkId=180380)la compatibilidad de [documentos](https://go.microsoft.com/fwlink/?LinkId=180380) (.  
  
 Para obtener más información sobre el uso de los controles ReportViewer, vea [implementar informes y controles ReportViewer](https://msdn.microsoft.com/library/ms251723.aspx) (https://msdn.microsoft.com/library/ms251723.aspx).  
  
## <a name="next-steps"></a>Pasos siguientes

 [Reporting Services herramientas](tools/reporting-services-tools.md) [Administrador de informes &#40;el modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) [visor HTML y la barra de herramientas del informe](html-viewer-and-the-report-toolbar.md)
