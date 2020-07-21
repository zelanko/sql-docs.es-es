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
ms.openlocfilehash: d305866fb884b62540cfbe2cc13a613981999749
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765285"
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
  
