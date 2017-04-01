---
title: "Tarea de Pig de Azure HDInsight | Microsoft Docs"
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
  - "sql13.dts.designer.afppigtask.f1"
  - "sql14.dts.designer.afppigtask.f1"
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tarea de Pig de Azure HDInsight
  Utilice la **tarea de Pig de Azure HDInsight** para ejecutar el script de Pig en un clúster de Azure HDInsight. 
    
Para agregar una **tarea de Pig de Azure HDInsight**, arrástrela al Diseñador de SSIS y haga doble clic o haga clic con el botón derecho y haga clic en **Editar** para ver el siguiente cuadro de diálogo: **Azure HDInsight Pig Task Editor** (Editor de tareas de Pig de Azure HDInsight).  
  
 La **tarea de Pig de Azure HDInsight** es un componente del paquete de características de SQL Server Integration Services (SSIS) para Azure para SQL Server 2016. Descargue el Feature Pack [aquí](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
1.  Para el campo **AzureSubscriptionConnection** , seleccione un Administrador de conexiones de suscripciones de Azure o cree uno nuevo que haga referencia a una suscripción de Azure que hospede el clúster de HDInsight.  
  
2.  Para el campo **HDInsightClusterName** , escriba el nombre del clúster de HDInsight en el que quiere ejecutar el script de Pig.  
  
3.  Para el campo **LocalLogFolder**, haga clic en **… (puntos suspensivos)** y seleccione la carpeta en la que quiere descargar los registros de procesamiento de Pig desde el clúster de HDInsight.  
  
4.  Hay dos maneras de especificar el script de Pig:  
  
    1.  **Script en línea**: haga clic en **… (puntos suspensivos)** junto al campo **Script** y escriba el script en línea en el cuadro de diálogo **Escriba el script**.  
  
    2.  **Archivo de script**: cargue el archivo de script en una ubicación de blob y especifique su valor de **BlobName**. Si el blob no está en el almacenamiento o contenedor predeterminado del clúster de HDInsight, se deben especificar los valores **ExternalStorageAccountName** y **ExternalBlobContainer** . Para blobs externos, asegúrese de que está configurado como accesible públicamente.  
  
     Si se especifican ambos, se usará el archivo de script y se omitirá el script en línea.  
  
  