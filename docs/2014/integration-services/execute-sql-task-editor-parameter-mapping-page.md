---
title: Editor de la tarea ejecutar SQL (página asignación de parámetros) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7508324be0bef23ba0590bb181135512d75701e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059041"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>Editor de la tarea Ejecutar SQL (página Asignación de parámetros)
  Use la página **Asignación de parámetros** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para asignar variables a los parámetros de la instrucción SQL.  
  
 Para obtener información sobre esta tarea, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de variable**  
 Tras agregar una asignación de parámetros haciendo clic en **Agregar**, seleccione en la lista una variable del sistema o definida por el usuario, o haga clic en \<**Nueva variable…**> para agregar una nueva variable mediante el cuadro de diálogo **Agregar variable**.  
  
 **Temas relacionados:** [Integration Services &#40;las variables&#41; de SSIS](integration-services-ssis-variables.md)  
  
 **Direcciona**  
 Permite seleccionar la dirección del parámetro. Asigne cada variable a un parámetro de entrada o de salida, o bien a un código de retorno.  
  
 **Tipo de datos**  
 Seleccione el tipo de datos del parámetro. La lista de tipos de datos disponibles es específica del proveedor seleccionado en el administrador de conexiones utilizado por la tarea.  
  
 **Nombre del parámetro**  
 Proporcione un nombre de parámetro.  
  
 Dependiendo del tipo de administrador de conexiones que utiliza la tarea, se utilizarán números o nombres de parámetro. Algunos tipos de administradores de conexión requieren que el primer carácter del nombre del parámetro sea el signo \@, nombres específicos como \@Param1 o nombres de columnas como nombres de parámetro.  
  
 **Temas relacionados:** [parámetros y códigos de retorno en la tarea ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **Tamaño del parámetro**  
 Proporcione el tamaño de los parámetros que tienen longitud variable, como cadenas y campos binarios.  
  
 Este valor garantiza que el proveedor asigna el espacio suficiente para los valores de parámetro de longitud variable.  
  
 **Add (Agregar)**  
 Haga clic para agregar una asignación de parámetros.  
  
 **Remove**  
 Seleccione una asignación de parámetros de la lista y después haga clic en **Quitar**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea ejecutar SQL &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de la tarea ejecutar SQL &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference)  
  
  
