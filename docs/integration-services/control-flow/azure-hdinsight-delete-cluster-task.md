---
title: "Tarea de eliminación de HDInsight de Azure de clúster | Documentos de Microsoft"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f98b69e8bd3b2e78f6dd20a19ca17a83a834c3b3
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-delete-cluster-task"></a>Tarea de eliminación de clúster de HDInsight de Azure
El **tarea de clúster de eliminación de HDInsight de Azure** permite que un paquete SSIS elimine un clúster de HDInsight de Azure en el grupo de recursos y la suscripción de Azure especificado.
  
El **tarea de clúster de eliminación de HDInsight de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]
> Eliminación de un clúster de HDInsight puede tardar 10 ~ 20 minutos.  
  
Para agregar una **tarea de eliminación de clúster de HDInsight de Azure**, arrástrela y suéltela en el Diseñador SSIS y haga doble clic o haga clic con el botón derecho y luego haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Delete Cluster Task Editor** (Editor de tareas de eliminación de clúster de HDInsight de Azure).  
  
En la tabla siguiente proporciona una descripción de los campos en el cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureResourceManagerConnection|Seleccione un administrador de conexiones del Administrador de recursos Azure existente o cree uno nuevo que se usarán para eliminar el clúster de HDInsight.|
|Id. de suscripción|Especificar el identificador de la suscripción en que es el clúster de HDInsight.|
|Grupo de recursos|Especifique el clúster de HDInsight está en el grupo de recursos de Azure.|
|nombreDeClúster|Especifique el nombre del clúster que se va a eliminar.|  
|FailIfNotExists|Especifique si la tarea debe generar un error si no existe el clúster.|

