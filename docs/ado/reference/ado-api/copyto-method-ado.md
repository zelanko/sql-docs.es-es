---
title: CopyTo (método) (ADO) | Microsoft Docs
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
ms.openlocfilehash: 25d57116e1fa24658d62a0c9083e00a3e320d2a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933370"
---
# <a name="copyto-method-ado"></a>CopyTo (método) (ADO)
Copia el número especificado de caracteres o bytes (dependiendo del [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) de la [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) en otro objeto de **flujo** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DestStream*  
 Valor de variable de objeto que contiene una referencia a un objeto de **secuencia** abierto. La **secuencia** actual se copia en la **secuencia** de destino especificada por *DestStream*. El **flujo** de destino ya debe estar abierto. Si no es así, se produce un error en tiempo de ejecución.  
  
> [!NOTE]
>  Es posible que el parámetro *DestStream* no sea un proxy de objeto de **flujo** porque requiere acceso a una interfaz privada en el objeto de **secuencia** que no se puede enviar de forma remota al cliente.  
  
 *NumChars*  
 Opcional. Valor **entero** que especifica el número de bytes o caracteres que se van a copiar desde la posición actual en la **secuencia** de origen al **flujo**de destino. El valor predeterminado es-1, que especifica que se copian todos los caracteres o bytes de la posición actual a [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Observaciones  
 Este método copia el número especificado de caracteres o bytes, empezando por la posición actual especificada por la propiedad [Position](../../../ado/reference/ado-api/position-property-ado.md) . Si el número especificado es mayor que el número de bytes disponible hasta **EOS**, solo se copian los caracteres o bytes de la posición actual a **EOS** . Si el valor de *NumChars* es-1, o se omite, se copian todos los caracteres o bytes a partir de la posición actual.  
  
 Si hay caracteres o bytes existentes en el flujo de destino, todo el contenido más allá del punto en el que finaliza la copia permanece y no se trunca. La **posición** se convierte en el byte inmediatamente posterior al último byte copiado. Si desea truncar estos bytes, llame a [seteos](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** se debe usar para copiar datos en un **flujo** de destino del mismo tipo que la **secuencia** de origen (la configuración de la propiedad de **tipo** es **adTypeText** o bien **adTypeBinary**). En el caso de los objetos de **flujo** de texto, puede cambiar la configuración de la propiedad [CharSet](../../../ado/reference/ado-api/charset-property-ado.md) del **flujo** de destino para convertir de un juego de caracteres a otro. Además, los objetos de **flujo** de texto se pueden copiar correctamente en objetos de **flujo** binario, pero los objetos de **flujo** binario no se pueden copiar en objetos de **flujo** de texto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
