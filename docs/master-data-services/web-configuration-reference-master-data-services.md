---
title: "Web de referencia de configuración (Master Data Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1be0e90d7d2ba9b2751677015957ca249d91119e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="web-configuration-reference-master-data-services"></a>Referencia de la configuración web (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]utiliza un archivo Web.config para contener los valores de configuración que permiten a los servicios de Internet Information Server (IIS) hospedar la [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] aplicación Web y el servicio Web. Este archivo Web.config se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información sobre la ruta y los permisos, consulte [Permisos de carpetas y archivos &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos de Web.Config  
 El archivo Web.config contiene un personalizado [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] elemento,  **\<masterDataServices >**, además de los elementos de configuración de IIS, .NET Framework, ASP.NET y Windows Communication Foundation (WCF) estándar. En la siguiente tabla se describen los elementos incluidos en el archivo Web.config.  
  
|Elemento de configuración|Description|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta el servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento connetionStrings (Esquema de configuración de ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178347) en MSDN Library.|  
|**system.web**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento system.web (Esquema de configuración de ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178348) en MSDN Library.|  
|**startup**|Elemento de .NET Framework. Para obtener más información, consulte [ \<Inicio > elemento](http://go.microsoft.com/fwlink/?LinkId=178349) en MSDN Library.|  
|**en tiempo de ejecución**|Elemento de .NET Framework. Para obtener más información, consulte [ \<en tiempo de ejecución > elemento](http://go.microsoft.com/fwlink/?LinkId=178350) en MSDN Library.|  
|**system.codedom**|Elemento de .NET Framework. Para obtener más información, consulte [ \<system.codedom > elemento](http://go.microsoft.com/fwlink/?LinkId=178351) en MSDN Library.|  
|**system.web.extensions**|Elemento de ASP.NET. Para obtener más información, consulte [system.web.extensions (Elemento, Esquema de configuración de ASP.NET)](http://go.microsoft.com/fwlink/?LinkId=178352) en MSDN Library.|  
|**system.webServer**|Grupo de sección que contiene los elementos IIS. Para obtener más información, consulte [system.webServer Section Group \[IIS 7 Settings Schema\]](http://go.microsoft.com/fwlink/?LinkId=178353) (Grupo de sección system.webServer [esquema de configuración de IIS 7]) en MSDN Library.|  
|**system.serviceModel**|Elemento de WCF. Para obtener más información, consulte [ \<system.serviceModel >](http://go.microsoft.com/fwlink/?LinkId=178354) en MSDN Library.|  
|**system.diagnostics**|Elemento de .NET Framework. Para obtener más información, consulte [ \<system.diagnostics > elemento](http://go.microsoft.com/fwlink/?LinkId=178355) en MSDN Library.|  
|**appSettings**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento appSetings (Esquema de configuración general)](http://go.microsoft.com/fwlink/?LinkId=178356) en MSDN Library.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 El  **\<masterDataServices >** trata de un elemento personalizado que se utiliza para conectar un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web servicio a un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos.  
  
### <a name="syntax"></a>Sintaxis  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Atributos y elementos  
  
|Elemento|Description|  
|----------|-----------------|  
|**instancia**|Elemento secundario. Contiene atributos que especifican información para el servicio web y la cadena de conexión a bases de datos.|  
|**virtualPath**|Atributo. Especifica la ruta de acceso virtual de la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esto corresponde a la **ruta de acceso** atributo de la  **\<aplicación >** elemento bajo el  **\<sitio >** elemento en el archivo ApplicationHost.config de IIS.|  
|**siteName**|Atributo. Especifica el nombre del sitio que hospeda la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esto corresponde a la **nombre** atributo de la  **\<sitio >** elemento bajo  **\<sitios >** en el archivo ApplicationHost.config de IIS.|  
|**connectionName**|Atributo. Especifica el nombre del administrador de conexiones que se va a usar. Esto corresponde a la **nombre** atributo de la  **\<Agregar >** elemento bajo el  **\<connectionStrings >** elemento en el archivo Web.config.|  
|**serviceName**|Atributo. Especifica el nombre del servicio web. Esto corresponde a la **nombre** atributo de la  **\<servicio >** elemento bajo el  **\<services >** elemento en el archivo Web.config.|  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra un servicio denominado MDS1 en el sitio de Contoso y la ruta de acceso /MDS que usa una cadena de conexión especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
