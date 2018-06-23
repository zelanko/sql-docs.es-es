---
title: Agregar columnas a las consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5480a1ff78132ac8273fde2d0f5756ce62fc263
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108919"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>Agregar columnas a las consultas (Visual Database Tools)
  Para utilizar una columna en una consulta, deberá agregarla a la consulta. Puede agregar una columna para mostrarla en los resultados de la consulta, para utilizarla al ordenar, para realizar búsquedas en el contenido de la columna o para resumir su contenido. Puede decidir cuáles de las columnas que utiliza en la consulta se van a incluir en el panel Resultados cuando la consulta se ejecute. Para más información, consulte [Quitar columnas de los resultados de una consulta &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
> [!NOTE]  
>  Para ver el tipo de datos de una columna en el Diseñador de consultas y vistas, seleccione la tabla o el objeto con valores de tabla en el **panel Diagrama** y, en la ventana Propiedades, haga clic en Lista de columnas. A continuación, haga clic en los **puntos suspensivos (…)** para abrir el cuadro de diálogo **Lista de columnas** .  
  
 Siempre que utilice una columna en una consulta, también podrá utilizar una expresión formada por cualquier combinación de columnas, literales, operadores y funciones.  
  
### <a name="to-add-an-individual-column"></a>Para agregar una columna individual  
  
-   En el **panel Diagrama**, active la casilla situada junto a la columna que desea incluir.  
  
     -o bien-  
  
-   En el **panel Criterios**, vaya a la primera fila en blanco de la cuadrícula, haga clic en el campo de la columna **Columna** y seleccione un nombre de columna de la lista desplegable.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Para agregar todas las columnas correspondientes a una tabla o a un objeto con valores de tabla  
  
-   En el **panel Diagrama**, active la casilla situada junto a  **\*(todas las columnas)**.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Para agregar todas las columnas correspondientes a todas las tablas y todos los objetos con estructura de tabla  
  
1.  Compruebe que no hay ninguna línea de combinación seleccionada en el **panel de operaciones de tablas** .  
  
2.  Haga clic con el botón derecho en el espacio vacío de la ventana Diseño y elija **Propiedades** en el menú contextual.  
  
3.  En la ventana Propiedades, haga clic en **Mostrar todas las columnas** y elija **Sí** o **No** en la lista desplegable.  
  
## <a name="see-also"></a>Vea también  
 [Quitar columnas de resultados de la consulta &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Quitar columnas de las consultas &#40;Visual Database Tools&#41;](remove-columns-from-queries-visual-database-tools.md)   
 [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Resumir los resultados de la consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  