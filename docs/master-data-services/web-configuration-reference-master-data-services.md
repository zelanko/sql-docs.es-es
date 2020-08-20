---
description: Referencia de la configuración web (Master Data Services)
title: Referencia de la configuración web
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
ms.openlocfilehash: 34e3e849a86cb23c3974b32b9d3d8c0721601274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456769"
---
# <a name="web-configuration-reference-master-data-services"></a>Referencia de la configuración web (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa un archivo Web.config para contener la configuración que permite a Internet Information Services (IIS) hospedar la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] y el servicio web. Este archivo Web.config se encuentra en la carpeta WebApplication de la ruta de instalación de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información sobre la ruta y los permisos, consulte [Permisos de carpetas y archivos &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementos de Web.Config  
 El archivo de Web.config contiene un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] elemento personalizado, **\<masterDataServices>** , además de los elementos de configuración de IIS estándar, .NET Framework, ASP.NET y Windows Communication Foundation (WCF). En la siguiente tabla se describen los elementos incluidos en el archivo Web.config.  
  
|Elemento de configuración|Descripción|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento personalizado. Conecta el servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento connetionStrings (Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178347) en MSDN Library.|  
|**System. Web**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento system.web (Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178348) en MSDN Library.|  
|**Inicio**|Elemento de .NET Framework. Para obtener más información, vea el [ \<startup> elemento](https://go.microsoft.com/fwlink/?LinkId=178349) en MSDN Library.|  
|**Runtime**|Elemento de .NET Framework. Para obtener más información, vea el [ \<runtime> elemento](https://go.microsoft.com/fwlink/?LinkId=178350) en MSDN Library.|  
|**system.codedom**|Elemento de .NET Framework. Para obtener más información, vea el [ \<system.codedom> elemento](https://go.microsoft.com/fwlink/?LinkId=178351) en MSDN Library.|  
|**System. Web. Extensions**|Elemento de ASP.NET. Para obtener más información, consulte [system.web.extensions (Elemento, Esquema de configuración de ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178352) en MSDN Library.|  
|**system.webServer**|Grupo de sección que contiene los elementos IIS. Para obtener más información, consulte [system.webServer Section Group \[IIS 7 Settings Schema\]](https://go.microsoft.com/fwlink/?LinkId=178353) (Grupo de sección system.webServer [esquema de configuración de IIS 7]) en MSDN Library.|  
|**system.serviceModel**|Elemento de WCF. Para obtener más información, vea [\<system.serviceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) en MSDN Library.|  
|**system.diagnostics**|Elemento de .NET Framework. Para obtener más información, vea el [ \<system.diagnostics> elemento](https://go.microsoft.com/fwlink/?LinkId=178355) en MSDN Library.|  
|**appSettings**|Elemento de ASP.NET. Para obtener más información, consulte [Elemento appSetings (Esquema de configuración general)](https://go.microsoft.com/fwlink/?LinkId=178356) en MSDN Library.|  
  
## <a name="masterdataservices-element"></a>Elemento masterDataServices  
 El **\<masterDataServices>** elemento es un elemento personalizado que se utiliza para conectar un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] servicio Web a una [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos.  
  
### <a name="syntax"></a>Sintaxis  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Atributos y elementos  
  
|Elemento|Descripción|  
|----------|-----------------|  
|**instance**|Elemento secundario. Contiene atributos que especifican información para el servicio web y la cadena de conexión a bases de datos.|  
|**virtualPath**|Atributo. Especifica la ruta de acceso virtual de la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esto corresponde al atributo **path** del **\<application>** elemento bajo el **\<site>** elemento en el archivo de ApplicationHost.config de IIS.|  
|**Nombresitio**|Atributo. Especifica el nombre del sitio que hospeda la aplicación web y servicio de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Esto corresponde al atributo **Name** del elemento de **\<site>** **\<sites>** en el archivo de ApplicationHost.config de IIS.|  
|**connectionName**|Atributo. Especifica el nombre del administrador de conexiones que se va a usar. Esto corresponde al atributo **Name** del **\<add>** elemento bajo el **\<connectionStrings>** elemento de Web.config.|  
|**serviceName**|Atributo. Especifica el nombre del servicio web. Esto corresponde al atributo **Name** del **\<service>** elemento bajo el **\<services>** elemento de Web.config.|  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra un servicio denominado MDS1 en el sitio de Contoso y la ruta de acceso /MDS que usa una cadena de conexión especificada por MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
