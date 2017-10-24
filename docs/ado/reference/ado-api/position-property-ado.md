---
title: "Posición (propiedad, ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76a3d94b97fa32e372cd6cc67367450d2f62530b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="position-property-ado"></a>Propiedad Position (ADO)
Indica la posición actual dentro de un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que especifica el desplazamiento, en número de bytes, de la posición actual desde el principio de la secuencia. El valor predeterminado es 0, que representa el primer byte de la secuencia.  
  
## <a name="remarks"></a>Comentarios  
 La posición actual puede aplicarse a un punto después del final de la secuencia. Si especifica la posición actual más allá del final de la secuencia, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **flujo** objeto aumentará en consecuencia. Cualquier byte nuevo agregado de esta forma será null.  
  
> [!NOTE]
>  **Posición** siempre mide los bytes. Para las secuencias de texto con juegos de caracteres multibyte, multiplique la posición por el tamaño de carácter para determinar el número de caracteres. Por ejemplo, para un juego de caracteres de dos bytes, el primer carácter está en la posición 0, el segundo carácter en la posición 2, el tercer carácter en la posición 4 y así sucesivamente.  
  
> [!NOTE]
>  Los valores negativos no se puede usar para cambiar la posición actual en un **flujo**. Solo los números positivos pueden usarse para **posición**.  
  
> [!NOTE]
>  Para sólo lectura **flujo** objetos, ADO no devolverá un error si **posición** está establecido en un valor mayor que el **tamaño** de la **flujo**. Esto no cambia el tamaño de la **flujo**, o modificar el **flujo** contenido de ninguna manera. Sin embargo, esto debería evitarse porque resulta en un sentido **posición**valor.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad de conjunto de caracteres (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)

