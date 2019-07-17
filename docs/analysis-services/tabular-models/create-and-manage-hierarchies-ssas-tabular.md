---
title: Crear y administrar jerarquías en los modelos tabulares de Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e785fe0e4a5f0030beceff7b9393932a29eaa52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163026"
---
# <a name="create-and-manage-hierarchies"></a>Crear y administrar jerarquías 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las jerarquías se pueden crear y administrar en la Vista de diagrama del diseñador de modelos. Para ver el diseñador de modelos en la Vista de diagrama, en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** , seleccione **Vista de modelo**y haga clic en **Vista de diagrama**.  
  
 En este artículo incluye las siguientes tareas:  
  
-   [Crear una jerarquía](#bkmk_create)  
  
-   [Editar una jerarquía](#bkmk_edit)  
  
-   [Eliminar una jerarquía](#bkmk_delete)  
  
##  <a name="bkmk_create"></a> Crear una jerarquía  
 Puede crear una jerarquía usando las columnas y el menú contextual de la tabla. Al crear una jerarquía, se muestra un nuevo nivel primario con las columnas seleccionadas como niveles secundarios.  
  
#### <a name="to-create-a-hierarchy-from-the-context-menu"></a>Para crear una jerarquía desde el menú contextual  
  
1.  En el diseñador de modelos (Vista de diagrama), en una ventana de tabla, haga clic con el botón derecho en una columna y, después, haga clic en **Crear jerarquía**.  
  
     Para seleccionar varias columnas, haga clic en cada columna, haga clic con el botón derecho para abrir el menú contextual y, después, haga clic en **Crear jerarquía**.  
  
     Se creará un nivel primario de la jerarquía en la parte inferior de la ventana de tabla y las columnas seleccionadas se copiarán debajo de la jerarquía como niveles secundarios.  
  
2.  Escriba el nombre de la jerarquía.  
  
 Puede arrastrar columnas adicionales al nivel primario de la jerarquía, que copia las columnas. Arrastre y coloque el nivel secundario para situarlo donde desea que aparezca en la jerarquía.  
  
> [!NOTE]  
>  El comando Crear jerarquía está deshabilitado en el menú contextual si realiza una selección múltiple de una medida junto con una o varias columnas, o si selecciona columnas de varias tablas.  
  
##  <a name="bkmk_edit"></a> Editar una jerarquía  
 Puede cambiar el nombre de una jerarquía, cambiar el nombre de un nivel secundario, cambiar el orden de los niveles secundarios, agregar columnas adicionales como niveles secundarios, quitar un nivel secundario de una jerarquía, mostrar el nombre del origen de un nivel secundario (el nombre de columna) y ocultar un nivel secundario si tiene el mismo nombre que el nivel primario de la jerarquía.  
  
#### <a name="to-change-the-name-of-a-hierarchy-or-child-level"></a>Para cambiar el nombre de una jerarquía o de un nivel secundario  
  
1.  Haga clic con el botón derecho en el nivel primario de la jerarquía o en un nivel secundario y, después, haga clic en **Cambiar nombre**.  
  
2.  Escriba un nuevo nombre o edite el nombre existente.  
  
#### <a name="to-change-the-order-of-a-child-level-in-a-hierarchy"></a>Para cambiar el orden de un nivel secundario de una jerarquía  
  
-   Haga clic en un nivel secundario y arrástrelo hasta una nueva posición en la jerarquía.  
  
-   O bien, haga clic con el botón secundario en un nivel secundario de la jerarquía y, a continuación, haga clic en Subir para mover el nivel hacia arriba en la lista o haga clic en Bajar para mover el nivel hacia abajo en la lista.  
  
-   O bien, haga clic en un nivel secundario para seleccionarlo y, a continuación, presione Alt + Flecha arriba para mover el nivel hacia arriba o Alt + Flecha abajo para mover el nivel hacia abajo en la lista.  
  
#### <a name="to-add-another-child-level-to-a-hierarchy"></a>Para agregar otro nivel secundario a una jerarquía  
  
-   Haga clic en una columna y arrástrela al nivel primario o a una ubicación específica de la jerarquía. La columna se copiará como un nivel secundario de la jerarquía.  
  
-   O bien, haga clic con el botón derecho en una columna, seleccione **Agregar a jerarquía**y, después, haga clic en la jerarquía.  
  
> [!NOTE]  
>  Puede agregar una columna oculta (una columna que no se muestra en los informes) como un nivel secundario de la jerarquía. El nivel secundario no está oculto.  
  
#### <a name="to-remove-a-child-level-from-a-hierarchy"></a>Para quitar un nivel secundario de una jerarquía  
  
-   Haga clic con el botón derecho en un nivel secundario y, después, haga clic en **Quitar de la jerarquía**.  
  
-   O bien, haga clic en un nivel secundario y, a continuación, presione **Supr**.  
  
> [!NOTE]  
>  Si cambia el nombre de un nivel secundario de la jerarquía, dejará de tener el mismo nombre que la columna de la que se copió. Use el comando **Mostrar nombre del origen** para ver de qué columna se copió.  
  
#### <a name="to-show-a-source-name"></a>Para mostrar un nombre de origen  
  
-   Haga clic con el botón derecho en un nivel secundario de la jerarquía y, después, haga clic en **Show Source Name**(Mostrar nombre del origen). Aparece el nombre de la columna de la que se copió la jerarquía.  
  
##  <a name="bkmk_delete"></a> Eliminar una jerarquía  
  
#### <a name="to-delete-a-hierarchy-and-remove-its-child-levels"></a>Para eliminar una jerarquía y quitar sus niveles secundarios  
  
-   Haga clic con el botón secundario en el nivel primario de la jerarquía y, a continuación, haga clic en Eliminar jerarquía.  
  
-   O bien, haga clic en el nivel primario de la jerarquía y, a continuación, presione Supr. Esto también quitará todos los niveles secundarios.  
  
## <a name="see-also"></a>Vea también  
 [Diseñador de modelos tabulares](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [Jerarquías](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
