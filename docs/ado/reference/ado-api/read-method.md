---
title: Método Read | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: reference
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
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 910d566d60afa2e255e05647e429af505bd5b4fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="read-method"></a>Método Read
Lee un número especificado de bytes de un archivo binario [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumBytes*  
 Opcional. A **largo** valor que especifica el número de bytes que se va a leer el archivo o la [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valor **adReadAll**, que es el valor predeterminado.  
  
## <a name="return-value"></a>Valor devuelto  
 El **lectura** método lee un número especificado de bytes o toda la secuencia de un **flujo** objeto y devuelve los datos resultantes como un **Variant**.  
  
## <a name="remarks"></a>Comentarios  
 Si *NumBytes* es mayor que el número de bytes restante en el **flujo**, se devuelven solo los bytes restantes. Los datos leídos no se rellenan para que coincida con la longitud especificada por *NumBytes*. Si no hay ningún quedas bytes para leer, se devuelve una variante con un valor null. **Lectura** no se puede usar para leer hacia atrás.  
  
> [!NOTE]
>  *NumBytes* siempre mide los bytes. Para el texto **flujo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**), utilice [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)
