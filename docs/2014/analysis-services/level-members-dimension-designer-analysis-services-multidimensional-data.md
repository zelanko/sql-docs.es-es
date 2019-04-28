---
title: Nivel y miembros (pestaña explorador, Diseñador de dimensiones) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.browsertab.levelsandmembers.f1
ms.assetid: 3f61e384-5b4e-4480-a7ed-b408de2fdea7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a737b79944635af1a45dd4fc51a9ef2e2967a31
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728162"
---
# <a name="level-and-members-browser-tab-dimension-designer-analysis-services---multidimensional-data"></a>Nivel y miembros (pestaña Explorador, Diseñador de dimensiones) (Analysis Services - Datos multidimensionales)
  Use este panel para examinar los miembros del idioma y la jerarquía seleccionados actualmente. Para seleccionar el idioma o la jerarquía que se examinará, use las opciones **Jerarquía** e **Idioma** del panel **Barra de herramientas** . Para obtener más información sobre el panel Barra de herramientas, vea [Toolbar &#40;Browser Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md).  
  
## <a name="writeback-mode"></a>Modo de reescritura  
 La funcionalidad de este panel cambia si el modo de reescritura está habilitado. La dimensión seleccionada debe permitir la escritura (es decir, la propiedad `WriteEnabled` de la dimensión debe establecerse en True) y la dimensión debe implementarse en una instantánea de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para habilitar el modo de reescritura.  
  
 Para habilitar el modo de reescritura, puede seleccionar **Reescritura** en el panel **Barra de herramientas** , o hacer clic con el botón derecho en el panel **Nivel y miembros** y seleccionar **Reescritura** en el menú contextual.  
  
 Si el modo de reescritura está habilitado, puede realizar las siguientes acciones adicionales en el panel **Nivel y miembros** :  
  
|Para|Acciones|  
|-----------|-------------|  
|Crear miembros del mismo nivel y miembros secundarios en la jerarquía seleccionada|Haga clic con el botón derecho en el miembro seleccionado y, en el menú contextual, seleccione **Crear igual**para crear un miembro del mismo nivel o **Crear secundario**para crear un miembro secundario.|  
|Mover un miembro seleccionado hacia arriba o hacia abajo en la jerarquía|Arrastre el miembro seleccionado al miembro primario o secundario adecuado o haga clic en **Aumentar sangría** o **Disminuir sangría** en el panel **Barra de herramientas** para mover el miembro seleccionado hacia arriba o hacia abajo en los niveles de la jerarquía.|  
|Cambiar el nombre del miembro seleccionado|Haga clic con el botón derecho en el miembro seleccionado y seleccione **Cambiar nombre**o haga clic en un miembro ya seleccionado.|  
|Editar valores de propiedad del miembro|Haga doble clic en el valor de la propiedad del miembro seleccionado para editar el valor.|  
  
## <a name="options"></a>Opciones  
 **Nivel actual**  
 Muestra el nivel al que pertenece el miembro seleccionado actualmente en **Árbol** .  
  
 **Árbol**  
 Muestra los miembros del idioma y la jerarquía seleccionada actualmente.  
  
 Si están seleccionadas las propiedades del miembro en la opción **Propiedades del miembro** del panel Barra de herramientas, cada propiedad del miembro se muestra como una columna.  
  
 Si el modo de reescritura está habilitado, se muestra una columna por cada columna de clave asociada con el atributo clave de la dimensión.  
  
## <a name="context-menu"></a>Menú contextual  
 Las siguientes opciones están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en cualquier parte del panel **Nivel y miembros** del miembro seleccionado:  
  
 **Creación del mismo nivel**  
 Crea un nuevo miembro en el mismo nivel que el miembro seleccionado.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se ha seleccionado un miembro en un nivel distinto de (Todos).  
  
> [!NOTE]  
>  Esta opción solo se muestra si se ha habilitado el modo de reescritura.  
  
 **Crear secundario**  
 Crea un nuevo miembro en el nivel inmediatamente inferior que el miembro seleccionado, como un miembro secundario del miembro seleccionado.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se ha seleccionado un miembro en un nivel distinto del nivel más bajo.  
  
> [!NOTE]  
>  Esta opción solo se muestra si se ha habilitado el modo de reescritura.  
  
 **Cut**  
 Copia los miembros seleccionados en el portapapeles y los quita de la jerarquía.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se ha seleccionado un miembro distinto del miembro Todos.  
  
> [!NOTE]  
>  Esta opción solo se muestra si se ha habilitado el modo de reescritura.  
  
 **Pegar**  
 Pega los miembros quitados anteriormente usando **Cortar** inmediatamente después del miembro seleccionado.  
  
> [!NOTE]  
>  Esta opción solo se muestra si se ha habilitado el modo de reescritura.  
  
 **Eliminar**  
 Quita los miembros seleccionados de la jerarquía.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se ha seleccionado un miembro distinto del miembro Todos.  
  
> [!NOTE]  
>  Esta opción solo se muestra si se ha habilitado el modo de reescritura.  
  
 **Cambiar el nombre**  
 Seleccione esta opción para modificar el nombre del miembro seleccionado.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se ha seleccionado un miembro distinto del miembro Todos.  
  
> [!NOTE]  
>  Esta opción solo se muestra si se ha habilitado el modo de reescritura.  
  
 **Filtrar miembros**  
 Muestra el cuadro de diálogo **Filtrar miembros** para filtrar los miembros mostrados en **Nivel y miembros** para la jerarquía seleccionada. Para más información sobre el cuadro de diálogo **Filtrar miembros**, vea [Cuadro de diálogo Filtrar miembros &#40;Analysis Services - Datos multidimensionales&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Expandir todo**  
 Expande todos los miembros del **Árbol**.  
  
> [!NOTE]  
>  Esta opción solo está habilitada si se ha seleccionado un miembro en un nivel distinto del nivel más bajo.  
  
 **Contraer todo**  
 Contrae todos los miembros del **Árbol**.  
  
 **Expandir miembro**  
 Expande el miembro seleccionado en el **Árbol**.  
  
 **Contraer miembro**  
 Contrae el miembro seleccionado en el **Árbol**.  
  
 **Writeback**  
 Seleccione esta opción para habilitar el modo de reescritura.  
  
## <a name="see-also"></a>Vea también  
 [Barra de herramientas &#40;pestaña del explorador, Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [Explorador &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](browser-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
