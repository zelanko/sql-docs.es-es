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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 006c9d5ae0ade37cc3ecbe4d7912c49eafbf4069
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918218"
---
# <a name="hadoop-file-system-task"></a>Tarea Sistema de archivos de Hadoop

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
|**operación**|Especifique la operación. Las operaciones disponibles son **CopyToHDFS**, **CopyFromHDFS**y **CopyWithinHDFS**.|  
|**Local File Connection (Conexión de archivo local)**|Especifique un administrador de conexiones de archivos existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos de origen.|  
|**Is Recursive (Recursivo)**|Especifique si desea copiar todas las subcarpetas de forma recursiva.|  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
