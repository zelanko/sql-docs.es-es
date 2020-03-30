---
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
ms.openlocfilehash: 39d3edc1b85dba6c223cc4b4e5b3d3250b48d489
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68132291"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
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
  
