---
title: Propiedad ordinal (celda de ADO MD) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6928eeeb7450b2edbd244d70d3c6a8aa999343a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="ordinal-property-ado-md-cell"></a>Propiedad ordinal (celda de ADO MD)
Identifica de forma única un [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md) por su posición dentro de un conjunto de celdas.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Valor ordinal de la celda identifica de forma única la celda dentro de un conjunto de celdas. Conceptualmente, las celdas se numeran en un conjunto de celdas como si el conjunto de celdas fuera una *p*-matriz unidimensional, donde *p* es el número de [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). Las celdas se numeran a partir de cero en orden de importancia de filas. Ésta es la fórmula para calcular el número ordinal de una celda:  
  
 Valor ordinal de la celda puede utilizarse con el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad de la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto que se va a recuperar rápidamente el [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de Axis (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propiedad Item (conjunto de celdas de ADO MD)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propiedad ordinal (posición de ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)

