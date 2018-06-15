---
title: Agregados secundarios | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05fc1ed0279157f581e5d5fd7bdad3eac555f34b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270214"
---
# <a name="grandchild-aggregates"></a>Agregados secundarios
La columna de capítulo creada en una cláusula de un comando shape puede recibir un *nombre de alias de capítulo* (normalmente con la palabra clave AS). Puede identificar cualquier columna de cualquier capítulo de la forma **Recordset** con un nombre completo que identifica el elemento secundario que contiene la columna. Por ejemplo, si el capítulo principal, Cap1, contiene un capítulo secundario, Cap2, tiene una columna de cantidad, amt, entonces el nombre completo sería chap1.chap2.amt. El nombre completo, a continuación, puede usarse como argumento a una de las funciones de agregado (SUM, AVG, MAX, MIN, recuento, STDEV o ninguno).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)
