---
title: Cambiar el alto de fila o el ancho de columna (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f061c204-5cd5-4467-9a9c-8a12803d93ba
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aef6ef0fe1f32f015abe3b48177f6e4d3e45648d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="change-row-height-or-column-width-report-builder-and-ssrs"></a>Cambiar el alto de fila o el ancho de columna (Generador de informes y SSRS)
  Cuando se establece un alto de fila, se está especificando el alto máximo para la fila en el informe representado. Sin embargo, de forma predeterminada, los cuadros de texto de la fila están configurados para crecer verticalmente con objeto de dar cabida a sus datos en tiempo de ejecución, y esto puede ocasionar que una fila crezca más allá del alto especificado. Para establecer un alto de fila fijo, debe cambiar las propiedades del cuadro de texto de modo que no se expandan automáticamente.  
  
 Cuando se establece un ancho de columna, se está especificando el ancho máximo para la columna en el informe representado. Las columnas no se ajustan horizontalmente de forma automática para dar cabida al texto.  
  
 Si una celda de una fila o columna contiene un rectángulo o una región de datos, el alto y el ancho mínimos de la celda están determinados por el alto y el ancho del elemento contenido. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-row-height-by-moving-row-handles"></a>Para cambiar la altura de la fila moviendo los identificadores de columna  
  
1.  En la vista Diseño, haga clic en cualquier punto de la región de datos Tablix para seleccionarla. Aparecen identificadores de fila grises en el borde externo de la región de datos Tablix.  
  
2.  Mantenga el mouse sobre el borde del identificador de fila que desea expandir. Aparece una flecha de dos puntas.  
  
3.  Haga clic para arrastrar el borde de la fila y muévalo más arriba o más abajo para ajustar el alto de fila.  
  
### <a name="to-change-row-height-by-setting-cell-properties"></a>Para cambiar la altura de la fila configurando las propiedades de la celda  
  
1.  En la vista Diseño, haga clic en una celda de la fila de la tabla.  
  
     ![La celda seleccionada en una tabla](../../reporting-services/report-design/media/table-selectcell.png "la celda seleccionada en una tabla")  
  
2.  En el panel **Propiedades** que aparece, modifique la propiedad **Alto** y, después, haga clic en cualquier parte que no sea el panel **Propiedades** .  
  
     ![Panel Propiedades de celda de la tabla seleccionada](../../reporting-services/report-design/media/cell-propertiespane.png "panel Propiedades de celda de la tabla seleccionada")  
  
### <a name="to-prevent-a-row-from-automatically-expanding-vertically"></a>Para evitar que una fila se expanda verticalmente de forma automática  
  
1.  En la vista Diseño, haga clic en cualquier punto de la región de datos Tablix para seleccionarla. Aparecen identificadores de fila grises en el borde externo de la región de datos Tablix.  
  
2.  Haga clic en el identificador de fila para seleccionar esta.  
  
3.  En el panel de propiedades, establezca CanGrow en **False**.  
  
    > [!NOTE]  
    >  Si no puede ver el panel Propiedades, haga clic en **Propiedades** en el menú **Ver**.  
  
### <a name="to-change-column-width"></a>Para cambiar el ancho de columna  
  
1.  En la vista Diseño, haga clic en cualquier punto de la región de datos Tablix para seleccionarla. Aparecen identificadores de columna grises en el borde externo de la región de datos Tablix.  
  
2.  Mantenga el mouse sobre el borde del identificador de columna que desea expandir. Aparece una flecha de dos puntas.  
  
3.  Haga clic para arrastrar el borde de la columna y muévalo hacia la derecha o hacia la izquierda para ajustar el ancho de columna.  
  
## <a name="see-also"></a>Vea también  
 [Región de datos Tablix (Generador de informes y SSRS)](https://msdn.microsoft.com/library/dd220587.aspx)   
 [Celdas, filas y columnas de la región de datos Tablix (Generador de informes y SSRS)](https://msdn.microsoft.com/library/dd220511.aspx)   
 [Tablas (Generador de informes y SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrices (Generador de informes y SSRS)](https://msdn.microsoft.com/library/dd207149.aspx)   
 [Listas (Generador de informes y SSRS)](https://msdn.microsoft.com/library/dd239330.aspx)   
 [Tablas, matrices y listas (Generador de informes y SSRS)](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
