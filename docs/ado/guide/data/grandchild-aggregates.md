---
title: Agregados secundarios | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f1bff3c8a155e1e9378acbb659f00817f478382e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602384"
---
# <a name="grandchild-aggregates"></a>Agregados secundarios
La columna de capítulo creada en una cláusula de un comando de forma puede recibir un *nombre de alias de capítulo* (normalmente con la palabra clave AS). Se puede identificar cualquier columna de cada capítulo de la forma **Recordset** con un nombre completo que identifica el elemento secundario que contiene la columna. Por ejemplo, si el capítulo principal, Cap1, contiene un capítulo secundario, Cap2, tiene una columna de cantidad, amt, entonces el nombre completo sería chap1.chap2.amt. El nombre completo, a continuación, se puede usar como argumento a una de las funciones de agregado (SUM, AVG, MAX, MIN, COUNT, STDEV o cualquiera).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)
