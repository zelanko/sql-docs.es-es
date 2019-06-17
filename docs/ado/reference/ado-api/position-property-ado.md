---
title: Position (propiedad, ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 7b777179ad83250d9707f7717b5833bbbff4fec7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703404"
---
# <a name="position-property-ado"></a>Propiedad Position (ADO)
Indica la posición actual dentro de un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que especifica el desplazamiento, en número de bytes, de la posición actual desde el principio de la secuencia. El valor predeterminado es 0, que representa el primer byte de la secuencia.  
  
## <a name="remarks"></a>Comentarios  
 La posición actual se puede mover a un punto después del final de la secuencia. Si especifica la posición actual más allá del final de la secuencia, el [tamaño](../../../ado/reference/ado-api/size-property-ado-stream.md) de la **Stream** objeto aumentará en consecuencia. Cualquier nueva bytes agregados de esta forma será nulos.  
  
> [!NOTE]
>  **Posición** siempre mide los bytes. Para las secuencias de texto con juegos de caracteres multibyte, multiplique la posición por el tamaño de caracteres para determinar el número de caracteres. Por ejemplo, para un juego de caracteres de doble byte, es el primer carácter en la posición 0, el segundo carácter en la posición 2, el tercer carácter en la posición 4 y así sucesivamente.  
  
> [!NOTE]
>  Los valores negativos no se puede usar para cambiar la posición actual en un **Stream**. Se pueden usar solo números positivos para **posición**.  
  
> [!NOTE]
>  De solo lectura **Stream** los objetos ADO no devolverá un error si **posición** se establece en un valor mayor que el **tamaño** del **Stream**. Esto no cambia el tamaño de la **Stream**, o modificar el **Stream** contenido de ninguna forma. Sin embargo, esto debe evitarse porque resulta en un sentido **posición**valor.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad de conjunto de caracteres (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)
