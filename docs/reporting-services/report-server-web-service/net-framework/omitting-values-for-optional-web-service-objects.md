---
title: Omitiendo los valores de objetos de servicio Web opcionales | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 3532a470bd036e0128a8df21ca391210cf7209a2
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="omitting-values-for-optional-web-service-objects"></a>Omitir valores para objetos de servicio web opcionales
  Las propiedades de algunos de los tipos complejos del servicio Web del servidor de informes tienen una propiedad acompañante conocida como la propiedad especificada. El nombre de la propiedad está compuesto del nombre de propiedad original con la palabra "Specified" anexada a él. La presencia de esta propiedad indica que en ocasiones se puede omitir un valor para la propiedad original. Éste es un resultado directo de la traducción del lenguaje de descripción de servicios web (WSDL) a una clase de proxy [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Por ejemplo, la propiedad del servicio web <xref:ReportService2010.DataSourceDefinition.Enabled%2A> del tipo complejo <xref:ReportService2010.DataSourceDefinition> tiene una propiedad acompañante denominada <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. Si está compilando una aplicación y no desea establecer un valor para el <xref:ReportService2010.DataSourceDefinition.Enabled%2A> propiedad, no es necesario proporcionar un valor para <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; el valor predeterminado de **true** se utiliza. Sin embargo, todavía debe establecer <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> a **false**. Si proporciona un valor para el <xref:ReportService2010.DataSourceDefinition.Enabled%2A> propiedad, es necesario establecer <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> igual a **true**. Éste es el caso para las propiedades en que se puede escribir. Para las propiedades de solo lectura, no necesita tomar ninguna medida.  
  
> [!IMPORTANT]  
>  El error para especificar una propiedad mediante la técnica mencionada anteriormente puede producir un comportamiento del servicio web imprevisible.  
  
 Los tipos de datos que normalmente exigen que administre la propiedad especificada adicional son **booleano**, **DateTime**, y **enumeración**.  
  
 Para obtener un ejemplo, vea el método <xref:ReportService2010.ReportingService2010.CreateDataSource%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referencia técnica de &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

