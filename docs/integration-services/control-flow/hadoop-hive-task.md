---
title: Tarea de Hive de Hadoop | Microsoft Docs
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
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff68c0634886c148325129a9c17394ba1dc43802
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35401477"
---
# <a name="hadoop-hive-task"></a>Tarea de Hive de Hadoop
  Utilice la tarea de Hive de Hadoop para ejecutar el script de Hive en un clúster de Hadoop.  
  
 Para agregar una tarea de Hive de Hadoop, arrástrela y suéltela en el diseñador. Después, haga doble clic en la tarea (o haga clic con el botón derecho y seleccione **Editar**) para abrir el cuadro de diálogo **Editor de la tarea Hive de Hadoop** .  
  
 ![Editor de la tarea Hive de Hadoop](../../integration-services/control-flow/media/hadoop-hive-task.png "Editor de la tarea Hive de Hadoop")  
  
## <a name="options"></a>Opciones  
 Configure las siguientes opciones en el cuadro de diálogo **Hadoop Hive Task Editor** (Editor de tareas de Hive de Hadoop).  
  
|Campo|Descripción|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospeda el servicio WebHCat.|  
|**Tipo de origen**|Especifique el tipo de origen de la consulta. Los valores disponibles son **ScriptFile** y **DirectInput**.|  
|**InlineScript**|Cuando el valor de **SourceType** sea **DirectInput**, especifique el script de Hive.|  
|**HadoopScriptFilePath**|Cuando el valor de **SourceType** sea **ScriptFile**, especifique la ruta de acceso del archivo de script en Hadoop.|  
|**TimeoutInMinutes**|Especifique un valor de tiempo de espera en minutos. El trabajo de Hadoop se detiene si no se ha terminado antes de que transcurra el tiempo de espera. Especifique 0 para programar el trabajo de Hadoop de modo que se ejecute de forma asincrónica.|  
  
## <a name="see-also"></a>Ver también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
