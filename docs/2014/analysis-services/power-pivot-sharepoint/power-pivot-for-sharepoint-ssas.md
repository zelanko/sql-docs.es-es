---
title: PowerPivot para SharePoint (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: c4c393d3-4856-47ac-ab5f-15da2f240d1d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 733842d4119c83835feff7c71b63f28d419593ab
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365827"
---
# <a name="powerpivot-for-sharepoint-ssas"></a>PowerPivot para SharePoint (SSAS)
  PowerPivot para SharePoint es un servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. PowerPivot para SharePoint proporciona hospedaje de servidor de datos PowerPivot en una granja de SharePoint. Los datos de PowerPivot son un modelo de datos analíticos que se genera mediante uno de los siguientes procedimientos:  
  
-   Complemento PowerPivot para Excel 2010  
  
-   Excel 2013  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 | [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010  
  
 El hospedaje de servidor de esos datos requiere SharePoint, Excel Services y una instalación de PowerPivot para SharePoint. Los datos se cargan en las instancias de PowerPivot para SharePoint donde pueden actualizarse en los intervalos programados mediante la capacidad de actualización de datos PowerPivot que el servidor proporciona para los libros de Excel 2010 o que SharePoint Excel Services 2013 proporciona para los libros de Excel 2013.  
  
## <a name="powerpivot-for-sharepoint-2013"></a>PowerPivot para SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] admite el uso por parte de Excel Services de [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 2013 de libros de Excel que contienen modelos de datos e informes de Power View de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Excel Services en SharePoint 2013 incluye funcionalidad de modelo de datos para habilitar la interacción con un libro PowerPivot en el explorador. No es necesario implementar el complemento PowerPivot para SharePoint 2013 en la granja de servidores. Solo se necesita instalar un servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y registrarlo dentro de la configuración de **Modelo de datos** de Excel Services.  
  
 La implementación del complemento PowerPivot para SharePoint 2013 habilita funcionalidad y características adicionales en la granja de servidores de SharePoint. Entre las características adicionales se incluyen Galería de PowerPivot, programar la actualización de datos y el panel de administración de PowerPivot.  
  
 ![Implementación del servidor de modo 2 de PowerPivot SSAS](../media/as-powerpivot-mode-2server-deployment.gif "implementación del servidor de modo 2 de PowerPivot SSAS")  
  
## <a name="powerpivot-for-sharepoint-2010"></a>PowerPivot para SharePoint 2010  
 PowerPivot para SharePoint 2010 proporciona hospedaje de servidor de datos PowerPivot en una granja de SharePoint 2010. Los datos de PowerPivot son un modelo de datos analíticos creado en Excel mediante el complemento PowerPivot para Excel. El hospedaje de servidor de esos datos requiere SharePoint 2010, Excel Services, y una instalación de PowerPivot para SharePoint. Los datos se cargan en las instancias de PowerPivot para SharePoint en la granja, donde pueden actualizarse a intervalos programados mediante la función de actualización de datos PowerPivot que el servidor proporciona.  
  
### <a name="components-of-powerpivot-for-sharepoint-2010"></a>Componentes de PowerPivot para SharePoint 2010  
 PowerPivot para SharePoint se implementa como un servicio compartido, lo que significa que las características integradas y la infraestructura se pueden utilizar para administrar, proteger y usar una aplicación de servicio PowerPivot. La detección, redirección y administración de conexiones del servidor y la base de datos se administran en el nivel de granja. Administración central proporciona la interfaz administrativa a los servicios utilizados para administrar la identidad del servidor, el estado del servidor y las propiedades de configuración.  
  
 Una implementación completa de cliente de PowerPivot para SharePoint incluye componentes de servidor que se integran con Excel y Excel Services en una granja de servidores de SharePoint. Los datos PowerPivot de un libro de Excel son una base de datos de Analysis Services que requiere un motor analítico en memoria xVelocity de Analysis Services (VertiPaq) para cargar y consultar los datos. En una estación de trabajo cliente, el motor xVelocity se ejecuta en proceso dentro de Excel. En una granja de servidores de SharePoint, Analysis Services se ejecuta en un servidor de aplicaciones donde está emparejado con servicios relacionados que administran solicitudes de datos PowerPivot. El siguiente diagrama ilustra los componentes de servidor y cliente de PowerPivot:  
  
 ![GMNI_GeminiArch2](../media/gmni-geminiarch2.gif "GMNI_GeminiArch2")  
  
 El servicio web de PowerPivot se ejecuta en un servidor de aplicaciones web. Redirige las solicitudes desde la aplicación Web a una instancia de Servicio de sistema de PowerPivot en la granja.  
  
 El Servicio de sistema de PowerPivot emite solicitudes de carga al servidor de Analysis Services y administra las conexiones salientes a los datos que ya están cargados en la memoria, almacenando en memoria caché o descargando los datos, si ya no se utilizan o si se produce alguna contención con los recursos del sistema. También realiza un seguimiento de la actividad de los usuarios. Los datos de estado de servidor y otros datos de uso se recopilan y se presentan en informes para indicar el grado de idoneidad del funcionamiento del sistema.  
  
 Una instancia de servidor de Analysis Services en modo integrado de SharePoint completa la implementación. Carga, consulta, y descarga los datos. También procesa los datos si el libro se configura para la actualización de datos PowerPivot.  Cada instancia está unida estrechamente al Servicio de sistema de PowerPivot local que forma parte de la misma instalación.  
  
##  <a name="bkmk_RelatedContent"></a> En esta sección  
 [Administración y configuración del servidor PowerPivot en Administración central](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Configuración de PowerPivot mediante Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [Herramientas de configuración de PowerPivot](power-pivot-configuration-tools.md)  
  
 [Autenticación y autorización de PowerPivot](power-pivot-authentication-and-authorization.md)  
  
 [Configurar reglas de mantenimiento de PowerPivot:](configure-power-pivot-health-rules.md)  
  
 [Panel de administración de PowerPivot y datos de uso](power-pivot-management-dashboard-and-usage-data.md)  
  
 [La Galería de PowerPivot](../../2014-toc/books-online-for-sql-server-2014.md)  
  
 [Acceso a datos PowerPivot](power-pivot-data-access.md)  
  
 [Actualización de datos PowerPivot](power-pivot-data-refresh.md)  
  
 [Fuentes de distribución de datos de PowerPivot](power-pivot-data-feeds.md)  
  
 [Conexión de modelo semántico de BI PowerPivot &#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)  
  
 **En otras secciones**  
  
## <a name="additional-topics"></a>Temas adicionales  
 [Actualizar PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [Instalación de PowerPivot para SharePoint 2013](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
 [Costes y topologías de licencia de ejemplo de inteligencia empresarial de autoasistencia de SQL Server 2014](../../sql-server/install/example-license-topologies-costs-self-service-business-intelligence.md)  
  
## <a name="see-also"></a>Vea también  
 [Planeación de PowerPivot e implementación](https://go.microsoft.com/fwlink/?linkID=220972)   
 [Recuperación ante desastres de PowerPivot para SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
