---
title: MSSQLSERVER_7711 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f75bef86a606da4f7103c3afd6c5846dc58e8e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7711"></a>MSSQLSERVER_7711
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7711|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PRT_RANGE_OVERLAP|  
|Texto del mensaje|La opción DATA_COMPRESSION se especificó más de una vez para la tabla o índice, o una de sus particiones.|  
  
## <a name="explanation"></a>Explicación  
Error en la opción DATA_COMPRESSION en una de las instrucciones siguientes:  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
Si la tabla o índice mencionado tiene particiones, la opción DATA_COMPRESSION se enumeró más de una vez para al menos una de las particiones. Si la tabla o índice no tiene particiones, la opción DATA_COMPRESSION se mencionó más de una vez.  
  
## <a name="user-action"></a>Acción del usuario  
Para una tabla o índice con particiones, asegúrese de que la opción DATA_COMPRESSION se especifica solo una vez para cada partición. Para una tabla o índice sin particiones, utilice la opción DATA_COMPRESSION solo una vez en la instrucción.  
  
