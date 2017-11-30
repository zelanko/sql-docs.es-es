---
title: Acceso a la API de SOAP | Microsoft Docs
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XML Web service [Reporting Services], WSDL
- Web service [Reporting Services], SOAP
- calling Web service
- SOAP [Reporting Services], accessing
- Report Server Web service, SOAP
- Web service [Reporting Services], WSDL
- WSDL [Reporting Services]
- XML Web service [Reporting Services], SOAP
- Report Server Web service, WSDL
- referencing WSDL
ms.assetid: 63bb870a-4dbf-46bd-8921-78f8ebe5fd75
caps.latest.revision: "38"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 9519a04820618fc8f3a59c16b8282b6be1cb0146
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="accessing-the-soap-api"></a>Acceso a la API SOAP
  El servicio web del servidor de informes utiliza el Protocolo simple de acceso a objetos (SOAP) sobre HTTP y actúa como interfaz de comunicaciones entre los programas clientes y el servidor de informes. El servicio web proporciona dos extremos, uno para la ejecución y otro para la administración de informes, y está compuesto de métodos y de un conjunto de objetos de tipo complejo que puede utilizar para tener acceso a la funcionalidad completa de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para llamar al servicio, debe hacer referencia al Lenguaje de descripción de servicios web (WSDL) de Reporting Services.  
  
## <a name="referencing-the-reporting-services-wsdl"></a>Referencia a WSDL de Reporting Services  
 Para llamar correctamente a un servicio web, debe saber cómo tener acceso al mismo, qué operaciones admite, qué parámetros espera y lo que devuelve. WSDL proporciona esta información en un documento XML que un equipo puede leer o procesar.  
  
 Los servicios web del servidor de informes se exponen en tres extremos diferentes. El nombre del archivo WSDL es diferente para cada extremo. El extremo <xref:ReportService2010> contiene métodos para administrar los objetos en un servidor de informes en modo nativo o en modo integrado de SharePoint. El acceso a WSDL para este extremo se realiza a través de `ReportService2010.asmx?wsdl.`.  
  
> [!NOTE]  
>  Los tipos de datos <xref:ReportService2005> y <xref:ReportService2006> están desusados en [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. El extremo <xref:ReportService2010> incluye las funcionalidades de ambos extremos y contiene características de administración adicionales.  
  
-   El extremo <xref:ReportExecution2005> permite a los desarrolladores procesar y representar mediante programación los informes en un servidor de informes. El acceso a WSDL para este punto de conexión se realiza a través de `ReportExecution2005.asmx?wsdl`.  
  
 Los kits de desarrollo que admiten SOAP y servicios web, como el SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], pueden usar el WSDL.  
  
 En el siguiente ejemplo se muestra el formato de la dirección URL del archivo WSDL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
```  
http://server/reportserver/ReportService2010.asmx?wsdl  
```  
  
 En la tabla siguiente se describe cada elemento de la dirección URL.  
  
|Elemento de dirección URL|Description|  
|-----------------|-----------------|  
|*servidor*|Nombre del servidor donde se implementa el servidor de informes.|  
|*servidorDeInformes*|Nombre de la carpeta que contiene el servicio web XML. Se configura durante la instalación.|  
|*\<nombreDelPuntoDeConexión>.asmx*|Nombre del extremo de servicios web.|  
  
 Para obtener más información acerca del formato de WSDL, vea la especificación de WSDL del World Wide Web Consortium (W3C) en http://www.w3.org/TR/wsdl.  
  
## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el servicio web y .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
