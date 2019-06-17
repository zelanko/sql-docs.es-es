---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec6663028f2c0e133996053a31acfc0e04b49738
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914684"
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
 None  
  
## <a name="see-also"></a>Vea también  
 [MSSQLSERVER_2518](mssqlserver-2518-database-engine-error.md)  
  
  
