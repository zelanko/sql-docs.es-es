---
title: Usar Reporting Services encabezados SOAP | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: 39
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 79f67a1d6e982aa9b83fcc5bf4c043eb378478d1
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="using-reporting-services-soap-headers"></a>Utilizar los encabezados SOAP de Reporting Services
  La comunicación con un método de servicio web utilizando SOAP sigue un formato estándar. Parte de este formato son los datos que están codificados en un documento XML. El documento XML consta de una raíz **sobres** elemento, que a su vez consta de una opción necesaria **cuerpo** elemento y un elemento opcional **encabezado** elemento. El **cuerpo** elemento contiene los datos específicos del mensaje. Opcional **encabezado** elemento puede contener información adicional no relacionada directamente con el mensaje determinado. Cada elemento secundario de la **encabezado** elemento se denomina un encabezado SOAP.  
  
 Aunque los encabezados SOAP pueden contener datos relacionados con el mensaje, normalmente contienen información procesada por la infraestructura del servidor web.  
  
 Los servicios web del servidor de informes definen varias clases para usarlas en el encabezado SOAP: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> y <xref:ReportExecution2005.ExecutionHeader>.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Métodos de procesamiento por lotes](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|Describe cómo crear un lote de varias operaciones en una única transacción utilizando <xref:ReportService2005.BatchHeader>.|  
|[Identificar el estado de ejecución](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|Describe cómo administrar el estado de sesión en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con **SessionHeader**.|  
|[Establecer el Namespace de elemento para el método GetProperties](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|Describe cómo recuperar las propiedades basándose en la ruta o el Id. de un elemento utilizando el método <xref:ReportService2010.ReportingService2010.GetProperties%2A> y el encabezado SOAP <xref:ReportService2010.ItemNamespaceHeader>.|  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referencia técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
