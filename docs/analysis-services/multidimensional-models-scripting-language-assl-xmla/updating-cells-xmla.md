---
title: Actualizar celdas (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0cfee2adf9d730b458fd482317d16d963f15ebc1
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146781"
---
# <a name="updating-cells-xmla"></a>Actualizar celdas (XMLA)
  Puede usar el [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comando para cambiar el valor de una o varias celdas en un cubo habilitado para la reescritura del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacena la información actualizada en una tabla de reescritura independiente para cada partición que contiene celdas que se va a actualizarse.  
  
> [!NOTE]  
>  El **UpdateCells** comando no es compatible con las asignaciones durante la reescritura del cubo. Para usar la reescritura asignada, debe usar el [instrucción](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando para enviar una instrucción UPDATE de expresiones multidimensionales (MDX). Para obtener más información, consulte [instrucción UPDATE CUBE &#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Especificar celdas  
 El [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propiedad de la **UpdateCells** comando contiene las celdas que se va a actualizarse. Identificar cada celda de la **celda** propiedad mediante el número ordinal de la celda. Conceptualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera las celdas de un cubo como si el cubo fuera una *p*-matriz dimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila. En la ilustración siguiente se muestra la fórmula para calcular el número ordinal de una celda.  
  
 ![Fórmula para calcular la posición ordinal de celda](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "fórmula para calcular la posición ordinal de celda")  
  
 Una vez que sepa el número ordinal de una celda, puede indicar el valor esperado de la celda en la [valor](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla) propiedad de la [celda](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
