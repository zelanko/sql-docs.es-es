---
title: Mejorar una salida de errores con el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 85978278c2a51cde45e18b742998b1f6229e8e7d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426972"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>Mejorar una salida de errores con el componente de script
  De forma predeterminada, las dos columnas adicionales en una salida de errores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], ErrorCode y ErrorColumn, únicamente contienen códigos numéricos que representan un número de error y el identificador de la columna en la que se produjo el error. Estos valores numéricos pueden tener un uso limitado sin la correspondiente descripción del error.  
  
 En este tema se describe cómo agregar una columna de descripción del error a los datos de salida de error existentes en el flujo de datos mediante el componente de script. En el ejemplo se agrega la descripción del error que corresponde a un determinado código de error de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] predefinido mediante el método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>, disponible a través de la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> del componente de script.  
  
> [!NOTE]  
>  Si desea crear un componente que pueda reutilizar más fácilmente en varias tareas de flujo de datos y varios paquetes, puede utilizar el código de este ejemplo de componente de script como punto de inicio para el componente de flujo de datos personalizado. Para obtener más información, vea [Desarrollar un componente de flujo de datos personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo que aparece aquí utiliza un componente de script configurado como una transformación para agregar una columna de descripción del error a los datos de salida de error existentes en el flujo de datos.  
  
 Para obtener más información sobre cómo configurar el componente de script para su uso como una transformación en el flujo de datos, vea [crear una transformación sincrónica con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)y [crear una transformación asincrónica con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar este ejemplo de componente de script  
  
1.  Antes de crear el nuevo componente de script, configure un componente de nivel superior en el flujo de datos para redirigir las filas a su salida de error cuando se produce un error o truncamiento. Con fines de prueba, puede que quiera configurar un componente de manera que garantice que se van a producir errores (por ejemplo, mediante la configuración de una transformación Búsqueda entre dos tablas donde se producirá un error en la búsqueda).  
  
2.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como una transformación.  
  
3.  Conecte la salida de error del componente de nivel superior al nuevo componente de script.  
  
4.  Abra el **Editor de transformación Script** y en la página **Script**, para la propiedad **ScriptLanguage**, seleccione el lenguaje de script.  
  
5.  Haga clic en **Editar script** para abrir el IDE de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) y agregue el código de ejemplo que se muestra a continuación.  
  
6.  Cierre VSTA.  
  
7.  En el editor de transformación script, en la página **columnas de entrada** , seleccione la columna ErrorCode.  
  
8.  En la página **entradas y salidas** , agregue una nueva columna de salida de tipo `String` denominada **ErrorDescription**. Aumente la longitud predeterminada de la nueva columna a 255 para admitir mensajes largos.  
  
9. Cierre el **Editor de transformación Script**.  
  
10. Adjunte la salida del componente de script a un destino conveniente. Para pruebas ad hoc, la manera más fácil de configurar es mediante un destino de archivo plano.  
  
11. Ejecute el paquete.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  Row.ErrorDescription = _  
    Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
  Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
    }  
}  
  
```  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Control de errores en los datos](../data-flow/error-handling-in-data.md)   
 [Usar las salidas de error en un componente de flujo de datos](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [Crear una transformación sincrónica con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
