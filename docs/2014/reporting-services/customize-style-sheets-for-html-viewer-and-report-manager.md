---
title: Personalizar hojas de estilos para el visor HTML y Administrador de informes | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 7c7745d69e234f81c2a331d214789e93e9fd4014
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "64568267"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>Personalizar hojas de estilos para el Visor HTML y el Administrador de informes
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]proporciona archivos de hojas de estilos en cascada (. CSS) predeterminados que definen estilos para la barra de herramientas de **Informe** en el visor HTML y para Administrador de informes. Si es un programador web o tiene experiencia creando hojas de estilos en cascada, puede modificar los estilos predeterminados bajo su responsabilidad para cambiar los colores, las fuentes y el diseño de la barra de herramientas o el Administrador de informes. En esta versión no se documentan las hojas de estilos predeterminadas ni las instrucciones para modificarlas.  
  
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
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>Configurar Reporting Services para utilizar una hoja de estilos personalizada  
 La hoja de estilos debe tener un archivo válido de hoja de estilos en cascada (.css) y debe estar ubicado en la carpeta Styles. De forma predeterminada, la carpeta Styles se \<encuentra en la *unidad*>: \Archivos de programa\Microsoft SQL Server\Mssql. *n*\Reporting Services\ReportServer\Styles.  
  
 Para utilizar una hoja de estilos predeterminada para el Visor HTML en tiempo de ejecución, puede elegir los siguientes enfoques:  
  
-   Agregue el valor `HTMLViewerStyleSheet` <> al archivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de configuración.  
  
-   Especifique la hoja de estilos en una dirección URL de informe.  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>Modificar el archivo RSReportServer.config  
 Puede modificar el archivo RSReportServer.config de modo que especifique una hoja de estilos personalizada para el Visor HTML. La configuración `HTMLViewerStyleSheet` de> de <no se incluye de forma predeterminada en el archivo. Debe escribirla en el <`Configuration`> selección del archivo Rsreportserver. config y, a continuación, especificar la hoja de estilos que desea utilizar. No incluya la extensión de archivo .css al especificar la hoja de estilos.  
  
 El ejemplo siguiente ilustra cómo debe especificar la hoja de estilos:  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>Especificar una hoja de estilos en una dirección URL de informe  
 Puede utilizar el parámetro de acceso URL `rc:StyleSheet` para especificar una hoja de estilos personalizada en la dirección URL de informe. Para obtener más información sobre cómo especificar parámetros de acceso URL, vea [referencia de parámetros de acceso URL](url-access-parameter-reference.md).  
  
 El ejemplo siguiente ilustra cómo agregar estilos personalizados:  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Visor HTML y la barra de herramientas de informe](html-viewer-and-the-report-toolbar.md)   
 [Archivo de configuración RSReportServer](report-server/rsreportserver-config-configuration-file.md)  
  
  
