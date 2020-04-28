---
title: Agregados terciarios | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac0b06479b3ad4feedaa63bdac227d028b7a9e09
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925237"
---
# <a name="grandchild-aggregates"></a>Agregados secundarios
A la columna de capítulo creada en una cláusula de un comando de forma se le puede asignar un *nombre de alias de capítulo* (normalmente con la palabra clave as). Puede identificar cualquier columna de cualquier capítulo del **conjunto de registros** con forma con un nombre completo que identifique el elemento secundario que contiene la columna. Por ejemplo, si el capítulo principal, chap1, contiene un capítulo secundario, chap2, que tiene una columna amount, AMT, el nombre completo sería chap1. chap2. AMT. El nombre completo se puede usar como argumento para una de las funciones de agregado (SUM, AVG, MAX, MIN, COUNT, STDEV o ANY).  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)
