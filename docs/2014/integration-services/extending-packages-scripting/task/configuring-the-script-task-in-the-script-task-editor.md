---
title: Configurar la tarea Script en el Editor de la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 57a82017982310634fc734634e7167a5a08ca8e8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376867"
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
  
 Para establecer el lenguaje de script predeterminado para las tareas Script y los componentes de script, utilice la propiedad **ScriptLanguage** en la página **General** del cuadro de diálogo **Opciones**. Para obtener más información, vea[página General](../../general-page-of-integration-services-designers-options.md).  
  
### <a name="entrypoint-property"></a>Propiedad EntryPoint  
 La propiedad `EntryPoint` especifica el método de la clase `ScriptMain` en el proyecto VSTA al que llama el motor en tiempo de ejecución de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] como punto de entrada al código de la tarea Script. La `ScriptMain` clase es la clase predeterminada que generan las plantillas de script.  
  
 Si cambia el nombre del método en el proyecto VSTA, deberá cambiar el valor de la propiedad `EntryPoint`.  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Propiedades ReadOnlyVariables y ReadWriteVariables  
 Puede escribir listas delimitada por comas de variables existentes como los valores de estas propiedades para que las variables estén disponibles con acceso de solo lectura o de lectura y escritura dentro del código de la tarea Script. El acceso a las variables de ambos tipos se realiza a través de la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> del objeto `Dts`. Para más información, consulte [Using Variables in the Script Task](../../extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
 Para seleccionar las variables, haga clic en el botón de puntos suspensivos (**…**) junto al campo de propiedades. Para más información, consulte [Página Seleccionar variables](../../control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Botón Editar script  
 El botón **Editar script** inicia el entorno de desarrollo VSTA donde escribe el script personalizado. Para obtener más información, vea [Programar y depurar la tarea Script](coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Página Expresiones del Editor de la tarea Script  
 En la página **Expresiones** del **Editor de la tarea Script**, puede utilizar expresiones para proporcionar valores a las propiedades de la tarea Script enumeradas anteriormente y para muchas otras propiedades de tarea. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md).  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, los artículos, los ejemplos y los vídeos más recientes de [!INCLUDE[msCoName](../../../includes/msconame-md.md)], así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Codificar y depurar la tarea Script](coding-and-debugging-the-script-task.md)  
  
  
