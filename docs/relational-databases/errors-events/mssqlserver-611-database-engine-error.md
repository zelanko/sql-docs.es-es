---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d32d67f02af9c377720480ec27dd7e3078c069a1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|611|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|VAR_SIZE_TOO_BIG|  
|Texto del mensaje|No se puede insertar ni actualizar una fila porque el tamaño total de columna variable, incluida la sobrecarga, es %d bytes más del límite.|  
  
## <a name="explanation"></a>Explicación  
El tamaño máximo de la columna de variable e es mayor que el permitido por el esquema. El Error 611 se devuelve cuando la columna de variable está por encima del límite en el caso fijo cuando el formato de almacenamiento vardecimal está habilitado, o cuando el tamaño de la columna de variable está por encima del límite permitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para un registro de datos comprimido.  
  
## <a name="user-action"></a>Acción del usuario  
Reduzca el tamaño del registro.  
  
