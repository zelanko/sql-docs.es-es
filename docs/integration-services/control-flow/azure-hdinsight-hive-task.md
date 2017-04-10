---
title: "Tarea de Hive de HDInsight de Azure | Microsoft Docs"
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
  - "sql13.dts.designer.afphivetask.f1"
  - "sql14.dts.designer.afphivetask.f1"
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Tarea de Hive de HDInsight de Azure
  Utilice la **tarea de Hive de HDInsight** para ejecutar el script de Hive en un clúster de HDInsight de Azure.
     
Para agregar una **tarea de Hive de HDInsight de Azure**, arrástrela al Diseñador de SSIS y haga doble clic o haga clic con el botón derecho y haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Hive Task Editor** (Editor de tareas de Hive de HDInsight de Azure).  
  
 La **tarea de Hive de HDInsight Azure** es un componente del Feature Pack de SQL Server Integration Services (SSIS) para Azure para SQL Server 2016. Descargue el Feature Pack [aquí](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
 La lista siguiente describe los campos de este cuadro de diálogo.  
  
1.  Para el campo **AzureSubscriptionConnection** , seleccione un Administrador de conexiones de suscripciones de Azure o cree uno nuevo que haga referencia a una suscripción de Azure que hospede el clúster de HDInsight.  
  
2.  Para el campo **HDInsightClusterName** , seleccione el nombre del clúster de HDInsight en el que desea ejecutar el script de Hive.  
  
3.  Para el campo **LocalLogFolder**, haga clic en **…** (puntos suspensivos) y seleccione la carpeta en la que quiere descargar los registros de procesamiento de Hive desde el clúster de HDInsight.  
  
4.  Hay dos maneras de especificar el script de Hive:  
  
    1.  **Script en línea**: haga clic en **… (puntos suspensivos)** junto al campo **Script** y escriba el script en línea en el cuadro de diálogo **Escriba el script**.  
  
    2.  **Archivo de script**: cargue el archivo de script en una ubicación de blob y especifique su valor de **BlobName**. Si el blob no está en el almacenamiento o contenedor predeterminado del clúster de HDInsight, se deben especificar los valores **ExternalStorageAccountName** y **ExternalBlobContainer** . Para blobs externos, asegúrese de que está configurado como accesible públicamente.  
  
     Si se especifican ambos, se usará el archivo de script y se omitirá el script en línea.  
  
  