---
title: "Integración de Reporting Services en aplicaciones | Documentos de Microsoft"
ms.custom: 
ms.date: 10/19/2017
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
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 26e1da5a720aab965d014cada16f85086e0f70a0
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="integrating-reporting-services-into-applications"></a>Integrar Reporting Services en las aplicaciones

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es una plataforma de informe abierta y extensible diseñada para proporcionar un conjunto completo de API a los programadores para desarrollar soluciones.

> [!NOTE]
> A partir de SQL Server de 2017 Reporting Services, el acceso de API de REST está disponible para el desarrollo de soluciones. El acceso de API de SOAP está en desuso. Para obtener más información, consulte [desarrollar con las API de REST para Reporting Services](../developer/rest-api.md).
  
 Hay tres opciones para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones personalizadas: servicio Web del servidor de informes, también conocido como el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API de SOAP, los controles ReportViewer para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]y el acceso URL. Cada opción proporciona un enfoque diferente para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones.
  
## <a name="report-server-web-service"></a>Servicio web del servidor de informes

 El servicio web del servidor de informes es la interfaz principal para el desarrollo de soluciones con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si está desarrollando código para administrar un catálogo de informe o representar informes en un formato admitido, el servicio web expone todos los métodos necesarios para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones. Un ejemplo de una de estas aplicaciones es el Administrador de informes, que se incluye con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; utiliza el servicio Web para administrar la base de datos del servidor de informes.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Controles ReportViewer para Visual Studio

 Los controles ReportViewer disponibles para [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] se utilizan para integrar la vista del informe en las aplicaciones. Hay dos controles: uno para las aplicaciones basadas en formularios Windows Forms y otro para las aplicaciones de formularios Web Forms. Cada control permite ver los informes implementados en un servidor de informes así como la capacidad de representar los informes que existen en un entorno donde no se haya instalado un servidor de informes.  
  
## <a name="url-access"></a>acceso URL  
 El acceso URL es otra opción para integrar la vista del informe en las aplicaciones si los controles ReportViewer no son factibles. Además, el acceso URL es útil para enviar vínculos a informes a los usuarios a través de correo electrónico.  
  
## <a name="in-this-section"></a>En esta sección

 [Integración de Reporting Services con SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Describe cómo integrar la navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la administración en las aplicaciones empresariales existentes utilizando el servicio web del servidor de informes.  
  
 [Integrar Reporting Services con los controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Describe cómo integrar la vista del informe en las aplicaciones existentes utilizando controles ReportViewer.  
  
 [Integración de Reporting Services con el acceso URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Describe cómo integrar la navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales existentes utilizando el acceso URL.  
  
## <a name="next-steps"></a>Pasos siguientes

Para decidir sobre el uso de acceso URL o las API de SOAP, vea [elegir entre acceso URL y SOAP de Reporting Services](choosing-between-url-access-and-soap.md).

Para obtener información sobre el SQL Server de 2017 REST API de Reporting Services, consulte [desarrollar con las API de REST para Reporting Services](../developer/rest-api.md).

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).

