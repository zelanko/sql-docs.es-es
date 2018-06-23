---
title: Herramientas Diseñador de consultas y vistas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.querydesigner
- vdt.pane.diagram
- vdt.pane.grid
- vdt.dlgbox.querybuilder
- vdt.pane.sql
- vdt.pane.results
helpviewer_keywords:
- Query Designer [SQL Server], panes
- View Designer, panes
- Query Designer [SQL Server], components
- View Designer, components
ms.assetid: 12e4b5a5-b793-4b6c-a0e5-c450c49bf26f
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ec0aafb394d43fa55fa940ca5ce23cca798b3ef4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113942"
---
# <a name="query-and-view-designer-tools-visual-database-tools"></a>Herramientas Diseñador de consultas y vistas (Visual Database Tools)
  Al diseñar una consulta, una vista, una función insertada o un procedimiento almacenado de una sola instrucción, el diseñador que utiliza está formado por cuatro paneles: el panel Diagrama, el panel Criterios, el panel de SQL y el panel Resultados.  
  
 ![Diseñador de consultas](../../database-engine/media//vs-queryviewdsgpanes.gif "Diseñador de consultas")  
  
-   En el panel Diagrama se muestran las tablas y otros objetos con valores de tabla que se están consultando. Cada rectángulo representa una tabla o un objeto con valores de tabla y muestra las columnas de datos disponibles. Las combinaciones se indican mediante líneas entre los rectángulos. Para más información, consulte [Panel Diagrama &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
-   El panel Criterios contiene una cuadrícula con forma de hoja de cálculo en la que se especifican opciones, como qué columnas de datos mostrar, qué filas seleccionar, cómo agrupar filas, etc. Para más información, consulte [Panel Criterios &#40;Visual Database Tools&#41;](criteria-pane-visual-database-tools.md).  
  
-   En el panel SQL se muestra la instrucción SQL para la consulta o vista. Puede editar la instrucción SQL creada por el Diseñador o puede especificar una instrucción SQL propia. Resulta especialmente útil para escribir instrucciones SQL que no se pueden crear mediante los paneles Diagrama y Cuadrícula, como las consultas de unión. Para más información, consulte [Panel SQL &#40;Visual Database Tools&#41;](sql-pane-visual-database-tools.md).  
  
-   En el panel Resultados se muestra una cuadrícula con datos recuperados por la consulta o vista. En el panel del Diseñador de consultas y vistas, se muestran los resultados de la consulta SELECT ejecutada más recientemente. Puede modificar la base de datos mediante la edición de los valores de las celdas de la cuadrícula y puede agregar filas o eliminarlas. Para más información, consulte [Panel Resultados &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md).  
  
 Puede crear una consulta o una vista en cualquiera de los paneles; para hacer aparecer una columna, puede elegirla en el panel Diagrama, puede introducirla en el panel Criterios o puede incluirla en la instrucción SQL del panel de SQL.  
  
## <a name="displaying-and-hiding-panes"></a>Mostrar y ocultar paneles  
 Para ocultar un panel o mostrar un panel que no esté visible, haga clic con el botón derecho en la superficie de diseño, seleccione **Panel**y, a continuación, haga clic en el nombre del panel. Si el Diseñador de consultas y vistas se abre en el modo de Diseñador de consultas, el panel **Resultados** no estará disponible.  
  
## <a name="see-also"></a>Vea también  
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Abra el Diseñador de consultas y vista &#40;Visual Database Tools&#41;](open-the-query-and-view-designer-visual-database-tools.md)   
 [Editor SQL &#40;Visual Database Tools&#41;](sql-editor-visual-database-tools.md)  
  
  