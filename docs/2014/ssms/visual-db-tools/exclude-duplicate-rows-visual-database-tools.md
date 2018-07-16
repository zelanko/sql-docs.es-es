---
title: Excluir filas duplicadas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- row duplicates [SQL Server]
- duplicate rows
- row excluded in search [SQL Server]
- result sets [SQL Server], duplicate values
- excluding rows
ms.assetid: ab35a363-421d-4665-946b-ae3f6397af50
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 83bb23a8262f1488eb7e603282bfb3f8d7905e41
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273771"
---
# <a name="exclude-duplicate-rows-visual-database-tools"></a>Excluir filas duplicadas (Visual Database Tools)
  Si solo desea ver los valores únicos de un conjunto de resultados, puede indicar que se excluyan los duplicados del conjunto de resultados.  
  
### <a name="to-exclude-duplicate-rows-from-the-result-set"></a>Para excluir filas duplicadas del conjunto de resultados  
  
1.  Haga clic con el botón derecho en el fondo del panel Diagrama y, luego, elija **Propiedades** en el menú contextual.  
  
2.  En la ventana Propiedades, haga clic en **Valores DISTINCT** y establezca el valor en **Sí**.  
  
     El Diseñador de consultas y vistas inserta la palabra clave DISTINCT delante de la lista de columnas mostradas en la instrucción SQL.  
  
    > [!NOTE]  
    >  Si utiliza la palabra clave DISTINCT , es posible que no pueda modificar el conjunto de resultados en el panel de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
