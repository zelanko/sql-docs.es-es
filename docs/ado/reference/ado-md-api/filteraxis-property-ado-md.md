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
manager: craigg
ms.openlocfilehash: 5015888cfafcce56c97f2369d418ed7be842dd28
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295370"
---
# <a name="filteraxis-property-ado-md"></a>Propiedad FilterAxis (ADO MD)
Indica la información del filtro actual [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) de objetos y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Use la **FilterAxis** propiedad para devolver información acerca de las dimensiones que se usaron para segmentar los datos. El [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) propiedad de la **eje** devuelve el número de dimensiones de la segmentación de datos. Este eje normalmente tiene una sola fila.  
  
 El **eje** devuelto por **FilterAxis** no está contenida en el [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) colección para un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount (propiedad, ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
