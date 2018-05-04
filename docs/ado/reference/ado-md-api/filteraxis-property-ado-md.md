---
title: Propiedad FilterAxis (ADO MD) | Documentos de Microsoft
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
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 671a56b9117ea77b479d1a0fff78729ca9c3f5ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="filteraxis-property-ado-md"></a>Propiedad FilterAxis (ADO MD)
Indica información de filtro sobre actual [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md) de objetos y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Use la **PivotView** propiedad para devolver información acerca de las dimensiones que se utilizaron para segmentar los datos. El [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) propiedad de la **eje** devuelve el número de dimensiones de segmentación de datos. Este eje normalmente tiene una sola fila.  
  
 El **eje** devuelto por **PivotView** no se encuentra en la [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) colección para un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [DimensionCount (propiedad, ADO MD)](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md)
