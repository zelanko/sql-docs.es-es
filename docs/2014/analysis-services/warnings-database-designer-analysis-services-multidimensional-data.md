---
title: ADVERTENCIAS (diseñador de bases de datos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 113f644d9f1da48790e7c8d59d34e6b143a1175a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938127"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>Advertencias (Diseñador de bases de datos) (Analysis Services - Datos multidimensionales)
  Use la pestaña **Advertencias** para ver y descartar reglas globalmente, así como para ver y volver a habilitar instancias específicas de advertencias descartadas. La pestaña **Advertencias** muestra dos cuadrículas: **Reglas de advertencia de diseño** y **Advertencias descartadas**.  
  
 **Para mostrar la pestaña Advertencias**  
  
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
  
 **Object**  
 Muestra un icono que representa el tipo y el nombre de objeto.  
  
 **Tipo**  
 Muestra el tipo de objeto.  
  
 **Descripción**  
 Muestra el nombre de la regla.  
  
 **Importancia**  
 Muestra la importancia asignada a la regla.  
  
 **Comentarios**  
 Muestra el comentario que se escribió cuando se descartó la advertencia. Puede agregar o modificar un comentario aquí.  
  
 **Rehabilitar**  
 Rehabilita las advertencias seleccionadas.  
  
> [!NOTE]  
>  Si un objeto tiene una advertencia, pero el objeto se encuentra en un estado no válido o se quitó manualmente del proyecto, aparece un icono de error al lado de la advertencia en la lista. Para descartar la advertencia, selecciónela y, después, haga clic en **Rehabilitar**.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo descartar ADVERTENCIA &#40;Analysis Services de datos multidimensionales&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [Diseñador de bases de datos de &#40;general&#41; &#40;Analysis Services de datos multidimensionales&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
