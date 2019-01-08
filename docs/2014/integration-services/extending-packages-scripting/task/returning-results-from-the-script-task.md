---
title: Devolver los resultados de la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d1bd490bb176ba1883786e2aa1c8cd16a3474d13
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360397"
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
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
