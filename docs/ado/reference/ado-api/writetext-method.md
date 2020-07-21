---
title: Método WriteText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ee7f4b99b40b6aec3e384f9f5739f8f5d2280f4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764416"
---
# <a name="writetext-method"></a>Método WriteText
Escribe una cadena de texto especificada en un objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Data*  
 Valor de **cadena** que contiene el texto en caracteres que se va a escribir.  
  
 *Opciones*  
 Opcional. Valor [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) que especifica si se debe escribir un carácter separador de línea al final de la cadena especificada.  
  
## <a name="remarks"></a>Comentarios  
 Las cadenas especificadas se escriben en el objeto de **secuencia** sin espacios ni caracteres intermedios entre cada cadena.  
  
 La [posición](../../../ado/reference/ado-api/position-property-ado.md) actual se establece en el carácter que sigue a los datos escritos. El método **WRITETEXT** no trunca el resto de los datos de una secuencia. Si desea truncar estos caracteres, llame a [seteos](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la posición actual de [EOS](../../../ado/reference/ado-api/eos-property.md) , se aumentará el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **secuencia** para que contenga cualquier carácter nuevo y **EOS** se moverá al nuevo último byte de la **secuencia**.  
  
> [!NOTE]
>  El método **WRITETEXT** se usa con secuencias de texto (el[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). En el caso de secuencias binarias (el**tipo** es **adTypeBinary**), utilice [Write](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Write (método)](../../../ado/reference/ado-api/write-method.md)
