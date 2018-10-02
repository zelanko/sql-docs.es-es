---
title: Backup Device (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b622b17b19d3fedf192eecc1d976330c685752c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602753"
---
# <a name="sql-server-backup-device-object"></a>Backup Device (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El objeto **Backup Device** proporciona contadores para supervisar los dispositivos de copia de seguridad de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utilizan para las operaciones de copias de seguridad y restauración. Supervise los dispositivos de copia de seguridad cuando desee determinar el rendimiento o el progreso de las operaciones de copias de seguridad y restauración en cada dispositivo. Para supervisar el rendimiento de la operación completa de copia de seguridad o restauración de la base de datos, use el contador **Rendimiento de copias de seguridad y restauración/seg.** del objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** object. Para más información, vea [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
 En la siguiente tabla se describe el contador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** .  
  
|Contadores de Dispositivo de copia de seguridad de SQL Server|Descripción|  
|---------------------------------------|-----------------|  
|**Rendimiento del dispositivo en bytes/seg.**|Rendimiento de las operaciones de lectura y escritura (en bytes por segundo) de un dispositivo de copia de seguridad utilizado para la copia de seguridad o la restauración de bases de datos. Este contador existe solo mientras se ejecuta la operación de copia de seguridad o restauración.|  
  
## <a name="see-also"></a>Ver también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
