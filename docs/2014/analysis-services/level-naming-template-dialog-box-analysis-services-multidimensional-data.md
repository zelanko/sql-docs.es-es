---
title: Nivel de nomenclatura de cuadro de diálogo de plantilla (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4b0a858c3e87aa657f02d106f6e6db453ee0cb0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088335"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Plantilla de asignación de nombres de nivel (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Plantilla de asignación de nombres de nivel** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para crear la plantilla de asignación de nombres de nivel para un atributo primario de una dimensión. Para obtener más información sobre el nivel de nomenclatura de plantillas, vea [Elemento NamingTemplate &#40;ASSL&#41;](scripting/properties/namingtemplate-element-assl.md). Puede mostrar el **Level Naming Template** cuadro de diálogo, haga clic en el botón de puntos suspensivos (**...** ) en el `NamingTemplate` valor de una traducción de un atributo en el **detalles de traducción** panel en el **traducciones** ficha de **delDiseñadordedimensiones**.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Definir la plantilla de nivel**|Muestra una cuadrícula en la que se puede diseñar la jerarquía de niveles del atributo primario. La cuadrícula contiene las columnas siguientes:<br /><br /> **Nivel**: muestra la posición ordinal del nivel para el que el nombre especificado en **nombre** se utiliza. Para agregar una nueva plantilla de asignación de nombres de nivel, seleccione **Nombre** en la fila que contenga un asterisco (\*) en **Nivel**.<br /><br /> **Nombre**: contiene la plantilla de nomenclatura usada para el nivel indicado en **nivel**. Si desea agregar un marcador de posición para la posición ordinal del nivel en la plantilla de asignación de nombres, agregue un asterisco (*). Para agregar un asterisco como parte del nombre creado por la plantilla de nomenclatura, deberá agregar dos asteriscos (\*\*).|  
|**Borrar todo**|Seleccione esta opción para borrar todas las filas de **Definir la plantilla de nivel**.|  
|**Resultado**|Muestra la plantilla de asignación de nombres de nivel generada en el cuadro de diálogo.|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Traducciones &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
