---
title: Seleccionar filas que no coinciden con un valor (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa3084d9b624f1836a3970da77c01677b7700ba4
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814291"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>Seleccionar filas que no coinciden con un valor (Visual Database Tools)
  Para buscar filas que no coinciden con un valor, utilice el operador NOT.  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>Para buscar filas que no coincidan con un valor  
  
1.  Si aún no lo ha hecho, agregue al [panel Criterios](visual-database-tools.md)las columnas o expresiones que desee utilizar en la condición de búsqueda.  
  
2.  Busque la fila que contiene la columna de datos o la expresión que desea buscar y, a continuación, en la columna de cuadrícula **Filtro** , escriba el operador NOT seguido de un valor de búsqueda.  
  
 Por ejemplo, para buscar todas las filas de una tabla `products` cuyos valores de la columna de código de producto empiecen por un carácter distinto de "A", escriba una condición de búsqueda como la siguiente:  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>Vea también  
 [Reglas para especificar los valores de búsqueda &#40;Visual Database Tools&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [Especificar criterios de búsqueda (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
