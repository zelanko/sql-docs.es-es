---
title: Elegir entre acceso URL y SOAP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], vs. URL access
- Report Server Web service, application integration
- URL access [Reporting Services], vs. SOAP
- Web service [Reporting Services], application integration
ms.assetid: bccdc243-4366-4ce5-8e63-3dd6c463fa52
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7d8d60cd6b91e93dbf0fcd71e8cc995a405af88b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280541"
---
# <a name="choosing-between-url-access-and-soap"></a>Elegir entre el acceso URL y SOAP
  Integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en aplicaciones personalizadas puede resultar complicado. El reto, sin embargo, no es la complejidad del modelo de programación o API, sino las muchas maneras posibles de integrarlo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se diseñó desde el principio como una plataforma para programadores y, como tal, se ha creado teniendo en mente la flexibilidad de la programación. Con la flexibilidad viene la necesidad de tomar decisiones importantes sobre cómo integrar la funcionalidad de la administración y navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales existentes.  
  
 ![Escenarios de programación de Reporting Services](../../../2014/reporting-services/media/bk-ext-04.gif "escenarios de programación de Reporting Services")  
La programación de Reporting Services admite una amplia variedad de escenarios.  
  
 Hay dos maneras de integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones personalizadas: el acceso URL y la API SOAP de Reporting Services. Cuál usar depende de varios factores. En algunos casos, integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales personalizadas requiere el uso tanto del acceso URL como de SOAP. Debería formular las preguntas siguientes:  
  
-   ¿Qué tipo de funcionalidad de informes empresariales requieren usted o sus usuarios finales? ¿Necesita una manera simple de iniciar y navegar por los informes, o más características avanzadas de administración de servidores de informes con la solución empresarial personalizada?  
  
-   ¿En qué tipo de entorno trabajan los usuarios normalmente? ¿La aplicación empresarial está destinada a la Web o a Windows? ¿Cómo pueden pasar los usuarios finales con facilidad de un entorno Win32 a un entorno web? ¿Qué tipo de control necesita sobre el entorno y qué informes se ejecutan y administran?  
  
 Cuando haya respondido las preguntas anteriores, podrá decidir cómo integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la infraestructura de IT. Normalmente, el acceso URL es más adecuado para ver informes individuales y navegar por ellos. El acceso URL permite navegar libre y rápidamente por los informes sin la sobrecarga del servicio web. Asimismo, el acceso URL es, en este momento, la única técnica de programación que utiliza el Visor HTML completo para la navegación por el informe, incluida su barra de herramientas. Además, el acceso URL proporciona mejor rendimiento que SOAP porque omite el cálculo de referencias de las solicitudes SOAP que proceden del servidor o se dirigen a él. En escenarios de integración que requieren un acceso rápido y fácil a los informes con herramientas integradas para la visualización y navegación, el acceso URL es la mejor opción.  
  
> [!NOTE]  
>  El acceso URL del servidor de informes admite el Visor HTML y la funcionalidad extendida de la barra de herramientas del informe. La API SOAP no admite este tipo de informe representado. Si representa informes mediante SOAP, tiene que diseñar y desarrollar su propia barra de herramientas del informe.  
  
 Para más información sobre la barra de herramientas de informes, vea [Visor HTML y la barra de herramientas del informe](../html-viewer-and-the-report-toolbar.md).  
  
 Para obtener más información acerca del acceso URL, vea [acceso URL &#40;SSRS&#41;](../url-access-ssrs.md).  
  
 El acceso URL es útil para ver los informes, pero no proporciona la funcionalidad de administración de espacios de nombres e informes que puede ser esencial para cualquier escenario con informes empresariales. En este caso, se recomienda la variada y completa funcionalidad de la API SOAP de Reporting Services. Con la API SOAP, puede administrar e implementar informes, crear calendarios, configurar las propiedades del servidor, administrar el espacio de nombres del servidor de informes, crear suscripciones, etcétera. La API SOAP expone el conjunto completo de funcionalidad de administración en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. La API SOAP también puede habilitar la visualización y navegación en los informes a través del método <xref:ReportExecution2005.ReportExecutionService.Render%2A> de la API. Sin embargo, al ver los informes a través de la API SOAP, no se habilita la funcionalidad de vista integrada de la barra de herramientas de informe, ni se administra automáticamente la interactividad de los informes que el acceso URL proporciona.  
  
 Para más información sobre la API de SOAP de Reporting Services, vea [Servicio web del servidor de informes](../report-server-web-service/report-server-web-service.md).  
  
 En la mayoría de los casos, para satisfacer las necesidades de funcionalidad de informe se requieren tanto el acceso URL como las llamadas a SOAP. SOAP se usa al conectarse inicialmente a la base de datos del servidor de informes y presentar la lista disponible de informes en una interfaz de usuario, mientras que el acceso URL se utiliza para obtener realmente acceso y navegar por informes individuales.  
  
 Para obtener un ejemplo de cómo combinar el acceso URL y el servicio web para proporcionar informes integrados, vea [SQL Server Reporting Services Product Samples (Ejemplos del producto SQL Server Reporting Services)](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Integración de Reporting Services en las aplicaciones](../../../2014/reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integración de Reporting Services con SOAP](../application-integration/integrating-reporting-services-using-soap.md)   
 [Integración de Reporting Services con el acceso URL](../application-integration/integrating-reporting-services-using-url-access.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
