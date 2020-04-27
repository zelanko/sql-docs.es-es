---
title: Editor de formulario de acción de obtención de detalles (pestaña acciones, diseñador de cubos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33d20da736308b4436c40a50b8b01da7445663c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081457"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulario de acción de obtención de detalles (pestaña Acciones, Diseñador de cubos) (Analysis Services -  Datos multidimensionales)
  Use el panel **Editor de Formulario de acción de obtención de detalles** de la pestaña **Acciones** del Diseñador de cubos para modificar la acción de obtención de detalles seleccionada en el panel **Organizador de acciones** . Para obtener más información sobre las acciones de obtención de detalles, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Las acciones de obtención de detalles ya no obtienen detalles del almacén de datos subyacente. La información a la que tienen acceso las acciones de obtención de detalles debe modelarse en el cubo utilizando miembros de jerarquía o dimensión.  
  
## <a name="options"></a>Opciones  
 **name**  
 Escriba el nombre de la acción.  
  
 **Destino de la acción**  
 Expanda esta opción para ver la opción **Miembros de grupo de medida** .  
  
 **Miembros de grupo de medida**  
 Seleccione el grupo de medida al que se asociará la acción de obtención de detalles.  
  
 **Condición (opcional)**  
 Escriba la expresión MDX (Expresiones multidimensionales) que describe una condición opcional, que se usa junto con **Miembros de grupo de medida**, con lo que restringe aún más el momento de disponibilidad de la acción. La expresión devuelve un valor booleano que, si es verdadero, indica que la acción se encuentra disponible.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 **Columnas de obtención de detalles**  
 Expanda esta opción para mostrar una cuadrícula en la que indicar los atributos que se devuelven cuando el usuario ejecuta esta acción.  
  
> [!NOTE]  
>  Puede seleccionar más de una dimensión, pero no se puede utilizar la misma dimensión más de una vez en una acción de obtención de detalles.  
  
 La cuadrícula contiene las columnas siguientes:  
  
|Columna|Descripción|  
|------------|-----------------|  
|**Dimensions**|Seleccione la dimensión de la que se deriva el atributo devuelto. Seleccione MEASURES para obtener detalles de medidas.|  
|**Columnas devueltas**|Seleccione el atributo o la medida de las dimensiones seleccionadas que se van a devolver cuando se ejecute la acción.|  
  
 **Propiedades adicionales**  
 Expanda esta opción para ver las opciones **Predeterminado**, **Número máximo de filas**, **Invocación**, **Aplicación**, **Descripción**, **Título**y **El título es MDX** .  
  
 **Valor predeterminado**  
 Seleccione **True** para incluir esta acción de obtención de detalles como la acción de obtención de detalles predeterminada; en caso contrario, seleccione **False**.  
  
 Si se `RETURN` omite la cláusula en una instrucción `DRILLTHROUGH` MDX ejecutada por una aplicación cliente, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] la instancia de evalúa todas las acciones de obtención de detalles predeterminadas y ejecuta la primera acción de obtención de detalles predeterminada que devuelve un conjunto no vacío. Para obtener más información acerca de `DRILLTHROUGH` la instrucción MDX, vea [instrucción DRILLTHROUGH &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough).  
  
> [!NOTE]  
>  Esta opción se utiliza por compatibilidad con versiones anteriores.  
  
 **Número máximo de filas**  
 Escriba el número máximo de filas que devolverá la acción de obtención de detalles. Al establecer esta opción en cero o en un valor vacío se indica que la acción de obtención de detalles devolverá todas las filas recuperadas por la acción a la aplicación cliente.  
  
 **Invocación**  
 Seleccione la configuración que indica cuándo debe realizarse la acción.  
  
> [!NOTE]  
>  Esta opción solo ofrece una recomendación a una aplicación cliente sobre cuándo ejecutar una acción, pero no controla directamente la invocación de la acción.  
  
 En la siguiente tabla se describen las configuraciones disponibles.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Batch|La acción debe ejecutarse como parte de una operación de lote o una tarea de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interactive (Interactivo)|La acción se ejecuta cuando el usuario invoca la acción.|  
|Al abrir|La acción se ejecuta cuando se abre el cubo por primera vez.|  
  
 **Aplicación**  
 Escriba el nombre de la aplicación que puede ejecutar la acción de obtención de detalles.  
  
 También puede utilizar esta opción para identificar qué aplicación cliente utiliza con más frecuencia esta acción, así como para mostrar los iconos adecuados junto a la acción en un menú emergente.  
  
> [!NOTE]  
>  Esta opción solo ofrece una recomendación a una aplicación cliente sobre qué aplicación debe ejecutar una acción, pero no controla directamente el acceso a la acción. Las aplicaciones cliente deben ocultar las acciones asociadas a otras aplicaciones cliente.  
  
 **Descripción**  
 Escriba la descripción opcional de la acción.  
  
 **Hayan**  
 Escriba el título que se mostrará para la acción en la aplicación cliente si establece **El título es MDX** en **False**.  
  
 Escriba la expresión de Expresiones multidimensionales (MDX) que devuelve una cadena para el título si establece **El título es MDX** en **True**.  
  
 **El título es MDX**  
 Seleccione **False** para indicar que **Título** contiene una cadena literal que representa un título que se mostrará para la acción en la aplicación cliente.  
  
 Seleccione **True** para indicar que **Título** contiene una expresión MDX que devuelve una cadena que representa un título que se mostrará para la acción en la aplicación cliente. La expresión MDX debe resolverse antes de devolver la acción a la aplicación cliente.  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones multidimensionales &#40;referencia de&#41; MDX](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Acciones &#40;diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de acciones &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Herramientas de cálculo &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de acción &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de acción de informe &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
