---
title: Desarrollar componentes de flujo de datos con varias entradas | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects-data-flow-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4fae151d8feb9753eca9704b1b58f6ab7c609cf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>Desarrollar componentes de flujo de datos con varias entradas
  Un componente de flujo de datos con varias entradas puede utilizar demasiada memoria si sus diversas entradas producen datos a velocidades desiguales. Al desarrollar un componente de flujo de datos personalizado que admite dos o más entradas, puede administrar esta presión de memoria mediante los siguientes miembros del espacio de nombres Microsoft.SqlServer.Dts.Pipeline:  
  
-   La propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Establezca el valor de esta propiedad en **true** si desea implementar el código que es necesario que el componente de flujo de datos personalizado administre datos que fluyen a velocidades desiguales.  
  
-   El método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Debe realizar la implementación de este método si establece la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> en **true**. Si no proporciona una implementación, el motor de flujo de datos produce una excepción en tiempo de ejecución.  
  
-   El método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. También debe realizar la implementación de este método si establece la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> en **true** y su componente personalizado admite más de dos entradas. Si no proporciona una implementación, el motor de flujo de datos produce una excepción en tiempo de ejecución si el usuario adjunta más de dos entradas.  
  
 Juntos, estos miembros le permiten desarrollar una solución para la presión de memoria que es similar a la solución que Microsoft desarrolló para las transformaciones Combinación y Combinación de mezcla.  
  
## <a name="setting-the-supportsbackpressure-property"></a>Establecer la propiedad SupportsBackPressure  
 El primer paso para implementar la mejor administración de memoria en un componente de flujo de datos personalizado que admita varias entradas es establecer el valor de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> en **true** en la clase <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Cuando el valor de <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> es **true**, el motor de flujo de datos llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> y, cuando hay más de dos entradas, también llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> en tiempo de ejecución.  
  
### <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, la implementación de <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> establece el valor de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> en **true**.  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>Implementar el método IsInputReady  
 Al establecer el valor de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> en **true** en el objeto <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>, también debe realizar una implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  Su implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> no debería llamar a las implementaciones en la clase base. La implementación predeterminada de este método en la clase base simplemente genera una **NotImplementedException**.  
  
 Al implementar este método, establece el estado de un elemento en la matriz *canProcess* Boolean para cada una de las entradas del componente. (Las entradas se identifican mediante los valores del id. en la matriz *inputIDs*). Al establecer el valor de un elemento en la matriz *canProcess* en **true** para una entrada, el motor de flujo de datos llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> del componente y proporciona más datos para la entrada especificada.  
  
 Aunque los datos del nivel superior estén disponibles, el valor del elemento de la matriz *canProcess* de una entrada al menos siempre debe ser **true**o procesar las detenciones.  
  
 El motor de flujo de datos llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> antes de enviar cada búfer de datos para determinar qué entradas esperan recibir más datos. Cuando el valor devuelto indica que se bloquea una entrada, el motor de flujo de datos almacena temporalmente en memoria caché los búferes adicionales de datos para esa entrada en lugar de enviarlos al componente.  
  
> [!NOTE]  
>  No llame a los métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> en su propio código. El motor de flujo de datos llama a estos métodos y a los otros métodos de la clase **PipelineComponent** que invalide, cuando ejecuta su componente.  
  
### <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, la implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica que una entrada está esperando recibir más datos cuando se cumplen las condiciones siguientes:  
  
-   Los datos de nivel superior están disponibles para la entrada (`!inputEOR`).  
  
-   El componente no tiene los datos disponibles actualmente para procesar la entrada en los búferes que el componente ya haya recibido (`inputBuffers[inputIndex].CurrentRow() == null`).  
  
 Si una entrada espera recibir más datos, el componente de flujo de datos lo indica estableciendo en **true** el valor del elemento en la matriz *canProcess* que corresponde a esa entrada.  
  
 Por el contrario, cuando el componente todavía tiene los datos disponibles para procesar la entrada, el ejemplo suspende su procesamiento. Para ello, en el ejemplo se establece en **false** el valor del elemento en la matriz *canProcess* que corresponde a esa entrada.  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 El ejemplo anterior utiliza la matriz `inputEOR` de tipo Boolean para indicar si los datos de nivel superior están disponibles para cada entrada. `EOR` en el nombre de la matriz representa "fin del conjunto de filas" y hace referencia a la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> de los búferes del flujo de datos. En una parte del ejemplo que no está incluido aquí, el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> comprueba el valor de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> cada búfer de datos que recibe. Cuando el valor **true** indica que no hay más datos de nivel superior disponibles para una entrada, en el ejemplo se establece el valor del elemento de la matriz `inputEOR` para esa entrada en **true**. Este ejemplo del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> establece en **false** el valor del elemento correspondiente a la matriz *canProcess* de una entrada, cuando el valor del elemento `inputEOR` de la matriz indica que no hay más datos ascendentes disponibles para esa misma entrada.  
  
## <a name="implementing-the-getdependentinputs-method"></a>Implementar el método GetDependentInputs  
 Cuando su componente de flujo de datos personalizado admite más de dos entradas, también debe proporcionar una implementación para el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  Su implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> no debería llamar a las implementaciones en la clase base. La implementación predeterminada de este método en la clase base simplemente genera una **NotImplementedException**.  
  
 El motor de flujo de datos solo llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> cuando el usuario adjunta más de dos entradas al componente. Cuando un componente solo tiene dos entradas y el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica que una está bloqueada (*canProcess* = **false**), el motor de flujo de datos sabe que la otra entrada está esperando recibir más datos. Sin embargo, cuando hay más de dos entradas y el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica que una está bloqueada, el código adicional del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> identifica qué entradas esperan recibir más datos.  
  
> [!NOTE]  
>  No llame a los métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> en su propio código. El motor de flujo de datos llama a estos métodos y a los otros métodos de la clase **PipelineComponent** que invalide, cuando ejecuta su componente.  
  
### <a name="example"></a>Ejemplo  
 Para una entrada concreta que se bloquea, la siguiente implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> devuelve una colección de las entradas que están esperando recibir más datos y, por consiguiente, bloquean la entrada especificada. El componente identifica las entradas del bloqueo comprobando las entradas distintas de la entrada bloqueada que no tienen actualmente datos disponibles para procesar en los búferes que el componente ya ha recibido (`inputBuffers[i].CurrentRow() == null`). A continuación, el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> devuelve la colección de entradas del bloqueo como una recopilación de identificadores de entrada.  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
