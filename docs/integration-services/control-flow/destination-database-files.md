---
title: Archivos de base de datos de destino | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 592000ef801a0845468d37a12a5e1515f590848a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="destination-database-files"></a>Archivos de la base de datos de destino
  Utilice el cuadro de diálogo **Archivos de la base de datos de destino** para ver o cambiar las ubicaciones y los nombres de archivos de la base de datos en el servidor de destino o para especificar una ubicación de archivo de red para la tarea Transferir bases de datos. Para más información sobre esta tarea, vea [Tarea Transferir bases de datos](../../integration-services/control-flow/transfer-database-task.md).  
  
 Para rellenar automáticamente este cuadro de diálogo con las ubicaciones y los nombres de archivos de la base de datos en el servidor de origen, especifique primero **SourceConnection**, **SourceDatabaseName**y **SourceDatabaseFiles** en la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** .  
  
## <a name="options"></a>Opciones  
 **Archivo de destino**  
 Nombres de los archivos de base de datos transferidos en el servidor de destino.  
  
 Escriba el nombre del archivo o haga clic en el nombre para editarlo.  
  
 **Carpeta de destino**  
 Carpeta del servidor de destino a la que se transferirán los archivos de la base de datos.  
  
 Escriba la ruta a la carpeta, haga clic en la ruta para editarla o bien, haga clic para examinar y buscar la carpeta donde desea transferir los archivos de la base de datos en el servidor de destino.  
  
 **Recurso compartido de archivos de red**  
 Carpeta compartida de red en el servidor de destino a la que se transferirán los archivos de la base de datos. Utilice **Recurso compartido de archivos de red** cuando transfiera una base de datos en el modo sin conexión especificando el **Método** **DatabaseOffline** en la página **Bases de datos** del cuadro de diálogo **Editor de la tarea Transferir bases de datos** .  
  
 Escriba la ubicación del recurso compartido de archivos de red o haga clic para examinar y buscar la ubicación del recurso compartido del archivo de red.  
  
 Cuando transfiera una base de datos en el modo sin conexión, los archivos se copian en la ubicación **Recurso compartido de archivos de red** antes de transferirlos a la ubicación **Carpeta de destino** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea de transferencia de base de datos &#40; Página general &#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [Editor de la tarea de transferencia de base de datos &#40; página bases de datos &#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  
