---
title: "Conectar componentes de flujo de datos mediante programación | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- paths [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 404ecab7-7698-447b-93d6-dd256beb11ff
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 02c874d6eaf6594343e74d9b7a1b3493e714160c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="connecting-data-flow-components-programmatically"></a>Conectar componentes de flujo de datos mediante programación
  Después de agregar componentes a la tarea de flujo de datos, los conecta para crear un árbol de ejecución que representa el flujo de datos desde los orígenes, pasando por las transformaciones, hasta los destinos. Utiliza <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> objeta para conectar los componentes en el flujo de datos.  
  
## <a name="creating-a-path"></a>Crear una ruta de acceso  
 Llame al método New de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.PathCollection%2A> de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipe> para crear una nueva ruta de acceso y agregarla a la colección de rutas de acceso en la tarea Flujo de datos. Este método devuelve un nuevo objeto <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> desconectado, que posteriormente utiliza para conectar dos componentes.  
  
 Llame al método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100.AttachPathAndPropagateNotifications%2A> para conectarse a la ruta de acceso y notificar a los componentes que participan en la ruta de acceso que se han conectado. Este método acepta como parámetros <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> del componente de nivel superior y <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> del componente de nivel inferior. De forma predeterminada, la llamada al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> del componente crea una entrada única para los componentes que tienen entradas y una salida única para los componentes que tienen salidas. En el ejemplo siguiente se utiliza esta salida predeterminada del origen y entrada predeterminada del destino.  
  
## <a name="next-step"></a>Paso siguiente  
 Después de establecer una ruta de acceso entre dos componentes, el paso siguiente consiste en asignar columnas de entrada en el componente de nivel inferior. Este paso se describe en el tema [Seleccionar columnas de entrada mediante programación](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md) siguiente.  
  
## <a name="sample"></a>Ejemplo  
 En el ejemplo de código siguiente se muestra cómo establecer una ruta de acceso entre dos componentes.  
  
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
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Create the source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      srcDesignTime.ProvideComponentProperties();  
  
      // Create the destination component.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
    }  
  }  
```  
  
 }  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Create the source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate()  
    srcDesignTime.ProvideComponentProperties()  
  
    ' Create the destination component.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate()  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New()  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Ver también  
 [Seleccionar columnas de entrada mediante programación](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
  
  
