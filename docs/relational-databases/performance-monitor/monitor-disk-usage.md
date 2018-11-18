---
title: Supervisión del uso del disco | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance-monitor"
ms.topic: conceptual
helpviewer_keywords:
- database monitoring [SQL Server], disk usage
- disks [SQL Server]
- monitoring performance [SQL Server], disk usage
- server performance [SQL Server], disk usage
- monitoring [SQL Server], disk activity
- excess paging [SQL Server]
- tuning databases [SQL Server], disk usage
- I/O [SQL Server], monitoring
- disks [SQL Server], monitoring activity
- isolating disk activity [SQL Server]
- database performance [SQL Server], disk usage
- monitoring server performance [SQL Server], disk usage
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 13d1a4539aabd51426c5756eccb72e849b07deb8
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672234"
---
# <a name="monitor-disk-usage"></a>Supervisar el uso del disco
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa llamadas de entrada/salida (E/S) del sistema operativo Microsoft Windows para realizar las operaciones de lectura y escritura en el disco. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra el momento y el modo en que se realizan las operaciones de E/S de disco, pero el sistema operativo Windows realiza las operaciones de E/S subyacentes. El subsistema de E/S incluye el bus del sistema, tarjetas controladoras de disco, discos, unidades de cinta, la unidad de CD-ROM y muchos otros dispositivos de E/S. La E/S del disco es una causa frecuente de los atascos en un sistema.  
  
 La supervisión de la actividad del disco implica dos aspectos básicos:  
  
-   Supervisar la E/S del disco y detectar la paginación excesiva  
  
-   Aislar la actividad del disco que crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para obtener más información, vea [Supervisar el uso del disco](https://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx).  
  
  
