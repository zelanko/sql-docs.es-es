---
title: 'Lección 2: Agregar una referencia Web | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
caps.latest.revision: 29
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ff574cf6ab00b4b368a7d372957b2348757ad0f5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196350"
---
# <a name="lesson-2-adding-a-web-reference"></a>Lección 2: agregar una referencia web
  Se llama detección de servicios web al proceso por el que un cliente busca un servicio web y obtiene la descripción del servicio. El proceso de detección de servicios web en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] conlleva la interrogación de un sitio web de acuerdo con un algoritmo predeterminado. El objetivo del proceso es encontrar la descripción del servicio, que es un documento XML que utiliza el Lenguaje de descripción de servicios web (WSDL).  
  
 En la descripción del servicio, se explican los servicios disponibles y la forma de interactuar con ellos. Sin una descripción del servicio, no se puede interactuar con el servicio web mediante programación.  
  
 La aplicación debe disponer de un método para comunicarse con el servicio web y buscarlo en tiempo de ejecución. Esto se consigue agregando al proyecto una referencia del servicio web, porque se genera una clase proxy que sirve de interfaz con el servicio web y proporciona una representación local del servicio web. Para obtener más información, vea el tema sobre generación de un proxy de servicio web XML en la documentación de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
### <a name="to-add-a-web-reference"></a>Para agregar una referencia web  
  
1.  En el **proyecto** menú, haga clic en **Agregar referencia de servicio**.  
  
2.  En el **Agregar referencia de servicio** cuadro de diálogo, haga clic en **avanzadas**.  
  
3.  En el **configuración de referencia de servicio** cuadro de diálogo, haga clic en **Agregar referencia Web**.  
  
4.  En el **URL** cuadro de la **Agregar referencia Web** cuadro de diálogo, escriba la dirección URL para obtener la descripción del servicio del servicio Web del servidor de informes, por ejemplo, http://localhost/reportserver/reportservice2010.asmx. A continuación, haga clic en el **vaya** para recuperar información sobre el servicio Web.  
  
     \- O bien  
  
     Si el servicio Web del servidor de informes no existe en el equipo local, haga clic en el **Web services en el equipo local** vínculo en el panel explorador. A continuación, haga clic en el vínculo del servicio web ReportService2010 de la lista proporcionada.  
  
5.  En el **nombre de referencia Web** cuadro, cambie el nombre de la referencia Web a ReportService2010, que es el espacio de nombres que se va a utilizar para esta referencia Web.  
  
6.  Haga clic en **Agregar referencia** para agregar una referencia Web para el servicio Web de destino.  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] descarga la descripción del servicio y genera una clase proxy que sirve de interfaz entre la aplicación y el servicio web del servidor de informes. También necesitará agregar una referencia al espacio de nombres <xref:System.Web.Services> para que su referencia web funcione.  
  
7.  En el menú proyecto, haga clic en **Agregar referencia**.  
  
8.  En el **Agregar referencia** cuadro de diálogo, en la **.NET** ficha, seleccione **System.Web.Services**, a continuación, haga clic en **Aceptar**.  
  
 Para más información, vea [Acceso a la API de SOAP](../reporting-services/report-server-web-service/accessing-the-soap-api.md).  
  
## <a name="see-also"></a>Vea también  
 [Servicio web del servidor de informes](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Lección 3: Obtener acceso al servicio de Web](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [Obtener acceso al servicio de Web del servidor de informes mediante Visual Basic o Visual C&#35; &#40;Tutorial de SSRS&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  