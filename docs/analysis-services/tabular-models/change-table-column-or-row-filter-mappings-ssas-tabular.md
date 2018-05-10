---
title: Cambiar las asignaciones de filtros de fila, columna o tabla | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5583e0747806453f92fcd98001299b31bd4c0ef8
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="change-table-column-or-row-filter-mappings"></a>Cambiar las asignaciones de filtros de tabla, columna o fila 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artículo describe cómo cambiar las asignaciones de filtros de fila, columna o tabla utilizando la **editar propiedades de tabla** cuadro de diálogo de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 Las opciones del cuadro de diálogo **Editar propiedades de tabla** serán diferentes dependiendo de si importó los datos originalmente seleccionando las tablas en una lista o usando una consulta SQL. Si importó originalmente los datos seleccionándolos en una lista, el cuadro de diálogo **Editar propiedades de tabla** mostrará el modo de vista previa de tabla. Este modo mostrará únicamente un subconjunto limitado a las primeras cincuenta filas de la tabla de origen. Si importó originalmente los datos mediante una instrucción SQL, el cuadro de diálogo **Editar propiedades de tabla** solo mostrará una instrucción SQL. Mediante una instrucción de consulta SQL, se puede recuperar un subconjunto de filas diseñando un filtro o editando la instrucción SQL manualmente.  
  
 Si se cambia el origen a una tabla que tiene columnas distintas que la tabla actual, aparece un mensaje que advierte que las columnas son distintas. En ese caso, debe seleccionar las columnas que desea poner en la tabla actual y hacer clic en **Guardar**. Puede reemplazar toda la tabla activando la casilla de la izquierda de la tabla.  
  
> [!NOTE]  
>  Si la tabla tiene más de una partición, no puede utilizar el cuadro de diálogo Editar propiedades de tabla para cambiar las asignaciones de filtro de fila. Para cambiar las asignaciones de filtro de fila para las tablas con varias particiones, utilice el Administrador de particiones. Para obtener más información, consulte [particiones](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>Para cambiar las asignaciones de filtros de tabla, columna o fila  
  
1.  En el diseñador de modelos, haga clic en la tabla, haga clic en el menú **Tabla** y, a continuación, en **Propiedades de tabla**.  
  
2.  En el cuadro de diálogo **Editar propiedades de tabla** , busque la columna que contiene los criterios por los que desea filtrar y, a continuación, haga clic en la flecha hacia abajo que hay a la derecha del encabezado de columna.  
  
3.  En el menú **Autofiltro** , siga uno de estos procedimientos:  
  
    -   En la lista de valores de columna, active o desactive uno o varios valores para filtrar y haga clic en Aceptar.  
  
         Si el número de valores es sumamente grande, algunos elementos individuales podrían no mostrarse en la lista. En su lugar, verá un mensaje similar a "Demasiados elementos para mostrar".  
  
    -   Haga clic en **Numerar filtros** o **Filtros de texto** (según el tipo de columna) y, después, haga clic en uno de los comandos de operador de comparación (como Es igual a) o haga clic en Filtro personalizado. En el cuadro de diálogo **Filtro personalizado** , cree el filtro y, a continuación, haga clic en **Aceptar**.  
  
         Si comete un error y necesita volver a empezar, haga clic en **Borrar filtros de fila**.  
  
  
  
