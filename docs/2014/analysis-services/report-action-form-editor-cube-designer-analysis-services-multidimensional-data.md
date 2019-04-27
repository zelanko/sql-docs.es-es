---
title: Editor de formulario de acción de informe (pestaña acciones, Diseñador de cubos) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.reportaction.f1
ms.assetid: cebfdd07-e376-46d6-86ef-b6f816a2f360
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb8659f916fa32c7b5c944bb525e64cf0551b0d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748387"
---
# <a name="report-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulario de acción de informe (pestaña Acciones, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Use el panel **Editor de Formulario de acción de informe** en la pestaña **Acciones** del Diseñador de cubos para modificar la acción de informe seleccionada en el panel **Organizador de acciones** .  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba el nombre de la acción.  
  
 **Destino de la acción**  
 Expanda esta opción para ver las opciones **Tipo de destino** y **Objeto de destino** .  
  
 **Tipo de destino**  
 Seleccione el tipo de objeto al que desea asociar la acción. El servidor devolverá al cliente solo aquellas acciones que se aplican al objeto del tipo especificado. La acción estará disponible para el cliente si se cumple la **Condición** y si se seleccionan los objetos especificados en la siguiente tabla.  
  
|Valor|Objeto seleccionado|  
|-----------|---------------------|  
|Miembros del atributo|Se seleccionará un miembro de un nivel según el atributo del **Objeto de destino**.<br /><br /> Nota: Otras jerarquías de usuarios que utilizan el atributo seleccionado heredan la acción de informe.|  
|Celdas|Se seleccionará el conjunto con nombre en **Objeto de destino** . Seleccione **Todas las celdas** para seleccionar todas las celdas del cubo.|  
|Cube|Se seleccionará el cubo en **Objeto de destino** . Seleccione CURRENTCUBE para utilizar el cubo actual.<br /><br /> Nota: Usa CurrentCube, obtendrá proporciona una portabilidad adicional en aquellos casos en que se cambie el nombre de cubo o copie la acción a otros cubos. Se recomienda utilizar CURRENTCUBE para representar el cubo actual.|  
|miembros de dimensión|Se seleccionará un miembro de la dimensión en **Objeto de destino** .|  
|Hierarchy|Se seleccionará la jerarquía en **Objeto de destino** .|  
|Miembros de la jerarquía|Se seleccionará un miembro de la jerarquía en **Objeto de destino** .|  
|Nivel|Se seleccionará el nivel en **Objeto de destino** .|  
|Miembros del nivel|Se seleccionará un miembro del nivel en **Objeto de destino** .|  
  
 **Objeto de destino**  
 Seleccione el objeto al que desea asociar la acción. La instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] devuelve al cliente solo aquellas acciones que se aplican al objeto seleccionado. La lista de objetos disponibles se restringe por la selección del **Tipo de destino**.  
  
 **Condición (opcional)**  
 Escriba la expresión de Expresiones multidimensionales (MDX) que describe una condición opcional que, usada con **Objeto de destino**, restringe aún más la lista si la acción está disponible. La expresión devuelve un valor booleano que, si es verdadero, indica que la acción se encuentra disponible.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 **Servidor de informes**  
 Expanda para ver las opciones **Nombre del servidor**, **Ruta de acceso al servidor**y **Formato de informe** .  
  
 **Nombre del servidor**  
 Escriba el nombre de la instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en la que la acción ejecuta el informe.  
  
 **Ruta de acceso al servidor**  
 Escriba la ruta del informe en la instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Por ejemplo, escriba **Sales/YearlySalesByCategory**.  
  
 **Formato de informe**  
 Seleccione el formato con el que desea que se devuelva el informe. En la tabla siguiente se describen los formatos disponibles.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|HTML5|El informe se devuelve en un formato compatible con HTML 5.0.|  
|HTML3|El informe se devuelve en un formato compatible con HTML 3.2.|  
|Excel|El informe se devuelve como un archivo de libro (.xls) de [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel.|  
|PDF|El informe se devuelve como un archivo con formato Adobe Portable Document (.pdf).|  
  
 **Parámetros (opcional)**  
 Expanda esta opción para ver una cuadrícula en la que es posible proporcionar parámetros de informe para el informe especificado en **Informe**. La cuadrícula contiene las columnas siguientes:  
  
|columna|Descripción|  
|------------|-----------------|  
|**Nombre de parámetro**|Escriba el nombre del parámetro del informe que desea pasar al informe.|  
|**Valor de parámetro**|Escriba el valor del parámetro del informe que desea pasar al informe.<br /><br /> Haga clic en el botón de puntos suspensivos (**...**) para mostrar el cuadro de diálogo **Generador MDX** y crear una expresión MDX que proporcione el valor del parámetro del informe. Para más información sobre el cuadro de diálogo **Generador MDX**, vea [Generador MDX &#40;Analysis Services - Datos multidimensionales&#41;](mdx-builder-analysis-services-multidimensional-data.md).<br /><br /> Si se establece una expresión MDX en el parámetro, se evaluará la expresión al ejecutar la acción o, de lo contrario, se pasará al informe sin modificación alguna.|  
  
 **Propiedades adicionales**  
 Expanda esta opción para ver las opciones **Invocación**, **Aplicación**, **Descripción**, **Título**y **El título es MDX** .  
  
 **Invocación**  
 Seleccione la configuración que indica cuándo debe realizarse la acción.  
  
> [!NOTE]  
>  Esta opción solo ofrece una recomendación a una aplicación cliente sobre cuándo ejecutar una acción, pero no controla directamente la invocación de la acción.  
  
 En la siguiente tabla se describen las configuraciones disponibles.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Lote|La acción debe ejecutarse como parte de una operación de lote o una tarea de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interactiva|La acción se ejecuta cuando el usuario invoca la acción.|  
|Al abrir|La acción se ejecuta cuando se abre el cubo por primera vez.|  
  
 **Aplicación**  
 Escriba el nombre de la aplicación que puede interpretar la cadena devuelta por la **Expresión de acción**.  
  
 También puede utilizar esta opción para identificar qué aplicación cliente utiliza con más frecuencia esta acción, así como para mostrar los iconos adecuados junto a la acción en un menú emergente.  
  
> [!NOTE]  
>  Esta opción solo ofrece una recomendación a una aplicación cliente sobre qué aplicación debe ejecutar una acción, pero no controla directamente el acceso a la acción. Las aplicaciones cliente deben ocultar las acciones asociadas a otras aplicaciones cliente.  
  
 **Descripción**  
 Escriba la descripción opcional de la acción.  
  
 **Caption**  
 Escriba el título que se mostrará para la acción en la aplicación cliente si establece **El título es MDX** en **False**.  
  
 Escriba la expresión MDX que devuelve una cadena para el título si establece **True** en **El título es MDX**.  
  
 **El título es MDX**  
 Seleccione **False** para indicar que **Título** contiene una cadena literal que representa un título que se mostrará para la acción en la aplicación cliente.  
  
 Seleccione **True** para indicar que **Título** contiene una expresión MDX que devuelve una cadena que representa un título que se mostrará para la acción en la aplicación cliente. La expresión MDX debe resolverse antes de devolver la acción a la aplicación cliente.  
  
## <a name="see-also"></a>Vea también  
 [Acciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña acciones, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de acciones &#40;pestaña acciones, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Herramientas de cálculo &#40;pestaña acciones, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de acción &#40;pestaña acciones, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de acción de obtención de detalles &#40;pestaña acciones, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
