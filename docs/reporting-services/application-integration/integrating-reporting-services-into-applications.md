---
title: "Integración de Reporting Services en aplicaciones | Documentos de Microsoft"
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
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
caps.latest.revision: 57
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8a1cabc088c7c0ec6c69c8290549e035a4cec7bb
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="integrating-reporting-services-into-applications"></a>Integrar Reporting Services en las aplicaciones
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es una plataforma de informe abierta y extensible diseñada para proporcionar un conjunto completo de API a los programadores para desarrollar soluciones.  
  
 Hay tres opciones para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones personalizadas: servicio Web del servidor de informes, también conocido como el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API de SOAP, los controles ReportViewer para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]y el acceso URL. Cada opción proporciona un enfoque diferente para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones.  
  
## <a name="report-server-web-service"></a>servicio web del servidor de informes  
 El servicio web del servidor de informes es la interfaz principal para el desarrollo de soluciones con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si está desarrollando código para administrar un catálogo de informe o representar informes en un formato admitido, el servicio web expone todos los métodos necesarios para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones. Un ejemplo de una de estas aplicaciones es el Administrador de informes, que se incluye con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; utiliza el servicio Web para administrar la base de datos del servidor de informes.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Controles ReportViewer para Visual Studio  
 Los controles ReportViewer incluidos con [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] se utilizan para integrar la vista del informe en las aplicaciones. Hay dos controles: uno para las aplicaciones basadas en formularios Windows Forms y otro para las aplicaciones de formularios Web Forms. Cada control permite ver los informes implementados en un servidor de informes así como la capacidad de representar los informes que existen en un entorno donde no se haya instalado un servidor de informes.  
  
## <a name="url-access"></a>Acceso URL  
 El acceso URL es otra opción para integrar la vista del informe en las aplicaciones si los controles ReportViewer no son factibles. Además, el acceso URL es útil para enviar vínculos a informes a los usuarios a través de correo electrónico.  
  
## <a name="in-this-section"></a>En esta sección  
 [Integrar Reporting Services con SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 Describe cómo integrar la navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la administración en las aplicaciones empresariales existentes utilizando el servicio web del servidor de informes.  
  
 [Integrar Reporting Services con los controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Describe cómo integrar la vista del informe en las aplicaciones existentes utilizando controles ReportViewer.  
  
 [Integración de Reporting Services mediante el acceso URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 Describe cómo integrar la navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales existentes utilizando el acceso URL.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Elegir entre SOAP y el acceso URL](../../reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [Referencia técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [Servicio Web de servidor de informes](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
