---
title: Documentación para desarrolladores de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.assetid: d8afa405-1012-4349-a72d-e10d94f8453d
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d11e62a8a0a1f90d894c32c82aef938f89a61851
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="reporting-services-developer-documentation"></a>Documentación para desarrolladores de Reporting Services
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona varias interfaces de programación que puede aprovechar en sus propias aplicaciones. Puede utilizar las características y capacidades existentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para generar herramientas personalizadas de administración y elaboración de informes en los sitios web y en las aplicaciones Windows, o para ampliar la plataforma de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Extender la plataforma [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluye crear nuevos componentes y recursos que se pueden utilizar para el acceso a los datos, la entrega de informes, etcétera. Puede comercializar estos componentes y recursos para las compañías que utilizan [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en la organización.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluye ejemplos de programación y tutoriales para ayudarle a empezar. Para más información, vea [Ejemplos de Reporting Services](https://msdn.microsoft.com/library/ms160954\(v=sql.110\).aspx) y [Guía del programador: Tutoriales (Reporting Services)](https://msdn.microsoft.com/library/aa337423\(v=sql.110\).aspx).  
  
## <a name="in-this-section"></a>En esta sección  
 [Integración de Reporting Services en las aplicaciones](../reporting-services/application-integration/integrating-reporting-services-into-applications.md)  
 Proporciona información general sobre cómo utilizar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para integrar los informes de errores en las aplicaciones personalizadas. Describe cuándo utilizar el acceso URL directo y el servicio web para tener acceso al servidor de informes.  
  
 [Servicio web del servidor de informes para aplicaciones ASP.NET y tradicionales](../reporting-services/report-server-web-service/report-server-web-service.md)  
 El servicio web del servidor de informes proporciona acceso a la funcionalidad completa del servidor de informes. El servicio web utiliza SOAP sobre HTTP y está diseñado para actuar como una interfaz de comunicaciones entre los programas clientes y el servidor de informes. El servicio web y sus métodos exponen la funcionalidad del servidor de informes y le permiten crear las herramientas personalizadas para cualquier parte del ciclo de vida del informe, desde la administración a la ejecución.  
 
 [Desarrollo con las API de REST para Reporting Services](developer/rest-api.md)</br>
 Las API de REST para Reporting Services proporcionan acceso mediante programación a los objetos de un catálogo del servidor de informes de Reporting Services. Cuando se usan las API de REST, se puede navegar a una jerarquía de carpetas, detectar el contenido de una carpeta o descargar una definición de informe. También puede crear, actualizar y eliminar objetos.

 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite un conjunto completo de solicitudes basadas en direcciones URL que se pueden usar como punto de acceso rápido y sencillo para la navegación y visualización de informes. Puede utilizar esta tecnología junto con el servicio web del servidor de informes para integrar una solución de informes completa en aplicaciones empresariales personalizadas. El acceso URL es particularmente útil al integrar informes como parte de un portal web o al ver los informes desde un explorador web.  
  
 [Extensiones de Reporting Services](../reporting-services/extensions/reporting-services-extensions.md)  
 La arquitectura modular de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se ha diseñado para permitir ampliaciones. Hay una API de código administrado que permite desarrollar, instalar y administrar con facilidad las extensiones que usan numerosos componentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Puede crear ensamblados mediante [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] y agregar una nueva funcionalidad de procesamiento de datos, representación, seguridad y entrega de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para satisfacer sus necesidades empresariales en evolución.  
  
 [Elementos de informe personalizados](../reporting-services/custom-report-items/custom-report-items.md)  
 Describe cómo crear los elementos de informe personalizado para agregar la funcionalidad a RDL o extender la funcionalidad de los controles existentes.  
  
 [Uso de ensamblados personalizados con informes](../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
 Describe cómo utilizar los ensamblados personalizados con los informes incluyendo referencias al código dentro de la definición de informe.  
  
 [Acceso al proveedor WMI de Reporting Services](../reporting-services/tools/access-the-reporting-services-wmi-provider.md)  
 Describe cómo utilizar el proveedor WMI de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar las implementaciones del servidor de informes.  
  
## <a name="see-also"></a>Ver también  
 [Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Lenguaje RDL (Report Definition Language) &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)   
 [Desarrollo seguro &#40;Reporting Services&#41;](../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
