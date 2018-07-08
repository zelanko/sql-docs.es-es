---
title: Cuadro de diálogo de propiedades de conjunto de datos, filtros (generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10025"
ms.assetid: 933a6f44-4eb7-4e73-9c40-ac0fd17b23d3
caps.latest.revision: 14
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dbe6bee60f4cee2ce99f5aadd1dc3cea14e85b1b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258171"
---
# <a name="dataset-properties-dialog-box-filters-report-builder"></a>Propiedades del conjunto de datos (cuadro de diálogo), Filtros (Generador de informes)
  Seleccione **Filtros** en el cuadro de diálogo **Propiedades del conjunto de datos** para crear filtros para el conjunto de datos.  
  
 Los filtros que forman parte de una definición de conjunto de datos compartido en el servidor de informes afectan a todos los informes que utilizan el conjunto de datos compartido. Los filtros adicionales para el conjunto de datos compartido se pueden especificar una vez agregado a un informe. Estos filtros solo afectan al informe en el que se definen.  
  
 Los filtros para un conjunto de datos incrustado solo afectan al informe en el que se definen.  
  
 Para más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Agrega una nueva cláusula de filtro a la lista.  
  
 **Eliminar**  
 Elimina de la lista la cláusula de filtro seleccionada.  
  
 **Flecha arriba**  
 Mueve el filtro seleccionado hacia arriba en la lista.  
  
 **Flecha abajo**  
 Mueve el filtro seleccionado hacia abajo en la lista.  
  
 **Expresión**  
 Escriba o elija la expresión a la que desea aplicar un filtro. Haga clic en el botón Expresión (**fx**) para editar la expresión.  
  
 **Data type**  
 Elija el tipo de datos para **Valor**. Si es posible, elija un tipo de datos que coincida con el tipo de datos de **Expresión**.  
  
 Los valores de **Expresión** y de **Valor** deben devolver el mismo tipo de datos. Por ejemplo, si **Expresión** se establece en un campo que tiene el tipo de datos System.Int32 y **Valor** se establece en 7, en la lista desplegable, elija **Integer**.  
  
 Si la opción de tipos de datos que necesita no está en la lista desplegable, escriba una expresión que convierta el valor al tipo de datos correcto. Para más información, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
 **Operador**  
 Elija el operador que se va a utilizar para comparar la expresión y el valor.  
  
 **Value**  
 Escriba la expresión o el valor que se debe usar al evaluar la expresión especificada en el cuadro **Expresión** . Haga clic en el botón Expresión (**fx**) para editar la expresión.  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar un filtro a un conjunto de datos &#40;generador de informes y SSRS&#41;](report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)   
 [Usar expresiones en informes &#40;generador de informes y SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
