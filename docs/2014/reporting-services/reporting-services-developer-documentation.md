---
title: Desarrollador&#39;guía (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.assetid: d8afa405-1012-4349-a72d-e10d94f8453d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e8c555d853fd791bed29a06f561021b138526ea1
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157961"
---
# <a name="developer39s-guide-reporting-services"></a>Desarrollador&#39;guía (Reporting Services)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona varias interfaces de programación que puede aprovechar en sus propias aplicaciones. Puede utilizar las características y capacidades existentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para generar herramientas personalizadas de administración y elaboración de informes en los sitios web y en las aplicaciones Windows, o para ampliar la plataforma de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 Extender la plataforma [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluye crear nuevos componentes y recursos que se pueden utilizar para el acceso a los datos, la entrega de informes, etcétera. Puede comercializar estos componentes y recursos para las compañías que utilizan [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en la organización.  
  
## <a name="in-this-section"></a>En esta sección  
 [Integración de Reporting Services en las aplicaciones](application-integration/integrating-reporting-services-into-applications.md)  
 Proporciona información general sobre cómo utilizar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para integrar los informes de errores en las aplicaciones personalizadas. Describe cuándo utilizar el acceso URL directo y el servicio web para tener acceso al servidor de informes.  
  
 [Servicio web del servidor de informes](report-server-web-service/report-server-web-service.md)  
 El servicio web del servidor de informes proporciona acceso a la funcionalidad completa del servidor de informes. El servicio web utiliza SOAP sobre HTTP y está diseñado para actuar como una interfaz de comunicaciones entre los programas clientes y el servidor de informes. El servicio web y sus métodos exponen la funcionalidad del servidor de informes y le permiten crear las herramientas personalizadas para cualquier parte del ciclo de vida del informe, desde la administración a la ejecución.  
  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite un conjunto completo de solicitudes basadas en direcciones URL que se pueden usar como punto de acceso rápido y sencillo para la navegación y visualización de informes. Puede utilizar esta tecnología junto con el servicio web del servidor de informes para integrar una solución de informes completa en aplicaciones empresariales personalizadas. El acceso URL es particularmente útil al integrar informes como parte de un portal web o al ver los informes desde un explorador web.  
  
 [Extensiones de Reporting Services](extensions/reporting-services-extensions.md)  
 La arquitectura modular de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se ha diseñado para permitir ampliaciones. Hay una API de código administrado que permite desarrollar, instalar y administrar con facilidad las extensiones que usan numerosos componentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Puede crear ensamblados mediante [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] y agregar una nueva funcionalidad de procesamiento de datos, representación, seguridad y entrega de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para satisfacer sus necesidades empresariales en evolución.  
  
 [Elementos de informe personalizados](custom-report-items/custom-report-items.md)  
 Describe cómo crear los elementos de informe personalizado para agregar la funcionalidad a RDL o extender la funcionalidad de los controles existentes.  
  
 [Uso de ensamblados personalizados con informes](custom-assemblies/using-custom-assemblies-with-reports.md)  
 Describe cómo utilizar los ensamblados personalizados con los informes incluyendo referencias al código dentro de la definición de informe.  
  
 [Acceso al proveedor WMI de Reporting Services](tools/access-the-reporting-services-wmi-provider.md)  
 Describe cómo utilizar el proveedor WMI de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar las implementaciones del servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Lenguaje RDL (Report Definition Language) &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)   
 [Referencia técnica &#40;SSRS&#41;](technical-reference-ssrs.md)   
 [Desarrollo seguro &#40;Reporting Services&#41;](extensions/secure-development/secure-development-reporting-services.md)  
  
  
