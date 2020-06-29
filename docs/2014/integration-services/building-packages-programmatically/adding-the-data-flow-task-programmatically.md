---
title: Agregar la tarea Flujo de datos mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9291673fec31064befed704560e96693c3641d7c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439292"
---
# <a name="adding-the-data-flow-task-programmatically"></a>Agregar la tarea de flujo de datos mediante programación
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] incluye una tarea denominada Flujo de datos, representada por el espacio de nombres <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> en el modelo de objetos. La tarea Flujo de datos es una tarea especializada de alto rendimiento que se dedica a transformar y mover datos durante la ejecución del paquete. Al igual que ocurre con otras tareas, la tarea Flujo de datos está incluida en el objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> y, desde la perspectiva del motor en tiempo de ejecución, esta tarea es simplemente una más del paquete. Sin embargo, el flujo de datos contiene objetos adicionales denominados componentes de flujo de datos. Estos componentes son aquellos que hacen que se muevan los datos de un origen a un destino, a veces a través de una transformación. Los componentes definen tanto la dirección del movimiento como la forma en que se transforman los datos. La configuración de la tarea Flujo de datos implica agregar componentes a la tarea y conectarlos después para establecer el flujo de datos y lograr la transformación deseada.  
  
 Existen tres tipos de componentes en una tarea Flujo de datos: **Orígenes de flujo de datos**, **Transformaciones de flujo de datos** y **Destinos de flujo de datos**, que aparecen en este orden en el cuadro de herramientas del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)]. También se hace referencia a estos tipos de forma más sencilla como orígenes, transformaciones o destinos. Como los nombres indican, los datos fluyen desde un origen a una transformación y, después, a un destino. Ésta es una descripción simplista del flujo de datos para ilustrar el concepto, pero la tarea Flujo de datos es suficientemente flexible y eficaz para controlar varios orígenes y conectar numerosas transformaciones que envíen resultados a múltiples destinos.  
  
 La tarea Flujo de datos se agrega a un paquete de la misma forma que otras tareas. Una vez agregada, la tarea se configura; para ello, se agregan componentes a la tarea de flujo de datos y, después, se configuran y conectan sus componentes.  
  
## <a name="sample"></a>Muestra  
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
 Entrada de blog sobre [EzAPI, actualizado para SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223), en blogs.msdn.com.  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Detectar componentes de flujo de datos mediante programación](../building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
