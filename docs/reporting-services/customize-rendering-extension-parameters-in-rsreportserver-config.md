---
title: Personalizar los parámetros de extensión de representación en RSReportServer.Config | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- configuration options [Reporting Services]
- DeviceInfo settings
- rendering extensions [Reporting Services], overriding behaviors
- parameters [Reporting Services], report rendering
- overriding report rendering behavior
- extensions [Reporting Services], rendering
ms.assetid: 3bf7ab2b-70bb-41c8-acda-227994d15aed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 615b14cc4d79f4ce206744946f55a0e9ddd0ed37
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274330"
---
# <a name="customize-rendering-extension-parameters-in-rsreportserverconfig"></a>Personalizar los parámetros de extensión de representación en RSReportServer.Config
  Es posible especificar parámetros de extensión de representación en el archivo de configuración RSReportServer para invalidar el comportamiento predeterminado de la representación de los informes que se ejecutan en un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Los parámetros de extensión de representación se pueden modificar para lograr los siguientes objetivos:  
  
-   Cambiar la manera en que aparece el nombre de la extensión de representación en la lista Exportar de la barra de herramientas de informe (por ejemplo, para cambiar "Archivo web" a "MHTML") o traducir el nombre a un idioma diferente.  
  
-   Crear varias instancias de la misma extensión de representación para admitir distintas opciones de presentación de informes (por ejemplo, una versión en modo horizontal y vertical de la extensión de representación en imágenes).  
  
