---
title: "Notificar la capacidad de programación de visor Web parte de la integración de SharePoint | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6e176aafa062c1184ff120cc1e886b9f5e244712
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>Capacidad de programación del elemento web Visor de informes en la integración de SharePoint
  El elemento Web de Visor de informes es un control de servidor, que contiene un conjunto de aplicaciones públicas (API) de interfaces de programación que permite a los desarrolladores crear aplicaciones personalizadas de SharePoint. Puede crear elementos web personalizados que proporcionan la ruta de acceso del informe y los parámetros al elemento web Visor de informes usando conexiones de elementos web. También puede incrustar el elemento web en una página personalizada de elemento web de SharePoint y personalizarlo usando la API pública.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>Conectar con el elemento web Visor de informes con elementos webs personalizados  
 El elemento Web de Visor de informes es un consumidor de conexión para los elementos Web de SharePoint que implementan <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> o T:Microsoft.SharePoint.WebPartPages.IFilterValues. Un <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> elemento Web, como el **documentos** elemento Web puede proporcionar una ruta de acceso de informe a un elemento de Web del Visor de informes cuando se coloca en la misma página de elementos Web que el elemento Web de Visor de informes. Del mismo modo, la parte Web T:Microsoft.SharePoint.WebPartPages.IFilterValues, como el **filtro de texto** o **Choice Filter**, puede proporcionar un parámetro de informe a un elemento de Web del Visor de informes cuando se coloca en la misma página de elementos Web que el elemento Web de Visor de informes.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>Implementar un proveedor de ruta de acceso de informe con IWebPartRow  
 Para proporcionar una ruta de acceso del informe al elemento web Visor de informes a través de las conexiones del elemento, haga lo siguiente:  
  
1.  Cree un elemento web que implemente la interfaz de <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>.  
  
2.  Agregue un elemento web a la misma página del elemento web Visor de informes.  
  
3.  Conecte el elemento web con el elemento web Visor de informes en la interfaz del usuario cuyo diseño de elemento web está basado en la Web.  
  
    > [!NOTE]  
    >  Sólo se puede conectar una <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> elemento Web para el elemento Web de Visor de informes en un momento y no se puede conectar un <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web y un elemento Web de T:Microsoft.SharePoint.WebPartPages.IFilterValues para el elemento Web de Visor de informes al mismo tiempo.  
  
 Para su <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> elemento Web para funcionar correctamente con el T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart, debe hacer lo siguiente en el <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> método:  
  
-   Invoque el método de devolución de llamada con un objeto <xref:System.Data.DataRowView> como parámetro de entrada.  
  
-   Asegurarse de que el objeto <xref:System.Data.DataRowView> contiene una columna llamada "DocUrl" que contiene la ruta de acceso al informe.  
  
    > [!NOTE]  
    >  El elemento web Visor de informes del complemento para [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 también permite recibir los datos de ruta de acceso de informe mediante la columna "FileRef".  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>Implementar un proveedor de parámetros de informe con IFilterValues  
 Un elemento Web que implementa T:Microsoft.SharePoint.WebPartPages.IFilterValues puede proporcionar un valor de parámetro para el elemento Web de Visor de informes. El valor de parámetro enviado al elemento web Visor de informes está sujeto a las mismas restricciones del parámetro de informe cuando se especificó la definición de informe, como tipo de datos, valores válidos, etc.  
  
 Para proporcionar un parámetro de informe al elemento web Visor de informes, haga lo siguiente:  
  
1.  Crear un elemento Web que implementa la interfaz T:Microsoft.SharePoint.WebPartPages.IFilterValues.  
  
2.  Agregar el elemento Web a la misma página que el T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart.  
  
3.  Conecte el elemento de Web T:Microsoft.SharePoint.WebPartPages.IFilterValues para el elemento Web de Visor de informes en la interfaz de usuario de diseño de elemento Web basada en Web.  
  
    > [!NOTE]  
    >  Puede conectar varios elementos Web de T:Microsoft.SharePoint.WebPartPages.IFilterValues para el elemento Web de Visor de informes a la vez. Sin embargo, no se puede conectar ambos un <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> Web y un elemento Web de T:Microsoft.SharePoint.WebPartPages.IFilterValues para el elemento Web de Visor de informes al mismo tiempo.  
  
  
