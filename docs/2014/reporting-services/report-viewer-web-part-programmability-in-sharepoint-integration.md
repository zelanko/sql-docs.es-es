---
title: Capacidad de programación del elemento web Visor de informes en la integración de SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a0bc7e2d99190e142647ab8732e2d2d48b3ea2b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63255124"
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>Capacidad de programación del elemento web Visor de informes en la integración de SharePoint
  El elemento web Visor de informes es un control de servidor de `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart`, que contiene un conjunto de interfaces de programación de aplicaciones (API) públicas que permite a los desarrolladores crear aplicaciones SharePoint personalizadas. Puede crear elementos web personalizados que proporcionan la ruta de acceso del informe y los parámetros al elemento web Visor de informes usando conexiones de elementos web. También puede incrustar el elemento web en una página personalizada de elemento web de SharePoint y personalizarlo usando la API pública.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>Conectar con el elemento web Visor de informes con elementos webs personalizados  
 El elemento web Visor de informes es un consumidor de conexión con elementos webs de SharePoint que implementan <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> o `T:Microsoft.SharePoint.WebPartPages.IFilterValues`. Un elemento web <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>, como **Documents**, puede proporcionar una ruta de informe a un elemento web Visor de informes cuando se coloca en la misma página de elementos web que el elemento web Visor de informes. Del mismo modo `T:Microsoft.SharePoint.WebPartPages.IFilterValues` , un elemento Web, como el **filtro de texto** o el filtro de **elección**, puede proporcionar un parámetro de informe a un elemento Web visor de informes cuando se coloca en la misma página de elementos Web que el elemento Web visor de informes.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>Implementar un proveedor de ruta de acceso de informe con IWebPartRow  
 Para proporcionar una ruta de acceso del informe al elemento web Visor de informes a través de las conexiones del elemento, haga lo siguiente:  
  
1.  Cree un elemento web que implemente la interfaz de <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>.  
  
2.  Agregue un elemento web a la misma página del elemento web Visor de informes.  
  
3.  Conecte el elemento web con el elemento web Visor de informes en la interfaz del usuario cuyo diseño de elemento web está basado en la Web.  
  
    > [!NOTE]  
    >  Solo puede conectar un elemento web <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> con el elemento web Visor de informes y no puede conectar al mismo tiempo un elemento web <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> y un elemento web `T:Microsoft.SharePoint.WebPartPages.IFilterValues` al elemento web Visor de informes.  
  
 Para que el elemento web <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> funcione correctamente con `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart`, debe hacer lo siguiente en el método <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A>:  
  
-   Invoque el método de devolución de llamada con un objeto <xref:System.Data.DataRowView> como parámetro de entrada.  
  
-   Asegurarse de que el objeto <xref:System.Data.DataRowView> contiene una columna llamada "DocUrl" que contiene la ruta de acceso al informe.  
  
    > [!NOTE]  
    >  El elemento web Visor de informes del complemento para [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010 también permite recibir los datos de ruta de acceso de informe mediante la columna "FileRef".  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>Implementar un proveedor de parámetros de informe con IFilterValues  
 Un elemento web que implementa `T:Microsoft.SharePoint.WebPartPages.IFilterValues` puede proporcionar un valor de parámetro al elemento web Visor de informes. El valor de parámetro enviado al elemento web Visor de informes está sujeto a las mismas restricciones del parámetro de informe cuando se especificó la definición de informe, como tipo de datos, valores válidos, etc.  
  
 Para proporcionar un parámetro de informe al elemento web Visor de informes, haga lo siguiente:  
  
1.  Cree un elemento web que implemente la interfaz de `T:Microsoft.SharePoint.WebPartPages.IFilterValues`.  
  
2.  Agregue el elemento web a la misma página que `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart`.  
  
3.  Conecte el elemento web `T:Microsoft.SharePoint.WebPartPages.IFilterValues` con el elemento web Visor de informes en la interfaz del usuario cuyo diseño de elemento web está basado en la Web.  
  
    > [!NOTE]  
    >  Puede conectar a la vez varios elementos web `T:Microsoft.SharePoint.WebPartPages.IFilterValues` al elemento web Visor de informes. Sin embargo, no puede conectar al mismo tiempo un elemento web <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> y un elemento web `T:Microsoft.SharePoint.WebPartPages.IFilterValues` al elemento web Visor de informes.  
  
## <a name="see-also"></a>Consulte también  
 [Interfaz IFilterValues](https://msdn.microsoft.com/library/office/microsoft.sharepoint.webpartpages.ifiltervalues\(v=office.15\).aspx)  
  
  
