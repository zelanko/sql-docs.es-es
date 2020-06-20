---
title: Crear un componente de flujo de datos personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 181e9d2d812dbf6ff4e3d232b5e48cdc1e63e0b3
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966555"
---
# <a name="creating-a-custom-data-flow-component"></a>Crear un componente de flujo de datos personalizado
  En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], la tarea Flujo de datos expone un modelo de objetos que permite a los desarrolladores crear componentes de flujo de datos personalizados, orígenes, transformaciones y destinos mediante [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] y código administrado.  
  
 Una tarea de flujo de datos consta de componentes que contienen una interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> y una colección de objetos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> que definen el movimiento de datos entre los componentes.  
  
> [!NOTE]  
>  Cuando crea un proveedor personalizado, necesita actualizar el archivo ProviderDescriptors.xml con los valores de la columna de metadatos.  
  
## <a name="design-time-and-run-time"></a>Tiempo de diseño y tiempo de ejecución  
 Antes de la ejecución, se dice que la tarea Flujo de datos se encuentra en un estado en tiempo de diseño, cuando sufre cambios incrementales. Los cambios pueden incluir la adición o eliminación de los componentes, la adición o eliminación de los objetos de ruta de acceso que conectan los componentes y cambios en los metadatos de los componentes. Cuando se producen cambios en los metadatos, el componente puede supervisar y reaccionar a los cambios. Por ejemplo, un componente puede no permitir ciertos cambios o realizar cambios adicionales en respuesta a un cambio. En tiempo de diseño, el diseñador interactúa con un componente a través de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> en tiempo de diseño.  
  
 En tiempo de ejecución, la tarea de flujo de datos examina la secuencia de componentes, prepara un plan de ejecución y administra un grupo de subprocesos de trabajo que ejecutan el plan de trabajo. Aunque cada subproceso de trabajo realiza algún trabajo que es interno a la tarea de flujo de datos, la tarea principal del subproceso de trabajo es llamar a los métodos del componente a través de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> de tiempo de ejecución.  
  
## <a name="creating-a-component"></a>Crear un componente  
 Para crear un componente de flujo de datos, puede derivar una clase de la clase base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>, aplicar la clase <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> y, a continuación, invalidar los métodos adecuados de la clase base. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> implementa las interfaces <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> y <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> y expone sus métodos para que los invalide en el componente.  
  
 En función de los objetos que utiliza el componente, el proyecto requerirá las referencias a algunos o a todos los ensamblados siguientes:  
  
|Característica|Ensamblado para referencia|Espacio de nombres a importar|  
|-------------|---------------------------|-------------------------|  
|flujo de datos|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|Contenedor de flujo de datos|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|Tiempo de ejecución|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|Contenedor en tiempo de ejecución|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 En el ejemplo de código siguiente se muestra un componente simple que deriva de la clase base y aplica <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Deberá agregar una referencia al ensamblado DTSPipelineWrap.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar una interfaz de usuario para un componente de flujo de datos](developing-a-user-interface-for-a-data-flow-component.md)  
  
  
