---
title: Editor de formulario de acción (pestaña acciones, diseñador de cubos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.action.f1
ms.assetid: c363a29b-6099-473c-9625-460cc15b3d95
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7c0a9b232a30fbaa4358bf9b23eb28ff16d79b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062958"
---
# <a name="action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulario de acción (pestaña Acciones, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Use el panel del Editor de Formulario de acción de la pestaña **Acciones** del Diseñador de cubos para crear y modificar acciones estándar.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba el nombre de la acción.  
  
 **Destino de la acción**  
 Expanda esta opción para ver las opciones **Tipo de destino** y **Objeto de destino** .  
  
 **Tipo de destino**  
 Seleccione el tipo de objeto al que desea asociar la acción. El servidor devolverá al cliente solo aquellas acciones que se aplican al objeto del tipo especificado. La acción estará disponible para el cliente si se cumple la **Condición** y si se seleccionan los objetos especificados en la siguiente tabla.  
  
|Value|Objeto seleccionado|  
|-----------|---------------------|  
|Miembros del atributo|Se seleccionará un miembro de un nivel según el atributo del **Objeto de destino**.|  
|Celdas|Se seleccionará el conjunto con nombre en **Objeto de destino** . Seleccione **Todas las celdas** para seleccionar todas las celdas del cubo.|  
|Cube|Se seleccionará el cubo en **Objeto de destino** . Seleccione CURRENTCUBE para utilizar el cubo actual.<br /><br /> Nota: Si usa CURRENTCUBE, obtendrá una portabilidad adicional en aquellos casos en que se cambie el nombre del cubo o se copie la acción a otros cubos. Se recomienda utilizar CURRENTCUBE para representar el cubo actual.|  
|miembros de dimensión|Se seleccionará un miembro de la dimensión en **Objeto de destino** .|  
|Hierarchy|Se seleccionará la jerarquía en **Objeto de destino** .|  
|Miembros de la jerarquía|Se seleccionará un miembro de la jerarquía en **Objeto de destino** .|  
|Nivel|Se seleccionará el nivel en **Objeto de destino** .|  
|Miembros del nivel|Se seleccionará un miembro del nivel en **Objeto de destino** .|  
  
 **Objeto de destino**  
 Seleccione el objeto al que desea asociar la acción. La instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] devuelve al cliente solo aquellas acciones que se aplican al objeto seleccionado. La lista de objetos disponibles se restringe por la selección del **Tipo de destino**.  
  
 **Condición (opcional)**  
 Escriba la expresión de Expresiones multidimensionales (MDX) que describe una condición opcional que, usada con **Objeto de destino**, restringe aún más la lista si la acción está disponible. La expresión devuelve un valor booleano que, si es verdadero, indica que la acción se encuentra disponible.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 **Contenido de la acción**  
 Expanda esta opción para ver las opciones **Tipo** y **Expresión de acción** .  
  
 **Tipo**  
 Seleccione el tipo de acción que desea realizar durante la ejecución de la acción. Están disponibles los siguientes tipos de acciones:  
  
|Value|Descripción|  
|-----------|-----------------|  
|Dataset|Devuelve una instrucción de Expresiones multidimensionales (MDX) que representa un conjunto de datos multidimensionales que se ejecutarán y se mostrarán en la aplicación cliente.|  
|Propietario|Devuelve una cadena del propietario que pueden interpretar las aplicaciones cliente asociadas a la configuración **Aplicación** para esta acción.|  
|Conjunto de filas|Devuelve una instrucción de Expresiones multidimensionales (MDX) que representa un conjunto de filas tabular que se ejecutará y se mostrará en la aplicación cliente.|  
|.|Devuelve una cadena de comandos que se ejecutará en la aplicación cliente.|  
|URL|Devuelve una cadena del localizador uniforme de recursos (URL) que abrirá la aplicación cliente, por lo general, con un explorador de Internet.|  
  
 Para más información sobre los tipos de acción, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 **Expresión de acción**  
 Escriba la expresión de Expresiones multidimensionales (MDX) que devolverá la cadena devuelta por la acción a la aplicación cliente para su ejecución.  
  
 **Propiedades adicionales**  
 Expanda esta opción para ver las opciones **Invocación**, **Aplicación**, **Descripción**, **Título**y **El título es MDX** .  
  
 **Invocación**  
 Seleccione la configuración que indica cuándo debe realizarse la acción.  
  
> [!NOTE]  
>  Esta opción solo ofrece una recomendación a una aplicación cliente sobre cuándo ejecutar una acción, pero no controla directamente la invocación de la acción.  
  
 En la siguiente tabla se describen las configuraciones disponibles.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Batch|La acción debe ejecutarse como parte de una operación de lote o una tarea de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interactive|La acción se ejecuta cuando el usuario invoca la acción.|  
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
  
 Escriba la expresión de Expresiones multidimensionales (MDX) que devuelve una cadena para el título si establece **El título es MDX** en **True**.  
  
 **El título es MDX**  
 Seleccione **False** para indicar que **Título** contiene una cadena literal que representa un título que se mostrará para la acción en la aplicación cliente.  
  
 Seleccione **True** para indicar que **Título** contiene una expresión MDX que devuelve una cadena que representa un título que se mostrará para la acción en la aplicación cliente. La expresión MDX debe resolverse antes de devolver la acción a la aplicación cliente.  
  
## <a name="see-also"></a>Consulte también  
 [Acciones &#40;diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de acciones &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Herramientas de cálculo &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services de datos multidimensionales&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de acción de obtención de detalles &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulario de acción de informe &#40;pestaña acciones, diseñador de cubos&#41; &#40;Analysis Services-datos multidimensionales&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
