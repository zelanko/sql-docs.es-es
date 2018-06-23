---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c46591374fc32ba20f4eb20c48bec171c76d9ac7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112925"
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
  
  