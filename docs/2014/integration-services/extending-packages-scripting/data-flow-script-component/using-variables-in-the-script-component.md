---
title: Utilizar variables en el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5dd1ad533b6327786195908452701161a94f9592
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967213"
---
# <a name="using-variables-in-the-script-component"></a>Utilizar variables en el componente de script
  Las variables almacenan valores que un paquete y sus contenedores, tareas y controladores de eventos pueden usar en tiempo de ejecución. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services-ssis-variables.md).  
  
 Puede hacer que las variables existentes estén disponibles para el acceso de solo lectura o de lectura y escritura por parte del script personalizado. para ello, escriba listas de variables delimitadas por comas en los `ReadOnlyVariables` campos y de la `ReadWriteVariables` página **script** del **Editor de script de transformación**. Tenga presente que los nombres de variable distinguen entre mayúsculas y minúsculas. Utilice la propiedad `Value` para leer de y escribir en las variables individuales. El componente de script administra en segundo plano cualquier bloqueo necesario cuando el script manipula las variables en tiempo de ejecución.  
  
> [!IMPORTANT]  
>  La colección de `ReadWriteVariables` solo está disponible en el método `PostExecute` para maximizar el rendimiento y minimizar el riesgo de conflictos de bloqueo. Por consiguiente no puede incrementar directamente el valor de una variable de paquete cuando procesa cada fila de datos. Incremente el valor de una variable local en su lugar y establezca el valor de la variable de paquete en el de la variable local en el método `PostExecute` una vez procesados todos los datos. También puede utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> para evitar esta limitación, tal y como se describe más adelante en este tema. Sin embargo, si se escribe directamente en una variable de paquete cuando se procesa cada fila afectará negativamente al rendimiento y aumentará el riesgo de conflictos de bloqueo.  
  
 Para obtener más información acerca de la página **Script** del **Editor de transformación Script**, vea [Configurar el componente de script en el editor de componentes de script](configuring-the-script-component-in-the-script-component-editor.md) y [Editor de transformación Script &#40;página Script&#41;](../../script-transformation-editor-script-page.md).  
  
 El componente de script crea una clase de colección `Variables` en el elemento de proyecto `ComponentWrapper` con una propiedad de descriptor de acceso con establecimiento inflexible de tipos para el valor de cada variable preconfigurada donde la propiedad tiene el mismo nombre que la propia variable. Esta colección se expone mediante la propiedad `Variables` de la clase `ScriptMain`. La propiedad de descriptor de acceso proporciona permiso de solo lectura o de lectura/escritura al valor de la variable según corresponda. Por ejemplo, si ha agregado una variable entera denominada `MyIntegerVariable` a la lista `ReadOnlyVariables`, puede recuperar el valor en el script utilizando el código siguiente:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 También puede utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, a la que se tiene acceso llamando a `Me.VariableDispenser`, para trabajar con variables del componente de script. En este caso no utiliza las propiedades de descriptor de acceso indicadas y escritas para las variables, sino que obtiene acceso directamente a las variables. Al utilizar <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, debe administrar la semántica de bloqueo y la conversión de tipos de datos para los valores de variables en su propio código. Tiene que utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> en lugar de las propiedades de descriptor de acceso con nombre y tipo si desea trabajar con una variable que no esté disponible en tiempo de diseño sino que se crea mediante programación en tiempo de ejecución.  
  
![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Integration Services &#40;&#41; variables de SSIS](../../integration-services-ssis-variables.md)   
 [Usar variables en paquetes](../../use-variables-in-packages.md)  
  
  
