---
title: "Detectar componentes de flujo de datos mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PipelineComponentInfos collection
- data flow task [Integration Services], components
- discovering data flow components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: ff92a96a-8af6-4532-82cc-c0bbff92401b
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 78090618d5025a6ab29c888d09db44ddfff278fa
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="discovering-data-flow-components-programmatically"></a>Detectar componentes de flujo de datos mediante programación
  Una vez que se ha agregado una tarea de flujo de datos a un paquete, el siguiente paso puede ser determinar los componentes de flujo de datos que están disponibles para su uso. Puede detectar mediante programación los orígenes del flujo de datos, transformaciones y destinos que están instalados y disponibles en el equipo local. Para obtener información acerca de cómo agregar una tarea de flujo de datos para el paquete, consulte [agregar los datos de flujo de tareas mediante programación](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md).  
  
## <a name="discovering-components"></a>Detectar componentes  
 La clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> proporciona la colección <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A>, que contiene un objeto <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> para cada componente instalado correctamente en el equipo local. Cada <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> contiene información acerca de un componente como su nombre, descripción y nombre de creación. Puede usar el valor devuelto en la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> para establecer la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> de <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> cuando agrega un componente a un paquete.  
  
## <a name="next-step"></a>Paso siguiente  
 Después de detectar los componentes disponibles, el paso siguiente es agregar y configurar los componentes, que se describe en el tema siguiente, [agregar datos de flujo de componentes mediante programación](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md).  
  
## <a name="sample"></a>Ejemplo  
 En el siguiente ejemplo de código se muestra cómo enumerar la colección <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfos> del objeto <xref:Microsoft.SqlServer.Dts.Runtime.Application> para detectar mediante programación los componentes de flujo de datos disponibles en el equipo local. Este ejemplo requiere una referencia al ensamblado Microsoft.SqlServer.ManagedDTS.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application application = new Application();  
      PipelineComponentInfos componentInfos = application.PipelineComponentInfos;  
  
      foreach (PipelineComponentInfo componentInfo in componentInfos)  
      {  
        Console.WriteLine("Name: " + componentInfo.Name + "\n" +  
          " CreationName: " + componentInfo.CreationName + "\n");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim application As Application = New Application()  
  
    Dim componentInfos As PipelineComponentInfos = application.PipelineComponentInfos  
  
    For Each componentInfo As PipelineComponentInfo In componentInfos  
      Console.WriteLine("Name: " & componentInfo.Name & vbCrLf & _  
        " CreationName: " & componentInfo.CreationName & vbCrLf)  
    Next  
  
    Console.Read()  
  
  End Sub  
  
End Module  
```
  
## <a name="see-also"></a>Vea también  
 [Agregar componentes de flujo de datos mediante programación](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  

