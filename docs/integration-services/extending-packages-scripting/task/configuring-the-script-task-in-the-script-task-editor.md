---
title: Configurar la tarea Script en el Editor de la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 223961d653fb102aa3060341b96f335e216b6e3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Configurar la tarea Script en el editor de la tarea Script
  Antes de escribir código personalizado en la tarea Script, debe configurar sus propiedades principales en las tres páginas del **Editor de la tarea Script**. Puede configurar propiedades de tarea adicionales que no son únicas de la tarea Script mediante la ventana Propiedades.  
  
> [!NOTE]  
>  A diferencia de las versiones anteriores en las que podía indicar si se precompilaban los scripts, todos los scripts se precompilan a partir de [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)].  
  
## <a name="general-page-of-the-script-task-editor"></a>Página General del Editor de la tarea Script  
 En la página **General** del **Editor de la tarea Script**, debe asignar un nombre único y una descripción a la tarea Script.  
  
## <a name="script-page-of-the-script-task-editor"></a>Página Script del Editor de la tarea Script  
 La página **Script** del **Editor de la tarea Script** muestra las propiedades personalizadas de la tarea Script.  
  
### <a name="scriptlanguage-property"></a>Propiedad ScriptLanguage  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) es compatible con los lenguajes de programación [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Después de crear un script en la tarea Script, no podrá cambiar el valor de la propiedad **ScriptLanguage**.  
  
 Para establecer el lenguaje de script predeterminado para las tareas Script y los componentes de script, utilice la propiedad **ScriptLanguage** en la página **General** del cuadro de diálogo **Opciones**. Para obtener más información, vea [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
### <a name="entrypoint-property"></a>Propiedad EntryPoint  
 La propiedad **EntryPoint** especifica el método de la clase **ScriptMain** en el proyecto de VSTA al que llama el motor en tiempo de ejecución de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] como punto de entrada al código de la tarea Script. La clase **ScriptMain** es la clase predeterminada que generan las plantillas de script.  
  
 Si cambia el nombre del método en el proyecto VSTA, deberá cambiar el valor de la propiedad **EntryPoint** .  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propiedades ReadOnlyVariables y ReadWriteVariables  
 Puede escribir listas delimitada por comas de variables existentes como los valores de estas propiedades para que las variables estén disponibles con acceso de solo lectura o de lectura y escritura dentro del código de la tarea Script. El acceso a las variables de ambos tipos se realiza a través del código con la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> del objeto **Dts**. Para más información, consulte [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
 Para seleccionar las variables, haga clic en el botón de puntos suspensivos (**…**) situado junto al campo de propiedades. Para más información, consulte [Página Seleccionar variables](../../../integration-services/control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Botón Editar script  
 El botón **Editar script** inicia el entorno de desarrollo VSTA donde escribe el script personalizado. Para obtener más información, vea [Programar y depurar la tarea Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Página Expresiones del Editor de la tarea Script  
 En la página **Expresiones** del **Editor de la tarea Script**, puede utilizar expresiones para proporcionar valores a las propiedades de la tarea Script enumeradas anteriormente y para muchas otras propiedades de tarea. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="see-also"></a>Ver también  
 [Codificar y depurar la tarea Script](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
