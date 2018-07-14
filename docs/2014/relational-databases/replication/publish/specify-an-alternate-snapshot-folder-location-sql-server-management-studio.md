---
title: Especificar una ubicación de carpeta de instantáneas alternativa (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48168354fd6609e4e43571c53c99cb80193aa98e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256117"
---
# <a name="specify-an-alternate-snapshot-folder-location-sql-server-management-studio"></a>Especificar una ubicación de carpeta de instantáneas alternativa (SQL Server Management Studio)
  Especifique una ubicación de instantáneas alternativa en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-specify-an-alternate-snapshot-location"></a>Para especificar una ubicación de instantánea alternativa  
  
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**:  
  
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.  
  
        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Proteger la carpeta de instantáneas](../security/secure-the-snapshot-folder.md).  
  
    2.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.  
  
     Para comprimir los archivos de instantáneas, seleccione **Comprimir archivos de instantánea en esta carpeta**. La compresión se utiliza generalmente para las conexiones con poco ancho de banda y las ubicaciones de instantánea alternativas en medios extraíbles, como un CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../alternate-snapshot-folder-locations.md)   
 [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Especificar la ubicación predeterminada de instantáneas &#40;SQL Server Management Studio&#41;](../specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md)   
 [Inicializar una suscripción con una instantánea](../initialize-a-subscription-with-a-snapshot.md)  
  
  
