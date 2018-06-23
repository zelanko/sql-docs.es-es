---
title: Utilizar los encabezados SOAP de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: 38
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e7dbac29f2bfa4a61c9d5c6cfe955d1f07a11189
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103038"
---
# <a name="using-reporting-services-soap-headers"></a>Utilizar los encabezados SOAP de Reporting Services
  La comunicación con un método de servicio web utilizando SOAP sigue un formato estándar. Parte de este formato son los datos que están codificados en un documento XML. El documento XML está compuesto de un elemento raíz **Envelope**, que a su vez está compuesto de un elemento **Body** necesario y un elemento **Header** opcional. El elemento **Body** contiene los datos específicos del mensaje. El elemento **Header** opcional puede contener información adicional no relacionada directamente con el mensaje determinado. Cada elemento secundario del elemento **Header** se denomina un encabezado SOAP.  
  
 Aunque los encabezados SOAP pueden contener datos relacionados con el mensaje, normalmente contienen información procesada por la infraestructura del servidor web.  
  
 Los servicios web del servidor de informes definen varias clases para usarlas en el encabezado SOAP: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> y <xref:ReportExecution2005.ExecutionHeader>.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Métodos de procesamiento por lotes](batching-methods.md)|Describe cómo crear un lote de varias operaciones en una única transacción utilizando <xref:ReportService2005.BatchHeader>.|  
|[Identificación del estado de ejecución](identifying-execution-state.md)|Describe cómo administrar el estado de sesión en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante **SessionHeader**.|  
|[Establecimiento del espacio de nombres de elemento para el método GetProperties](setting-the-item-namespace-for-the-getproperties-method.md)|Describe cómo recuperar las propiedades basándose en la ruta o el Id. de un elemento utilizando el método <xref:ReportService2010.ReportingService2010.GetProperties%2A> y el encabezado SOAP <xref:ReportService2010.ItemNamespaceHeader>.|  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referencia técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  