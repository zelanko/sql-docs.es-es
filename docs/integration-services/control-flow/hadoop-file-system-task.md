---
title: "Tarea Sistema de archivos de Hadoop | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.hadoopfiletask.f1"
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Tarea Sistema de archivos de Hadoop
  La tarea Sistema de archivos de Hadoop permite que un paquete SSIS copie archivos de, en o dentro de un clúster de Hadoop.  
  
 Para agregar una tarea Sistema de archivos de Hadoop, arrástrela y colóquela en el diseñador. Luego, haga doble clic en la tarea, o bien haga clic en ella con el botón derecho y, después, haga clic en **Editar** para abrir el cuadro de diálogo **Editor de la tarea Sistema de archivos de Hadoop**.  
  
 ![Hadoop File System Task Editor](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Hadoop File System Task Editor")  
  
## Opciones  
 Configure las siguientes opciones en el cuadro de diálogo **Hadoop File System Task Editor** (Editor de la tarea Sistema de archivos de Hadoop).  
  
|Campo|Description|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos de destino.|  
|**Hadoop File Path (Ruta de acceso del archivo de Hadoop)**|Especifique la ruta del archivo o del directorio en HDFS.|  
|**Hadoop File Type (Tipo de archivo de Hadoop)**|Especifique si el objeto del sistema de archivos HDFS es un archivo o directorio.|  
|**Overwrite Destination (Sobrescribir destino)**|Especifique si sobrescribir el archivo de destino si ya existe.|  
|**Operación**|Especifique la operación. Las operaciones disponibles son **CopyToHDFS**, **CopyFromHDFS**y **CopyWithinHDFS**.|  
|**Local File Connection (Conexión de archivo local)**|Especifique un administrador de conexiones de archivos existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos de origen.|  
|**Is Recursive (Recursivo)**|Especifique si desea copiar todas las subcarpetas de forma recursiva.|  
  
## Vea también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md)  
  
  