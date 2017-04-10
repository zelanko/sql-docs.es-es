---
title: "Origen de blobs de Azure | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobsrc.f1"
  - "sql14.dts.designer.afpblobsrc.f1"
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Origen de blobs de Azure
  El componente **Azure Blob Source** (Origen de blobs de Azure) permite que un paquete SSIS lea datos de un blob de Azure. Los formatos de archivo admitidos son: CSV y AVRO.
  
>   [!NOTE] Para garantizar que el Administrador de conexiones de Almacenamiento de Azure y los componentes que lo usan (es decir, el origen y el destino de blob y las tareas de carga y descarga de blobs) se puedan conectar tanto a las cuentas de almacenamiento general como a las cuentas de almacenamiento de blobs, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). Para obtener más información sobre estos dos tipos de cuentas de almacenamiento, vea [Introducción a Almacenamiento de Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).
  
  Para ver el editor del origen de blob de Azure, arrastre y coloque el **origen de blob de Azure** en el diseñador de flujos de datos y haga doble clic en él para abrir el editor.  
  
 El **origen de blobs de Azure** es un componente de SQL Server Integration Services (SSIS) Feature Pack para Azure para SQL Server 2016. Descargue el Feature Pack [aquí](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
1.  En el campo **Azure storage connection manager** (Administrador de conexiones de almacenamiento de Azure), especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure.  
  
2.  En el campo **Nombre de contenedor de blobs** , especifique el nombre del contenedor de blobs que contiene los archivos de origen.  
  
3.  En el campo **Nombre de blob** , especifique la ruta de acceso al blob.  
  
4.  En el campo **Blob file format** (Formato de archivo de blob), especifique el formato de blob que desea utilizar.  
  
5.  Si el formato de archivo es CSV, debe especificar el valor **Column delimiter character** (Carácter delimitador de columna). Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
6.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
  
  