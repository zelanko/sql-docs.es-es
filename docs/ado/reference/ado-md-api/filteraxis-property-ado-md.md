---
title: Propiedad FilterAxis (ADO MD) | Documentos de Microsoft
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
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 81424fbe54417a16df85f31dfec1f7322da9974e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
