---
title: Propiedad ordinal (celda de ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c4a40c59ad222c943cefe089ffaddd53f2cec25a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708816"
---
# <a name="ordinal-property-ado-md-cell"></a>Propiedad ordinal (celda de ADO MD)
Identifica de forma única un [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md) por su posición dentro de un conjunto de celdas.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Valor ordinal de la celda identifica la celda dentro de un conjunto de celdas. Conceptualmente, las celdas se numeran en un conjunto de celdas como si fuera el conjunto de celdas una *p*-matriz dimensional, donde *p* es el número de [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). Las celdas se numeran a partir de cero en orden fila principal. Esta es la fórmula para calcular el número ordinal de una celda:  
  
 Valor ordinal de la celda puede utilizarse con el [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad de la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto para recuperar rápidamente el [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de Axis (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propiedad Item (ADO MD Cellset)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propiedad ordinal (posición de ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
