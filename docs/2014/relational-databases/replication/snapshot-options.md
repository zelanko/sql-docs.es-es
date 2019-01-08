---
title: Opciones de instantánea | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1fa6361199b52eabcd8eb321001f6565a5c3d1cb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753649"
---
# <a name="snapshot-options"></a>Opciones de instantánea
  Hay una serie de opciones disponibles al inicializar una suscripción con una instantánea:  
  
-   Especificar una ubicación alternativa para la carpeta de instantáneas en lugar de, o además de, la predeterminada. Para más información, consulte [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md).  
  
-   Comprimir instantáneas para su almacenamiento en medios extraíbles o para su transferencia a través de una red lenta. Para más información, consulte [Compressed Snapshots](compressed-snapshots.md).  
  
-   Ejecutar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] antes o después de aplicar la instantánea. Para obtener más información, consulte [Ejecutar scripts antes y después de aplicar la instantánea](execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Transferir la instantánea mediante el Protocolo de transferencia de archivos (FTP). Para obtener más información, consulte [Transferir instantáneas mediante FTP](transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)  
  
  
