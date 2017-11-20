---
title: Uso de Variables en el componente de Script | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bac1e6d96e872be0355282c3e12fc81054ca41cd
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-component"></a>Utilizar variables en el componente de script
  Las variables almacenan valores que un paquete y sus contenedores, tareas y controladores de eventos pueden usar en tiempo de ejecución. Para más información, vea [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 Puede disponer de variables existentes de solo lectura o acceso de lectura/escritura mediante un script personalizado escribiendo listas delimitada por comas de variables en el **ReadOnlyVariables** y **ReadWriteVariables** campos en el **Script** página de la **Editor de transformación Script**. Tenga presente que los nombres de variable distinguen entre mayúsculas y minúsculas. Use la **valor** propiedad para leer y escribir en las variables individuales. El componente de script administra en segundo plano cualquier bloqueo necesario cuando el script manipula las variables en tiempo de ejecución.  
  
> [!IMPORTANT]  
>  La colección de **ReadWriteVariables** sólo está disponible en la **PostExecute** método para maximizar el rendimiento y minimizar el riesgo de conflictos de bloqueo. Por consiguiente no puede incrementar directamente el valor de una variable de paquete cuando procesa cada fila de datos. Aumentar el valor de una variable local en su lugar y establezca el valor de la variable de paquete en el valor de la variable local en el **PostExecute** método después de todos los datos se ha procesado. También puede utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> para evitar esta limitación, tal y como se describe más adelante en este tema. Sin embargo, si se escribe directamente en una variable de paquete cuando se procesa cada fila afectará negativamente al rendimiento y aumentará el riesgo de conflictos de bloqueo.  
  
 Para obtener más información sobre la **Script** página de la **Editor de transformación Script**, consulte [configurar el componente de Script en el Editor de componentes de secuencia de comandos](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) y [Editor de transformación Script &#40; Página script &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 El componente de Script crea una **Variables** clase de colección en el **ComponentWrapper** elemento de proyecto con una propiedad de descriptor de acceso fuertemente tipado para el valor de cada variable preconfigurada donde la propiedad tiene el mismo nombre que la propia variable. Esta colección se expone a través de la **Variables** propiedad de la **ScriptMain** clase. La propiedad de descriptor de acceso proporciona permiso de solo lectura o de lectura/escritura al valor de la variable según corresponda. Por ejemplo, si ha agregado una variable entera denominada `MyIntegerVariable` a la **ReadOnlyVariables** lista, puede recuperar su valor en la secuencia de comandos mediante el código siguiente:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 También puede utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, a la que se tiene acceso llamando a `Me.VariableDispenser`, para trabajar con variables del componente de script. En este caso no utiliza las propiedades de descriptor de acceso indicadas y escritas para las variables, sino que obtiene acceso directamente a las variables. Al utilizar <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, debe administrar la semántica de bloqueo y la conversión de tipos de datos para los valores de variables en su propio código. Tiene que utilizar la propiedad <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> en lugar de las propiedades de descriptor de acceso con nombre y tipo si desea trabajar con una variable que no esté disponible en tiempo de diseño sino que se crea mediante programación en tiempo de ejecución.  
  
## <a name="see-also"></a>Vea también  
 [Integration Services &#40; SSIS &#41; Variables](../../../integration-services/integration-services-ssis-variables.md)   
 [Usar Variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

