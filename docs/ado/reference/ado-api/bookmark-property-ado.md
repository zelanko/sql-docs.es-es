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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b1c27eb728c3cd368b4d2acc10609785c06514a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748617"
---
# <a name="bookmark-property-ado"></a>Bookmark (propiedad) (ADO)
Indica un marcador que identifica de forma única el registro actual en un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) o establece el registro actual de un objeto de **conjunto de registros** en el registro identificado por un marcador válido.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve una expresión **Variant** que se evalúa como un marcador válido.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la propiedad **Bookmark** para guardar la posición del registro actual y volver a ese registro en cualquier momento. Los marcadores solo están disponibles en los objetos de **conjunto de registros** que admiten la funcionalidad de marcador.  
  
 Al abrir un objeto de **conjunto de registros** , cada uno de sus registros tiene un marcador único. Para guardar el marcador del registro actual, asigne el valor de la propiedad **Bookmark** a una variable. Para volver rápidamente a ese registro en cualquier momento después de desplazarse a otro registro, establezca la propiedad **Bookmark** del objeto de **conjunto de registros** en el valor de esa variable.  
  
 Es posible que el usuario no pueda ver el valor del marcador. Además, los usuarios no deben esperar que los marcadores sean comparables directamente, ya que dos marcadores que hacen referencia al mismo registro pueden tener valores diferentes.  
  
 Si usa el método [Clone](../../../ado/reference/ado-api/clone-method-ado.md) para crear una copia de un objeto de **conjunto de registros** , los valores de propiedad de **marcador** para los objetos de conjunto de **registros** original y duplicado son idénticos y se pueden usar indistintamente. Sin embargo, no puede usar los marcadores de distintos objetos de **conjunto de registros** indistintamente, aunque se hayan creado a partir del mismo origen o comando.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conjunto de registros** del lado cliente, la propiedad de **marcador** siempre está disponible.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades BOF, EOF y Bookmark (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Ejemplo de las propiedades BOF, EOF y Bookmark (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
