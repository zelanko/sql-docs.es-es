---
title: Destino de archivo HDFS | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d07d4efaa0b26a19f60ca27e465177d0ea7b797c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="hdfs-file-destination"></a>HDFS File Destination
  El componente HDFS File Destination (Destino de archivo HDFS) permite que un paquete SSIS escriba datos en un archivo HDFS. Los formatos de archivo admitidos son Text, Avro y ORC.  
  
 Para configurar el componente HDFS File Destination, arrastre y coloque el componente HDFS File Source (Origen de archivo HDFS) en el diseñador de flujo de datos y haga doble clic en el componente para abrir el editor.  
  
 ![Editor de destino de archivo HDFS](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS File Destination Editor")  
  
## <a name="options"></a>Opciones  
 Configure las siguientes opciones en la pestaña **General** del cuadro de diálogo **Hadoop File Destination Editor** (Editor de destino de archivo Hadoop).  
  
|Campo|Description|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos HDFS.|  
|**Ruta del archivo**|Especifique el nombre del archivo HDFS.|  
|**Formato de archivo**|Especifique el formato del archivo HDFS. Las opciones disponibles son Text, Avro y ORC.|  
|**Carácter delimitador de columna**|Si selecciona el formato Text, especifique el carácter delimitador de columna.|  
|**Nombres de columna de la primera fila de datos**|Si selecciona el formato Text, indique si la primera fila del archivo contiene nombres de columnas.|  
  
 Después de configurar estas opciones, seleccione la pestaña **Columna** para asignar columnas de origen a columnas de destino del flujo de datos.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Origen de archivo HDFS](../../integration-services/data-flow/hdfs-file-source.md)  
  
  
