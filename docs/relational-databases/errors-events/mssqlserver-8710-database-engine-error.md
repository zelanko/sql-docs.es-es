---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 427ae245dc58fddae8b9c78145a8a6601839ed7e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|8710|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Texto del mensaje|Las funciones de agregado que se utilizan con consultas CUBE, ROLLUP o GROUPING SET se deben proporcionar para la combinación de subagregados. Para solucionar este problema, quite la función de agregado o escriba la consulta utilizando UNION ALL en cláusulas GROUP BY.|  
  
## <a name="explanation"></a>Explicación  
Se ha usado una función de agregado con CUBE, ROLLUP o GROUPING SETS que no proporciona un método para combinar subagregados.  
  
## <a name="user-action"></a>Acción del usuario  
Para solucionar este problema, quite la función de agregado o escriba la consulta utilizando UNION ALL en cláusulas GROUP BY.  
  
