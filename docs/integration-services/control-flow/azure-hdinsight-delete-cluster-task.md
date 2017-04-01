---
title: "Tarea de eliminaci&#243;n de cl&#250;ster de HDInsight de Azure | Microsoft Docs"
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
  - "sql13.dts.designer.afpdelcltask.f1"
  - "sql14.dts.designer.afpdelcltask.f1"
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tarea de eliminaci&#243;n de cl&#250;ster de HDInsight de Azure
  La **tarea de eliminación de clúster de HDInsight de Azure** permite que un paquete SSIS elimine un clúster de HDInsight de Azure en la suscripción de Azure especificada.  
  
 La **tarea de eliminación de clúster de HDInsight de Azure** es un componente del Feature Pack de SQL Server Integration Services (SSIS) para Azure para SQL Server 2016. Descargue el Feature Pack [aquí](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
> [!NOTE]  
>  La eliminación de un clúster de HDInsight normalmente tarda 10 minutos.  
  
 Para agregar una **tarea de eliminación de clúster de HDInsight de Azure**, arrástrela y suéltela en el Diseñador SSIS y haga doble clic o haga clic con el botón derecho y luego haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Delete Cluster Task Editor** (Editor de tareas de eliminación de clúster de HDInsight de Azure).  
  
 En la tabla siguiente se proporciona la descripción de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureSubscriptionConnection|Seleccione un administrador de conexión de suscripción de Azure existente o cree uno nuevo que haga referencia a una suscripción de Azure que hospede el clúster de HDInsight.|  
|nombreDeClúster|Especifique el nombre del clúster que se va a eliminar.|  
|FailIfNotExists|Especifique si la tarea debe generar un error si no existe el clúster.|  
  
  