---
title: "Especificar una ubicaci&#243;n de carpeta de instant&#225;neas alternativa (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantáneas [replicación de SQL Server], ubicaciones de carpetas alternativas"
  - "replicación de instantáneas [SQL Server], ubicaciones de carpetas alternativas"
  - "carpetas de instantáneas alternativas [replicación de SQL Server]"
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Especificar una ubicaci&#243;n de carpeta de instant&#225;neas alternativa (SQL Server Management Studio)
  Especificar una ubicación de instantáneas alternativa en el **instantánea** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para especificar una ubicación de instantánea alternativa  
  
1.  En el **instantánea** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo:  
  
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.  
  
        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como una ruta de nomenclatura universal (UNC) de la convención, como \\\computername\snapshot. Para obtener más información, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.  
  
     Para comprimir los archivos de instantáneas, seleccione **Comprimir archivos de instantánea en esta carpeta**. La compresión se utiliza generalmente para las conexiones con poco ancho de banda y las ubicaciones de instantánea alternativas en medios extraíbles, como un CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Configurar propiedades de la instantánea & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Especificar la ubicación predeterminada de instantáneas & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  