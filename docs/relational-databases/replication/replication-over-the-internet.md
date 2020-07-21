---
title: Replicación a través de Internet | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web publishing [SQL Server replication], about Web publishing
- Web publishing [SQL Server replication]
- Internet [SQL Server replication]
- Internet [SQL Server replication], publishing
ms.assetid: 04e7f4ed-e244-4bbe-ba12-09c33abea09e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c5a1244ed340dcfd4794c14635d570530b88f5d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716726"
---
# <a name="replication-over-the-internet"></a>Replicación por Internet
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La replicación de datos por Internet permite a usuarios desconectados y remotos obtener acceso a los datos cuando los necesiten, por medio de una conexión a Internet. Los datos se replican a través de Internet mediante:  
  
-   Una red privada virtual (VPN). Para más información, vea [Publicar datos a través de Internet mediante VPN](../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
-   La opción de sincronización web para replicación de mezcla. Para más información, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Todos los tipos de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden replicar datos a través de VPN, pero tenga en cuenta la sincronización web si está utilizando replicación de combinación.  
  
  
