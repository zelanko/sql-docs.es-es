---
title: Propiedad ordinal (celda ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b0563912d49ba6baff085fd83be88693e8f8ba1f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765076"
---
# <a name="ordinal-property-ado-md-cell"></a>Propiedad ordinal (celda de ADO MD)
Identifica de forma única una [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md) por su posición dentro de un Cellset.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un entero **largo** y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 El valor ordinal de la celda identifica de forma única la celda dentro de un Cellset. Conceptualmente, las celdas se numeran en un conjunto de celdas como si el conjunto de celdas fuera una matriz de dimensión *p*, donde *p* es el número de [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). Las celdas se numeran a partir de cero en orden principal de fila. Esta es la fórmula para calcular el número ordinal de una celda:  
  
 El valor ordinal de la celda se puede usar con la propiedad [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) del objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) para recuperar rápidamente la [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de eje (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propiedad Item (ADO MD Cellset)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propiedad ordinal (posición de ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
