---
title: Propiedad ordinal (posición de ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Position::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: 6efe8b5d-a2d5-43a9-a5ea-f9244f8d4ec9
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dac93d9c0c9fa57139b15fde2ce1c691883e68a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ordinal-property-ado-md-position"></a>Propiedad ordinal (posición de ADO MD)
Identifica de forma única un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) a lo largo de un eje.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 El **Ordinal** propiedad de un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto corresponde al índice de la **posición** dentro de la [posiciones](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) colección.  
  
 Una celda se puede recuperar rápidamente mediante el **Ordinal** de la **posición** a lo largo de cada eje con la [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propiedad de la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Propiedad Item (conjunto de celdas de ADO MD)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Propiedad ordinal (celda de ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)
