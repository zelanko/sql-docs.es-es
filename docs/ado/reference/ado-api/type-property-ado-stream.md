---
title: Propiedad Type (secuencia de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: rothja
ms.author: jroth
ms.openlocfilehash: de61f4877dc6adcdfaa9644f5f266cd827a1d096
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765346"
---
# <a name="type-property-ado-stream"></a>Propiedad Type (objeto Stream de ADO)
Indica el tipo de datos contenidos en la [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) (binario o de texto).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) que especifica el tipo de datos contenidos en el objeto de **secuencia** . El valor predeterminado es **adTypeText**. Sin embargo, si los datos binarios se escriben inicialmente en una **secuencia**nueva y vacía, el **tipo** se cambiará a **adTypeBinary**.  
  
## <a name="remarks"></a>Comentarios  
 La propiedad **Type** es de lectura y escritura solo cuando la posición actual está al principio de la **secuencia** ([Position](../../../ado/reference/ado-api/position-property-ado.md) es 0) y de solo lectura en cualquier otra posición.  
  
 La propiedad**Type** determina qué métodos deben usarse para leer y escribir la **secuencia**. En el caso de las **secuencias**de texto, use [READTEXT](../../../ado/reference/ado-api/readtext-method.md) y [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md). En el caso de las **secuencias**binarias, use [lectura](../../../ado/reference/ado-api/read-method.md) y [escritura](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [RecordType (propiedad, ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Tipo (propiedad, ADO)](../../../ado/reference/ado-api/type-property-ado.md)
