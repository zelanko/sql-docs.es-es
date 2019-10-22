---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 68829d55be0b080e9b4beb9d7b284e3f57a46581
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305908"
---
# <a name="mssqlserver_10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10507|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_STMT_DOES_NOT_MATCH|  
|Texto del mensaje|No se puede crear la guía de plan "%.\*ls" porque la instrucción que especifican **\@stmt** y **\@module_or_batch**, o **\@plan_handle** y **\@statement_start_offset**, no coincide con ninguna instrucción del módulo o lote especificado. Modifique los valores para que coincidan con una instrucción del módulo o lote.|  
  
## <a name="explanation"></a>Explicación  
Una instrucción en el módulo o lote especificado no se pudo hacer coincidir con la instrucción o valor de desplazamiento de instrucción especificados.  
  
## <a name="user-action"></a>Acción del usuario  
Modifique los valores de los parámetros especificados para que coincidan con una instrucción del módulo o lote.  
  
## <a name="see-also"></a>Consulte también  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
