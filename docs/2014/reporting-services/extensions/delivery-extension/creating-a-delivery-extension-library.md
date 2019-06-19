---
title: Crear una biblioteca de extensiones de entrega | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 133d97cc2d4c04e147d5f4a88c13674429f5c784
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164907"
---
# <a name="creating-a-delivery-extension-library"></a>Crear la biblioteca de una extensión de entrega
  Cada extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que cree debería tener asignado un espacio de nombres único e integrarse en archivo de ensamblado o biblioteca. El nombre exacto del espacio de nombres no es importante, pero debe ser único y no compartirse con ninguna otra extensión. Debería crear sus propios espacios de nombres únicos para las extensiones de entrega de su compañía.  
  
 En el ejemplo siguiente se muestra el código para comenzar una extensión de entrega [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], que utiliza los espacios de nombres que contienen las interfaces de entrega y alguna clase de utilidades.  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 Al compilar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], debe proporcionar al compilador una referencia a Microsoft.ReportingServices.Interfaces.dll, porque allí se encuentran las interfaces de extensión de entrega y las clases. El espacio de nombres <xref:Microsoft.ReportingServices.Interfaces> es necesario para implementar la interfaz <xref:Microsoft.ReportingServices.Interfaces.IExtension>, la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> y más. Por ejemplo, si todos los archivos que contienen el código para implementar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] escrita en C# estuvieran en un único directorio con la extensión .cs, el comando siguiente se ejecutaría desde ese directorio para compilar los archivos almacenados en CompanyName.ExtensionName.dll.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 En el ejemplo de código siguiente se muestra el comando que se usaría para los archivos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] con la extensión .vb.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  También puede diseñar, desarrollar y generar su extensión de entrega mediante [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Para obtener más información sobre cómo desarrollar ensamblados en [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], vea la documentación de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Implementar una extensión de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
