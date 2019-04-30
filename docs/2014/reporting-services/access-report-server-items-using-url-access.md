---
title: Obtener acceso a elementos del servidor de informes mediante acceso URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a345cd609c4cfd79f9e93a2b63e71bbddde36ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233567"
---
# <a name="access-report-server-items-using-url-access"></a>Acceso a elementos del servidor de informes mediante acceso URL
  Este tema describe cómo acceder a los elementos del catálogo de diferentes tipos en un informe de datos del servidor de base o en un sitio de SharePoint mediante *rs: Command*=*valor*.  
  
 No es necesario agregar esta cadena de parámetro. Si se omite, el servidor de informes evalúa el tipo de elemento y selecciona automáticamente el valor del parámetro correspondiente. Sin embargo, mediante la *rs: Command*=*valor* cadena en la dirección URL mejora el rendimiento del servidor de informes.  
  
 Tenga en cuenta el `_vti_bin` sintaxis de proxy en los ejemplos siguientes. Para obtener más información sobre el uso de la sintaxis de proxy, consulte [URL Access Parameter Reference](url-access-parameter-reference.md).  
  
## <a name="access-a-report"></a>Obtener acceso a un informe  
 Para ver un informe en el explorador, use el *rs: Command*=*representar* parámetro. Por ejemplo:  
  
 `Native` `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  Es importante incluir la dirección URL de la `_vti_bin` sintaxis de proxy para enrutar la solicitud a través de SharePoint y el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proxy HTTP. El proxy agrega algún contexto a la solicitud HTTP, contexto que es necesario para garantizar la correcta ejecución del informe para los servidores de informes de modo de SharePoint.  
  
## <a name="access-a-resource"></a>Acceso a un recurso  
 Para obtener acceso a un recurso, use el *rs: Command*=*GetResourceContents* parámetro. Si el recurso es compatible con el explorador, como una imagen, se abre en el explorador. En caso contrario, se le pedirá que abra o guarde el archivo o recurso en el disco.  
  
 `Native` `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>Obtener acceso a un origen de datos  
 Para obtener acceso a un origen de datos, utilice el *rs: Command*=*GetDataSourceContents* parámetro. Si el explorador admite código XML, se muestra la definición del origen de datos si es un usuario autenticado con `Read Contents` permiso en el origen de datos. Por ejemplo:  
  
 `Native` `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 La estructura XML podría ser similar al ejemplo siguiente:  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 La cadena de conexión se devuelve en función de la **SecureConnectionLevel** configuración del servidor de informes. Para obtener más información sobre la **SecureConnectionLevel** , vea [Using Secure Web Service Methods](report-server-web-service/net-framework/using-secure-web-service-methods.md).  
  
## <a name="access-the-contents-of-a-folder"></a>Acceso al contenido de una carpeta  
 Para obtener acceso al contenido de una carpeta, use el *rs: Command*=*GetChildren* parámetro. Se devuelve una página de navegación por carpetas genérica que contiene vínculos a las subcarpetas, informes, orígenes de datos y recursos en la carpeta solicitada. Por ejemplo:  
  
 `Native` `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 La interfaz de usuario que aparece es similar al utilizado por el modo de exploración de directorios [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS). El número de versión, incluido el número de compilación del servidor de informes también se muestra debajo de la lista de carpetas.  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
  
