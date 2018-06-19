---
title: Tarea de Pig con Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4027f5762330f694e24058d9b9583d57fa6e0fbd
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410597"
---
# <a name="hadoop-pig-task"></a>Tarea de Pig con Hadoop
  Utilice la tarea de Pig con Hadoop para ejecutar el script de Pig en un clúster de Hadoop.  
  
 Para agregar una tarea de Pig con Hadoop, arrástrela y colóquela en el diseñador. Después, haga doble clic en la tarea, o bien haga clic con el botón derecho en ella y luego haga clic en **Editar**para ver el cuadro de diálogo **Editor de la tarea Pig de Hadoop** .  
  
 ![Editor de la tarea Pig de Hadoop](../../integration-services/control-flow/media/hadoop-pig-task.png "Editor de la tarea Pig de Hadoop")  
  
## <a name="options"></a>Opciones  
 Configure las siguientes opciones en el cuadro de diálogo **Hadoop Pig Task Editor** (Editor de tareas de Pig con Hadoop).  
  
|Campo|Descripción|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospeda el servicio WebHCat.|  
|**Tipo de origen**|Especifique el tipo de origen de la consulta. Los valores disponibles son **ScriptFile** y **DirectInput**.|  
|**InlineScript**|Cuando el valor de **SourceType** sea **DirectInput**, especifique el script de Pig.|  
|**HadoopScriptFilePath**|Cuando el valor de **SourceType** sea **ScriptFile**, especifique la ruta de acceso del archivo de script en Hadoop.|  
|**TimeoutInMinutes**|Especifique un valor de tiempo de espera en minutos. El trabajo de Hadoop se detiene si no se ha terminado antes de que transcurra el tiempo de espera. Especifique 0 para programar el trabajo de Hadoop de modo que se ejecute de forma asincrónica.|  
  
## <a name="see-also"></a>Ver también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
