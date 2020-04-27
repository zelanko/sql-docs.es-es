---
title: Referencia de la configuración web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ee3582e7de37b99cd7f665f563e789259954b722
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478481"
---
# <a name="web-configuration-reference-master-data-services"></a>Referencia de la configuración web (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa un archivo Web.config para contener la configuración que permite a Internet Information Services (IIS) hospedar la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] y el servicio web. Este archivo Web.config se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información sobre la ruta y los permisos, consulte [Permisos de carpetas y archivos &#40;Master Data Services&#41;](folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos de Web.Config  
 El archivo Web. config contiene un elemento [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] personalizado, ** \<masterDataServices>**, además de los elementos de configuración de IIS estándar, .NET Framework, ASP.net y Windows Communication Foundation (WCF). En la siguiente tabla se describen los elementos incluidos en el archivo Web.config.  
  
|Elemento de configuración|Descripción|  
|---------------------------|-----------------|  
|`masterDataServices`|Elemento personalizado. Conecta el servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|`connectionStrings`|Elemento de ASP.NET. Para obtener más información, consulte [Elemento connetionStrings (Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178347) en MSDN Library.|  
|`system.web`|Elemento de ASP.NET. Para obtener más información, consulte [Elemento system.web (Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178348) en MSDN Library.|  
|`startup`|Elemento de .NET Framework. Para obtener más información, vea [ \<startup> elemento](https://go.microsoft.com/fwlink/?LinkId=178349) en MSDN Library.|  
|`runtime`|Elemento de .NET Framework. Para obtener más información, vea [ \<elemento> en tiempo de ejecución](https://go.microsoft.com/fwlink/?LinkId=178350) en MSDN Library.|  
|`system.codedom`|Elemento de .NET Framework. Para obtener más información, vea [ \<elemento System. CodeDom>](https://go.microsoft.com/fwlink/?LinkId=178351) en MSDN Library.|  
|`system.web.extensions`|Elemento de ASP.NET. Para obtener más información, consulte [system.web.extensions (Elemento, Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178352) en MSDN Library.|  
|`system.webServer`|Grupo de sección que contiene los elementos IIS. Para obtener más información, consulte [system.webServer Section Group \[IIS 7 Settings Schema\]](https://go.microsoft.com/fwlink/?LinkId=178353) (Grupo de sección system.webServer [esquema de configuración de IIS 7]) en MSDN Library.|  
|`system.serviceModel`|Elemento de WCF. Para obtener más información, vea [ \<System. ServiceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) en MSDN Library.|  
|`system.diagnostics`|Elemento de .NET Framework. Para obtener más información, vea [ \<elemento System. Diagnostics>](https://go.microsoft.com/fwlink/?LinkId=178355) en MSDN Library.|  
|`appSettings`|Elemento de ASP.NET. Para obtener más información, consulte [Elemento appSetings (Esquema de configuración general)](https://go.microsoft.com/fwlink/?LinkId=178356) en MSDN Library.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 El ** \<elemento>masterDataServices** es un elemento personalizado que se usa para conectar un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] servicio Web a una [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos.  
  
### <a name="syntax"></a>Sintaxis  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Atributos y elementos  
  
|Elemento|Descripción|  
|----------|-----------------|  
|`instance`|Elemento secundario. Contiene atributos que especifican información para el servicio web y la cadena de conexión a bases de datos.|  
|`virtualPath`|Atributo. Especifica la ruta de acceso virtual de la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esto corresponde al `path` atributo del elemento ** \<Application>** en el ** \<elemento>del sitio** en el archivo ApplicationHost. config de IIS.|  
|`siteName`|Atributo. Especifica el nombre del sitio que hospeda la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esto corresponde al `name` atributo del elemento>del ** \<sitio** en ** \<sitios>** en el archivo ApplicationHost. config de IIS.|  
|`connectionName`|Atributo. Especifica el nombre del administrador de conexiones que se va a usar. Esto corresponde al `name` atributo del elemento ** \<Add>** bajo el ** \<elemento connectionStrings>** en Web. config.|  
|`serviceName`|Atributo. Especifica el nombre del servicio web. Esto corresponde al `name` atributo del elemento>del ** \<servicio** en el ** \<elemento>de servicios** de Web. config.|  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra un servicio denominado MDS1 en el sitio de Contoso y la ruta de acceso /MDS que usa una cadena de conexión especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
