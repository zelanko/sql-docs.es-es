---
title: Administrar las advertencias y casos que no producen excepciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], warnings that don't cause
- warnings [Reporting Services]
ms.assetid: 475c0713-6265-44e7-9ebc-ebdd1b89e0af
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 491a461dab0cf89d4e314f24e91da5b3aa7a6026
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022377"
---
# <a name="handling-warnings-and-cases-that-do-not-cause-exceptions"></a>Administrar las advertencias y casos que no producen excepciones
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no genera excepciones para las advertencias y ciertos errores. Por ejemplo, al utilizar el método <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> para publicar un nuevo informe en un servidor de informes, cualquier advertencia que se produzca se devuelve como una matriz de objetos <xref:ReportService2010.Warning>. Estas advertencias se deberían administrar y mostrar para que se puedan tomar las medidas adecuadas.  
  
```vb  
Try  
   rs.CreateCatalogItem(name, parentFolder, False, definition, Nothing, warnings)  
  
   If Not (warnings.Length = 0) Then  
      Dim warning As Warning  
      For Each warning In warnings  
         Console.WriteLine(warning.Message)  
      Next warning  
   Else  
      Console.WriteLine("Report {0} created successfully with no warnings", name)  
   End If  
  
Catch ex As SoapException  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.CreateCatalogItem("Report", name, parentFolder, false, definition, null, out warnings);  
  
   if (warnings.Length != 0)  
   {  
      foreach (Warning warning in warnings)  
      {  
         Console.WriteLine(warning.Message);  
      }  
   }  
   else  
      Console.WriteLine("Report {0} created successfully with no warnings", name);  
}  
  
catch (SoapException ex)  
{  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
 Otra manera de administrar los errores es evaluar los valores que devuelven ciertos métodos. Por ejemplo, el método <xref:ReportService2010.ReportingService2010.FindItems%2A> se puede utilizar para buscar los elementos específicos en la base de datos del servidor de informes. Si no se encuentra ningún elemento que coincida con el criterio de búsqueda, se devuelve una matriz NULL de los objetos <xref:ReportService2010.CatalogItem>. Debería evaluar la matriz, comprobar si es `null` y permitir que el usuario sepa si no se encontró ningún elemento.  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportService2010.CatalogItem>   
 [Introducción a la administración de excepciones en Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
