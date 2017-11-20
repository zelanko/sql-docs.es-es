---
title: Desarrollar componentes de flujo de datos con varias entradas | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects-data-flow-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2cafe3a18fbe930088347304ed758afe505771d6
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>Desarrollar componentes de flujo de datos con varias entradas
  Un componente de flujo de datos con varias entradas puede utilizar demasiada memoria si sus diversas entradas producen datos a velocidades desiguales. Al desarrollar un componente de flujo de datos personalizado que admite dos o más entradas, puede administrar esta presión de memoria mediante los siguientes miembros en el espacio de nombres Microsoft.SqlServer.Dts.Pipeline:  
  
-   La propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Establezca el valor de esta propiedad en **true** si desea implementar el código que es necesario que el componente de flujo de datos personalizado administre datos que fluyen a velocidades desiguales.  
  
-   El método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. También debe proporcionar una implementación de este método si establece la <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> propiedad **true**. Si no proporciona una implementación, el motor de flujo de datos produce una excepción en tiempo de ejecución.  
  
-   El método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. También debe proporcionar una implementación de este método si establece la <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> propiedad **true** y su componente personalizado admite más de dos entradas. Si no proporciona una implementación, el motor de flujo de datos produce una excepción en tiempo de ejecución si el usuario adjunta más de dos entradas.  
  
 Juntos, estos miembros le permiten desarrollar una solución para la presión de memoria que es similar a la solución que Microsoft desarrolló para las transformaciones Combinación y Combinación de mezcla.  
  
## <a name="setting-the-supportsbackpressure-property"></a>Establecer la propiedad SupportsBackPressure  
 El primer paso para implementar una mejor administración de memoria para un componente de flujo de datos personalizado que admite varias entradas es establecer el valor de la <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> propiedad **true** en el <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Cuando el valor de <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> es **true**, el flujo de datos motor llama el <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> método y, cuando hay más de dos entradas, también llama a la <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> método en tiempo de ejecución.  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, la implementación de la <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> establece el valor de <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> a **true**.  
  
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
 Al establecer el valor de la <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> propiedad **true** en el <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> objeto, también debe proporcionar una implementación para el <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> método de la <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> clase.  
  
> [!NOTE]  
>  Su implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> no debería llamar a las implementaciones en la clase base. La implementación predeterminada de este método en la clase base simplemente genera una **NotImplementedException**.  
  
 Al implementar este método, establece el estado de un elemento en la matriz *canProcess* Boolean para cada una de las entradas del componente. (Las entradas se identifican por sus valores de Id. de la *inputIDs* matriz.) Al establecer el valor de un elemento en el *canProcess* matriz **true** para una entrada, el motor de flujo de datos llama el componente <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> método y proporciona más datos para la entrada especificada.  
  
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
  
 El ejemplo anterior utiliza la matriz `inputEOR` de tipo Boolean para indicar si los datos de nivel superior están disponibles para cada entrada. `EOR` en el nombre de la matriz representa "fin del conjunto de filas" y hace referencia a la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> de los búferes del flujo de datos. En una parte del ejemplo que no está incluido aquí, el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> comprueba el valor de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> cada búfer de datos que recibe. Cuando el valor **true** indica que no hay más datos de nivel superior disponibles para una entrada, en el ejemplo se establece el valor del elemento de la matriz `inputEOR` para esa entrada en **true**. En este ejemplo de la <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> método establece el valor del elemento correspondiente en el *canProcess* matriz **false** para una entrada cuando el valor de la `inputEOR` elemento de la matriz indica que No hay datos de nivel superior no disponible para la entrada.  
  
## <a name="implementing-the-getdependentinputs-method"></a>Implementar el método GetDependentInputs  
 Cuando su componente de flujo de datos personalizado admite más de dos entradas, también debe proporcionar una implementación para el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> de la clase <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  Su implementación del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> no debería llamar a las implementaciones en la clase base. La implementación predeterminada de este método en la clase base simplemente genera una **NotImplementedException**.  
  
 El motor de flujo de datos solo llama al método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> cuando el usuario adjunta más de dos entradas al componente. Cuando un componente tiene solo dos entradas y el <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> método indica que una entrada está bloqueada (*canProcess* = **false**), el motor de flujo de datos sepa que la otra entrada es esperando recibir más datos. Sin embargo, cuando hay más de dos entradas y el método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica que una está bloqueada, el código adicional del método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> identifica qué entradas esperan recibir más datos.  
  
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
  
  

