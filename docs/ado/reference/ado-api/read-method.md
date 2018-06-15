---
title: Método Read | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 371574fdaa0f6f9f82a40f8caf5f622633f4fa19
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280814"
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
  
## <a name="remarks"></a>Notas  
 Si *NumBytes* es mayor que el número de bytes restante en el **flujo**, se devuelven solo los bytes restantes. Los datos leídos no se rellenan para que coincida con la longitud especificada por *NumBytes*. Si no hay ningún quedas bytes para leer, se devuelve una variante con un valor null. **Lectura** no se puede usar para leer hacia atrás.  
  
> [!NOTE]
>  *NumBytes* siempre mide los bytes. Para el texto **flujo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**), utilice [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)
