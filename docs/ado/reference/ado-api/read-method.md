---
title: Read (método) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 992631b8fb3864b6d7404f86d2f65de222f0b1c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917415"
---
# <a name="read-method"></a>Método Read
Lee un número especificado de bytes de un objeto de [flujo](../../../ado/reference/ado-api/stream-object-ado.md) binario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *NumBytes*  
 Opcional. Valor de **tipo Long** que especifica el número de bytes que se van a leer del archivo o el valor de [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) **adReadAll**, que es el valor predeterminado.  
  
## <a name="return-value"></a>Valor devuelto  
 El método **Read** Lee un número especificado de bytes o el flujo completo de un objeto de **secuencia** y devuelve los datos resultantes como una **variante**.  
  
## <a name="remarks"></a>Observaciones  
 Si *numbytes* es mayor que el número de bytes que quedan en la **secuencia**, solo se devuelven los bytes restantes. Los datos leídos no se rellenan para coincidir con la longitud especificada por *numbytes*. Si no quedan bytes para leer, se devuelve una variante con un valor null. **Read** no se puede usar para leer hacia atrás.  
  
> [!NOTE]
>  *Numbytes* siempre mide bytes. En el caso de los objetos de **flujo** de texto (el[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **AdTypeText**), use [READTEXT](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)
