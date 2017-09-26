---
title: Tarea de Pig de HDInsight de Azure | Documentos de Microsoft
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
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9874b119b634966b146f8fa9d22c016bcd91617b
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-pig-task"></a>Tarea de Pig de Azure HDInsight
Utilice la **tarea de Pig de Azure HDInsight** para ejecutar el script de Pig en un clúster de Azure HDInsight.
     
Para agregar una **tarea de Pig de Azure HDInsight**, arrástrela al Diseñador de SSIS y haga doble clic o haga clic con el botón derecho y haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Pig Task Editor** (Editor de tareas de Pig de Azure HDInsight).  
  
El **tarea de Pig de HDInsight de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 La lista siguiente describe los campos de este cuadro de diálogo.  
  
1.  Para el **HDInsightConnection** campo, seleccione un administrador de conexiones de HDInsight de Azure existente o cree uno nuevo que hace referencia al clúster de HDInsight de Azure usa para ejecutar el script.
  
2.  Para el **AzureStorageConnection** campo, seleccione un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que hace referencia a la cuenta de almacenamiento de Azure asociado con el clúster. Esto solo es necesario si desea descargar los registros de salida y el error de ejecución de secuencia de comandos.
 
3.  Para el **BlobContainer** , a continuación, especifique el nombre de contenedor de almacenamiento asociado con el clúster. Esto solo es necesario si desea descargar los registros de salida y el error de ejecución de secuencia de comandos.
  
4.  Para el **LocalLogFolder** campo, especifique la carpeta a la que se descargarán los registros de salida y el error de ejecución de scripts en. Esto solo es necesario si desea descargar los registros de salida y el error de ejecución de secuencia de comandos.   
  
5.  Hay dos maneras de especificar el script de Pig para ejecutar:
  
    1.  **Secuencia de comandos en línea**: especifique la **Script** campo escribiendo en línea de la secuencia de comandos para ejecutar en el **escribir Script** cuadro de diálogo.
  
    2.  **Archivo de script**: cargue el archivo de script al almacenamiento de blobs de Azure y especifique el **BlobName** campo. Si el blob no está en la cuenta de almacenamiento predeterminada o el contenedor asociado con el clúster de HDInsight, el **ExternalStorageAccountName** y **ExternalBlobContainer** campos deben especificarse. Para un blob externo, asegúrese de que está configurado como públicamente accesible.  
  
     Si se especifican ambos, se usará el archivo de script y se pasará por alto la secuencia de comandos en línea.

