---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bbf8c071d0f64b4fe09322179c7d71c538d9d6e7
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17130|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NOLOCKSPACE|  
|Texto del mensaje|Memoria insuficiente para el número de bloqueos configurado. Se está intentando iniciar con una tabla hash de bloqueos más pequeña, lo que puede afectar al rendimiento. Póngase en contacto con el administrador de la base de datos para configurar más memoria para esta instancia del motor de base de datos.|  
  
## <a name="explanation"></a>Explicación  
No hay suficiente memoria para el tamaño de tabla hash del administrador de bloqueos deseado.  Se intentará asignar una tabla hash menor.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe los parámetros de configuración de memoria del servidor (memoria de servidor máxima, memoria de servidor mínima) y si hay presiones de memoria. Proporcione más memoria para SQL Server.  
  

