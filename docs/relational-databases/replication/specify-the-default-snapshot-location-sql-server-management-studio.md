---
title: Especificar la ubicación predeterminada de instantáneas (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47a4aa5c534a2edff08865d26d72d47965838448
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>Especificar la ubicación predeterminada de instantáneas (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique la ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para configurar la distribución. Para obtener más información sobre cómo usar este asistente, vea [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md) (Configurar la publicación y la distribución). Si crea una publicación en un servidor que no está configurado como un distribuidor, especifique una ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para nueva publicación. Para obtener más información sobre cómo usar este asistente, vea [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md) (Crear una publicación).  
  
 Modifique la ubicación de instantáneas predeterminada en la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor \<distribuidor>**. Para obtener más información, vea [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md) (Ver y modificar las propiedades del distribuidor y del publicador). Establezca la carpeta de instantáneas para cada publicación en el cuadro de diálogo **Propiedades de la publicación - \<publicación>**. Para más información, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Para modificar la ubicación predeterminada de instantáneas  
  
1.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>**, haga clic en el botón de propiedades (**…**) correspondiente al publicador para el que quiere cambiar la ubicación de instantáneas predeterminada.  
  
2.  En el cuadro de diálogo **Propiedades del publicador - \<publicador>**, escriba un valor para la propiedad **Carpeta de instantáneas predeterminada**.  
  
    > [!NOTE]  
    >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Secure the Snapshot Folder](../../relational-databases/replication/security/secure-the-snapshot-folder.md) (Proteger la carpeta de instantáneas).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
