---
title: Propiedad NamedParameters (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Command::NamedParameters
helpviewer_keywords: NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da97908abd0b7ba06231c4cd20567e80cfdfed20
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="namedparameters-property-ado"></a>Propiedad NamedParameters (ADO)
Indica si los nombres de parámetro se deberían pasar al proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Cuando esta propiedad es true, ADO pasa el valor de la **nombre** propiedad de cada parámetro en el **parámetro** colección para el [objeto de comando](../../../ado/reference/ado-api/command-object-ado.md). El proveedor usa un nombre de parámetro para que coincida con los parámetros en la **CommandText** o **CommandStream** propiedades. Si esta propiedad es false (valor predeterminado), se omiten los nombres de parámetro y el proveedor usa el orden de parámetros para que coincida con los valores a los parámetros en la **CommandText** o **CommandStream** propiedades.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propiedad CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
