---
title: Write (método) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 911a9dfb21c054dc95c54d9fb429d628d8e01fa4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764436"
---
# <a name="write-method"></a>Método Write
Escribe datos binarios en un objeto de [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Búfer*  
 **Variante** que contiene una matriz de bytes que se va a escribir.  
  
## <a name="remarks"></a>Comentarios  
 Los bytes especificados se escriben en el objeto de **secuencia** sin ningún espacio intermedio entre cada byte.  
  
 La [posición](../../../ado/reference/ado-api/position-property-ado.md) actual se establece en el byte que sigue a los datos escritos. El método **Write** no trunca el resto de los datos de una secuencia. Si desea truncar estos bytes, llame a [seteos](../../../ado/reference/ado-api/seteos-method.md).  
  
 Si escribe más allá de la posición actual de [EOS](../../../ado/reference/ado-api/eos-property.md) , se aumentará el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **secuencia** para que contenga cualquier byte nuevo y **EOS** se moverá al nuevo último byte de la **secuencia**.  
  
> [!NOTE]
>  El método **Write** se usa con secuencias binarias ([Type](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeBinary**). En el caso de secuencias de texto (el**tipo** es **adTypeText**), use [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Método WriteText](../../../ado/reference/ado-api/writetext-method.md)
