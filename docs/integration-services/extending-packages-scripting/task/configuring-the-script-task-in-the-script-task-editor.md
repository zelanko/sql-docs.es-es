---
title: Configurar la tarea de secuencia de comandos en el Editor de la tarea de secuencia de comandos | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 182a7b8f04c2339a8f3d3b986c978a7998c8a9c3
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Configurar la tarea Script en el editor de la tarea Script
  Antes de escribir código personalizado en la tarea de secuencia de comandos, configurar sus propiedades principales en las tres páginas de la **Editor de la tarea de secuencia de comandos**. Puede configurar propiedades de tarea adicionales que no son únicas de la tarea Script mediante la ventana Propiedades.  
  
> [!NOTE]  
>  A diferencia de las versiones anteriores en las que podía indicar si se precompilaban los scripts, todos los scripts se precompilan a partir de [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)].  
  
## <a name="general-page-of-the-script-task-editor"></a>Página General del Editor de la tarea Script  
 En el **General** página de la **Editor de la tarea de secuencia de comandos**, asigne un nombre único y una descripción para la tarea de secuencia de comandos.  
  
## <a name="script-page-of-the-script-task-editor"></a>Página Script del Editor de la tarea Script  
 El **Script** página de la **Editor de la tarea de secuencia de comandos** muestra las propiedades personalizadas de la tarea de secuencia de comandos.  
  
### <a name="scriptlanguage-property"></a>Propiedad ScriptLanguage  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA) es compatible con la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] lenguajes de programación de Visual C#. Después de crear una secuencia de comandos en la tarea de secuencia de comandos, no se puede cambiar el valor de la **ScriptLanguage** propiedad.  
  
 Para establecer el lenguaje de script predeterminado para crear scripts para tareas y componentes de Script, utilice la **ScriptLanguage** propiedad en el **General** página de la **opciones** cuadro de diálogo. Para obtener más información, vea [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
### <a name="entrypoint-property"></a>Propiedad EntryPoint  
 El **EntryPoint** propiedad especifica el método en el **ScriptMain** proyecto de clase en el VSTA el [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] runtime llama como punto de entrada en el código de la tarea de secuencia de comandos. El **ScriptMain** es la clase predeterminada generada por las plantillas de script.  
  
 Si cambia el nombre del método en el proyecto VSTA, deberá cambiar el valor de la propiedad **EntryPoint** .  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propiedades ReadOnlyVariables y ReadWriteVariables  
 Puede escribir listas delimitada por comas de variables existentes como los valores de estas propiedades para que las variables estén disponibles con acceso de solo lectura o de lectura y escritura dentro del código de la tarea Script. Se tiene acceso a las variables de ambos tipos de código a través de la <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> propiedad de la **Dts** objeto. Para más información, consulte [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
 Para seleccionar las variables, haga clic en el botón de puntos suspensivos (**...** ) situado junto al campo de propiedad. Para obtener más información, consulte [la página Seleccionar Variables](../../../integration-services/control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Botón Editar script  
 El **editar Script** botón inicia el entorno de desarrollo VSTA en el que escribir un script personalizado. Para obtener más información, consulte [codificar y depurar la tarea Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Página Expresiones del Editor de la tarea Script  
 En el **expresiones** página de la **Editor de la tarea de secuencia de comandos**, puede usar expresiones para proporcionar valores para las propiedades de la tarea de secuencia de comandos enumerados anteriormente y para muchas otras propiedades de la tarea. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="see-also"></a>Vea también  
 [Codificar y depurar la tarea de secuencia de comandos](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
