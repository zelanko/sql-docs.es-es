---
title: Posición (propiedad, ADO) | Documentos de Microsoft
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
- _Stream::Position
helpviewer_keywords:
- Position property [ADO]
ms.assetid: daa8319a-49aa-4c1c-9af6-0b01e9ab2f9d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 407ef25ebc55685436f61acaa42cbdf964619b09
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280694"
---
# <a name="position-property-ado"></a>Propiedad Position (ADO)
Indica la posición actual dentro de un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que especifica el desplazamiento, en número de bytes, de la posición actual desde el principio de la secuencia. El valor predeterminado es 0, que representa el primer byte de la secuencia.  
  
## <a name="remarks"></a>Notas  
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
