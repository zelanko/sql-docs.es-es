---
title: Escribir el método | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52561b6d240a58e59490d607c8729b5d878b96a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642429"
---
# <a name="write-method"></a>Método Write
Escribe datos binarios en un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parámetros  
 *búfer*  
 Un **Variant** que contiene una matriz de bytes que se escribirán.  
  
## <a name="remarks"></a>Comentarios  
 Se escriben los bytes especificados en el **Stream** objeto sin espacios intermedios entre cada byte.  
  
 Actual [posición](../../../ado/reference/ado-api/position-property-ado.md) está establecido en el byte que sigue a los datos escritos. El **escribir** método no trunca el resto de los datos en una secuencia. Si desea truncar estos bytes, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la actual [EOS](../../../ado/reference/ado-api/eos-property.md) posición, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **Stream** se incrementará para contener los bytes nuevos, y **EOS** moverá hasta el último byte nuevo en el **Stream**.  
  
> [!NOTE]
>  El **escribir** método se utiliza con secuencias binarias ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**). Para las secuencias de texto (**tipo** es **adTypeText**), utilice [WriteText](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
