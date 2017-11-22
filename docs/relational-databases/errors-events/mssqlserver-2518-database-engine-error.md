---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9bc87ebba32ddec6710eed0ed59298563a9c66fb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2518|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|Texto del mensaje|Id. de objeto ID O_ID (objeto "O_NAME"): no es posible comprobar las columnas calculadas y los tipos definidos por el usuario para este objeto porque el entorno Common Language Runtime (CLR) está deshabilitado.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje informativo indica que el procesador de consultas no pudo proporcionar a DBCC un objeto interno para permitir la evaluación de las columnas calculadas y los tipos definidos por el usuario CLR (Common Language Runtime). Este problema se produjo porque una de las columnas utilizaba el CLR, pero éste no estaba habilitado. El objeto interno cubre todas las columnas. Por tanto, la imposibilidad de evaluar una sola columna evita que se cree el objeto interno. Esto significa que no se comprobará si las columnas calculadas son correctas o que no se usarán cuando DBCC compruebe la coherencia entre índices y tablas base.  
  
## <a name="user-action"></a>Acción del usuario  
Habilite el CLR y vuelva a ejecutar la instrucción DBCC.  
  
## <a name="see-also"></a>Vea también  
[Habilitar la integración con CLR](~/relational-databases/clr-integration/clr-integration-enabling.md)  
  
