---
title: Personalizar hojas de estilos para el Visor de HTML y el Administrador de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- style sheets [Reporting Services]
ms.assetid: df805cff-b1de-4062-b2ac-423f37390fbd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d9c4a57413db37c8f93b1a311542398417bfeff0
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969531"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>Personalizar hojas de estilos para el Visor HTML y el Administrador de informes
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ofrece estilos en cascada de forma predeterminada los archivos de hoja (.css) que definen estilos para el **informe** barra de herramientas en el Visor de HTML y para el Administrador de informes. Si es un programador web o tiene experiencia creando hojas de estilos en cascada, puede modificar los estilos predeterminados bajo su responsabilidad para cambiar los colores, las fuentes y el diseño de la barra de herramientas o el Administrador de informes. En esta versión no se documentan las hojas de estilos predeterminadas ni las instrucciones para modificarlas.  
  
 Modificar las hojas de estilos incorrectamente puede provocar errores al abrir los informes. Si no sabe cómo modificar las hojas de estilos, debe utilizar las hojas de estilos predeterminadas. Si decide personalizar las hojas de estilos, asegúrese de crear una copia de seguridad para todos los archivos .css personalizados antes de hacer cambios.  
  
 Modificar las hojas de estilos no afecta al aspecto de los informes publicados que ejecute en un servidor de informes. En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], los informes no hacen referencia a hojas de estilos. Los informes ad hoc que el servidor de informes genera automáticamente utilizan información de estilo que se almacena como un recurso incrustado en los archivos de programa del servidor de informes. Los informes que cree en el Diseñador de informes utilizarán las fuentes, los colores y el diseño que especifique en la definición de informe. Los estilos se crean en sintonía con el resto del diseño.  
  
> [!NOTE]  
>  Si desea utilizar estilos de informe predefinidos, utilice el Asistente para informes para crear un informe. El Asistente para informes ofrece varios temas que puede utilizar para crear informes estilizados con diferentes combinaciones de colores y fuentes. Las plantillas de estilo que definen los temas para un informe pueden modificarse.  
  
## <a name="reporting-services-style-sheets"></a>Hojas de estilos de Reporting Services  
 La siguiente tabla describe los archivos de hoja de estilos (.css) que se usan en una instalación de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
|Hoja de estilos|Descripción|  
|-----------------|-----------------|  
|Htmlviewer.css|Ofrece un ejemplo de hoja de estilos que puede utilizar como una plantilla para crear estilos personalizados para la barra de herramientas de **informe** en el Visor HTML.<br /><br /> Los estilos predeterminados utilizados por el Visor HTML se compilan en el servidor de informes. El archivo Htmlviewer.css ofrece un ejemplo de los estilos que utiliza el visor.|  
|ReportingServices.css|Define estilos para el Administrador de informes.|  
  
> [!NOTE]  
>  Las siguientes hojas de estilos se usan para la documentación en línea del Administrador de informes y no deben modificarse nunca: SQL.CSS y Mailto.css. Otras hojas de estilos definen estilos para los informes y el Administrador de informes que se abren en elementos web de SharePoint. Estas hojas de estilos incluyen Rswebparts.css, Sp_full.css, y Sp_small.css. No se recomienda modificar las hojas de estilos de SharePoint. Para obtener más información sobre cómo se usan los elementos Web, consulte [ver y explorar nativo modo informes utilizando elementos Web de SharePoint &#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md).  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>Configurar Reporting Services para utilizar una hoja de estilos personalizada  
 La hoja de estilos debe tener un archivo válido de hoja de estilos en cascada (.css) y debe estar ubicado en la carpeta Styles. De forma predeterminada, la carpeta Styles se encuentra en \< *unidad*>: \Program Files\Microsoft SQL Server\MSSQL. *n*\Reporting Services\ReportServer\Styles.  
  
 Para utilizar una hoja de estilos predeterminada para el Visor HTML en tiempo de ejecución, puede elegir los siguientes enfoques:  
  
-   Agregue el <`HTMLViewerStyleSheet`> Si se establece en el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] archivo de configuración.  
  
-   Especifique la hoja de estilos en una dirección URL de informe.  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>Modificar el archivo RSReportServer.config  
 Puede modificar el archivo RSReportServer.config de modo que especifique una hoja de estilos personalizada para el Visor HTML. El <`HTMLViewerStyleSheet`> configuración no se incluye en el archivo de forma predeterminada. Debe escribirla en el <`Configuration`> selección de RSReportServer.config archivo y, a continuación, especifique la hoja de estilos que desea usar. No incluya la extensión de archivo .css al especificar la hoja de estilos.  
  
 El ejemplo siguiente ilustra cómo debe especificar la hoja de estilos:  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>Especificar una hoja de estilos en una dirección URL de informe  
 Puede utilizar el parámetro de acceso URL `rc:StyleSheet` para especificar una hoja de estilos personalizada en la dirección URL de informe. Para obtener más información sobre cómo especificar parámetros de acceso URL, vea [URL Access Parameter Reference](url-access-parameter-reference.md).  
  
 El ejemplo siguiente ilustra cómo agregar estilos personalizados:  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Visor HTML y la barra de herramientas de informe](html-viewer-and-the-report-toolbar.md)   
 [Archivo de configuración RSReportServer](report-server/rsreportserver-config-configuration-file.md)  
  
  
