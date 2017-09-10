---
title: Cambiar las asignaciones de filtros de fila (SSAS Tabular) de tabla, columna o | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b80323e5aaf1dd6c469ddffefb5d92542e9d3a19
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="change-table-column-or-row-filter-mappings-ssas-tabular"></a>Cambiar las asignaciones de filtros de tabla, columna o fila (SSAS tabular)
  Este tema describe cómo cambiar las asignaciones de filtros de tabla, columna o fila mediante el cuadro de diálogo **Editar propiedades de tabla** de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 Las opciones del cuadro de diálogo **Editar propiedades de tabla** serán diferentes dependiendo de si importó los datos originalmente seleccionando las tablas en una lista o usando una consulta SQL. Si importó originalmente los datos seleccionándolos en una lista, el cuadro de diálogo **Editar propiedades de tabla** mostrará el modo de vista previa de tabla. Este modo mostrará únicamente un subconjunto limitado a las primeras cincuenta filas de la tabla de origen. Si importó originalmente los datos mediante una instrucción SQL, el cuadro de diálogo **Editar propiedades de tabla** solo mostrará una instrucción SQL. Mediante una instrucción de consulta SQL, se puede recuperar un subconjunto de filas diseñando un filtro o editando la instrucción SQL manualmente.  
  
 Si se cambia el origen a una tabla que tiene columnas distintas que la tabla actual, aparece un mensaje que advierte que las columnas son distintas. En ese caso, debe seleccionar las columnas que desea poner en la tabla actual y hacer clic en **Guardar**. Puede reemplazar toda la tabla activando la casilla de la izquierda de la tabla.  
  
> [!NOTE]  
>  Si la tabla tiene más de una partición, no puede utilizar el cuadro de diálogo Editar propiedades de tabla para cambiar las asignaciones de filtro de fila. Para cambiar las asignaciones de filtro de fila para las tablas con varias particiones, utilice el Administrador de particiones. Para más información, vea [Particiones &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>Para cambiar las asignaciones de filtros de tabla, columna o fila  
  
1.  En el diseñador de modelos, haga clic en la tabla, haga clic en el menú **Tabla** y, a continuación, en **Propiedades de tabla**.  
  
2.  En el cuadro de diálogo **Editar propiedades de tabla** , busque la columna que contiene los criterios por los que desea filtrar y, a continuación, haga clic en la flecha hacia abajo que hay a la derecha del encabezado de columna.  
  
3.  En el menú **Autofiltro** , siga uno de estos procedimientos:  
  
    -   En la lista de valores de columna, active o desactive uno o varios valores para filtrar y haga clic en Aceptar.  
  
         Si el número de valores es sumamente grande, algunos elementos individuales podrían no mostrarse en la lista. En su lugar, verá un mensaje similar a "Demasiados elementos para mostrar".  
  
    -   Haga clic en **Numerar filtros** o **Filtros de texto** (según el tipo de columna) y, después, haga clic en uno de los comandos de operador de comparación (como Es igual a) o haga clic en Filtro personalizado. En el cuadro de diálogo **Filtro personalizado** , cree el filtro y, a continuación, haga clic en **Aceptar**.  
  
         Si comete un error y necesita volver a empezar, haga clic en **Borrar filtros de fila**.  
  
## <a name="see-also"></a>Vea también  
 [Editar propiedades de tabla, cuadro de diálogo &#40;SSAS&#41;](http://msdn.microsoft.com/library/8d913e83-7246-44cc-8fc7-31729023c0d8)  
  
  
