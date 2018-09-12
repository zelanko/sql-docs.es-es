---
title: Backup Device (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d24d22fe3a2790f9dce20902b34cd192e572c3bd
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811641"
---
# <a name="sql-server-backup-device-object"></a>Backup Device (objeto de SQL Server)
  El objeto **Backup Device** proporciona contadores para supervisar los dispositivos de copia de seguridad de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utilizan para las operaciones de copias de seguridad y restauración. Supervise los dispositivos de copia de seguridad cuando desee determinar el rendimiento o el progreso de las operaciones de copias de seguridad y restauración en cada dispositivo. Para supervisar el rendimiento de la operación completa de copia de seguridad o restauración de la base de datos, use el contador **Rendimiento de copias de seguridad y restauración/seg.** del objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** object. Para más información, vea [SQL Server, Databases Object](sql-server-databases-object.md).  
  
 En la siguiente tabla se describe el contador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** .  
  
|Contadores de Dispositivo de copia de seguridad de SQL Server|Descripción|  
|---------------------------------------|-----------------|  
|**Rendimiento del dispositivo en bytes/seg.**|Rendimiento de las operaciones de lectura y escritura (en bytes por segundo) de un dispositivo de copia de seguridad utilizado para la copia de seguridad o la restauración de bases de datos. Este contador existe solo mientras se ejecuta la operación de copia de seguridad o restauración.|  
  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../backup-restore/backup-devices-sql-server.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
