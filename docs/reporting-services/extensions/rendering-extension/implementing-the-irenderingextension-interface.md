---
title: Implementar la interfaz IRenderingExtension | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
caps.latest.revision: 43
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3b5772901cfaabedab1b42db39dcd85c49119509
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-the-irenderingextension-interface"></a>Implementar la interfaz IRenderingExtension
  La extensión de representación toma los resultados de una definición de informe que se combina con los datos reales y representa los datos resultantes en un formato que se puede usar. La transformación de los datos combinados y el formato se efectúan utilizando una clase de Common Language Runtime (CLR) que implementa <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension>. De esta forma se transforma el modelo de objetos en un formato de salida que puede usar un visor, impresora u otro destino de salida.  
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> tiene tres métodos que deben estar codificados:  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A>: representa el informe.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A>: representa un flujo concreto del informe.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>: obtiene la información adicional, como iconos, necesaria para el informe.  
  
 En las siguientes secciones se describen los métodos con más detalle.  
  
## <a name="render-method"></a>Método Render  
 El método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> contiene argumentos que representan los objetos siguientes:  
  
-   El *informe* que desea representar. Este objeto contiene propiedades, datos e información de presentación para el informe. El informe es la raíz del árbol del modelo de objetos de informe.  
  
-   El *ServerParameters* que contienen el objeto de diccionario de cadena, con los parámetros del servidor de informes, si lo hay.  
  
-   El *deviceInfo* parámetro que contienen la configuración del dispositivo. Para obtener más información, consulte [pasar la configuración de información de dispositivo para las extensiones de representación](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
-   El *clientCapabilities* parámetro que contiene un <xref:System.Collections.Specialized.NameValueCollection> objeto de diccionario que tiene información sobre el cliente al que está representando.  
  
-   El *RenderProperties* que contiene información sobre el resultado de la representación.  
  
-   El *createAndRegisterStream* es una función de delegado que se llamará para obtener un flujo que se va a representar.  
  
### <a name="deviceinfo-parameter"></a>Parámetro de deviceInfo  
 El *deviceInfo* parámetro contiene parámetros de representación, no los parámetros de informe. Estos parámetros de representación se pasan a la extensión de representación. El *deviceInfo* valores se convierten en un <xref:System.Collections.Specialized.NameValueCollection> objeto por el servidor de informes. Los elementos de la *deviceInfo* parámetro se tratan como valores entre mayúsculas y minúsculas. Si la solicitud de representación se produjo como resultado de la dirección URL de acceso, los parámetros de dirección URL en el formulario `rc:key=value` se convierten en pares de clave/valor la *deviceInfo* objeto de diccionario. El código de detección de explorador también proporciona los siguientes elementos en el *clientCapabilities* diccionario: EcmaScriptVersion, JavaScript, MajorVersion, MinorVersion, Win32, tipo y AcceptLanguage. Cualquier par de nombre y valor la *deviceInfo* se omite el parámetro que no entiende la extensión de representación. La muestra de código siguiente muestra un método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> de muestra que recupera los iconos.  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>Método RenderStream  
 El método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> representa un flujo determinado del informe. Todos los flujos se crean durante la llamada de <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> inicial, pero los flujos no se devuelven inicialmente al cliente. Este método se utiliza para flujos secundarios (similares a las imágenes en la representación HTML) o páginas adicionales de una extensión de representación de varias páginas (similar a Image/EMF).  
  
## <a name="getrenderingresource-method"></a>Método GetRenderingResource  
 El método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A> recupera la información sin ejecutar una representación completa del informe. Hay ocasiones en que el informe requiere información que no requiere representar el propio informe. Por ejemplo, si necesita el icono asociado a la extensión de representación, utilice la *deviceInfo* parámetro que contiene la etiqueta única  **\<icono >**. En estos casos, puede usar el método <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de representación](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Introducción a las extensiones de representación](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  
