---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b57f8a7985c9fb092209bc5a80b9d0c3294d98c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781499"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|10519|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Texto del mensaje|No se puede crear la guía de plan "%.\*ls" porque las sugerencias especificadas en **\@hints** no se pueden aplicar a la instrucción especificada por **\@stmt** o **\@statement_start_offset**. Compruebe que las sugerencias pueden aplicarse a la instrucción.|  
  
## <a name="explanation"></a>Explicación  
Las sugerencias especificadas en **\@hints** no se pueden aplicar a la instrucción especificada por **\@stmt** o **\@statement_start_offset**.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique sugerencias que puedan aplicarse a la instrucción.  
  
## <a name="see-also"></a>Consulte también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
