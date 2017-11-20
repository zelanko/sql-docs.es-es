---
title: "HDInsight de Azure crear tarea de clúster | Documentos de Microsoft"
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
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 71a24dc15253916c32b07e6024e2ab32514c9d39
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-create-cluster-task"></a>Tarea de creación de clúster de HDInsight de Azure
El **crear tarea a clúster de HDInsight de Azure** permite que un paquete SSIS crear un clúster de HDInsight de Azure en el grupo de recursos y la suscripción de Azure especificado.
  
El **crear tarea a clúster de HDInsight de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
> [!NOTE]  
> - Crear un nuevo clúster de HDInsight puede tardar 10 ~ 20 minutos.  
> - Hay un costo asociado a la creación y ejecución de un clúster de HDInsight de Azure. Vea [precios HDInsight](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) para obtener más información.  
  
Para agregar una **tarea de creación de clúster de HDInsight de Azure**, arrástrela y colóquela en el Diseñador SSIS y haga doble clic (o haga clic con el botón derecho y, después, haga clic en **Editar** ) para ver el siguiente cuadro de diálogo del **Editor de la tarea de creación de clúster de HDInsight de Azure** .  
  
En la tabla siguiente proporciona una descripción de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureResourceManagerConnection|Seleccione un administrador de conexiones del Administrador de recursos Azure existente o cree uno nuevo que se usará para crear el clúster de HDInsight.|  
|AzureStorageConnection|Seleccione un administrador de conexiones de almacenamiento de Azure existente o cree uno que haga referencia a una cuenta de almacenamiento de Azure que se asociará con el clúster de HDInsight.|
|Id. de suscripción|Especificar el identificador de la suscripción que se creará en el clúster de HDInsight.|
|Grupo de recursos|Especifique el recurso de Azure agrupar el clúster se creará en de HDInsight.|
|Ubicación|Especifique la ubicación del clúster de HDInsight. El clúster debe crearse en la misma ubicación que la cuenta de almacenamiento de Azure especificada.|  
|nombreDeClúster|Especifique un nombre para el clúster de HDInsight que se va a crear.|  
|ClusterSize|Especifique el número de nodos que se va a crear en el clúster.|  
|BlobContainer|Especifique el nombre del contenedor de almacenamiento predeterminado que se asociará con el clúster de HDInsight.|  
|UserName|Especifique el nombre de usuario que se usará para conectarse al clúster de HDInsight.|  
|Contraseña|Especifique la contraseña que se usará para conectarse al clúster de HDInsight.|
|SshUserName|Especifique el nombre de usuario utilizado para acceder de forma remota el clúster de HDInsight mediante SSH.|
|SshPassword|Especifique la contraseña utilizada para acceder de forma remota el clúster de HDInsight mediante SSH.|
|FailIfExists|Especifique si la tarea debe generar un error si el clúster ya existe.|  
  
> [!NOTE]  
> Las ubicaciones del clúster de HDInsight y la cuenta de almacenamiento de Azure deben ser el mismo.

