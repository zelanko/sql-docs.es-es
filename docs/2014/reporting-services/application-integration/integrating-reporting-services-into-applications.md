---
title: Integrar Reporting Services en las aplicaciones | Microsoft Docs
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
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
caps.latest.revision: 56
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3a27e580a6558b6574b1bdb166f6bdbfb250f01c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103261"
---
# <a name="integrating-reporting-services-into-applications"></a>Integrar Reporting Services en las aplicaciones
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es una plataforma de informe abierta y extensible diseñada para proporcionar un conjunto completo de API a los programadores para desarrollar soluciones.  
  
 Existen tres opciones para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en aplicaciones personalizadas: el servicio web del servidor de informes, que también se denomina API de SOAP de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], los controles ReportViewer para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] y el acceso URL. Cada opción proporciona un enfoque diferente para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones.  
  
## <a name="report-server-web-service"></a>servicio web del servidor de informes  
 El servicio web del servidor de informes es la interfaz principal para el desarrollo de soluciones con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si está desarrollando código para administrar un catálogo de informe o representar informes en un formato admitido, el servicio web expone todos los métodos necesarios para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones. Un ejemplo de tal aplicación es el Administrador de informes, que se incluye con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]; usa el servicio web para administrar la base de datos del servidor de informes.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Controles ReportViewer para Visual Studio  
 Los controles ReportViewer incluidos con [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] se utilizan para integrar la vista del informe en las aplicaciones. Hay dos controles: uno para las aplicaciones basadas en formularios Windows Forms y otro para las aplicaciones de formularios Web Forms. Cada control permite ver los informes implementados en un servidor de informes así como la capacidad de representar los informes que existen en un entorno donde no se haya instalado un servidor de informes.  
  
## <a name="url-access"></a>Acceso URL  
 El acceso URL es otra opción para integrar la vista del informe en las aplicaciones si los controles ReportViewer no son factibles. Además, el acceso URL es útil para enviar vínculos a informes a los usuarios a través de correo electrónico.  
  
## <a name="in-this-section"></a>En esta sección  
 [Integración de Reporting Services con SOAP](../application-integration/integrating-reporting-services-using-soap.md)  
 Describe cómo integrar la navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y la administración en las aplicaciones empresariales existentes utilizando el servicio web del servidor de informes.  
  
 [Integrar Reporting Services con los controles ReportViewer](../application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Describe cómo integrar la vista del informe en las aplicaciones existentes utilizando controles ReportViewer.  
  
 [Integración de Reporting Services con el acceso URL](../application-integration/integrating-reporting-services-using-url-access.md)  
 Describe cómo integrar la navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales existentes utilizando el acceso URL.  
  
## <a name="see-also"></a>Vea también  
 [El Administrador de informes &#40;modo nativo de SSRS&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Elegir entre SOAP y el acceso URL](../../../2014/reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)   
 [Servicio web del servidor de informes](../report-server-web-service/report-server-web-service.md)  
  
  