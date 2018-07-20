---
title: Ejecutar el Editor de la tarea SQL (página de asignación de parámetros) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
caps.latest.revision: 42
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9c35360c4cddebecf7f6237071bc430b74f726cb
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082957"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>Editor de la tarea Ejecutar SQL (página Asignación de parámetros)
  Use la página **Asignación de parámetros** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para asignar variables a los parámetros de la instrucción SQL.  
  
 Para obtener información sobre esta tarea, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de variable**  
 Tras agregar una asignación de parámetros haciendo clic en **Agregar**, seleccione en la lista una variable del sistema o definida por el usuario, o haga clic en \<**Nueva variable…**> para agregar una nueva variable mediante el cuadro de diálogo **Agregar variable**.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
 **Dirección**  
 Permite seleccionar la dirección del parámetro. Asigne cada variable a un parámetro de entrada o de salida, o bien a un código de retorno.  
  
 **Tipo de datos**  
 Seleccione el tipo de datos del parámetro. La lista de tipos de datos disponibles es específica del proveedor seleccionado en el administrador de conexiones utilizado por la tarea.  
  
 **Nombre de parámetro**  
 Proporcione un nombre de parámetro.  
  
 Dependiendo del tipo de administrador de conexiones que utiliza la tarea, se utilizarán números o nombres de parámetro. Algunos tipos de administradores de conexión requieren que el primer carácter del nombre del parámetro es el \@ iniciar sesión, nombres específicos como \@Param1 o columna se denomina como los nombres de parámetro.  
  
 **Temas relacionados:** [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **Tamaño del parámetro**  
 Proporcione el tamaño de los parámetros que tienen longitud variable, como cadenas y campos binarios.  
  
 Este valor garantiza que el proveedor asigna el espacio suficiente para los valores de parámetro de longitud variable.  
  
 **Agregar**  
 Haga clic para agregar una asignación de parámetros.  
  
 **Quitar**  
 Seleccione una asignación de parámetros de la lista y después haga clic en **Quitar**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Ejecutar el Editor de la tarea SQL &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Ejecutar el Editor de la tarea SQL &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference)  
  
  
