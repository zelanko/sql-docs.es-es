---
title: Actualizar celdas (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: f0eab50aa7e70aedee93eef2cefee648e6ceb5c9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81387895"
---
# <a name="updating-cells-xmla"></a>Actualizar celdas (XMLA)
  Puede usar el comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) para cambiar el valor de una o más celdas de un cubo habilitado para la reescritura del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena la información actualizada en una tabla de reescritura independiente para cada partición que contiene celdas que se van a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] actualizar.  
  
> [!NOTE]  
>  El comando `UpdateCells` no admite las asignaciones durante la reescritura del cubo. Para usar la reescritura asignada, debe utilizar el comando [Statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) para enviar una instrucción UPDATE de expresiones multidimensionales (MDX). Para obtener más información, vea [instrucción UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
## <a name="specifying-cells"></a>Especificar celdas  
 La propiedad de [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) del `UpdateCells` comando contiene las celdas que se van a actualizar. Para identificar cada una de las celdas en la propiedad `Cell`, utilice el número ordinal de esa celda. Conceptualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera las celdas de un cubo como si el cubo fuera *una matriz unidimensional,* donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila. En la ilustración siguiente se muestra la fórmula para calcular el número ordinal de una celda.  
  
 ![Fórmula para calcular la posición ordinal de la celda](../../analysis-services/dev-guide/media/cellordinalformula.gif "Fórmula para calcular la posición ordinal de la celda")  
  
 Una vez que conozca el número ordinal de una celda, puede indicar el valor previsto de la celda en la propiedad [Value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) de la propiedad [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) .  
  
## <a name="see-also"></a>Consulte también  
 [Elemento Update &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desarrollar con XMLA en Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
