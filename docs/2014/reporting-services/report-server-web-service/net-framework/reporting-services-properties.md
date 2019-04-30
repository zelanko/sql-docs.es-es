---
title: Propiedades de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 61f1f50ea7a49acc616a36a4eaf1d3d5fcdf269a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63260916"
---
# <a name="reporting-services-properties"></a>Propiedades de Reporting Services
  El servidor de informes define un conjunto de propiedades del sistema que son globales al servidor de informes y un conjunto de propiedades de elementos que están asociadas a un elemento individual almacenado en la base de datos del servidor de informes. Las propiedades definidas por el servidor de informes no se pueden eliminar y en algunos casos son de solo lectura. Una aplicación puede extender las propiedades del sistema y las propiedades de los elementos agregando propiedades definidas por el usuario adicionales a las propiedades de los elementos y del sistema.  
  
 Los métodos de servicio web siguientes recuperan y establecen las propiedades de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Método|Acción|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|Devuelve los valores de una o más propiedades en un elemento de la base de datos del servidor de informes.|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|Devuelve una o más propiedades del sistema.|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|Establece una o varias propiedades de un elemento en la base de datos del servidor de informes.|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|Establece una o más propiedades del sistema.|  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Propiedades de los elementos del servidor de informes](reporting-services-properties-report-server-item-properties.md)|Describe las propiedades específicas del elemento en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Propiedades del sistema del servidor de informes](reporting-services-properties-report-server-system-properties.md)|Describe las propiedades específicas del sistema en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
