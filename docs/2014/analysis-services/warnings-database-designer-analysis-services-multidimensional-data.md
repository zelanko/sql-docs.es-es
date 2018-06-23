---
title: Advertencias (Diseñador de la base de datos) (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e00890be8fac0fb97f0887034d5c7b04c049ebd0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112532"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>Advertencias (Diseñador de bases de datos) (Analysis Services - Datos multidimensionales)
  Use la pestaña **Advertencias** para ver y descartar reglas globalmente, así como para ver y volver a habilitar instancias específicas de advertencias descartadas. La pestaña **Advertencias** muestra dos cuadrículas: **Reglas de advertencia de diseño** y **Advertencias descartadas**.  
  
 **Para mostrar la pestaña advertencias**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
2.  En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , haga clic en **Editar base de datos**y, después, haga clic en la pestaña **Advertencias** .  
  
## <a name="design-warning-rules-grid"></a>Cuadrícula Reglas de advertencia de diseño  
 La cuadrícula **Reglas de advertencia de diseño** muestra todas las reglas de advertencia de diseño. Esta cuadrícula también controla qué reglas están habilitadas para la base de datos. Para habilitar o deshabilitar una regla de la advertencia, active o desactive su casilla.  
  
 La cuadrícula **Reglas de advertencia de diseño** tiene las columnas siguientes:  
  
 **Descripción**  
 Muestra el nombre de la regla. Las reglas se agrupan por categoría.  
  
 **Importancia**  
 Muestra la importancia asignada a la regla.  
  
 **Comentarios**  
 (Opcional) Permite al usuario escribir un comentario que explica por qué está descartando la advertencia.  
  
## <a name="dismissed-warnings-grid"></a>Cuadrícula de advertencias descartadas  
 La cuadrícula **Advertencias descartadas** muestra todas las repeticiones de advertencias específicas que se han descartado de la **Lista de errores**. Para volver a habilitar una advertencia, selecciónela en la cuadrícula y, después, haga clic en **Rehabilitar**.  
  
 La cuadrícula **Advertencias descartadas** tiene lo siguiente:  
  
 **Objeto**  
 Muestra un icono que representa el tipo y el nombre de objeto.  
  
 **Tipo**  
 Muestra el tipo de objeto.  
  
 **Descripción**  
 Muestra el nombre de la regla.  
  
 **Importancia**  
 Muestra la importancia asignada a la regla.  
  
 **Comentarios**  
 Muestra el comentario que se escribió cuando se descartó la advertencia. Puede agregar o modificar un comentario aquí.  
  
 **Volver a habilitar**  
 Rehabilita las advertencias seleccionadas.  
  
> [!NOTE]  
>  Si un objeto tiene una advertencia, pero el objeto se encuentra en un estado no válido o se quitó manualmente del proyecto, aparece un icono de error al lado de la advertencia en la lista. Para descartar la advertencia, selecciónela y, después, haga clic en **Rehabilitar**.  
  
## <a name="see-also"></a>Vea también  
 [Descartar el cuadro de diálogo de advertencia &#40;Analysis Services - datos multidimensionales&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [General &#40;Diseñador de la base de datos&#41; &#40;Analysis Services - datos multidimensionales&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  