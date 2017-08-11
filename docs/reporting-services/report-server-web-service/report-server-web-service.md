---
title: Servicio Web del servidor de informes | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 10769f49396bcf32d437e4bee9b04cbc2a3c8d9c
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-web-service"></a>servicio web del servidor de informes
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona acceso a la funcionalidad completa del servidor de informes a través del servicio Web del servidor de informes. El servicio web del servidor de informes es un servicio web XML con una API SOAP. Utiliza SOAP sobre HTTP y actúa como interfaz de comunicaciones entre los programas clientes y el servidor de informes. El servicio web proporciona dos extremos, uno para la ejecución y otro para la administración de informes, con métodos que exponen la funcionalidad del servidor de informes y le permiten crear herramientas personalizadas para cualquier parte del ciclo de vida del informe.  
  
 Hay tres modos principales para desarrollar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicaciones basadas en el servicio Web. Puede hacer lo siguiente:  
  
-   Desarrollar aplicaciones con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Para obtener más información sobre el uso de la [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para compilar aplicaciones de servicio Web, consulte [creación de aplicaciones con el servicio Web y .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
-   Desarrollar aplicaciones con el **rs** utilidad (RS.exe), el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] entorno de secuencia de comandos. Con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] secuencias de comandos, puede ejecutar cualquiera de las operaciones del servicio Web del servidor de informes. Para obtener más información acerca del scripting en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [secuencia de comandos con el rs.exe Utilidad y el servicio Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
-   Desarrollar aplicaciones con cualquier conjunto habilitado para SOAP de herramientas de desarrollo. Para obtener más información, consulte [The Role of SOAP de Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md).  
  
## <a name="programming-diagram"></a>Diagrama de programación  
 ![Opciones de desarrollo del servicio Web del servidor de informes](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "opciones de desarrollo del servicio Web del servidor de informes")  
Opciones de desarrollo de servicio web disponibles en Reporting Services  
  
## <a name="in-this-section"></a>En esta sección  
 [Métodos de servicio web del servidor de informes](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 Describe las características y métodos de cada servicio web del servidor de informes.  
  
 [El rol de SOAP en Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 Proporciona información general de SOAP y de cómo se utiliza en los servicios web del servidor de informes.  
  
 [Acceso a la API SOAP](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 Describe el lenguaje de descripción de servicios web (WSDL) y proporciona direcciones URL para tener acceso a un archivo WSDL de Reporting Services.  
  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Contiene información sobre cómo desarrollar aplicaciones y servicios web que llaman a la API SOAP de Reporting Services.  
  
 [Secuencia de comandos con la utilidad rs.exe y el servicio Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 Proporciona información general del entorno de scripting de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Referencia técnica de &#40; SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
 Contiene material de referencia específico de los métodos de servicios web del servidor de informes y los tipos complejos correspondientes.  
  
## <a name="user-requirements-for-web-service-development"></a>Requisitos del usuario para el desarrollo de servicios web  
 Para desarrollar aplicaciones con el servicio web del servidor de informes, necesita:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]Internet Explorer 5.5 o posterior instalado en un equipo con una conexión a Internet y el acceso al servidor de informes.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK instalado en un equipo si desea desarrollar e implementar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] las aplicaciones que usan el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
-   Una comprensión detallada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] características y capacidades.  
  
-   Conocimientos sólidos de SOAP y [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)].  
  
-   Experiencia de desarrollo de un [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-lenguaje compatible con como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], si tiene previsto usar el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] como plataforma de desarrollo.  
  
## <a name="see-also"></a>Vea también  
 [Servicio Web de servidor de informes](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
