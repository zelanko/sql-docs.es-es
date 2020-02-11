---
title: Diagrama de relación de los atributos (pestaña diseñador de relación de los atributos, diseñador de dimensiones) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.ardesigner.ardiagram.f1
ms.assetid: 320989ad-bd95-43f4-a2e7-b262d66dbda7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8fbd67f8a6fcc88a3821583d1e06ec3e8a75ab91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66063098"
---
# <a name="attribute-relationship-diagram-attribute-relationship-designer-tab-dimension-designer-analysis-services---multidimensional-data"></a>Diagrama Relación de los atributos (pestaña Diseñador de Relación de los atributos, Diseñador de dimensiones) (Analysis Services - Datos multidimensionales)
  Use el panel que se encuentra inmediatamente debajo de la barra de herramientas en la pestaña **Relación de los atributos** para ver el diagrama de la relación de los atributos y para crear, modificar y eliminar relaciones de atributo.  
  
 **Para ver el panel que contiene el diagrama de la relación de los atributos**  
  
-   En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga doble clic en una dimensión para abrir el Diseñador de dimensiones y, después, haga clic en la pestaña **Relación de los atributos** .  
  
## <a name="using-the-attribute-relationship-diagram"></a>Usar el diagrama de la relación de los atributos  
 Use el diagrama de la relación de los atributos para crear, modificar o eliminar relaciones de atributo. El diagrama de la relación de los atributos también resaltará las relaciones de atributo problemáticas y mostrará una descripción del problema en la información sobre herramientas.  
  
 Hay tres menús contextuales independientes disponibles en el diagrama: el menú contextual de diagrama, el menú contextual de atributo y el menú contextual de relación.  
  
### <a name="diagram-shortcut-menu"></a>Menú contextual de diagrama  
 Para abrir el menú contextual para el diagrama de la relación de los atributos, haga clic con el botón secundario en el fondo del diagrama. El menú contextual de diagrama presenta los siguientes comandos:  
  
 **Nueva relación de atributo**  
 Abre el cuadro de diálogo **Crear relación de atributo** en el que puede definir una nueva relación de atributo.  
  
 Para más información, vea [Cuadros de diálogo Crear relación de atributo y Editar relación de atributo &#40;pestaña Diseñador de Relación de los atributos, Diseñador de dimensiones&#41; &#40;Analysis Services - Datos multidimensionales&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) y [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md).  
  
 **Organizar formas**  
 Organiza las formas según el algoritmo del diseño que usa el Diseñador de dimensiones.  
  
 **Organización automática de las formas**  
 Organiza automáticamente las formas en el diagrama según el algoritmo del diseño que usa el Diseñador de dimensiones. De forma predeterminada, la opción **Organización automática de las formas** está habilitada.  
  
 **Mostrar vistas de lista**  
 Muestra u oculta las listas **Atributos** y **Relación de los atributos** . Estas listas aparecen en sus propios paneles, inmediatamente debajo del panel que contiene el diagrama de la relación de los atributos.  
  
 **Expandir todas las formas**  
 Muestra los atributos agrupados que se asocian a los atributos de nivel superior. Los atributos agrupados solo están visibles cuando se expanden las formas en el diagrama de la relación de los atributos.  
  
> [!NOTE]  
>  Si hace clic en esta opción, el Diseñador de dimensiones devolverá las formas del diagrama de la relación de los atributos al diseño predeterminado que usa el diseñador.  
  
 **Contraer todas las formas**  
 Oculta los atributos agrupados que se asocian a los atributos de nivel superior.  
  
> [!NOTE]  
>  Si hace clic en esta opción, el Diseñador de dimensiones devolverá las formas del diagrama de la relación de los atributos al diseño predeterminado que usa el diseñador.  
  
 **Zoom**  
 Muestra una lista de las opciones de zoom disponibles.  
  
### <a name="attribute-shortcut-menu"></a>Menú contextual de atributo  
 Para abrir el menú contextual de atributo, haga clic con el botón secundario en un atributo del diagrama de la relación de los atributos. El menú contextual de atributo presenta los siguientes comandos:  
  
 **Nueva relación de atributo**  
 Abre el cuadro de diálogo **Crear relación de atributo** en el que puede definir una nueva relación de atributo.  
  
 Para más información, vea [Cuadros de diálogo Crear relación de atributo y Editar relación de atributo &#40;pestaña Diseñador de Relación de los atributos, Diseñador de dimensiones&#41; &#40;Analysis Services - Datos multidimensionales&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) y [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md).  
  
 **Propiedades**  
 Muestra las propiedades del atributo en la ventana **Propiedades** .  
  
### <a name="relationship-shortcut-menu"></a>Menú contextual de relación  
 Para abrir el menú contextual de relación, haga clic con el botón secundario en la flecha que identifica la relación entre dos atributos. El menú contextual de relación presenta los siguientes comandos:  
  
 **Editar relación de atributo**  
 Abre el cuadro de diálogo **Editar relación de atributo** en el que puede modificar la relación de atributo.  
  
 Para más información, vea [Cuadros de diálogo Crear relación de atributo y Editar relación de atributo &#40;pestaña Diseñador de Relación de los atributos, Diseñador de dimensiones&#41; &#40;Analysis Services - Datos multidimensionales&#41;](create-edit-attribute-relationships-dialog-boxes-analysis-services-multidimensional-data.md) y [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md).  
  
 **Tipo de relación**  
 Establece el tipo de relación en **Flexible** o **Rígida**. En una relación flexible, las relaciones entre los miembros cambian con el tiempo. En una relación rígida, las relaciones entre los miembros no cambian con el tiempo.  
  
 **Eliminar**  
 Elimina la relación de atributo.  
  
 **Propiedades**  
 Muestra las propiedades de la relación en la ventana **Propiedades** .  
  
## <a name="see-also"></a>Consulte también  
 [Relaciones de atributo &#40;diseñador de dimensiones&#41; &#40;Analysis Services de datos multidimensionales&#41;](attribute-relationships-dimension-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña diseñador de relación de los atributos, diseñador de dimensiones&#41; &#40;Analysis Services-datos multidimensionales&#41;](toolbar-attribute-relationship-dimension-designer-analysis-services-multidimensional-data.md)   
 [Atributos &#40;pestaña diseñador de relación de los atributos, diseñador de dimensiones&#41; &#40;Analysis Services-datos multidimensionales&#41;](attributes-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [Relaciones de atributo &#40;pestaña diseñador de relación de los atributos, diseñador de dimensiones&#41; &#40;Analysis Services-datos multidimensionales&#41;](attribute-relationships-designer-tab-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
