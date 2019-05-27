---
title: Filtrar datos en una tabla (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.customfilterdb.f1
- sql12.asvs.bidtoolset.autofiltermenu.f1
- sql12.asvs.bidtoolset.notallitemsshowing.f1
ms.assetid: 3223059d-f525-4835-bf88-ebc195d9dbdc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 869185e56db9a4ffb07282d3ce51ced191a6bac8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067127"
---
# <a name="filter-data-in-a-table-ssas-tabular"></a>Filtrar los datos de una tabla (SSAS tabular)
  Puede aplicar filtros al importar datos para controlar las filas que se cargan en una tabla. Después de haber importado los datos, no podrá eliminar filas individuales. Sin embargo, puede aplicar filtros personalizados para controlar la manera en que se muestran las filas. Las filas que no cumplen los criterios de filtrado se ocultan. Puede filtrar por una o más columnas. Los filtros son aditivos, lo que significa que cada filtro adicional se basa en el actual y reduce aún más el subconjunto de datos.  
  
> [!NOTE]  
>  La ventana de vista previa del filtro limita el número de valores diferentes que se muestran. Si se supera el límite, aparece un mensaje.  
  
### <a name="to-filter-data-based-on-column-values"></a>Para filtrar datos según los valores de las columnas  
  
1.  En el diseñador de modelos, seleccione una tabla y, a continuación, haga clic en la flecha del encabezado de la columna por la que desea filtrar.  
  
2.  En el menú Autofiltro, siga uno de estos procedimientos:  
  
    -   En la lista de valores de columna, active o desactive uno o varios valores para filtrar y haga clic en **Aceptar**.  
  
         Si el número de valores es sumamente grande, algunos elementos individuales podrían no mostrarse en la lista. En su lugar, verá un mensaje similar a "Demasiados elementos para mostrar".  
  
    -   Haga clic en **Filtros de números** o **Filtros de texto** (en función del tipo de columna) y, después, haga clic en uno de los comandos de operador de comparación (como **Es igual a**) o haga clic en **Filtro personalizado**. En el cuadro de diálogo **Filtro personalizado** , cree el filtro y, a continuación, haga clic en **Aceptar**.  
  
### <a name="to-clear-a-filter-for-a-column"></a>Para borrar un filtro para una columna  
  
1.  Haga clic en la flecha del encabezado de la columna en la que desea borrar un filtro.  
  
2.  Haga clic en **Borrar filtro de \<nombre de columna >**.  
  
### <a name="to-clear-all-filters-for-a-table"></a>Para borrar todos los filtros de una tabla  
  
1.  En el diseñador de modelos, seleccione la tabla en la que desea borrar los filtros.  
  
2.  Haga clic en el menú **Columna** y, a continuación, haga clic en **Borrar todos los filtros**.  
  
## <a name="see-also"></a>Vea también  
 [Filtrar y ordenar datos &#40;SSAS tabular&#41;](../filter-and-sort-data-ssas-tabular.md)   
 [Perspectivas &#40;SSAS tabular&#41;](perspectives-ssas-tabular.md)   
 [Roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md)  
  
  
