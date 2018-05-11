---
title: Actualizar celdas (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9458e2fb58a3e1fe7806db1bb27147561ef94e5d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="updating-cells-xmla"></a>Actualizar celdas (XMLA)
  Puede usar el [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) comando para cambiar el valor de una o más celdas en un cubo habilitado para reescritura del cubo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacena la información actualizada en una tabla de reescritura independiente para cada partición que contiene celdas que se va a actualizar.  
  
> [!NOTE]  
>  El **UpdateCells** comando no es compatible con las asignaciones durante la reescritura del cubo. Para usar la reescritura asignada, debe utilizar el [instrucción](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando que se envía una instrucción UPDATE de expresiones multidimensionales (MDX). Para obtener más información, consulte [instrucción UPDATE CUBE &#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>Especificar celdas  
 El [celda](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) propiedad de la **UpdateCells** comando contiene las celdas que se va a actualizar. Identificar cada celda de la **celda** propiedad mediante el número ordinal de la celda. Conceptualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] numera las celdas de un cubo como si el cubo fuera una *p*-matriz unidimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila. En la ilustración siguiente se muestra la fórmula para calcular el número ordinal de una celda.  
  
 ![Fórmula para calcular la posición ordinal de celda](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "fórmula para calcular la posición ordinal de celda")  
  
 Una vez que sepa el número ordinal de una celda, puede indicar el valor esperado de la celda en la [valor](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md) propiedad de la [celda](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
