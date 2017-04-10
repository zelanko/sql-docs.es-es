---
title: "Tarea de creaci&#243;n de cl&#250;ster de HDInsight de Azure | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpcreatecltask.f1"
  - "sql14.dts.designer.afpcreatecltask.f1"
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Tarea de creaci&#243;n de cl&#250;ster de HDInsight de Azure
  La **tarea de creación de clúster de HDInsight de Azure** permite que un paquete SSIS cree un clúster de HDInsight de Azure en la suscripción de Azure especificada.  
  
 La **tarea de creación de clúster de HDInsight de Azure** es un componente de SQL Server Integration Services (SSIS) Feature Pack para Azure para SQL Server 2016. Descargue el Feature Pack [aquí](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
> [!NOTE]  
>  -   La creación de un clúster de HDInsight normalmente tarda 10 minutos.  
> -   Hay un costo asociado con la creación y ejecución de un clúster de HDInsight de Azure. Vea el tema [HDInsight Precios](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) para más información.  
  
 Para agregar una **tarea de creación de clúster de HDInsight de Azure**, arrástrela y colóquela en el Diseñador SSIS y haga doble clic (o haga clic con el botón derecho y, después, haga clic en **Editar**) para ver el siguiente cuadro de diálogo del **Editor de la tarea de creación de clúster de HDInsight de Azure**.  
  
 En la tabla siguiente se proporciona la descripción de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureSubscriptionConnection|Seleccione un administrador de conexión de suscripción de Azure existente o cree uno nuevo que haga referencia a una suscripción de Azure que hospede el clúster de HDInsight.|  
|AzureStorageConnection|Seleccione un administrador de conexiones de almacenamiento de Azure existente o cree uno que haga referencia a una cuenta de almacenamiento de Azure que se asociará con el clúster de HDInsight.|  
|Ubicación|Especifique la ubicación del clúster de HDInsight. El clúster debe crearse en la misma ubicación que el almacenamiento de Azure.|  
|nombreDeClúster|Especifique un nombre para el clúster de HDInsight que se va a crear.|  
|ClusterSize|Especifique el número de nodos que desea tener en el clúster.|  
|BlobContainer|Especifique el nombre del contenedor de almacenamiento predeterminado asociado con el clúster de HDInsight.|  
|UserName|Especifique el nombre del usuario que tiene acceso al clúster.|  
|Contraseña|Especifique la contraseña para el usuario.|  
|FailIfExists|Especifique si la tarea debe generar un error si el clúster ya existe.|  
  
> [!NOTE]  
>  La ubicación del clúster de HDInsight y del almacenamiento de Azure debe ser la misma.  
  
  