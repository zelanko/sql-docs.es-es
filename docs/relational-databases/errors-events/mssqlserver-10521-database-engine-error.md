---
description: MSSQLSERVER_10521
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3c7b3bad98a125072b88e3a009c97d1011d8872c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338551"
---
# <a name="mssqlserver_10521"></a>MSSQLSERVER_10521
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|10521|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_PARAM_NEEDED|  
|Texto del mensaje|No se puede crear la guía de plan "%.\*ls" porque se ha especificado **\@type** como "%ls" y el valor del parámetro "%ls" es NULL. Este tipo requiere un valor no NULL para el parámetro. Especifique un valor no NULL para el parámetro o cambie el tipo por otro que admita un valor NULL para el parámetro.|  
  
## <a name="explanation"></a>Explicación  
El tipo especificado en **\@type** requiere un valor distinto de NULL para el parámetro especificado; sin embargo, se ha proporcionado un valor NULL.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique un valor no NULL para el parámetro o cambie el tipo por otro que admita un valor NULL para el parámetro.  
  
## <a name="see-also"></a>Consulte también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
