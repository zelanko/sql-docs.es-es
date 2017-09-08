---
title: Elemento HelpLink | Documentos de Microsoft
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 683da36a3015ee177935823d234968c8486eb51c
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="helplink-element"></a>Elemento HelpLink
  El **HelpLink** elemento de la **detalle** propiedad es una cadena de dirección URL generada por el servidor de informes. Las direcciones URL se dirigen a una página web que administra la Ayuda y soporte técnico de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y proporcionan ayuda adicional y artículos de Knowledge Base sobre los errores concretos que se producen en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. La dirección URL tiene la siguiente sintaxis:  
  
 **http://**www.microsoft.com**/**products**/**ee**/**transform.aspx**? EvtSrc**=v*alue***&EvtID**=*value***&ProdName**=*value***&ProdVer**=*value*  
  
 En la tabla siguiente se enumera los argumentos de la **HelpLink** dirección URL.  
  
|Argumento|Value|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|Código de error del servidor de informes, por ejemplo, rsReservedItem.|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services". El valor del nombre del producto es la dirección URL codificada.|  
|**ProdVer**|Número de versión de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Indica un valor "8.00" [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
 En el ejemplo siguiente se muestra la **HelpLink** dirección URL que se devuelve para el código de error **rsReservedItem**. Este error se produce cuando un usuario intenta modificar o eliminar un elemento reservado en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:  
  
```  
http://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 Puede tener acceso a la **HelpLink** elemento en el código utilizando la **SoapException** clase.  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a control de excepciones en Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Usar la propiedad Detail para administrar errores concretos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
