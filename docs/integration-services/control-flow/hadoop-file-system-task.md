---
title: Tarea Sistema de archivos de Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 21322c2b4c6cc410cdfae62e59f3e24094740c2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757003"
---
# <a name="hadoop-file-system-task"></a>Tarea Sistema de archivos de Hadoop
  La tarea Sistema de archivos de Hadoop permite que un paquete SSIS copie archivos de, en o dentro de un clúster de Hadoop.  
  
 Para agregar una tarea Sistema de archivos de Hadoop, arrástrela y colóquela en el diseñador. Luego, haga doble clic en la tarea, o bien haga clic en ella con el botón derecho y, después, haga clic en **Editar**para abrir el cuadro de diálogo **Editor de la tarea Sistema de archivos de Hadoop** .  
  
 ![Editor de la tarea Sistema de archivos de Hadoop](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Editor de la tarea Sistema de archivos de Hadoop")  
  
## <a name="options"></a>Opciones  
 Configure las siguientes opciones en el cuadro de diálogo **Hadoop File System Task Editor** (Editor de la tarea Sistema de archivos de Hadoop).  
  
|Campo|Descripción|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos de destino.|  
|**Hadoop File Path (Ruta de acceso del archivo de Hadoop)**|Especifique la ruta del archivo o del directorio en HDFS.|  
|**Hadoop File Type (Tipo de archivo de Hadoop)**|Especifique si el objeto del sistema de archivos HDFS es un archivo o directorio.|  
|**Overwrite Destination (Sobrescribir destino)**|Especifique si sobrescribir el archivo de destino si ya existe.|  
|**Operación**|Especifique la operación. Las operaciones disponibles son **CopyToHDFS**, **CopyFromHDFS**y **CopyWithinHDFS**.|  
|**Local File Connection (Conexión de archivo local)**|Especifique un administrador de conexiones de archivos existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos de origen.|  
|**Is Recursive (Recursivo)**|Especifique si desea copiar todas las subcarpetas de forma recursiva.|  
  
## <a name="see-also"></a>Ver también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
