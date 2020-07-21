---
title: Cambiar el nombre de una tabla o una columna (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
author: minewiskan
ms.author: owend
ms.openlocfilehash: d7d0fa1fde56ab4293e7733a974ec57d77c55151
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938686"
---
# <a name="rename-a-table-or-column-ssas-tabular"></a>Cambiar el nombre de una tabla o una columna (SSAS tabular)
  Puede cambiar el nombre de una tabla durante el proceso de importación si escribe un **Nombre descriptivo** en la página **Seleccionar tablas y vistas** del **Asistente para importación de tablas**. También puede cambiar los nombres de tabla y de columna si importa los datos especificando una consulta en la página **Especificar una consulta SQL** del **Asistente para la importación de tablas**.  
  
 Después de haber agregado los datos al modelo, el nombre (o el título) de una tabla aparece en la pestaña de tabla, en la parte inferior del diseñador de modelos. Puede cambiar el nombre de la tabla para darle otro más adecuado. También puede cambiar el nombre de una columna una vez que los datos se hayan agregado al modelo. Esta opción es especialmente importante si ha importado los datos de varios orígenes y desea asegurarse de que las columnas de tablas diferentes tengan nombres que son fáciles de distinguir.  
  
### <a name="to-rename-a-table"></a>Para cambiar el nombre de una tabla  
  
1.  En el diseñador de modelos, haga clic con el botón derecho en la pestaña que contenga la tabla cuyo nombre quiera cambiar y, después, haga clic en **Cambiar nombre**.  
  
2.  Escriba el nuevo nombre.  
  
    > [!NOTE]  
    >  Puede modificar otras propiedades de una tabla, como la información de conexión y las asignaciones de columnas, con el cuadro de diálogo **Editar propiedades de tabla** . Sin embargo, no puede cambiar el nombre en este cuadro de diálogo.  
  
### <a name="to-rename-a-column"></a>Para cambiar el nombre de una columna  
  
1.  En el diseñador de modelos, haga doble clic en el encabezado de la columna cuyo nombre quiera cambiar, o bien haga clic con el botón derecho en el encabezado y seleccione **Cambiar el nombre de la columna** en el menú contextual.  
  
2.  Escriba el nuevo nombre.  
  
## <a name="naming-requirements-for-columns-and-tables"></a>Requisitos de los nombres de columnas y tablas  
 Las palabras y caracteres siguientes no se pueden utilizar en el nombre de una tabla o columna:  
  
-   Espacios iniciales o finales  
  
-   Caracteres de control  
  
-   Los siguientes caracteres (que no son válidos en los nombres de objetos Analysis Services):.,; ':/ \\ *|? &% $! + = () [] {}<>  
  
-   Palabras clave reservadas de Analysis Services, incluidos los nombres y operadores de funciones de las expresiones multidimensionales (MDX) y las extensiones de minería de datos (DMX).  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>Efecto de cambiar el nombre en las tablas, columnas y cálculos existentes  
 Siempre que cambia el nombre de una tabla, cambia el nombre del objeto de tabla subyacente, que puede contener varias columnas o medidas. Por consiguiente, cualquier columna de la tabla, y cualquier relación que utilice las tabla, debe actualizarse para utilizar el nuevo nombre en sus definiciones. Esta actualización tiene lugar automáticamente en algunos casos. Las medidas no se actualizan automáticamente.  
  
 Además, cualquier cálculo que utilice la tabla con el nombre cambiado o que use columnas de dicha tabla también debe actualizarse, así como los datos derivados de esos cálculos. Esto puede tardar un tiempo que depende de cuántas tablas y cálculos se vean afectados. Por consiguiente, el mejor momento para cambiar el nombre de las tablas es bien durante el proceso de importación o antes de empezar a generar relaciones y cálculos complejos.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas y columnas &#40;SSAS tabular&#41;](tables-and-columns-ssas-tabular.md)   
 [Importar desde PowerPivot &#40;SSAS tabular&#41;](import-from-power-pivot-ssas-tabular.md)   
 [Importación desde Analysis Services &#40;SSAS tabular&#41;](import-from-analysis-services-ssas-tabular.md)  
  
  
