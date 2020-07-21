---
title: Servicio web del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b577fd9a78dbb5f12af79e190709065931ec463a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62520575"
---
# <a name="report-server-web-service"></a>servicio web del servidor de informes
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona acceso a la funcionalidad completa del servidor de informes a través del servicio Web del servidor de informes. El servicio web del servidor de informes es un servicio web XML con una API SOAP. Utiliza SOAP sobre HTTP y actúa como interfaz de comunicaciones entre los programas clientes y el servidor de informes. El servicio web proporciona dos extremos, uno para la ejecución y otro para la administración de informes, con métodos que exponen la funcionalidad del servidor de informes y le permiten crear herramientas personalizadas para cualquier parte del ciclo de vida del informe.  
  
 Hay tres modos principales para desarrollar aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] basadas en el servicio web. Puede:  
  
-   Desarrolle aplicaciones [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] con y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] el SDK de. Para más información sobre cómo usar [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para generar las aplicaciones del servicio web, vea [Creación de aplicaciones con el servicio Web y .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
-   Desarrollar aplicaciones con la utilidad **rs** (RS.exe), el entorno de script de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Con los scripts de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] puede ejecutar cualquiera de las operaciones del servicio web del servidor de informes. Para más información sobre cómo crear scripts en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Script con la utilidad rs.exe y el servicio web](../tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
-   Desarrollar aplicaciones con cualquier conjunto habilitado para SOAP de herramientas de desarrollo. Para más información, vea [El rol de SOAP en Reporting Services](../report-server-web-service/the-role-of-soap-in-reporting-services.md).  
  
## <a name="programming-diagram"></a>Diagrama de programación  
 ![Opciones de desarrollo del servicio web del servidor de informes](../../../2014/reporting-services/media/reportserviceswebserviceprog-01.gif "Opciones de desarrollo del servicio web del servidor de informes")  
Opciones de desarrollo de servicio web disponibles en Reporting Services  
  
## <a name="in-this-section"></a>En esta sección  
 [Métodos del servicio web del servidor de informes](../report-server-web-service/methods/report-server-web-service-methods.md)  
 Describe las características y métodos de cada servicio web del servidor de informes.  
  
 [El rol de SOAP en Reporting Services](../report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 Proporciona información general de SOAP y de cómo se utiliza en los servicios web del servidor de informes.  
  
 [Acceso a la API SOAP](../report-server-web-service/accessing-the-soap-api.md)  
 Describe el lenguaje de descripción de servicios web (WSDL) y proporciona direcciones URL para tener acceso a un archivo WSDL de Reporting Services.  
  
 [Creación de aplicaciones con el servicio web y .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Contiene información sobre cómo desarrollar aplicaciones y servicios web que llaman a la API SOAP de Reporting Services.  
  
 [Script con la utilidad rs.exe y el servicio Web](../tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 Proporciona información general del entorno de scripting de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 [Referencia técnica &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)  
 Contiene material de referencia específico de los métodos de servicios web del servidor de informes y los tipos complejos correspondientes.  
  
## <a name="user-requirements-for-web-service-development"></a>Requisitos del usuario para el desarrollo de servicios web  
 Para desarrollar aplicaciones con el servicio web del servidor de informes, necesita:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 5.5 o posteriores instalados en un equipo con una conexión a Internet a y acceso al servidor de informes.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK de instalado en un equipo si desea desarrollar e implementar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicaciones de mediante el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
-   Una comprensión detallada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] las características y capacidades.  
  
-   Conocimientos sólidos de SOAP y [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)].  
  
-   Experiencia de desarrollo en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]un lenguaje [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] compatible con, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]o, si piensa usar [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] como plataforma de desarrollo.  
  
## <a name="see-also"></a>Consulte también  
 [Servicio web del servidor de informes](../report-server-web-service/report-server-web-service.md)  
  
  
