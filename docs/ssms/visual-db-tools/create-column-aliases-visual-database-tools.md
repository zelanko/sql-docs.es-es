---
title: Crear alias de columna (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bbbf69c55fcd0225583c43b3b4ae4089cc2f40ea
ms.contentlocale: es-es
ms.lasthandoff: 08/18/2017

---
# <a name="create-column-aliases-visual-database-tools"></a>Crear alias de columna (Visual Database Tools)
Puede crear alias para nombres de columnas con el fin de facilitar el trabajo con nombres de columnas, cálculos y valores de resumen. Por ejemplo, puede crear un alias de columna para:  
  
-   Crear un nombre de columna, como "Importe total", para una expresión como `(quantity * unit_price)` o para una función de agregado.  
  
-   Crear un nombre abreviado de un nombre de columna, como `"d_id"` para `"discounts.stor_id."`  
  
Cuando haya definido un alias de columna, podrá utilizarlo en una consulta Select para especificar los resultados de la consulta.  
  
### <a name="to-create-a-column-alias"></a>Para crear un alias de columna  
  
1.  En el panel **Criterios**, busque la fila que contiene la columna de datos para la que desea crear un alias y, si es necesario, márquela como columna de resultados. Si la columna de datos no está en la cuadrícula, agréguela.  
  
2.  Escriba el alias en la columna **Alias** de la fila. El alias debe cumplir todas las convenciones de nomenclatura de SQL. Si el nombre de alias escrito contiene espacios, el Diseñador de consultas y vistas colocará automáticamente delimitadores en torno al mismo.  
  
## <a name="see-also"></a>Vea también  
[Agregar columnas a las consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Realizar operaciones básicas con consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

