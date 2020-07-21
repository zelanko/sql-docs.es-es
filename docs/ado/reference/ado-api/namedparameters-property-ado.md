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
author: rothja
ms.author: jroth
ms.openlocfilehash: 432a4968a301e51c1ca69e3b84ea80e0a19e32bb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762416"
---
# <a name="namedparameters-property-ado"></a>Propiedad NamedParameters (ADO)
Indica si los nombres de parámetro se deben pasar al proveedor.  
  
## <a name="remarks"></a>Observaciones  
 Cuando esta propiedad es true, ADO pasa el valor de la propiedad **Name** de cada parámetro de la colección de **parámetros** para el [objeto de comando](../../../ado/reference/ado-api/command-object-ado.md). El proveedor usa un nombre de parámetro para hacer coincidir los parámetros de las propiedades **CommandText** o **CommandStream** . Si esta propiedad es false (el valor predeterminado), los nombres de parámetro se omiten y el proveedor usa el orden de los parámetros para hacer coincidir los valores con los parámetros de las propiedades **CommandText** o **CommandStream** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [CommandText (propiedad, ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandStream (propiedad, ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
