---
title: Tarea de Hive de HDInsight de Azure | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f9e67e91b5cd38482ab1151d5942c9c55c04136c
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-hive-task"></a>Tarea de Hive de HDInsight de Azure
Utilice la **tarea de Hive de HDInsight** para ejecutar el script de Hive en un clúster de HDInsight de Azure.
     
Para agregar una **tarea de Hive de HDInsight de Azure**, arrástrela al Diseñador de SSIS y haga doble clic o haga clic con el botón derecho y haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Hive Task Editor** (Editor de tareas de Hive de HDInsight de Azure).  
  
El **tarea de Hive de HDInsight de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 La lista siguiente describe los campos de este cuadro de diálogo.  
  
1.  Para el **HDInsightConnection** campo, seleccione un administrador de conexiones de HDInsight de Azure existente o cree uno nuevo que hace referencia al clúster de HDInsight de Azure usa para ejecutar el script.
  
2.  Para el **AzureStorageConnection** campo, seleccione un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que hace referencia a la cuenta de almacenamiento de Azure asociado con el clúster. Esto solo es necesario si desea descargar los registros de salida y el error de ejecución de secuencia de comandos.
 
3.  Para el **BlobContainer** , a continuación, especifique el nombre de contenedor de almacenamiento asociado con el clúster. Esto solo es necesario si desea descargar los registros de salida y el error de ejecución de secuencia de comandos.
  
4.  Para el **LocalLogFolder** campo, especifique la carpeta a la que se descargarán los registros de salida y el error de ejecución de scripts en. Esto solo es necesario si desea descargar los registros de salida y el error de ejecución de secuencia de comandos.   
  
5.  Hay dos maneras de especificar el script de Hive para ejecutar:
  
    1.  **Secuencia de comandos en línea**: especifique la **Script** campo escribiendo en línea de la secuencia de comandos para ejecutar en el **escribir Script** cuadro de diálogo.
  
    2.  **Archivo de script**: cargue el archivo de script al almacenamiento de blobs de Azure y especifique el **BlobName** campo. Si el blob no está en la cuenta de almacenamiento predeterminada o el contenedor asociado con el clúster de HDInsight, el **ExternalStorageAccountName** y **ExternalBlobContainer** campos deben especificarse. Para un blob externo, asegúrese de que está configurado como públicamente accesible.  
  
     Si se especifican ambos, se usará el archivo de script y se pasará por alto la secuencia de comandos en línea.

