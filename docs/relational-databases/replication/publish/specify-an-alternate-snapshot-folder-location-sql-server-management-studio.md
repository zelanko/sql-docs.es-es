---
title: "Especificar una ubicación de carpeta de instantáneas alternativa (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d848053cc583e27c473f651a5a9d52039d4f8cbd
ms.lasthandoff: 04/11/2017

---
# <a name="specify-an-alternate-snapshot-folder-location-sql-server-management-studio"></a>Especificar una ubicación de carpeta de instantáneas alternativa (SQL Server Management Studio)
  Especifique una ubicación de instantáneas alternativa en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-an-alternate-snapshot-location"></a>Para especificar una ubicación de instantánea alternativa  
  
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**:  
  
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.  
  
        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para más información, vea [Proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.  
  
     Para comprimir los archivos de instantáneas, seleccione **Comprimir archivos de instantánea en esta carpeta**. La compresión se utiliza generalmente para las conexiones con poco ancho de banda y las ubicaciones de instantánea alternativas en medios extraíbles, como un CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Especificar la ubicación predeterminada de instantáneas &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
