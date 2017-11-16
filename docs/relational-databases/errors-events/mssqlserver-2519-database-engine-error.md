---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: e4879dd4c6b83527a84ec7e7616736f21679975f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2519"></a>MSSQLSERVER_2519
  
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
Ninguno  
  
## <a name="see-also"></a>Vea también  
[MSSQLSERVER_2518](~/relational-databases/errors-events/mssqlserver-2518-database-engine-error.md)  
  
