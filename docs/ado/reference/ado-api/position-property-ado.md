---
title: Propiedad Position (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dba8636f07b88f1c05d465b844376c6ef3e61240
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931656"
---
# <a name="position-property-ado"></a>Propiedad Position (ADO)
Indica la posición actual dentro de un objeto de [flujo](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **tipo Long** que especifica el desplazamiento, en número de bytes, de la posición actual desde el principio de la secuencia. El valor predeterminado es 0, que representa el primer byte de la secuencia.  
  
## <a name="remarks"></a>Observaciones  
 La posición actual se puede mover a un punto después del final de la secuencia. Si especifica la posición actual más allá del final de la secuencia, se aumentará el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) del objeto de **flujo** en consecuencia. Los nuevos bytes que se agreguen de esta manera serán null.  
  
> [!NOTE]
>  **Position** siempre mide bytes. En el caso de las secuencias de texto que usan juegos de caracteres multibyte, multiplique la posición por el tamaño de carácter para determinar el número de carácter. Por ejemplo, para un juego de caracteres de dos bytes, el primer carácter está en la posición 0, el segundo carácter en la posición 2, el tercer carácter en la posición 4, etc.  
  
> [!NOTE]
>  No se pueden usar valores negativos para cambiar la posición actual en una **secuencia**. Solo se pueden usar números positivos para la **posición**.  
  
> [!NOTE]
>  En el caso de los objetos de **secuencia** de solo lectura, ADO no devolverá un error si la **posición** está establecida en un valor mayor que el **tamaño** de la **secuencia**. Esto no cambia el tamaño de la **secuencia**ni modifica el contenido de la **secuencia** de ninguna manera. Sin embargo, esto se debe evitar porque da como resultado un valor de **posición**sin sentido.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad de conjunto de caracteres (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
