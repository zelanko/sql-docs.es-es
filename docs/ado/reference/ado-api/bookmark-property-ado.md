---
title: Bookmark (propiedad) (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4bf6ae9d0ca300aa6db2665a52a27aace52b6bcc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="bookmark-property-ado"></a>Bookmark (propiedad) (ADO)
Indica un marcador que identifica de forma única el registro actual en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de un objeto o establece el registro actual un **Recordset** objeto en el registro identificado por un marcador válido.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** expresión que se evalúe como un marcador válido.  
  
## <a name="remarks"></a>Comentarios  
 Use la **marcador** propiedad para guardar la posición del registro actual y volver a ese registro en cualquier momento. Marcadores solo están disponibles en **Recordset** objetos que admiten la funcionalidad de los marcadores.  
  
 Cuando se abre un **Recordset** de objetos, cada uno de sus registros tiene un marcador único. Para guardar el marcador para el registro actual, asigne el valor de la **marcador** propiedad a una variable. Para volver rápidamente a ese registro en cualquier momento después de moverse a un registro diferente, establezca la **Recordset** del objeto **marcador** en el valor de esa variable.  
  
 Es posible que el usuario no pueda ver el valor del marcador. Además, los usuarios no deben esperar que marcadores sean comparables directamente porque dos marcadores que hacen referencia al mismo registro pueden tener valores diferentes.  
  
 Si usas el [clon](../../../ado/reference/ado-api/clone-method-ado.md) método para crear una copia de un **Recordset** objeto, el **marcador** valores de propiedad para la versión original y el duplicado **conjunto de registros**  objetos son idénticos y se pueden usar indistintamente. Sin embargo, no puede utilizar marcadores de diferentes **Recordset** objetos de forma intercambiable, incluso si se crearon a partir del mismo origen o comando.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **Recordset** objeto, el **marcador** propiedad siempre está disponible.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [BOF, EOF y ejemplo de propiedades de marcador (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF y ejemplo de propiedades de marcador (VC ++)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
