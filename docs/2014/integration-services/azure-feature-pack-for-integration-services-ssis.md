---
title: Azure Feature Pack de | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 536dce64880c1e70b1b8a0c4b419811c1b32a975
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394533"
---
# <a name="azure-feature-pack"></a>Feature Pack de Azure
Feature Pack de SQL Server Integration Services (SSIS) para Azure es una extensión que proporciona los componentes que se muestran en esta página para que SSIS se conecte a los servicios de Azure, para transferir datos entre Azure y orígenes de datos locales, y para procesar los datos almacenados en Azure.

## <a name="components-in-the-feature-pack"></a>Componentes de Feature Pack
  
-   Administradores de conexión  
  
    -   [Administrador de conexiones de almacenamiento de Azure](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Administrador de conexiones de suscripciones de Azure](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Administrador de conexiones de Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Administrador de conexiones de Azure Resource Manager](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Administrador de conexiones de Azure HDInsight](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   Tareas  
  
    -   [Tarea de carga de blobs de Azure](control-flow/azure-blob-upload-task.md)  
  
    -   [Tarea de descarga de blobs de Azure](control-flow/azure-blob-download-task.md)  
  
    -   [Tarea de Hive de HDInsight de Azure](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Tarea de Pig de Azure HDInsight](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Tarea de creación de clúster de HDInsight de Azure](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Tarea de eliminación de clúster de HDInsight de Azure](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Tarea de carga de Azure SQL DW](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Tarea Sistema de archivos de Azure Data Lake Store](control-flow/file-system-task.md)    
  
-   Componentes de flujo de datos  
  
    -   [Origen de blobs de Azure](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Destino de blobs de Azure](data-flow/azure-blob-destination.md)  
    
    -   [Origen de Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Destino de Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Enumerador de blobs de Azure y enumerador de archivos ADLS. Consulte [Foreach Loop Container](control-flow/foreach-loop-container.md).  
  
 
## <a name="download-the-feature-pack"></a>Descarga del Feature Pack  
Descargue Feature Pack de SQL Server Integration Services (SSIS) para Azure.  
  
-   [Microsoft SQL Server 2014 Integration Services Feature Pack para Azure](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>Requisitos previos  
Necesita instalar los siguientes requisitos previos antes de instalar este Feature Pack.  
  
-   SQL Server Integration Services  
-   .Net Framework 4.5  
  
## <a name="scenarios"></a>Escenarios  
  
### <a name="big-data-processing"></a>Procesamiento de macrodatos  
 Use el Conector Azure para completar el trabajo de procesamiento de macrodatos siguiente:  
  
1.  Utilice la tarea de carga de blobs de Azure para cargar datos de entrada en el almacenamiento de blobs de Azure.  
  
2.  Utilice la tarea de creación de clúster de HDInsight de Azure para crear un clúster de HDInsight de Azure. Este paso es opcional si quiere utilizar su propio clúster.  
  
3.  Utilice la tarea de Hive de HDInsight de Azure o la tarea de Pig de HDInsight de Azure para invocar un trabajo de Pig o Hive en el clúster de HDInsight de Azure.  
  
4.  Utilice la tarea de eliminación de clúster de HDInsight de Azure para eliminar el clúster de HDInsight tras su uso si creó un clúster de HDInsight a petición en el paso 2.  
  
5.  Utilice la tarea de descarga de blobs de HDInsight de Azure para descargar los datos de salida de Pig o Hive del almacenamiento de blobs de Azure.  
  
 ![SSIS-AzureConnector-BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "SSIS-AzureConnector-BigDataScenario")  
  
### <a name="cloud-data-archiving"></a>Archivado de datos en la nube  
 Use el destino de blobs de Azure en un paquete de SSIS para escribir los datos de salida en un almacenamiento de blobs de Azure o para utilizar el origen de blobs de Azure para leer datos desde un almacenamiento de blobs de Azure.  
  
 ![SSIS-AzureConnector-CloudArchive-1](media/ssis-azureconnector-cloudarchive-1.png "SSIS-AzureConnector-CloudArchive-1")  
  
 ![SSIS-AzureConnector-CloudArchive-2](media/ssis-azureconnector-cloudarchive-2.png "SSIS-AzureConnector-CloudArchive-2")  
  
 Y utilice el contenedor de bucles Foreach con el enumerador de blobs de Azure para procesar los datos de varios archivos de blob.  
  
 ![SSIS-AzureConnector-CloudArchive-3](media/ssis-azureconnector-cloudarchive-3.png "SSIS-AzureConnector-CloudArchive-3")  
  
  
