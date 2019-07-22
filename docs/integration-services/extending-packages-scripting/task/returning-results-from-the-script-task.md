---
title: Devolver los resultados de la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9a291a51aee2160d3b6680a2c5baac415e66bdf5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102863"
---
# <a name="returning-results-from-the-script-task"></a>Devolver los resultados de la tarea Script

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
