---
title: Tarea de Pig de Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b07d792d2b73b6fd400835bbfe656bb02db8e18
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727951"
---
# <a name="azure-hdinsight-pig-task"></a>Tarea de Pig de Azure HDInsight

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Utilice la **tarea de Pig de Azure HDInsight** para ejecutar el script de Pig en un clúster de Azure HDInsight.
     
Para agregar una **tarea de Pig de Azure HDInsight**, arrástrela al Diseñador de SSIS y haga doble clic o haga clic con el botón derecho y haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Pig Task Editor** (Editor de tareas de Pig de Azure HDInsight).  
  
La **tarea de Pig de Azure HDInsight** es un componente del paquete de características de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 La lista siguiente describe los campos de este cuadro de diálogo.  
  
1.  Para el campo **HDInsightConnection**, seleccione un Administrador de conexiones de Azure HDInsight existente o cree uno nuevo que haga referencia al clúster de Azure que se usó para ejecutar el script.
  
2.  Para el campo **AzureStorageConnection**, seleccione un Administrador de conexiones de Azure Storage existente o cree uno nuevo que haga referencia a una cuenta de Azure Storage asociada con el clúster. Esto solo es necesario si quiere descargar los registros de error y la salida de ejecución del script.
 
3.  Para el campo **BlobContainer**, especifique el nombre del contenedor de almacenamiento asociado con el clúster. Esto solo es necesario si quiere descargar los registros de error y la salida de ejecución del script.
  
4.  Para el campo **LocalLogFolder**, especifique la carpeta en la que se descargarán los registros de error y la salida de ejecución de script. Esto solo es necesario si quiere descargar los registros de error y la salida de ejecución de script.   
  
5.  Hay dos maneras de especificar el script de Pig que se va a ejecutar:
  
    1.  **Script insertado**: para especificar el campo **Script**, escriba el script insertado que quiere ejecutar en el cuadro de diálogo **Escriba el script**.
  
    2.  **Archivo de script**: cargue el archivo de script en Azure Blob Storage y especifique el campo **BlobName**. Si el blob no está en el contenedor ni en la cuenta de almacenamiento predeterminados asociados con el clúster de HDInsight, deben especificarse los campos **ExternalStorageAccountName** y **ExternalBlobContainer**. Para un blob externo, asegúrese de que está configurado como accesible públicamente.  
  
     Si se especifican ambos, se usará el archivo de script y se omitirá el script en línea.
