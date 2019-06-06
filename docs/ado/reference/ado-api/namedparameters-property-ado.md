---
title: Propiedad NamedParameters (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ce517f4ba3f2fc4a80932024a8fe51ac285cdb7d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707296"
---
# <a name="namedparameters-property-ado"></a>Propiedad NamedParameters (ADO)
Indica si los nombres de parámetro se deben pasar al proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Cuando esta propiedad es true, ADO pasa el valor de la **nombre** propiedad de cada parámetro en el **parámetro** recopilación para el [objeto Command](../../../ado/reference/ado-api/command-object-ado.md). El proveedor usa un nombre de parámetro para que coincida con los parámetros en el **CommandText** o **CommandStream** propiedades. Si esta propiedad es false (valor predeterminado), se omiten los nombres de parámetro y el proveedor utiliza el orden de parámetros para que coincida con los valores de parámetros en el **CommandText** o **CommandStream** propiedades.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propiedad CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
