---
title: Tipo de propiedad (Stream de ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e4df670c5fe6ca42015e7e85445dafde47738f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042634"
---
# <a name="type-property-ado-stream"></a>Propiedad Type (objeto Stream de ADO)
Indica el tipo de datos contenidos en el [Stream](../../../ado/reference/ado-api/stream-object-ado.md) (binario o texto).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) valor que especifica el tipo de datos contenidos en el **Stream** objeto. El valor predeterminado es **adTypeText**. Sin embargo, si se escriben datos binarios a una nueva, vacía **Stream**, **tipo** cambiará a **adTypeBinary**.  
  
## <a name="remarks"></a>Comentarios  
 El **tipo** propiedad es de lectura/escritura solo cuando la posición actual está al principio de la **Stream** ([posición](../../../ado/reference/ado-api/position-property-ado.md) es 0) y de solo lectura en cualquier otra posición.  
  
 El**tipo** propiedad determina qué métodos se deben usar para leer y escribir el **Stream**. Para el texto **secuencias**, utilice [ReadText](../../../ado/reference/ado-api/readtext-method.md) y [WriteText](../../../ado/reference/ado-api/writetext-method.md). Binario **secuencias**, utilice [lectura](../../../ado/reference/ado-api/read-method.md) y [escribir](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Tipo (propiedad, ADO)](../../../ado/reference/ado-api/type-property-ado.md)
