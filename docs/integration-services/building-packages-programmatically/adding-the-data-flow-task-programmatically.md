---
title: "Agregar la tarea de flujo de datos mediante programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
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
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0a7b0c3e51d7df76689f16ed91f60972d171bd9a
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="adding-the-data-flow-task-programmatically"></a>Agregar la tarea de flujo de datos mediante programación
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] incluye una tarea denominada Flujo de datos, representada por el espacio de nombres <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> en el modelo de objetos. La tarea Flujo de datos es una tarea especializada de alto rendimiento que se dedica a transformar y mover datos durante la ejecución del paquete. Al igual que ocurre con otras tareas, la tarea Flujo de datos está incluida en el objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> y, desde la perspectiva del motor en tiempo de ejecución, esta tarea es simplemente una más del paquete. Sin embargo, el flujo de datos contiene objetos adicionales denominados componentes de flujo de datos. Estos componentes son aquellos que hacen que se muevan los datos de un origen a un destino, a veces a través de una transformación. Los componentes definen tanto la dirección del movimiento como la forma en que se transforman los datos. La configuración de la tarea Flujo de datos implica agregar componentes a la tarea y conectarlos después para establecer el flujo de datos y lograr la transformación deseada.  
  
 Hay tres tipos de componentes dentro de una tarea de flujo de datos: **orígenes de flujo de datos**, **transformaciones de flujo de datos**, y **destinos de flujo de datos**, como se muestra en este orden en el [!INCLUDE[ssIS](../../includes/ssis-md.md)] cuadro de herramientas del diseñador. También se hace referencia a estos tipos de forma más sencilla como orígenes, transformaciones o destinos. Como los nombres indican, los datos fluyen desde un origen a una transformación y, después, a un destino. Ésta es una descripción simplista del flujo de datos para ilustrar el concepto, pero la tarea Flujo de datos es suficientemente flexible y eficaz para controlar varios orígenes y conectar numerosas transformaciones que envíen resultados a múltiples destinos.  
  
 La tarea Flujo de datos se agrega a un paquete de la misma forma que otras tareas. Una vez agregada, la tarea se configura; para ello, se agregan componentes a la tarea de flujo de datos y, después, se configuran y conectan sus componentes.  
  
## <a name="sample"></a>Ejemplo  
 En el ejemplo de código siguiente se muestra cómo agregar una tarea Flujo de datos a un paquete. En este ejemplo, es necesario establecer una referencia a los ensamblados Microsoft.SqlServer.PipelineHost, Microsoft.SqlServer.DTSPipelineWrap y Microsoft.SqlServer.ManagedDTS.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      Executable e = p.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;   
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim e As Executable = p.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As TaskHost = CType(e, TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [EzAPI, actualizado para SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223), en blogs.msdn.com.  
  
## <a name="see-also"></a>Vea también  
 [Detectar componentes de flujo de datos mediante programación](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
