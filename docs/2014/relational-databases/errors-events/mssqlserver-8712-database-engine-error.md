---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 465f47fd69f8e6477ede13892a079f069042c57b
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553040"
---
# <a name="mssqlserver_8712"></a>MSSQLSERVER_8712
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|8712|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|USEPLAN_ERR_NO_INDEX|  
|Texto del mensaje|El índice '%.*ls', especificado en la sugerencia USE PLAN, no existe. Especifique un índice existente o cree un índice con el nombre especificado.|  
  
## <a name="explanation"></a>Explicación  
 Uno de los índices que se especifican en la sugerencia USE PLAN no existe.  
  
## <a name="user-action"></a>Acción del usuario  
 Asegurarse de que todos los índices que se especifican en la sugerencia USE PLAN existen.  
  
## <a name="see-also"></a>Consulte también  
 [Sugerencias de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guías de plan](../performance/plan-guides.md)  
  
  
