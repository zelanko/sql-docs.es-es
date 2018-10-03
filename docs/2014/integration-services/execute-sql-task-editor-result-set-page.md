---
title: Ejecutar el Editor de la tarea SQL (página de conjunto de resultados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b342b166a879af2db677f70753b9e53cd0f2bc8a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162235"
---
# <a name="execute-sql-task-editor-result-set-page"></a>Editor de la tarea Ejecutar SQL (página Conjunto de resultados)
  Utilice la página **Conjunto de resultados** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para asignar el resultado de la instrucción SQL a variables nuevas o existentes. Las opciones de este cuadro de diálogo están deshabilitadas si se define **Conjunto de resultados** de la página General como **Ninguno**.  
  
 Para más información sobre esta tarea, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md) y [Conjuntos de resultados en la tarea Ejecutar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opciones  
 **Nombre del resultado**  
 Después de hacer clic en **Agregar**y de agregar un conjunto de asignaciones de conjuntos de resultados, asigne un nombre al resultado. Deberá utilizar nombres de resultados específicos dependiendo del tipo de conjunto de resultados.  
  
 Si el tipo de conjunto de resultados es **Fila única**, puede utilizar el nombre de una columna devuelta por la consulta o el número que representa la posición de una columna en la lista de columnas de una de las columnas devueltas por la consulta.  
  
 Si el tipo de conjunto de resultados es **Conjunto de resultados completo** o **XML**, debe utilizar 0 como nombre del conjunto de resultados.  
  
 **Temas relacionados**: [Conjuntos de resultados en la tarea Ejecutar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
 **Nombre de variable**  
 Para asignar el conjunto de resultados a una variable, seleccione una variable o haga clic en \<**Nueva variable…**> para agregar una variable nueva con el cuadro de diálogo **Agregar variable**.  
  
 **Agregar**  
 Haga clic para agregar una asignación de conjuntos de resultados.  
  
 **Quitar**  
 Seleccione de la lista una asignación de conjuntos de resultados y, después, haga clic en **Quitar**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Ejecutar el Editor de la tarea SQL &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Ejecutar el Editor de la tarea SQL &#40;página asignación de parámetros&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference)  
  
  
