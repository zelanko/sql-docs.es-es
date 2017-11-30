---
title: Validar los permisos en ensamblados personalizados | Microsoft Docs
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
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: dc3e6e84c3f0a70a3c794b5cfd803e228e5dcce0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="asserting-permissions-in-custom-assemblies"></a>Validar los permisos en ensamblados personalizados
  De forma predeterminada, el código de ensamblado personalizado se ejecuta con el conjunto de permisos de **Ejecución** limitado. En algunos casos, puede desear implementar un ensamblado personalizado que realice llamadas protegidas a los recursos protegidos dentro del sistema de seguridad (como un archivo o el Registro). Para ello, debe hacer lo siguiente:  
  
1.  Identifique los permisos exactos que el código necesita para realizar la llamada segura. Si este método forma parte de una biblioteca de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], esta información debe incluirse en la documentación del método.  
  
2.  Modifique los archivos de configuración de directiva de servidor de informes para conceder los permisos necesarios al ensamblado personalizado. Para más información sobre los archivos de configuración de directivas de seguridad, vea [Usar los archivos de directivas de seguridad de Reporting Services](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
3.  Valide los permisos necesarios como parte del método en el que se realiza la llamada segura. Esto es necesario porque el código de ensamblado personalizado al que llama el servidor de informes forma parte del ensamblado de expresiones del informe, que se ejecuta de forma predeterminada con el permiso de **Ejecución**. El conjunto de permisos de **Ejecución** permite la ejecución del código, pero no usar recursos protegidos.  
  
4.  Marque el ensamblado personalizado con **AllowPartiallyTrustedCallersAttribute** si está firmado con un nombre seguro. Esto es necesario porque a los ensamblados personalizados se les llama desde una expresión de informe que forma parte del ensamblado de expresiones del informe, al que, de forma predeterminada, no se le concede **FullTrust**; por tanto, realiza las llamadas de forma "parcialmente confiable". Para más información, vea [Usar ensamblados personalizados con nombre seguro](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md).  
  
## <a name="implementing-a-secure-call"></a>Implementar una llamada segura  
 Puede modificar los archivos de configuración de directiva para conceder permisos concretos al ensamblado. Por ejemplo, si estuviera escribiendo un ensamblado personalizado para administrar la conversión de moneda, podría necesitar leer las tasas de cambio de moneda actuales de un archivo. Para recuperar la información de la tasa, necesitaría agregar un permiso de seguridad adicional, **FileIOPermission**, al conjunto de permisos del ensamblado. Puede realizar la entrada adicional siguiente en el archivo de configuración de directiva:  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 A continuación, agrega un grupo de código que hace referencia a ese conjunto de permisos:  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 Para que el código adquiera el permiso adecuado, debe validar el permiso dentro del código de ensamblado personalizado. Por ejemplo, si desea agregar acceso de solo lectura a un archivo XML, C:\CurrencyRates.xml, debe agregar el código siguiente al método:  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 También puede agregar la aserción como un atributo de método:  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 Para obtener más información, vea el tema sobre la seguridad de .NET Framework en la Guía del programador de .NET Framework.  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