-   Cambiar los parámetros de la extensión de representación predeterminada para que utilicen valores diferentes (por ejemplo, la extensión de representación en imágenes utiliza TIFF como el formato de salida predeterminado; se pueden modificar los parámetros de la extensión de manera que se utilice EMF).  
  
 La modificación de los parámetros de extensión de representación solo afecta a las operaciones de representación del servidor de informes. La configuración de la extensión de representación no se puede reemplazar en la vista previa del informe del Diseñador de informes.  
  
 Cuando se especifican parámetros de extensión de representación en los archivos de configuración, las extensiones de representación se ven afectadas globalmente. Los valores de los archivos de configuración se usarán en lugar de los valores predeterminados siempre que se utilice una extensión de representación determinada. Si se quiere establecer parámetros de extensión de representación para un informe o una operación de representación específicos, debe especificarse la información de dispositivo mediante programación, usando el método <xref:ReportExecution2005.ReportExecutionService.Render%2A> o especificando la configuración de información de dispositivo en una dirección URL de informe. Para obtener más información sobre cómo especificar los valores de información de dispositivo para una operación de representación, y ver la lista completa de valores de información de dispositivo, vea [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="finding-and-modifying-rsreportserverconfig"></a>Buscar y modificar RSReportServer.config  
 Los ajustes de configuración para los formatos de la salida de informes se especifican como parámetros de extensión de representación en el archivo RSReportServer.config. Para especificar parámetros de extensión de representación en los archivos de configuración, es necesario saber cómo se definen las estructuras XML que establecen los parámetros de representación. Hay dos estructuras XML que se pueden modificar:  
  
-   El elemento **OverrideNames** define el nombre para mostrar y el idioma de la extensión de representación.  
  
-   La estructura XML **DeviceInfo** define la configuración de información de dispositivo que utiliza una extensión de representación. La mayoría de los parámetros de extensión de representación se especifican como valores de información de dispositivo.  
  
 Para modificarlo, se puede usar un editor de texto. El archivo RSReportServer.config se encuentra en la carpeta \Reporting Services\Report Server\Bin. Para más información sobre cómo modificar archivos de configuración, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## <a name="changing-the-display-name"></a>Cambiar el nombre para mostrar  
 El nombre para mostrar de una extensión de representación aparece en la lista Exportar de la barra de herramientas de informe. Algunos ejemplos de nombres para mostrar predeterminados son Archivo web, Archivo TIFF y Archivo PDF de Acrobat. El nombre para mostrar predeterminado se puede sustituir por un valor personalizado especificando el elemento **OverrideNames** en los archivos de configuración. Además, si se van a definir dos instancias de una extensión de representación, se puede utilizar el elemento **OverrideNames** para distinguirlas en la lista Exportar.  
  
 Dado que los nombres para mostrar se traducen, será necesario establecer el atributo **Language** si se va a sustituir el nombre para mostrar predeterminado por un valor personalizado. Si no, se pasará por alto cualquier nombre que se especifique. El valor de idioma que se establezca debe ser válido en el equipo del servidor de informes. Por ejemplo, si el servidor de informes se ejecuta en un sistema operativo en francés, deberá especificarse "fr-FR" como valor del atributo.  
  
 En el ejemplo siguiente se muestra cómo especificar un nombre personalizado en un servidor de informes en inglés:  
  
```  
<Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering">  
   <OverrideNames>  
     <Name Language="en-US">My Custom Display Name for XML Rendering</Name>  
   </OverrideNames>  
</Extension>  
```  
  
## <a name="changing-device-information-settings"></a>Cambiar la configuración de la información del dispositivo  
 Para modificar la configuración predeterminada de la información del dispositivo que utiliza una extensión de representación ya implementada en el servidor de informes, debe incluirse la estructura XML **DeviceInfo** en los archivos de configuración. Cada extensión de representación admite valores de información de dispositivo exclusivos para esa extensión. Para ver la lista completa de la configuración de la información de dispositivos, vea [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 En el ejemplo siguiente se muestran la estructura XML y la sintaxis que modifica la configuración predeterminada de la extensión de representación en imágenes:  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">Image (EMF)</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <ColorDepth>32</ColorDepth>  
                <DpiX>300</DpiX>  
                <DpiY>300</DpiY>  
                <OutputFormat>EMF</OutputFormat>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="configuring-multiple-entries-for-a-rendering-extension"></a>Configurar varias entradas para una extensión de representación  
 Se pueden crear varias instancias de la misma extensión de representación para admitir diferentes opciones de presentación de informes. Cada instancia que se defina puede tener una combinación distinta de valores de parámetro. Cuando defina nuevas instancias de una extensión de representación existente, realice los pasos siguientes:  
  
-   Especifique un nombre único para la extensión.  
  
     Cada instancia debe tener un valor único para el atributo **Name** . En el ejemplo siguiente se utilizan los nombres "IMAGE (EMF Landscape)" e "IMAGE (EMF Portrait)" para distinguir las dos instancias.  
  
     Tenga cuidado al cambiar el nombre de una extensión de representación ya implementada. Los programadores que especifican extensiones de representación mediante programación usan el nombre de la extensión para identificar la instancia que se va a utilizar en una operación de representación determinada. Si se ejecutan aplicaciones de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] personalizadas en el servidor de informes, asegúrese de que el programador sabe que ha modificado un nombre de extensión existente o ha agregado uno nuevo.  
  
-   Especifique un nombre para mostrar único de manera que los usuarios entiendan las diferencias de cada formato de salida.  
  
     Si configura varias versiones de la misma extensión, puede asignar a cada versión un nombre único, proporcionando un valor para **OverrideNames**. En caso contrario, todas las versiones de la extensión aparentemente tendrán el mismo nombre en la lista de opciones de exportación de la barra de herramientas de informe.  
  
 En el siguiente ejemplo se muestra cómo utilizar la extensión de representación en imágenes predeterminada (que genera salida TIFF) para generar salida EMF en modo vertical, junto con una segunda instancia que genera informes en formato EMF en modo horizontal. Observe cómo el nombre de cada extensión es único. Cuando pruebe este ejemplo, no olvide elegir informes que no contengan funciones interactivas, como opciones de mostrar u ocultar, matrices o vínculos de obtención de detalles (las funciones interactivas no funcionan en la extensión de representación en imágenes):  
  
```  
<Render>  
    <Extension Name="IMAGE (EMF Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Landscape Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>8.5in</PageHeight>  
                <PageWidth>11in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
    <Extension Name="IMAGE (EMF Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering">  
        <OverrideNames>  
            <Name Language="en-US">EMF in Portait Mode</Name>  
        </OverrideNames>  
        <Configuration>  
            <DeviceInfo>  
                <OutputFormat>EMF</OutputFormat>  
                <PageHeight>11in</PageHeight>  
                <PageWidth>8.5in</PageWidth>  
            </DeviceInfo>  
        </Configuration>  
    </Extension>  
</Render>  
```  
  
## <a name="see-also"></a>Ver también  
 [El archivo de configuración RSReportServer.config](../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Archivo de configuración RSReportDesigner](../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Configuración de la información del dispositivo CSV](../reporting-services/csv-device-information-settings.md)   
 [Configuración de la información del dispositivo Excel](../reporting-services/excel-device-information-settings.md)   
 [Configuración de la información del dispositivo HTML](../reporting-services/html-device-information-settings.md)   
 [Configuración de la información del dispositivo de imagen](../reporting-services/image-device-information-settings.md)   
 [Configuración de la información del dispositivo MHTML](../reporting-services/mhtml-device-information-settings.md)   
 [Configuración de la información del dispositivo PDF](../reporting-services/pdf-device-information-settings.md)   
 [Configuración de la información del dispositivo XML](../reporting-services/xml-device-information-settings.md)  
  
  
