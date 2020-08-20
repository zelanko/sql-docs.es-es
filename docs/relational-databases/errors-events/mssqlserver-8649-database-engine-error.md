---
description: MSSQLSERVER_8649
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b599848c71b465d80c01eecd594f841ab5c0e72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499451"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|8649|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|COST_TOO_HIGH|  
|Texto del mensaje|Se ha cancelado la consulta porque el costo estimado de esta consulta (%d) supera el umbral configurado de %d. Póngase en contacto con el administrador del sistema.|  
  
## <a name="explanation"></a>Explicación  
La consulta se canceló porque el costo estimado de la misma supera el umbral configurado establecido para QUERY_GOVERNOR_COST_LIMIT.  
  
## <a name="user-action"></a>Acción del usuario  
Establezca la opción QUERY_GOVERNOR_COST_LIMIT en un valor mayor.  
  
## <a name="see-also"></a>Consulte también  
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
