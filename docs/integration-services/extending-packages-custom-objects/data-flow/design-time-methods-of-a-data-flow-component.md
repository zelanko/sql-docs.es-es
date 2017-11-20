---
title: "Componente de flujo de métodos en tiempo de diseño de los datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
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
- custom data flow components [Integration Services], method execution sequence
- ProcessInput method
- method execution sequence [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], method execution sequence
ms.assetid: b5a121a1-b87c-441b-a42c-2cec628dc81c
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf248d93b1b1e581c3315cde9b1f96edc58bcfde
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="design-time-methods-of-a-data-flow-component"></a>Métodos en tiempo de diseño de un componente de flujo de datos
  Antes de la ejecución, se dice que la tarea Flujo de datos se encuentra en un estado en tiempo de diseño, cuando sufre cambios incrementales. Los cambios pueden incluir la adición o eliminación de los componentes, la adición o eliminación de los objetos de ruta de acceso que conectan los componentes y cambios en los metadatos de los componentes. Cuando se producen cambios en los metadatos, el componente puede supervisar y reaccionar a los cambios. Por ejemplo, un componente puede no permitir ciertos cambios o realizar cambios adicionales en respuesta a un cambio. En tiempo de diseño, el diseñador interactúa con un componente a través de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> en tiempo de diseño.  
  
## <a name="design-time-implementation"></a>Implementación en tiempo de diseño  
 La interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> describe la interfaz en tiempo de diseño de un componente. Aunque no implemente explícitamente esta interfaz, algunos conocimientos sobre los métodos definidos en esta interfaz le servirán de ayuda para entender qué métodos de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> corresponden a la instancia en tiempo de diseño de un componente.  
  
 Cuando se carga un componente en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], se crea la instancia en tiempo de diseño del componente y se llama a los métodos de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> cuando se edita el componente. La implementación de la clase base le permite invalidar únicamente los métodos que requieren su componente. En muchos casos, puede invalidar estos métodos para impedir las modificaciones inapropiadas a un componente. Por ejemplo, para evitar que los usuarios agreguen una salida a un componente, invalide el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.InsertOutput%2A>. De lo contrario, cuando la clase base llama a la implementación de este método, agrega una salida al componente.  
  
 Independientemente del propósito o funcionalidad del componente, debería invalidar los métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> y <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>. Para obtener más información acerca de <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> y <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>, consulte [validar un componente de flujo de datos](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md).  
  
## <a name="providecomponentproperties-method"></a>Método ProvideComponentProperties  
 La inicialización de un componente se produce en el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>. El Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] llama a este método cuando se agrega un componente a la tarea de flujo de datos, y es similar a un constructor de clase. Los desarrolladores de componentes deberían crear e inicializar sus entradas, salidas y propiedades personalizadas durante esta llamada al método. El método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> se diferencia de un constructor porque no se llama cada vez que se crea la instancia en tiempo de diseño o la instancia en tiempo de ejecución del componente.  
  
 La implementación de la clase base del método agrega una entrada y una salida al componente y asigna el identificador de la entrada a la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A>. Sin embargo, en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], no se asigna ningún nombre a los objetos de entrada y salida que agrega la clase base. No se cargarán los paquetes que contienen un componente con una entrada o los objetos de resultado cuya propiedad Name no está establecida correctamente. Por lo tanto, cuando se usa la implementación base, deben asignar valores explícitamente a la propiedad de nombre de la entrada y salida predeterminada.  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    /// TODO: Reset the component.  
    /// TODO: Add custom properties.  
    /// TODO: Add input objects.  
    /// TODO: Add output objects.  
}  
```  
  
```vb  
Public Overrides Sub ProvideComponentProperties()  
    ' TODO: Reset the component.  
    ' TODO: Add custom properties.  
    ' TODO: Add input objects.  
    ' TODO: Add output objects.  
End Sub  
```  
  
### <a name="creating-custom-properties"></a>Crear propiedades personalizadas.  
 La llamada al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> es donde los desarrolladores de componentes deberían agregar al componente las propiedades personalizadas (<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100>). Las propiedades personalizadas no tienen una propiedad de tipo de datos. El tipo de datos de una propiedad personalizada se establece por el tipo de datos del valor que asigne a su propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.Value%2A>. Sin embargo, después de haber asignado un valor inicial a la propiedad personalizada, no puede asignar un valor con un tipo de datos diferente.  
  
> [!NOTE]  
>  El <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> interfaz tiene compatibilidad limitada para los valores de propiedad de tipo **objeto**. El único objeto que puede almacenar como el valor de una propiedad personalizada es una matriz de tipos simples como cadenas o enteros.  
  
 Puede indicar que la propiedad personalizada admite las expresiones de propiedad estableciendo el valor de su <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.ExpressionType%2A> propiedad **CPET_NOTIFY** desde el <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSCustomPropertyExpressionType> enumeración, tal como se muestra en el ejemplo siguiente. No tiene que agregar cualquier código para controlar o validar la expresión de propiedad especificada por el usuario. Puede establecer un valor predeterminado de la propiedad, validar su valor y leer y utilizar su valor normalmente.  
  
```csharp  
IDTSCustomProperty100 myCustomProperty;  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY;  
```  
  
```vb  
Dim myCustomProperty As IDTSCustomProperty100  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY  
```  
  
 Puede limitar los usuarios a seleccionar un valor de propiedad personalizada de una enumeración mediante el uso de la <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A> propiedad, como se muestra en el ejemplo siguiente, que se da por supuesto que ha definido una enumeración pública denominada **MyValidValues**.  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the type with the custom property.  
customProperty.TypeConverter = typeof(MyValidValues).AssemblyQualifiedName;  
// Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne;    
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the type with the custom property.  
customProperty.TypeConverter = GetType(MyValidValues).AssemblyQualifiedName   
' Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne  
```  
  
 Para obtener más información, vea "Conversión de tipos generalizada" y "Implementar un convertidor de tipos" en el [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=7022).  
  
 Puede especificar un cuadro de diálogo del editor personalizado para el valor de su propiedad personalizada mediante la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A>, como se muestra en el ejemplo siguiente. En primer lugar, debe crear un tipo personalizado editor que hereda de **System.Drawing.Design.UITypeEditor**, si no puede encontrar una clase de editor de tipo de interfaz de usuario existente que se adapte a sus necesidades.  
  
```csharp  
public class MyCustomTypeEditor : UITypeEditor  
{  
...  
}  
```  
  
```vb  
Public Class MyCustomTypeEditor  
  Inherits UITypeEditor   
  ...  
End Class  
```  
  
 A continuación, especifique esta clase como el valor de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> de su propiedad personalizada.  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the editor with the custom property.  
customProperty.UITypeEditor = typeof(MyCustomTypeEditor).AssemblyQualifiedName;  
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the editor with the custom property.  
customProperty.UITypeEditor = GetType(MyCustomTypeEditor).AssemblyQualifiedName  
```  
  
 Para obtener más información, vea "Implementar un Editor de tipos de interfaz de usuario" en el [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=7022).  
  
## <a name="see-also"></a>Vea también  
 [Métodos en tiempo de ejecución de un componente de flujo de datos](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
  
  

