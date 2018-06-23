---
title: Actualizar celdas (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f2a4a8976602080f28f736814783397bc6611e64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200234"
---
# <a name="updating-cells-xmla"></a>Actualizar celdas (XMLA)
  Puede usar el [UpdateCells](../xmla/xml-elements-commands/updatecells-element-xmla.md) comando para cambiar el valor de una o más celdas en un cubo habilitado para reescritura del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacena la información actualizada en una tabla de reescritura independiente para cada partición que contiene celdas que se va a actualizar.  
  
> [!NOTE]  
>  El comando `UpdateCells` no admite las asignaciones durante la reescritura del cubo. Para usar la reescritura asignada, debe utilizar el [instrucción](../xmla/xml-elements-commands/statement-element-xmla.md) comando que se envía una instrucción UPDATE de expresiones multidimensionales (MDX). Para obtener más información, consulte [instrucción UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificar celdas  
 El [celda](../xmla/xml-elements-properties/cell-element-xmla.md) propiedad de la `UpdateCells` comando contiene las celdas que se va a actualizar. Para identificar cada una de las celdas en la propiedad `Cell`, utilice el número ordinal de esa celda. Conceptualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera las celdas de un cubo como si el cubo fuera una *p*-matriz unidimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila. En la ilustración siguiente se muestra la fórmula para calcular el número ordinal de una celda.  
  
 ![Fórmula para calcular la posición ordinal de celda](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "fórmula para calcular la posición ordinal de celda")  
  
 Una vez que sepa el número ordinal de una celda, puede indicar el valor esperado de la celda en la [valor](../xmla/xml-elements-properties/value-element-xmla.md) propiedad de la [celda](../xmla/xml-elements-properties/cell-element-xmla.md) propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/update-element-xmla.md)   
 [Desarrollo con XMLA en Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
