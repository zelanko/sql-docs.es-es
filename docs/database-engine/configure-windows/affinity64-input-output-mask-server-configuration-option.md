---
title: affinity64 I/O mask (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b8e4499d960ac2e96e494754920f124371f56c3e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 I/O mask (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  La opción **affinity64 I/O mask** enlaza la E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un subconjunto específico de CPU, de forma similar a la opción **affinity I/O mask** . Use **affinity I/O mask** para enlazar los primeros 32 procesadores y **affinity64 I/O mask** para enlazar los demás procesadores del equipo. Si vuelve a configurar **affinity64 I/O mask**, debe reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opción solo está visible en la versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Ver también  
 [affinity Input-Output mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
