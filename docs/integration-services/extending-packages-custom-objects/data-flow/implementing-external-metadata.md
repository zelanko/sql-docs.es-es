---
title: Implementar metadatos externos | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96d413bca20ec171d515ac6d0ad81b5b994bd854
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-external-metadata"></a>Implementar metadatos externos
  Cuando un componente está desconectado de su origen de datos, puede validar las columnas de las colecciones de columnas de entrada y de resultados con las columnas en su origen de datos externo mediante la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100>. Esta interfaz permite mantener una instantánea de las columnas en el origen de datos externo y asignar estas columnas a las columnas de la colección de columnas de entrada y de resultados del componente.  
  
 La implementación de columnas de metadatos externos agrega un nivel de sobrecarga y complejidad al desarrollo del componente, porque debe mantener y validar una colección de columnas adicional, pero la capacidad de evitar los caros viajes de ida y vuelta (round trip) al servidor para la validación puede hacer que este trabajo de desarrollo valga la pena.  
  
## <a name="populating-external-metadata-columns"></a>Rellenar columnas de metadatos externos  
 Las columnas de metadatos externos se agregan normalmente a la colección cuando se crea la columna de entrada o de resultados correspondiente. Para crear una nueva columna se llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A>. Las propiedades de la columna se establecen después para coincidir con el origen de datos externo.  
  
 Para asignar la columna de metadatos externos a la columna de entrada o de resultados correspondiente se asigna el identificador de la columna de metadatos externos a la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> de la columna de entrada o de resultados. Esto le permite buscar con facilidad la columna de metadatos externos para una columna de entrada o de resultados concreta utilizando el método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> de la colección.  
  
 En el ejemplo siguiente se muestra cómo crear una columna de metadatos externos y después asignar la columna a una columna de resultados estableciendo la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A>.  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>Validar con columnas de metadatos externos  
 La validación requiere pasos adicionales para los componentes que mantienen una colección de columnas de metadatos externos, porque debe validar una colección de columnas adicional. La validación se puede dividir en validación con conexión o validación sin conexión.  
  
### <a name="connected-validation"></a>Validación con conexión  
 Cuando un componente está conectado a un origen de datos externo, las columnas de las colecciones de entrada o de salida se comprueban directamente con el origen de datos externo. Además, se deben validar las columnas de la recopilación de metadatos externos. Esto es necesario porque la colección de metadatos externos puede modificarse mediante el uso de la **Editor avanzado** en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], y los cambios realizados en la colección no son detectables. Por consiguiente, cuando se está conectado, los componentes deben asegurarse de que las columnas de la colección de columnas de metadatos externos continúan reflejando las columnas en el origen de datos externo.  
  
 Puede ocultar la colección de metadatos externos en el **Editor avanzado** estableciendo la <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A> propiedad de la colección a **false**. Sin embargo, esto también oculta la **asignación de columnas** pestaña del editor, lo que permite a los usuarios asignar columnas de la colección de entrada o de salida a las columnas de la colección de columnas de metadatos externos. Si se establece esta propiedad en **false** impide que los desarrolladores modificar mediante programación la colección, pero proporciona un nivel de protección para la colección de columnas de metadatos externos de un componente que se utiliza exclusivamente en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="disconnected-validation"></a>Validación sin conexión  
 Cuando un componente está desconectado de un origen de datos externo, se simplifica la validación porque las columnas de la colección de entrada o de salida se comprueban directamente con las columnas de la recopilación de metadatos externos y no con el origen externo. Un componente debe realizar la validación sin conexión cuando no se ha establecido la conexión a su origen de datos externo o cuando el <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> propiedad es **false**.  
  
 En el ejemplo de código siguiente se muestra una implementación de un componente que realiza la validación con su colección de columnas de metadatos externos.  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  

## <a name="see-also"></a>Vea también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)  
  
  

