---
title: Omitir valores para objetos de servicio web opcionales | Microsoft Docs
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a963fcad77a6c916b4726cf62b0dd09b49d6152f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128867"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>Omitir valores para objetos de servicio web opcionales
  Las propiedades de algunos de los tipos complejos del servicio web del servidor de informes tienen una propiedad acompañante conocida como la propiedad Specified. El nombre de la propiedad está compuesto del nombre de propiedad original con la palabra "Specified" anexada a él. La presencia de esta propiedad indica que en ocasiones se puede omitir un valor para la propiedad original. Éste es un resultado directo de la traducción del lenguaje de descripción de servicios web (WSDL) a una clase de proxy [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Por ejemplo, la propiedad del servicio web <xref:ReportService2010.DataSourceDefinition.Enabled%2A> del tipo complejo <xref:ReportService2010.DataSourceDefinition> tiene una propiedad acompañante denominada <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. Si está generando una aplicación y no quiere establecer un valor para la propiedad <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, no tiene que proporcionar un valor para <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; se utiliza el valor predeterminado **true**. Aun así debe establecer <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> en **false**. Si proporciona un valor para la propiedad <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, debe establecer <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> también en **true**. Éste es el caso para las propiedades en que se puede escribir. Para las propiedades de solo lectura, no necesita tomar ninguna medida.  
  
> [!IMPORTANT]  
>  El error para especificar una propiedad mediante la técnica mencionada anteriormente puede producir un comportamiento del servicio web imprevisible.  
  
 Los tipos de datos que normalmente le exigen que administre la propiedad Specified adicional son **Boolean**, **DateTime** y **Enumeration**.  
  
 Para obtener un ejemplo, vea el método <xref:ReportService2010.ReportingService2010.CreateDataSource%2A>.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
