---
title: Dar formato a un archivo de script de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], formats
- formats [Reporting Services], script files
ms.assetid: 85a207dd-4e0f-4d40-a41e-0c75f65d719c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df4585dfa4b1e45b2de9d396a59dcbf132b1a505
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100247"
---
# <a name="format-a-reporting-services-script-file"></a>Dar formato a un archivo de script de Reporting Services
  Un script de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es un archivo de código de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET, escrito frente a un proxy generado en el Lenguaje de descripción de servicios web (WSDL), que define la API de SOAP de Reporting Services. Un archivo de script se almacena como archivo de texto Unicode o UTF-8 con la extensión .rss.  
  
 El archivo de script actúa como módulo [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] y contiene procedimientos definidos por el usuario y variables de nivel de módulo. Para que el archivo de script se ejecute correctamente, debe contener un procedimiento Main. El procedimiento Main es el primer procedimiento al que se tiene acceso cuando se ejecuta su archivo de script. Main es donde puede agregar sus operaciones del servicio web y ejecutar sus subprocedimientos definidos por el usuario. El código siguiente crea un procedimiento Main:  
  
```  
Public Sub Main()  
    ' Your code goes here.  
End Sub  
```  
  
 El entorno de scripts se conecta automáticamente al servidor de informes, crea la clase de proxy web y genera una variable de referencia (*rs*) al objeto proxy del servicio web. Las instrucciones individuales que cree solo tienen que hacer referencia a la variable a nivel del módulo *rs* para realizar cualquiera de las operaciones del servicio web que están disponibles en la biblioteca del servicio web. El código [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] siguiente llama al método <xref:ReportService2010.ReportingService2010.ListChildren%2A> del servicio web desde dentro de un archivo de script:  
  
```  
Public Sub Main()  
    Dim items() As CatalogItem  
    items = rs.ListChildren("/", True)  
  
    Dim item As CatalogItem  
    For Each item In items  
        Console.WriteLine(item.Name)  
    Next item  
End Sub   
```  
  
> [!IMPORTANT]  
>  Las credenciales de usuario se administran por el entorno de script y pasan a través de los argumentos del símbolo del sistema mediante el uso de RS.exe. Aunque puede usar la variable *rs* para establecer la autenticación del servicio web, se recomienda que use el entorno de script. No tiene que autenticar el servicio web en el propio archivo de script. Para más información sobre la autenticación del entorno de scripts, vea [Utilidad RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md).  
  
 No declara espacios de nombres dentro del archivo de script. El entorno de scripting hace que varios útil [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] espacios de nombres disponibles: **System.Web.Services**, **System.Web.Services.Protocols**, **System.Xml**, y **System.IO**.  
  
 Para obtener ejemplos del script, vea [Muestras de productos de SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [servicio web del servidor de informes](../report-server-web-service/report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)   
 [Utilidad RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md)  
  
  
