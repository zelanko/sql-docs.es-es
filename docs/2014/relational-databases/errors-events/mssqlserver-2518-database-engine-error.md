---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4fc661059240f626c9f61e3b81f4a80350680fa
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425065"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
    
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
 [Habilitar la integración con CLR](../clr-integration/clr-integration-enabling.md)  
  
  
