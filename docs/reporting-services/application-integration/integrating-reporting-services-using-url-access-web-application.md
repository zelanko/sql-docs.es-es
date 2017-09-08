---
title: "Mediante el acceso URL en una aplicación Web | Documentos de Microsoft"
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
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: b8d7aff6c9afdfa6e6fb322d028b9bccf5cbaaf5
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="integrating-reporting-services-using-url-access---web-application"></a>Integración de Reporting Services Using URL Access - aplicación Web
  El acceso URL en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está diseñado específicamente para habilitar el acceso a informes individuales a través de una red. Este tipo de acceso es mejor para integrar la visualización y navegación por los informes en una aplicación web personalizada. Para utilizar el acceso URL en las aplicaciones web, puede:  
  
-   Enviar una dirección URL a un servidor de informes concreto desde un sitio web o portal.  
  
-   Usar un método POST de formulario y pasar parámetros de cadena de consulta a una dirección URL del servidor de informes utilizando campos de formulario.  
  
## <a name="url-access-through-direct-addressing"></a>Acceso URL a través de direccionamiento directo  
 Para obtener acceso a un servidor de informes o el elemento de base de datos del servidor de informes mediante una dirección URL, basta con proporcionar la dirección URL desde un explorador Web o una aplicación. También puede proporcionar los parámetros a la dirección URL que pueda afectar a la apariencia del informe o recurso al que se tiene acceso. Una dirección URL puede tener como destino un servidor de informes a través de la barra de direcciones de un explorador Web o una dirección URL puede ser el origen de un **IFrame** que forma parte de un portal o una aplicación Web más grande. Puede incluir hipervínculos a los informes en varias páginas web de un portal, así como destinar un marco concreto para el informe o abrir una ventana nueva del explorador en el proceso.  
  
 En el ejemplo siguiente, el hipervínculo se destina a un marco denominado "main", que podría ser diferente del que incluye el hipervínculo. El hipervínculo podría formar parte del portal web.  
  
```  
<a href="http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 En el ejemplo anterior, la información de configuración de dispositivo **LinkTarget** se pasa con un valor de "main" en la cadena de consulta de la dirección URL. De esta forma se asegura de que cualquier hipervínculo de obtención de detalles del informe también estará destinado al marco denominado "main".  
  
 Para obtener más información sobre la configuración de información de dispositivo, consulte [pasar la configuración de información de dispositivo para las extensiones de representación](../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Observe que muchos servidores y exploradores limitan el número de caracteres permitidos en una dirección URL. En algunos casos, se impone un límite de 256 caracteres. Para evitar esta limitación, puede utilizar solicitudes POST que usan un envío de formulario.  
  
> [!NOTE]  
>  Internet Explorer tiene una longitud máxima de 2.083 caracteres para la dirección URL. Este límite se aplica a las direcciones URL de solicitudes POST y GET. Sin embargo, el tamaño de la dirección URL no limita a POST para enviar pares de nombre y valor como parte de un formulario, porque se transfieren en el encabezado y no en la dirección URL.  
  
## <a name="url-access-through-a-form-post-method"></a>Acceso URL a través de un método POST de formulario  
 Cuando un usuario solicita los datos de un servidor de informes utilizando el acceso URL, la solicitud HTTP utiliza el método GET. Esto es equivalente al envío de un formulario donde METHOD = "GET". Las solicitudes URL o los envíos de formularios que utilizan METHOD="GET" están limitadas por el número máximo de caracteres que un servidor o un explorador web pueden procesar.  
  
 Con las solicitudes POST (METHOD="POST" y campos de entrada), los pares de nombre y valor se transfieren en el encabezado y no en la dirección URL. Por consiguiente, los pares de nombre y valor de la cadena de consulta no forman parte de la dirección URL, con lo que puede proporcionar listas de parámetros más largas y complejas.  
  
 Con el acceso directo, un usuario puede ver la dirección URL del servidor de informes y quizá pueda modificar la cadena de consulta o anotar la solicitud de dirección URL determinada y los parámetros del servidor de informes para usarlos posteriormente.  
  
 El siguiente ejemplo HTML demuestra el uso de un formulario que puede utilizar para llegar a un servidor de informes con una dirección URL concreta y pasar parámetros de cadena de la consulta como parte de los campos de entrada del formulario.  
  
```  
<FORM id="frmRender" action="http://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 En el ejemplo anterior, si un usuario hace clic en el botón en el formulario, el servidor de informes devuelve el informe objetivo representado por HTML en el marco actual. Una cadena de acceso URL comparable podría ser similar a la siguiente:  
  
```  
http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>Vea también  
 [Integración de Reporting Services en aplicaciones](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integración de Reporting Services mediante el acceso URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Mediante el acceso URL en una aplicación de Windows](../../reporting-services/application-integration/integrating-reporting-services-using-url-access-windows-application.md)   
 [Acceso URL &#40; SSRS &#41;](../../reporting-services/url-access-ssrs.md)  
  
  
