---
title: Acceso a la API de SOAP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab8db976275a60cfbf1e0afb78457afad18fc366
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63012257"
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
  
|Elemento de dirección URL|Descripción|  
|-----------------|-----------------|  
|*servidor*|Nombre del servidor donde se implementa el servidor de informes.|  
|*servidorDeInformes*|Nombre de la carpeta que contiene el servicio web XML. Se configura durante la instalación.|  
|*\<nombreDelPuntoDeConexión>.asmx*|Nombre del extremo de servicios web.|  
  
 Para más información acerca del formato de WSDL, consulte la especificación de WSDL del World Wide Web Consortium (W3C) en http://www.w3.org/TR/wsdl.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](report-server-web-service.md)  
  
  
