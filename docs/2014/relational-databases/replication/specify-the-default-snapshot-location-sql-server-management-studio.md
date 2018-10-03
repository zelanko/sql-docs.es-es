---
title: Especificar la ubicación predeterminada de instantáneas (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc9734cb3da7c61da7c15ce108cd86f09be8ea1b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148845"
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>Especificar la ubicación predeterminada de instantáneas (SQL Server Management Studio)
  Especifique la ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para configurar la distribución. Para obtener más información sobre cómo usar este asistente, vea [Configure Publishing and Distribution](configure-publishing-and-distribution.md) (Configurar la publicación y la distribución). Si crea una publicación en un servidor que no está configurado como un distribuidor, especifique una ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para nueva publicación. Para obtener más información sobre cómo usar este asistente, vea [Create a Publication](publish/create-a-publication.md) (Crear una publicación).  
  
 Modifique la ubicación de instantáneas predeterminada en la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor \<distribuidor>**. Para obtener más información, vea [View and Modify Distributor and Publisher Properties](view-and-modify-distributor-and-publisher-properties.md) (Ver y modificar las propiedades del distribuidor y del publicador). Establezca la carpeta de instantáneas para cada publicación en el cuadro de diálogo **Propiedades de la publicación - \<publicación>**. Para más información, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Para modificar la ubicación predeterminada de instantáneas  
  
1.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>**, haga clic en el botón de propiedades (**…**) correspondiente al publicador para el que quiere cambiar la ubicación de instantáneas predeterminada.  
  
2.  En el cuadro de diálogo **Propiedades del publicador - \<publicador>**, escriba un valor para la propiedad **Carpeta de instantáneas predeterminada**.  
  
    > [!NOTE]  
    >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Secure the Snapshot Folder](security/secure-the-snapshot-folder.md) (Proteger la carpeta de instantáneas).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](alternate-snapshot-folder-locations.md)   
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)  
  
  
