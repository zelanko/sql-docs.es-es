---
title: CopyTo (método, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b2e7dc8b70c109fc6cf998cec2bbad1147692c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308908"
---
# <a name="copyto-method-ado"></a>CopyTo (método) (ADO)
Copia el número especificado de caracteres o bytes (en función de [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) en el [Stream](../../../ado/reference/ado-api/stream-object-ado.md) a otro **Stream** objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DestStream*  
 Un valor de variable de objeto que contiene una referencia a un circuito abierto **Stream** objeto. Actual **Stream** se copian en el destino **Stream** especificado por *DestStream*. El destino **Stream** ya debe estar abierto. Si no, se produce un error en tiempo de ejecución.  
  
> [!NOTE]
>  El *DestStream* parámetro no puede ser un proxy de **Stream** objeto porque esto requiere acceso a una interfaz privada en el **Stream** objeto que no se puede enviar de forma remota a la cliente.  
  
 *NumChars*  
 Opcional. Un **entero** valor que especifica el número de bytes o caracteres que se copian desde la posición actual en el origen de **Stream** al destino **Stream**. El valor predeterminado es -1, que especifica que todos los caracteres o bytes que se copian desde la posición actual para [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Comentarios  
 Este método copia el número especificado de caracteres o bytes, desde la posición actual especificada por el [posición](../../../ado/reference/ado-api/position-property-ado.md) propiedad. Si el número especificado es mayor que el número de bytes hasta disponibles **EOS**, entonces solo caracteres o bytes desde la posición actual para **EOS** se copian. Si el valor de *NumChars* es -1, o se omite, se copian todos los caracteres o bytes a partir de la posición actual.  
  
 Si existen caracteres o bytes en la secuencia de destino, permanece todo el contenido más allá del punto donde finaliza la copia y no se trunca. **Posición** se convierte en el byte inmediatamente después del último byte copiado. Si desea truncar estos bytes, llame a [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** debe usarse para copiar datos a un destino **Stream** del mismo tipo como el origen **Stream** (sus **tipo** valores de propiedad son ambos **adTypeText** o ambos **adTypeBinary**). Para el texto **Stream** objetos, puede cambiar el [Charset](../../../ado/reference/ado-api/charset-property-ado.md) configuración de la propiedad del destino **Stream** para traducir de un juego de caracteres a otro. Además, el texto **Stream** objetos se pueden copiar correctamente en binario **Stream** objetos pero binario **Stream** no se copiarán los objetos en texto **Stream**  objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
