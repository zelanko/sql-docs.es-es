---
title: Integrar Reporting Services con los controles ReportViewer | Microsoft Docs
ms.custom: 
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: application-integration
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
caps.latest.revision: "26"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b43ad81f907ff035170095bebbebc08b93526553
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls"></a>Integrar Reporting Services con los controles ReportViewer
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 proporciona dos controles ReportViewer para integrar la funcionalidad de visualización de informes en las aplicaciones. Hay una versión para las aplicaciones basadas en formularios Windows Forms y otra para las aplicaciones de formularios Web Forms. Cada control proporciona una funcionalidad similar, pero cada uno está diseñado para sus entornos individuales. Ambos controles pueden procesar los informes que se hayan implementado en un servidor de informes (modo de procesamiento remoto) o se hayan copiado en un equipo donde no se haya instalado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (modo de procesamiento local).  
  
 El control ReportViewer no incluye compatibilidad integrada para adaptarse dinámicamente a distintos dispositivos con diferentes resoluciones de pantalla.  
  
## <a name="remote-processing-mode"></a>Modo de procesamiento remoto  
 El modo del procesamiento remoto es el método preferido para ver los informes implementados en un servidor de informes. El modo de procesamiento remoto proporciona las ventajas siguientes:  
  
-   El procesamiento remoto proporciona una solución optimizada para ejecutar informes porque el servidor de informes los procesa.  
  
-   Dado que el servidor de informes controla todo el procesamiento, en una implementación escalada, varios servidores de informes pueden procesar una solicitud de informe o bien, en un escenario de ampliación de la capacidad, puede procesarla un servidor que tenga varios procesadores.  
  
 Además, los informes que se ejecutan en modo remoto pueden utilizar la funcionalidad completa del servidor de informes incluidas todas las extensiones de datos y de representación.  
  
> [!NOTE]  
>  La lista de extensiones disponibles para el control ReportViewer cuando se ejecuta en modo de procesamiento remoto depende de la edición de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que esté instalada en el servidor de informes.  
  
## <a name="local-processing-mode"></a>Modo de procesamiento local  
 El modo de procesamiento local proporciona un método alternativo para ver y representar los informes cuando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no está instalado. A diferencia del procesamiento remoto, en el control solo está disponible un subconjunto de la funcionalidad que proporciona el servidor de informes. En el modo de procesamiento local, el control no administra el procesamiento de los datos sino que se implementa mediante la aplicación de host. Pero el propio control controla el procesamiento de informes. En el modo de procesamiento local, solo están disponibles las extensiones de representación PDF, Excel, Word e Image.  
  
## <a name="see-also"></a>Vea también  
 [Integración de Reporting Services en las aplicaciones](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Usar el control ReportViewer de WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [Usar el control ReportViewer de WinForms](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
