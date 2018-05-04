---
title: Agregados secundarios | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
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
ms.openlocfilehash: 79f5d0d06631f6fcdbdcd85c726a03bdc834faeb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="grandchild-aggregates"></a>Agregados secundarios
La columna de capítulo creada en una cláusula de un comando shape puede recibir un *nombre de alias de capítulo* (normalmente con la palabra clave AS). Puede identificar cualquier columna de cualquier capítulo de la forma **Recordset** con un nombre completo que identifica el elemento secundario que contiene la columna. Por ejemplo, si el capítulo principal, Cap1, contiene un capítulo secundario, Cap2, tiene una columna de cantidad, amt, entonces el nombre completo sería chap1.chap2.amt. El nombre completo, a continuación, puede usarse como argumento a una de las funciones de agregado (SUM, AVG, MAX, MIN, recuento, STDEV o ninguno).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)
