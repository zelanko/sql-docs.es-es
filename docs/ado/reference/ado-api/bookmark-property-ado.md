---
title: Bookmark (propiedad) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61fa4619bd70b170f13dbc879748364f019f8bdd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716303"
---
# <a name="bookmark-property-ado"></a>Bookmark (propiedad) (ADO)
Indica un marcador que identifica de forma única el registro actual en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto o establece el registro actual un **Recordset** objeto en el registro identificado por un marcador válido.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** expresión que se evalúa como un marcador válido.  
  
## <a name="remarks"></a>Comentarios  
 Use la **marcador** propiedad para guardar la posición del registro actual y volver a ese registro en cualquier momento. Los marcadores solo están disponibles en **Recordset** objetos que admiten la funcionalidad de los marcadores.  
  
 Al abrir un **Recordset** de objetos, cada uno de sus registros tiene un marcador único. Para guardar el marcador para el registro actual, asigne el valor de la **marcador** propiedad a una variable. Para volver rápidamente a ese registro en cualquier momento después de mover a un registro diferente, establezca la **Recordset** del objeto **marcador** en el valor de esa variable.  
  
 El usuario puede no ser capaz de ver el valor del marcador. Además, los usuarios no deben esperar marcadores estén comparables directamente, porque los dos marcadores que hacen referencia al mismo registro pueden tener valores diferentes.  
  
 Si usas el [clon](../../../ado/reference/ado-api/clone-method-ado.md) método para crear una copia de un **Recordset** objeto, el **marcador** valores de propiedad para el original y el duplicado **conjunto de registros**  objetos son idénticos y se pueden usar indistintamente. Sin embargo, no se puede usar marcadores de diferentes **Recordset** objetos de forma intercambiable, incluso si se crearon desde el mismo origen o el comando.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **Recordset** objeto, el **marcador** propiedad siempre está disponible.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [BOF, EOF y Bookmark propiedades ejemplo (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF y Bookmark ejemplo de propiedades (VC ++)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
