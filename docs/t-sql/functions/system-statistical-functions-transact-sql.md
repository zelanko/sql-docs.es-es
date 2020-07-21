---
title: Funciones estadísticas del sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statistical functions [SQL Server]
- system statistical functions [SQL Server]
- functions [SQL Server], statistical
ms.assetid: 45828c67-1b9a-4653-bb24-86246084d8ba
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: ff5025ce34155432736bd341a332f602cf94d337
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85714698"
---
# <a name="system-statistical-functions-transact-sql"></a>Funciones estadísticas del sistema (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Las siguientes funciones escalares devuelven información estadística acerca del sistema:  
  
|||  
|-|-|  
|[@@CONNECTIONS](../../t-sql/functions/connections-transact-sql.md)|[@@PACK_RECEIVED](../../t-sql/functions/pack-received-transact-sql.md)|  
|[@@CPU_BUSY](../../t-sql/functions/cpu-busy-transact-sql.md)|[@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)|  
|[fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)|[@@TIMETICKS](../../t-sql/functions/timeticks-transact-sql.md)|  
|[@@IDLE](../../t-sql/functions/idle-transact-sql.md)|[@@TOTAL_ERRORS](../../t-sql/functions/total-errors-transact-sql.md)|  
|[@@IO_BUSY](../../t-sql/functions/io-busy-transact-sql.md)|[@@TOTAL_READ](../../t-sql/functions/total-read-transact-sql.md)|  
|[@@PACKET_ERRORS](../../t-sql/functions/packet-errors-transact-sql.md)|[@@TOTAL_WRITE](../../t-sql/functions/total-write-transact-sql.md)|  
  
 Todas las funciones estadísticas del sistema son no deterministas, Por ello, estas funciones no siempre devuelven el mismo resultado cada vez que se invocan, incluso con el mismo conjunto de valores de entrada. Para más información sobre el determinismo de las funciones, vea [Funciones deterministas y no deterministas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
