---
title: Referencia de la configuración web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ef92aa3410ee12fd5edc4ea602e64a6fa06fdc9c
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65477218"
---
# <a name="web-configuration-reference-master-data-services"></a>Referencia de la configuración web (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa un archivo Web.config para contener la configuración que permite a Internet Information Services (IIS) hospedar la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] y el servicio web. Este archivo Web.config se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información sobre la ruta y los permisos, consulte [Permisos de carpetas y archivos &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos de Web.Config  
 El archivo Web.config contiene un elemento personalizado de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], **\<masterDataServices>**, además de elementos de configuración de Windows Communication Foundation (WCF), IIS estándar, .NET Framework y ASP.NET. En la siguiente tabla se describen los elementos incluidos en el archivo Web.config.  
  
|Elemento de configuración|Descripción|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta el servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento connetionStrings (Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178347) en MSDN Library.|  
|**system.web**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento system.web (Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178348) en MSDN Library.|  
|**startup**|Elemento de .NET Framework. Para más información, vea [\<startup> Element](https://go.microsoft.com/fwlink/?LinkId=178349) (Elemento <startup>) en MSDN Library.|  
|**en tiempo de ejecución**|Elemento de .NET Framework. Para más información, vea [\<runtime> Element](https://go.microsoft.com/fwlink/?LinkId=178350) (Elemento <runtime>) en MSDN Library.|  
|**system.codedom**|Elemento de .NET Framework. Para más información, vea [\<system.codedom> Element](https://go.microsoft.com/fwlink/?LinkId=178351) (Elemento <system.codedom>) en MSDN Library.|  
|**system.web.extensions**|Elemento de ASP.NET. Para obtener más información, consulte [system.web.extensions (Elemento, Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178352) en MSDN Library.|  
|**system.webServer**|Grupo de sección que contiene los elementos IIS. Para obtener más información, consulte [system.webServer Section Group \[IIS 7 Settings Schema\]](https://go.microsoft.com/fwlink/?LinkId=178353) (Grupo de sección system.webServer [esquema de configuración de IIS 7]) en MSDN Library.|  
|**system.serviceModel**|Elemento de WCF. Para más información, vea [\<system.serviceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) en MSDN Library.|  
|**system.diagnostics**|Elemento de .NET Framework. Para más información, vea [\<system.diagnostics> Element](https://go.microsoft.com/fwlink/?LinkId=178355) (Elemento <system.diagnostics>) en MSDN Library.|  
|**appSettings**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento appSetings (Esquema de configuración general)](https://go.microsoft.com/fwlink/?LinkId=178356) en MSDN Library.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 El elemento **\<masterDataServices>** es un elemento personalizado que se usa para conectar un servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
### <a name="syntax"></a>Sintaxis  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Atributos y elementos  
  
|Elemento|Descripción|  
|----------|-----------------|  
|**instancia**|Elemento secundario. Contiene atributos que especifican información para el servicio web y la cadena de conexión a bases de datos.|  
|**virtualPath**|Atributo. Especifica la ruta de acceso virtual de la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Este valor corresponde al atributo **path** del elemento **\<application>** en el elemento **\<site>** del archivo ApplicationHost.config de IIS.|  
|**siteName**|Atributo. Especifica el nombre del sitio que hospeda la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Este valor corresponde al atributo **name** del elemento **\<site>** en el elemento **\<sites>** del archivo ApplicationHost.config de IIS.|  
|**connectionName**|Atributo. Especifica el nombre del administrador de conexiones que se va a usar. Este valor corresponde al atributo **name** del elemento **\<add>** en el elemento **\<connectionStrings>** del archivo Web.config.|  
|**serviceName**|Atributo. Especifica el nombre del servicio web. Este valor corresponde al atributo **name** del elemento **\<service>** en el elemento **\<services>** del archivo Web.config.|  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra un servicio denominado MDS1 en el sitio de Contoso y la ruta de acceso /MDS que usa una cadena de conexión especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
