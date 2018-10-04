---
title: Utilizar variables en el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c16b25e5f56c9beb5bec2b9946d26440e48e0440
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154785"
---
# <a name="using-variables-in-the-script-component"></a>Utilizar variables en el componente de script
  Las variables almacenan valores que un paquete y sus contenedores, tareas y controladores de eventos pueden usar en tiempo de ejecución. Para más información, vea [Integration Services &#40;SSIS&#41; Variables](../../integration-services-ssis-variables.md).  
  
 Puede hacer disponibles para las variables existentes de solo lectura o acceso de lectura/escritura por parte del script personalizado escribiendo listas delimitada por comas de variables en el `ReadOnlyVariables` y `ReadWriteVariables` campos de la **Script** página de la **Editor de transformación script**. Tenga presente que los nombres de variable distinguen entre mayúsculas y minúsculas. Utilice la propiedad `Value` para leer de y escribir en las variables individuales. El componente de script administra en segundo plano cualquier bloqueo necesario cuando el script manipula las variables en tiempo de ejecución.  
  
> [!IMPORTANT]  
>  La colección de `ReadWriteVariables` solo está disponible en el método `PostExecute` para maximizar el rendimiento y minimizar el riesgo de conflictos de bloqueo. Por consiguiente no puede incrementar directamente el valor de una variable de paquete cuando procesa cada fila de datos. Incremente el valor de una variable local en su lugar y establezca el valor de la variable de paquete en el de la variable local en el método `PostExecute` una vez procesados todos los datos. También puede utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> para evitar esta limitación, tal y como se describe más adelante en este tema. Sin embargo, si se escribe directamente en una variable de paquete cuando se procesa cada fila afectará negativamente al rendimiento y aumentará el riesgo de conflictos de bloqueo.  
  
 Para obtener más información sobre la **Script** página de la **Editor de transformación Script**, consulte [configuración del componente de Script en el Editor del componente de Script] (( Configuring-the-Script-Component-in-the-Script-Component-Editor.MD) y [Editor de transformación Script &#40;página Script&#41;](../../script-transformation-editor-script-page.md).  
  
 El componente de script crea una clase de colección `Variables` en el elemento de proyecto `ComponentWrapper` con una propiedad de descriptor de acceso con establecimiento inflexible de tipos para el valor de cada variable preconfigurada donde la propiedad tiene el mismo nombre que la propia variable. Esta colección se expone mediante la propiedad `Variables` de la clase `ScriptMain`. La propiedad de descriptor de acceso proporciona permiso de solo lectura o de lectura/escritura al valor de la variable según corresponda. Por ejemplo, si ha agregado una variable entera denominada `MyIntegerVariable` a la lista `ReadOnlyVariables`, puede recuperar el valor en el script utilizando el código siguiente:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 También puede utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, a la que se tiene acceso llamando a `Me.VariableDispenser`, para trabajar con variables del componente de script. En este caso no utiliza las propiedades de descriptor de acceso indicadas y escritas para las variables, sino que obtiene acceso directamente a las variables. Al utilizar <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, debe administrar la semántica de bloqueo y la conversión de tipos de datos para los valores de variables en su propio código. Tiene que utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> en lugar de las propiedades de descriptor de acceso con nombre y tipo si desea trabajar con una variable que no esté disponible en tiempo de diseño sino que se crea mediante programación en tiempo de ejecución.  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services** <br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Servicios de integración &#40;SSIS&#41; Variables](../../integration-services-ssis-variables.md)   
 [Usar variables en paquetes](../../use-variables-in-packages.md)  
  
  
