---
title: MSSQLSERVER_2519 | Microsoft Docs
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
- 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4fdcb3ccc1ccbc22f179a851b5d77ae45ab925e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2519"></a>MSSQLSERVER_2519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2519|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_NO_EXPRESSION_EVALUATOR|  
|Texto del mensaje|Las columnas calculadas y los tipos definidos por el usuario no se pueden comprobar para el Id. de objeto O_ID (objeto "O_NAME") porque el evaluador interno de expresiones no se pudo inicializar.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje informativo indica que el procesador de consultas no pudo proporcionar a DBCC un objeto interno para permitir la evaluación de columnas calculadas y tipos definidos por el usuario CLR (Common Language Runtime). Como consecuencia, no se comprobará si las columnas calculadas y los tipos definidos por el usuario CLR son correctos ni se utilizarán cuando DBCC compruebe la coherencia entre los índices y las tablas base.  
  
## <a name="user-action"></a>Acción del usuario  
None  
  
## <a name="see-also"></a>Ver también  
[MSSQLSERVER_2518](~/relational-databases/errors-events/mssqlserver-2518-database-engine-error.md)  
  
