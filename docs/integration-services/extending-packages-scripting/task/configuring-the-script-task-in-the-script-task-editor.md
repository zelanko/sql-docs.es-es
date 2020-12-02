---
description: Configurar la tarea Script en el editor de la tarea Script
title: Configurar la tarea Script en el Editor de la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b4a052ea59e3c72adda887c3084bca278059f0b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122926"
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Configurar la tarea Script en el editor de la tarea Script

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Antes de escribir código personalizado en la tarea Script, debe configurar sus propiedades principales en las tres páginas del **Editor de la tarea Script**. Puede configurar propiedades de tarea adicionales que no son únicas de la tarea Script mediante la ventana Propiedades.  
  
> [!NOTE]  
>  A diferencia de las versiones anteriores en las que podía indicar si se precompilaban los scripts, todos los scripts se precompilan a partir de [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)].  
  
## <a name="general-page-of-the-script-task-editor"></a>Página General del Editor de la tarea Script  
 En la página **General** del **Editor de la tarea Script**, debe asignar un nombre único y una descripción a la tarea Script.  
  
## <a name="script-page-of-the-script-task-editor"></a>Página Script del Editor de la tarea Script  
 La página **Script** del **Editor de la tarea Script** muestra las propiedades personalizadas de la tarea Script.  
  
### <a name="scriptlanguage-property"></a>Propiedad ScriptLanguage  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) es compatible con los lenguajes de programación [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Después de crear un script en la tarea Script, no podrá cambiar el valor de la propiedad **ScriptLanguage**.  
  
 Para establecer el lenguaje de script predeterminado para las tareas Script y los componentes de script, utilice la propiedad **ScriptLanguage** en la página **General** del cuadro de diálogo **Opciones**. Para obtener más información, vea [General Page](../../general-page-of-integration-services-designers-options.md).  
  
### <a name="entrypoint-property"></a>Propiedad EntryPoint  
 La propiedad **EntryPoint** especifica el método de la clase **ScriptMain** en el proyecto de VSTA al que llama el motor en tiempo de ejecución de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] como punto de entrada al código de la tarea Script. La clase **ScriptMain** es la clase predeterminada que generan las plantillas de script.  
  
 Si cambia el nombre del método en el proyecto VSTA, deberá cambiar el valor de la propiedad **EntryPoint** .  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propiedades ReadOnlyVariables y ReadWriteVariables  
 Puede escribir listas delimitada por comas de variables existentes como los valores de estas propiedades para que las variables estén disponibles con acceso de solo lectura o de lectura y escritura dentro del código de la tarea Script. El acceso a las variables de ambos tipos se realiza a través del código con la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> del objeto **Dts**. Para más información, consulte [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
 Para seleccionar las variables, haga clic en el botón de puntos suspensivos ( **…** ) junto al campo de propiedades. Para más información, consulte [Página Seleccionar variables](../../../integration-services/control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Botón Editar script  
 El botón **Editar script** inicia el entorno de desarrollo VSTA donde escribe el script personalizado. Para obtener más información, vea [Programar y depurar la tarea Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Página Expresiones del Editor de la tarea Script  
 En la página **Expresiones** del **Editor de la tarea Script**, puede utilizar expresiones para proporcionar valores a las propiedades de la tarea Script enumeradas anteriormente y para muchas otras propiedades de tarea. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Codificar y depurar la tarea Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
