---
title: Componente de flujo de provocar y definir eventos en datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a900b27c9056d95fb2284d8ba9d6b09d9c6635b5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>Provocar y definir eventos en un componente de flujo de datos
  Los desarrolladores de componentes pueden producir un subconjunto de los eventos definido en la interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> mediante una llamada a los métodos expuestos en la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>. También puede definir eventos personalizados con la colección <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> y provocarlos durante la ejecución con el método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>. En esta sección se describe cómo crear y provocar un evento y se proporcionan instrucciones sobre el momento en que se deben provocar los eventos en tiempo de diseño.  
  
## <a name="raising-events"></a>Generar eventos  
 Componentes provocan eventos mediante el uso de la **activan\<X >** métodos de la <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> interfaz. Puede provocar eventos durante el diseño y la ejecución de los componentes. Normalmente, en el diseño de los componentes, se llama a los métodos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> y <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A> durante la validación. Estos eventos muestran mensajes en el **lista de errores** panel de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] y proporcionar comentarios a los usuarios del componente cuando un componente está configurado incorrectamente.  
  
 Los componentes también pueden provocar eventos en cualquier momento durante la ejecución. Los eventos permiten a los programadores de componentes proporcionar información a los usuarios del componente cuando éste se ejecuta. Es probable que la llamada al método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> durante la ejecución produzca un error en el paquete.  
  
## <a name="defining-and-raising-custom-events"></a>Definir y provocar eventos personalizados  
  
### <a name="defining-a-custom-event"></a>Definir un evento personalizado  
 Los eventos personalizados se crean mediante una llamada al método <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> de la colección <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A>. La tarea de flujo de datos establece esta colección, que se proporciona al programador de componentes a través de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Esta clase contiene eventos personalizados definidos por la tarea de flujo de datos y eventos personalizados definidos por el componente durante el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A>.  
  
 Los eventos personalizados de un componente no se conservan en el paquete XML. Por tanto, se llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> durante el diseño y la ejecución para permitir al componente definir los eventos que provoca.  
  
 El *allowEventHandlers* parámetro de la <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> método especifica si el componente permite <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> objetos que se crean para el evento. Observe que los objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> son sincrónicos. Por tanto, el componente no reanuda la ejecución hasta que ha terminado de ejecutarse un objeto <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> adjuntado al evento personalizado. Si el *allowEventHandlers* parámetro es **true**, cada parámetro del evento estará disponible para todos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> objetos a través de las variables que se crean y rellenan automáticamente mediante la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en tiempo de ejecución.  
  
### <a name="raising-a-custom-event"></a>Provocar un evento personalizado  
 Los componentes provocan eventos personalizados mediante una llamada al método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> y proporcionando el nombre, texto y parámetros del evento. Si el *allowEventHandlers* parámetro es **true**, cualquier <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> que se crean para el evento personalizado son ejecutados por el [!INCLUDE[ssIS](../../../includes/ssis-md.md)] motor en tiempo de ejecución.  
  
### <a name="custom-event-sample"></a>Ejemplo de evento personalizado  
 En el ejemplo de código siguiente se muestra un componente que define un evento personalizado durante el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> y, a continuación, provoca el evento en tiempo de ejecución mediante una llamada al método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>.  
  
```csharp  
public override void RegisterEvents()  
{  
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};  
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};  
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};  
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref paramterTypes, ref parameterDescriptions);  
}  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
    while (buffer.NextRow())  
    {  
       // Process buffer rows.  
    }  
  
    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];  
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };  
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);  
}  
```  
  
```vb  
Public  Overrides Sub RegisterEvents()   
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"}   
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)}   
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."}   
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, paramterTypes, parameterDescriptions)   
End Sub   
  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
  While buffer.NextRow   
  End While   
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort")   
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now}   
  ComponentMetaData.FireCustomEvent("StartingSort", _  
    "Beginning sort operation.", arguments, _  
    ComponentMetaData.Name, FireSortEventAgain)   
End Sub  
```  

## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Controladores de eventos](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [Agregar un controlador de eventos a un paquete](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

