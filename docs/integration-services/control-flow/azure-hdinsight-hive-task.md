---
title: Tarea de Hive de Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af68d13b1391d1e6890f42e8bbba0e0da70ddfed
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="azure-hdinsight-hive-task"></a>Tarea de Hive de HDInsight de Azure
Utilice la **tarea de Hive de HDInsight** para ejecutar el script de Hive en un clúster de HDInsight de Azure.
     
Para agregar una **tarea de Hive de HDInsight de Azure**, arrástrela al Diseñador de SSIS y haga doble clic o haga clic con el botón derecho y haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Hive Task Editor** (Editor de tareas de Hive de HDInsight de Azure).  
  
La **tarea de Hive de Azure HDInsight** es un componente del paquete de características de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 La lista siguiente describe los campos de este cuadro de diálogo.  
  
1.  Para el campo **HDInsightConnection**, seleccione un Administrador de conexiones de Azure HDInsight existente o cree uno nuevo que haga referencia al clúster de Azure que se usó para ejecutar el script.
  
2.  Para el campo **AzureStorageConnection**, seleccione un Administrador de conexiones de Azure Storage existente o cree uno nuevo que haga referencia a una cuenta de Azure Storage asociada con el clúster. Esto solo es necesario si quiere descargar los registros de error y la salida de ejecución del script.
 
3.  Para el campo **BlobContainer**, especifique el nombre del contenedor de almacenamiento asociado con el clúster. Esto solo es necesario si quiere descargar los registros de error y la salida de ejecución del script.
  
4.  Para el campo **LocalLogFolder**, especifique la carpeta en la que se descargarán los registros de error y la salida de ejecución de script. Esto solo es necesario si quiere descargar los registros de error y la salida de ejecución del script.   
  
5.  Hay dos maneras de especificar el script de Hive que se va a ejecutar:
  
    1.  **Script en línea**: especifique el campo **Script** escribiendo en línea el script que quiere ejecutar en el cuadro de diálogo **Escriba el script**.
  
    2.  **Archivo de script**: cargue el archivo de script en Azure Blob Storage y especifique el campo **BlobName**. Si el blob no está en el contenedor ni en la cuenta de almacenamiento predeterminados asociados con el clúster de HDInsight, deben especificarse los campos **ExternalStorageAccountName** y **ExternalBlobContainer**. Para un blob externo, asegúrese de que está configurado como accesible públicamente.  
  
     Si se especifican ambos, se usará el archivo de script y se omitirá el script en línea.
