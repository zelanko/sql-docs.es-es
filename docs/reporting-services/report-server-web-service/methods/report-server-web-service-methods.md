---
title: "Métodos de servicio Web del servidor de informes | Documentos de Microsoft"
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
caps.latest.revision: 49
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ec79e5169ff32294cc68f5bee24c3df677d8b38b
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="report-server-web-service-methods"></a>Métodos de servicio web del servidor de informes
  Los servicios web del servidor de informes incluyen varias categorías de métodos que están basados en las características de componente. Estos métodos se proporcionan a través de varios extremos de servicios web (tres para la administración de informes y uno para la ejecución de informes) que se exponen como miembros de las clases <xref:ReportService2010.ReportingService2010> y <xref:ReportExecution2005.ReportExecutionService>. Estas clases se pueden generar mediante una herramienta de la clase de proxy como wsdl.exe, que se incluye con la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK. Para obtener más información acerca de los servicios Web del servidor de informes y el [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], consulte [creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
## <a name="endpoints-and-methods"></a>Puntos finales y métodos  
 En la tabla siguiente se muestra una lista de extremos del servicio web del servidor de informes, así como las categorías de los métodos proporcionadas por el extremo <xref:ReportService2010.ReportingService2010>. Para obtener información sobre los métodos disponibles en los demás extremos, vea [referencia técnica &#40; SSRS &#41; ](../../../reporting-services/technical-reference-ssrs.md).  
  
|Tema|Description|  
|-----------|-----------------|  
|[Extremos de servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-web-service-endpoints.md)|Describe los puntos finales de ejecución y administración del servicio web del servidor de informes.|  
|[Métodos de administración de Namespace de servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-namespace-management-methods.md)|Describe los métodos que puede utilizar para administrar la base de datos del servidor de informes. Específicamente, puede administrar carpetas y recursos y establecer propiedades de elementos.|  
|[Métodos de autorización](../../../reporting-services/report-server-web-service/methods/authorization-methods.md)|Describe métodos que puede utilizar para administrar tareas, roles y directivas.|  
|[Orígenes de datos y métodos de conexión](../../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md)|Describe métodos que puede utilizar para establecer y administrar una conexión a un origen de datos y la información de credenciales para los informes.|  
|[Métodos de parámetros de informe](../../../reporting-services/report-server-web-service/methods/report-parameters-methods.md)|Describe métodos que puede utilizar para establecer y recuperar los parámetros para los informes.|  
|[Métodos del modelo - servicio de Web del servidor de informes](../../../reporting-services/report-server-web-service/methods/model-methods-report-server-web-service.md)|Describe métodos que puede utilizar para administrar los modelos.|  
|[Representación y métodos de ejecución](../../../reporting-services/report-server-web-service/methods/rendering-and-execution-methods.md)|Describe métodos que puede utilizar para administrar la ejecución, representación y almacenamiento en memoria caché de los informes.|  
|[Métodos de historial de informes](../../../reporting-services/report-server-web-service/methods/report-history-methods.md)|Describe métodos que puede utilizar para crear y administrar las instantáneas del historial de informes.|  
|[Métodos de programación](../../../reporting-services/report-server-web-service/methods/scheduling-methods.md)|Describe métodos que puede utilizar para crear y administrar programaciones compartidas y planes de actualización de caché que utiliza el servidor de informes.|  
|[Métodos de suscripción y entrega](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)|Describe métodos que puede utilizar para crear y administrar suscripciones y entrega de informes.|  
|[Métodos de informes vinculados](../../../reporting-services/report-server-web-service/methods/linked-reports-methods.md)|Describe métodos que puede utilizar para crear y administrar los informes vinculados.|  
  
## <a name="see-also"></a>Vea también  
 [Obtener acceso a la API SOAP](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referencia técnica de &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
