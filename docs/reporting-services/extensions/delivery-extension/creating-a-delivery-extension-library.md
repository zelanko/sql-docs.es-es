---
title: "Crear una biblioteca de extensión de entrega | Documentos de Microsoft"
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
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bcfb5b69df148108531e9e5b843f127af0e3fbb4
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

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
  
 Al compilar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], debe proporcionar al compilador una referencia a Microsoft.ReportingServices.Interfaces.dll, porque allí se encuentran las interfaces de extensión de entrega y las clases. El espacio de nombres <xref:Microsoft.ReportingServices.Interfaces> es necesario para implementar la interfaz <xref:Microsoft.ReportingServices.Interfaces.IExtension>, la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> y más. Por ejemplo, si todos los archivos que contienen el código para implementar un [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de entrega que se escriben en C# estuvieran en un único directorio con la extensión. cs, el comando siguiente se ejecutaría desde ese directorio para compilar los archivos almacenados en CompanyName.ExtensionName.dll.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 En el ejemplo de código siguiente se muestra el comando que se usaría para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] archivos con la extensión. vb.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  También puede diseñar, desarrollar y generar su extensión de entrega mediante [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Para obtener más información sobre cómo desarrollar ensamblados en [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], vea la documentación de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

