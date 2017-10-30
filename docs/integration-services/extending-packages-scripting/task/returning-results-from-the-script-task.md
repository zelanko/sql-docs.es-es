---
title: Devolver los resultados de la tarea de secuencia de comandos | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd3772ed20abbc594d171ea83a2f330d44a5be85
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="returning-results-from-the-script-task"></a>Devolver los resultados de la tarea Script
  La tarea Script utiliza las propiedades <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> y <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> opcional para devolver información de estado al módulo ejecutable de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que se puede utilizar para determinar la ruta de acceso del flujo de trabajo después de que la tarea Script ha finalizado.  
  
## <a name="taskresult"></a>TaskResult  
 La propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> notifica si la tarea tuvo éxito o no. Por ejemplo:  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 La propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> devuelve, de manera opcional, un objeto definido por el usuario que cuantifica o proporciona más información sobre si se ha realizado correctamente la tarea Script o ha dado un error. Por ejemplo, la tarea FTP utiliza la propiedad <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> para devolver el número de archivos transferidos. La tarea Ejecutar SQL devuelve el número de filas afectadas por la tarea. <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> también se puede utilizar para determinar la ruta de acceso del flujo de trabajo. Por ejemplo:  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  

