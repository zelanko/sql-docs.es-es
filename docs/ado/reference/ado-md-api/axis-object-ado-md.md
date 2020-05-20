---
title: Objeto de eje (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axis
helpviewer_keywords:
- Axis object [ADO MD]
ms.assetid: 5f498c9a-b1e7-4e6e-9ae6-71eadaf9aada
author: rothja
ms.author: jroth
ms.openlocfilehash: c251355637c5d57729a7d4aa737f2face1c9ace2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765186"
---
# <a name="axis-object-ado-md"></a>Objeto Axis (ADO MD)
Representa un eje posicional o de filtro de un objeto Cellset, que contiene los miembros seleccionados de una o más dimensiones.  
  
## <a name="remarks"></a>Comentarios  
 Un objeto de **eje** puede estar incluido en una colección de [ejes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) o ser devuelto por la propiedad [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) de un conjunto de [celdas](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
 Con las colecciones y las propiedades de un objeto de **eje** , puede hacer lo siguiente:  
  
-   Identifique el **eje** con la propiedad [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) .  
  
-   Recorrer en iteración cada posición a lo largo de un **eje** mediante la colección [positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) .  
  
-   Obtenga el número de dimensiones del **eje** con la propiedad [DimensionCount](../../../ado/reference/ado-md-api/dimensioncount-property-ado-md.md) .  
  
-   Obtener los atributos específicos del proveedor del **eje** con la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/axis-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de eje (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Colección axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Colección positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
