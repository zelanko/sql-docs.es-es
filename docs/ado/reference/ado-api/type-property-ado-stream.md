---
title: Type (propiedad) (Stream de ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords: Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c935ffe744d73e31483f030a6efd122773909755
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="type-property-ado-stream"></a>Propiedad Type (objeto Stream de ADO)
Indica el tipo de datos contenidos en el [flujo](../../../ado/reference/ado-api/stream-object-ado.md) (binario o texto).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) valor que especifica el tipo de datos contenidos en el **flujo** objeto. El valor predeterminado es **adTypeText**. Sin embargo, si inicialmente se escriben datos binarios en un nuevo, vacía **flujo**, **tipo** cambiará a **adTypeBinary**.  
  
## <a name="remarks"></a>Comentarios  
 El **tipo** propiedad es de lectura/escritura solo cuando la actual posición está al principio de la **flujo** ([posición](../../../ado/reference/ado-api/position-property-ado.md) es 0) y de solo lectura en cualquier otra posición.  
  
 El**tipo** propiedad determina qué métodos se deben usar para leer y escribir el **flujo**. Para el texto **secuencias**, use [ReadText](../../../ado/reference/ado-api/readtext-method.md) y [WriteText](../../../ado/reference/ado-api/writetext-method.md). Para el binario **secuencias**, use [lectura](../../../ado/reference/ado-api/read-method.md) y [escribir](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Tiporegistro (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Tipo (propiedad, ADO)](../../../ado/reference/ado-api/type-property-ado.md)
