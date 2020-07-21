---
title: Ordenar datos en una tabla (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
author: minewiskan
ms.author: owend
ms.openlocfilehash: cf1a9c8782e1771d5a53700b5f72c48dbb300c7a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938656"
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>Ordenar datos en una tabla (SSAS tabular)
  Puede ordenar los datos por texto (de A a Z o de Z a A) y los números (de menor a mayor o viceversa) en una o varias columnas.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>Para ordenar los datos de una tabla según una columna de texto  
  
1.  En el Diseñador de modelos, seleccione una columna de datos alfanuméricos o un rango de celdas de una columna, o asegúrese de que la celda activa está en una columna de la tabla que contenga datos alfanuméricos; a continuación, haga clic en la flecha del encabezado de la columna que desea usar para el filtrado.  
  
2.  En el menú Autofiltro, siga uno de estos procedimientos:  
  
    -   Para clasificar en orden alfanumérico ascendente, haga clic en **Ordenar de A a Z**.  
  
    -   Para clasificar en orden alfanumérico descendente, haga clic en **Ordenar de Z a A.**  
  
    > [!NOTE]  
    >  En algunos casos, los datos importados de otra aplicación podrían tener espacios iniciales incrustados antes de los datos. Debe quitar los espacios iniciales para ordenar los datos correctamente.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>Para ordenar los datos en una tabla según una columna numérica  
  
1.  En el Diseñador de modelos, seleccione una columna de datos alfanuméricos o un rango de celdas de una columna, o asegúrese de que la celda activa está en una columna de la tabla que contenga datos alfanuméricos; a continuación, haga clic en la flecha del encabezado de la columna que desea usar para el filtrado.  
  
2.  En el menú Autofiltro, siga uno de estos procedimientos:  
  
    -   Para ordenar de los números bajos a los números altos, haga clic en **Ordenar de menor a mayor**.  
  
    -   Para ordenar de los números altos a los números bajos, haga clic en **Ordenar de mayor a menor**.  
  
    > [!NOTE]  
    >  Si los resultados no son los que esperaba, la columna podría contener números almacenados como texto y no como números. Por ejemplo, los números negativos importados de algunos sistemas contables o un número escrito con un símbolo ' inicial (apóstrofo) se almacenan en forma de texto.  
  
## <a name="see-also"></a>Consulte también  
 [Filtrar y ordenar datos &#40;SSAS tabular&#41;](../filter-and-sort-data-ssas-tabular.md)   
 [Perspectivas &#40;SSAS tabular&#41;](perspectives-ssas-tabular.md)   
 [Roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md)  
  
  
