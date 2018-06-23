---
title: Backup Device (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 62ba36e83f08cabda85fd71a02d4e22842fb0e8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199350"
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
  
  