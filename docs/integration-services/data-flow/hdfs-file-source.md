---
title: Origen de archivo HDFS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9cb4cf4a297a362ada965c3135f7e03fc8304ac2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720523"
---
# <a name="hdfs-file-source"></a>Origen de archivo HDFS
  El componente de origen de archivo HDFS permite que un paquete SSIS lea datos desde un archivo HDFS. Los formatos de archivo admitidos son Text y Avro. (No se admiten los orígenes ORC).  
  
 Para configurar el componente de origen de archivo HDFS, arrastre y suelte el origen de archivo HDFS en el diseñador de flujo de datos y haga doble clic en el componente para abrir el editor.  
  
 ![Editor de origen de archivo HDFS](../../integration-services/data-flow/media/hdfs-file-source.png "HDFS File Source Editor")  
  
## <a name="options"></a>Opciones  
 Configure las opciones siguientes en la pestaña **General** del cuadro de diálogo **Hadoop File Source Editor** (Editor de origen de archivo Hadoop).  
  
|Campo|Descripción|  
|-----------|-----------------|  
|**Hadoop Connection (Conexión de Hadoop)**|Especifique un administrador de conexiones de Hadoop existente o cree uno nuevo. Este administrador de conexiones indica dónde se hospedan los archivos HDFS.|  
|**Ruta del archivo**|Especifique el nombre del archivo HDFS.|  
|**Formato de archivo**|Especifique el formato del archivo HDFS. Las opciones disponibles son Text y Avro. (No se admiten los orígenes ORC).|  
|**Carácter delimitador de columna**|Si selecciona el formato Text, especifique el carácter delimitador de columna.|  
|**Nombres de columna de la primera fila de datos**|Si selecciona el formato Text, indique si la primera fila del archivo contiene nombres de columnas.|  
  
 Después de configurar estas opciones, seleccione la pestaña **Columna** para asignar columnas de origen a columnas de destino del flujo de datos.  
  
## <a name="see-also"></a>Ver también  
 [Administrador de conexiones de Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Destino de archivo HDFS](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
