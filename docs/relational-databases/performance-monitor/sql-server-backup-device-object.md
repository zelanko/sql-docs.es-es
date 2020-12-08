---
title: Backup Device (objeto de SQL Server) | Microsoft Docs
description: Obtenga información sobre el objeto Backup Device, que proporciona contadores para supervisar los dispositivos de copia de seguridad de Microsoft SQL Server que se utilizan para las operaciones de copias de seguridad y restauración.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 383e1cd4ccca7a466817ac5ca226785fa56560ce
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505909"
---
# <a name="sql-server-backup-device-object"></a>Backup Device (objeto de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  El objeto **Backup Device** proporciona contadores para supervisar los dispositivos de copia de seguridad de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utilizan para las operaciones de copias de seguridad y restauración. Supervise los dispositivos de copia de seguridad cuando desee determinar el rendimiento o el progreso de las operaciones de copias de seguridad y restauración en cada dispositivo. Para supervisar el rendimiento de la operación completa de copia de seguridad o restauración de la base de datos, use el contador **Rendimiento de copia de seguridad y restauración/** del objeto **Databases** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, vea [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
 En la siguiente tabla se describe el contador **Dispositivo de copia de seguridad** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de Dispositivo de copia de seguridad de SQL Server|Descripción|  
|---------------------------------------|-----------------|  
|**Rendimiento del dispositivo en bytes/seg.**|Rendimiento de las operaciones de lectura y escritura (en bytes por segundo) de un dispositivo de copia de seguridad utilizado para la copia de seguridad o la restauración de bases de datos. Este contador existe solo mientras se ejecuta la operación de copia de seguridad o restauración.|  
  
## <a name="see-also"></a>Consulte también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
