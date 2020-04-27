---
title: affinity64 I/O mask (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f32c35aabf7d95a31624ca5c507fccac8ba1053e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62811573"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 I/O mask (opción de configuración del servidor)
  La opción **affinity64 I/O mask** enlaza la E/S del disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un subconjunto específico de CPU, de forma similar a la opción **affinity I/O mask** . Use **affinity I/O mask** para enlazar los primeros 32 procesadores y **affinity64 I/O mask** para enlazar los demás procesadores del equipo. Si vuelve a configurar **affinity64 I/O mask**, debe reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opción solo está visible en la versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [affinity Input-Output mask (opción de configuración del servidor)](affinity-input-output-mask-server-configuration-option.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
