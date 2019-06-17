---
title: Elemento HelpLink | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bdd18641663003a1878fe0af0ac1d39a16eda1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046031"
---
# <a name="helplink-element"></a>Elemento HelpLink
  El elemento **HelpLink** de la propiedad **Detail** es una cadena URL que genera el servidor de informes. Las direcciones URL se dirigen a una página web que administra la Ayuda y soporte técnico de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y proporcionan ayuda adicional y artículos de Knowledge Base sobre los errores concretos que se producen en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. La dirección URL tiene la siguiente sintaxis:  
  
 **¿ http://** www.microsoft.com **/** productos **/** ee **/** transform.aspx **? EvtSrc**=_valor_ **& EvtID**=_valor_ **& ProdName** = _valor_ **& ProdVer**=_valor_  
  
 En la tabla siguiente se enumeran los argumentos de la dirección URL **HelpLink**.  
  
|Argumento|Valor|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|Código de error del servidor de informes, por ejemplo, rsReservedItem.|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services". El valor del nombre del producto es la dirección URL codificada.|  
|**ProdVer**|Número de versión de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. El valor "8.00" indica [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
 El ejemplo siguiente ilustra la **HelpLink** dirección URL que se devuelve para el código de error `rsReservedItem`. Este error se produce cuando un usuario intenta modificar o eliminar un elemento reservado en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:  
  
```  
https://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 Puede obtener acceso al elemento **HelpLink** en el código usando la clase **SoapException**.  
  
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
 [Introducción a la administración de excepciones en Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](reporting-services-soapexception-class.md)   
 [Uso de la propiedad Detail para administrar errores concretos](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
