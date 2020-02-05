---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a9abebe50426f671e444514b29ccc2235e4a2109
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68120482"
---
# <a name="mssqlserver_8712"></a>MSSQLSERVER_8712
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|8712|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|USEPLAN_ERR_NO_INDEX|  
|Texto del mensaje|El índice '%.*ls', especificado en la sugerencia USE PLAN, no existe. Especifique un índice existente o cree un índice con el nombre especificado.|  
  
## <a name="explanation"></a>Explicación  
Uno de los índices que se especifican en la sugerencia USE PLAN no existe.  
  
## <a name="user-action"></a>Acción del usuario  
Asegurarse de que todos los índices que se especifican en la sugerencia USE PLAN existen.  
  
## <a name="see-also"></a>Consulte también  
[Sugerencias de consulta &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
  
