---
title: Omitir valores para objetos de servicio web opcionales | Microsoft Docs
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
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3713e1e401133e8a272e80f2b4060493aa405440
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294075"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>Omitir valores para objetos de servicio web opcionales
  Las propiedades de algunos de los tipos complejos del servicio web del servidor de informes tienen una propiedad acompañante conocida como la propiedad Specified. El nombre de la propiedad está compuesto del nombre de propiedad original con la palabra "Specified" anexada a él. La presencia de esta propiedad indica que en ocasiones se puede omitir un valor para la propiedad original. Éste es un resultado directo de la traducción del lenguaje de descripción de servicios web (WSDL) a una clase de proxy [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Por ejemplo, la propiedad del servicio web <xref:ReportService2010.DataSourceDefinition.Enabled%2A> del tipo complejo <xref:ReportService2010.DataSourceDefinition> tiene una propiedad acompañante denominada <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. Si está generando una aplicación y no desea establecer un valor para la propiedad <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, no tiene que proporcionar un valor para <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; se utiliza el valor predeterminado `true`. Sin embargo, todavía necesita establecer <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> en `false`. Si proporciona un valor para la propiedad <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, debe establecer <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> igual a `true`. Éste es el caso para las propiedades en que se puede escribir. Para las propiedades de solo lectura, no necesita tomar ninguna medida.  
  
> [!IMPORTANT]  
>  El error para especificar una propiedad mediante la técnica mencionada anteriormente puede producir un comportamiento del servicio web imprevisible.  
  
 Los tipos de datos que normalmente exigen que administre la propiedad Specified adicional son `Boolean`, `DateTime`, y `Enumeration`.  
  
 Para obtener un ejemplo, vea el método <xref:ReportService2010.ReportingService2010.CreateDataSource%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referencia técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
