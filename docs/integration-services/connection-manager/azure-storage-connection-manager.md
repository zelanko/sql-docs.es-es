---
title: "Administrador de conexiones de Almacenamiento de Azure | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpstorageconn.f1"
  - "sql14.dts.designer.afpstorageconn.f1"
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Administrador de conexiones de Almacenamiento de Azure
  El **Administrador de conexiones de Almacenamiento de Azure** habilita un paquete SSIS para conectarse a una cuenta de Almacenamiento de Azure utilizando los valores especificados para las propiedades nombre de cuenta y clave de cuenta de almacenamiento.  
  
>   [!NOTE] Para garantizar que el Administrador de conexiones de Almacenamiento de Azure y los componentes que lo usan (es decir, el origen y el destino de blob y las tareas de carga y descarga de blobs) se puedan conectar tanto a las cuentas de almacenamiento general como a las cuentas de almacenamiento de blobs, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). Para obtener más información sobre estos dos tipos de cuentas de almacenamiento, vea [Introducción a Almacenamiento de Microsoft Azure](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).
  
 El **Administrador de conexiones de Almacenamiento de Azure** es un componente de SQL Server Integration Services (SSIS) Feature Pack para Azure para SQL Server 2016. Descargue el Feature Pack [aquí](http://go.microsoft.com/fwlink/?LinkID=626967).  
  
1.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **AzureStorage**y haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo Azure Storage Connection Manager Editor (Editor del administrador de conexiones de Almacenamiento de Azure), elija **Use Azure account** (Usar cuenta de Azure) para conectarse a un servicio de Almacenamiento de Azure a través de Internet o elija **Use local developer account** (Usar cuenta de desarrollador local) para conectarse al servicio local hospedado en el Emulador de almacenamiento de Azure.  
  
3.  Si ha seleccionado la opción **Use Azure account** (Usar cuenta de Azure), realice lo siguiente:  
  
    1.  Especifique los valores para los campos **Nombre de cuenta de almacenamiento** y **Clave de cuenta** . Estos valores se almacenarán como información confidencial en el paquete SSIS.  
  
    2.  Seleccione **Use HTTPS** (Usar HTTPS) si desea utilizar HTTPS en lugar de HTTP para conectarse con el servicio de Almacenamiento de Azure.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
5.  Puede ver las propiedades del Administrador de conexiones que creó en la ventana **Propiedades** .  
  
  