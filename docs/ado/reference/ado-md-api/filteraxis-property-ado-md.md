---
title: Propiedad FilterAxis (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d44ac908c04338f80c18699319f75a068370c3e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938459"
---
# <a name="filteraxis-property-ado-md"></a>Propiedad FilterAxis (ADO MD)
Indica la información de filtro sobre el [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)actual.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un objeto de [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Use la propiedad **FilterAxis** para devolver información sobre las dimensiones que se usaron para segmentar los datos. La propiedad [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) del **eje** devuelve el número de dimensiones de segmentación. Este eje normalmente tiene solo una fila.  
  
 El **eje** devuelto por **FilterAxis** no está incluido en la colección [Axes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) de un objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto AXIS (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount (propiedad, ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
