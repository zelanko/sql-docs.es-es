---
title: Actualizar celdas (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6237bb773709aa7f5eb8bc29fa2436bf69b08030
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146040"
---
# <a name="updating-cells-xmla"></a>Actualizar celdas (XMLA)
  Puede usar el [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comando para cambiar el valor de una o varias celdas en un cubo habilitado para la reescritura del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacena la información actualizada en una tabla de reescritura independiente para cada partición que contiene celdas que se va a actualizarse.  
  
> [!NOTE]  
>  El comando `UpdateCells` no admite las asignaciones durante la reescritura del cubo. Para usar la reescritura asignada, debe usar el [instrucción](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando para enviar una instrucción UPDATE de expresiones multidimensionales (MDX). Para obtener más información, consulte [instrucción UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificar celdas  
 El [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propiedad de la `UpdateCells` comando contiene las celdas que se va a actualizarse. Para identificar cada una de las celdas en la propiedad `Cell`, utilice el número ordinal de esa celda. Conceptualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera las celdas de un cubo como si el cubo fuera una *p*-matriz dimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila. En la ilustración siguiente se muestra la fórmula para calcular el número ordinal de una celda.  
  
 ![Fórmula para calcular la posición ordinal de celda](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "fórmula para calcular la posición ordinal de celda")  
  
 Una vez que sepa el número ordinal de una celda, puede indicar el valor esperado de la celda en la [valor](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) propiedad de la [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desarrollo con XMLA en Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
