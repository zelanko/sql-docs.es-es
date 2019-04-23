---
title: Métodos de servicio web del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37d0031ebfb4ec6d31da6aad9a8842c0623cb75b
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158241"
---
# <a name="report-server-web-service-methods"></a>Métodos de servicio web del servidor de informes
  Los servicios web del servidor de informes incluyen varias categorías de métodos que están basados en las características de componente. Estos métodos se proporcionan a través de varios extremos de servicios web (tres para la administración de informes y uno para la ejecución de informes) que se exponen como miembros de las clases <xref:ReportService2010.ReportingService2010> y <xref:ReportExecution2005.ReportExecutionService>. Estas clases se pueden generar a través de una herramienta de clase de proxy como wsdl.exe, que está incluida con el SDK de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Para más información sobre los servicios web del servidor de informes y [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], vea [Generar aplicaciones mediante el servicio web y .NET Framework](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
## <a name="endpoints-and-methods"></a>Puntos finales y métodos  
 En la tabla siguiente se muestra una lista de extremos del servicio web del servidor de informes, así como las categorías de los métodos proporcionadas por el extremo <xref:ReportService2010.ReportingService2010>. Para obtener información sobre los métodos disponibles en los demás puntos de conexión, vea [Referencia técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md).  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Puntos de conexión del servicio web del servidor de informes](report-server-web-service-endpoints.md)|Describe los puntos finales de ejecución y administración del servicio web del servidor de informes.|  
|[Métodos de administración de los espacios de nombres del servidor de informes](report-server-namespace-management-methods.md)|Describe los métodos que puede utilizar para administrar la base de datos del servidor de informes. Específicamente, puede administrar carpetas y recursos y establecer propiedades de elementos.|  
|[Métodos de autorización](authorization-methods.md)|Describe métodos que puede utilizar para administrar tareas, roles y directivas.|  
|[Orígenes de datos y métodos de conexión](data-sources-and-connection-methods.md)|Describe métodos que puede utilizar para establecer y administrar una conexión a un origen de datos y la información de credenciales para los informes.|  
|[Métodos de parámetros de informes](report-parameters-methods.md)|Describe métodos que puede utilizar para establecer y recuperar los parámetros para los informes.|  
|[Métodos de modelo](../report-server-web-service.md)|Describe métodos que puede utilizar para administrar los modelos.|  
|[Métodos de representación y ejecución](rendering-and-execution-methods.md)|Describe métodos que puede utilizar para administrar la ejecución, representación y almacenamiento en memoria caché de los informes.|  
|[Métodos de historial de informes](report-history-methods.md)|Describe métodos que puede utilizar para crear y administrar las instantáneas del historial de informes.|  
|[Métodos de programación](scheduling-methods.md)|Describe métodos que puede utilizar para crear y administrar programaciones compartidas y planes de actualización de caché que utiliza el servidor de informes.|  
|[Métodos de suscripción y entrega](subscription-and-delivery-methods.md)|Describe métodos que puede utilizar para crear y administrar suscripciones y entrega de informes.|  
|[Métodos de informes vinculados](linked-reports-methods.md)|Describe métodos que puede utilizar para crear y administrar los informes vinculados.|  
  
## <a name="see-also"></a>Vea también  
 [Acceso a la API de SOAP](../accessing-the-soap-api.md)   
 [Creación de aplicaciones con el servicio web y .NET Framework](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
